Resources: https://missing.csail.mit.edu/2020/shell-tools/

# 1. Shell Scripting

## 1.1 Variable

```bash
foo=bar
echo $foo
```

- spaces are critical
  - `foo = bar` won't work, here we are calling the program 'foo' with arguments

- `"` VS `'`: " can interpret inner variables
  - `echo "Value is $foo"`

## 1.2 Function

### Useful Operator

- $0 is the name of the script

- $1 to \$9 are special characters means the first to ninth argument

- $# number of arguments

- \$$ current pid

- $@ expand to all arguments

- $? error code from the previous command

  - has a value of 0 when everything is good

- $_  the last argument of the previous command

  - ```bash
    mkdir test
    cd $_
    ```

- !! Entire last command, including arguments. A common pattern is to execute a command only for it to fail due to missing permissions; you can quickly re-execute the command with sudo by doing `sudo !!`

- Logical operator: && OR ||
  - `false || echo 'Opps, fail' output: Ooops, fail`: if the first one is false, then do the second one
  - `true && echo "Things went well" output: Things went well`: if the first one is true, then do the second one
  - you can also concatenate command using `;`
    - `true ; echo "This will always run" output: This will always run`

### Define a function

mcd.sh

```bash
mcd() {
	mkdir -p "$1"
	cd "$1"
}
```

1. write the above content into a file called mcd.sh
2. `source mcd.sh`
3. `mcd test`

### Function and variable

- \$() command substitution

  ```bash
  # print the current directory
  echo "We are in $(pwd)"
  ```

- {}

  ```bash
  # use {}, the following 2 are the same
  convert image.png image.jpg
  convert image.{png,jpg}
  # can use more than 1 {} in a cmd
  ```

- < process substitution

  ```bash
  # store things into tmp files and then concatenate them together
  cat <(ls) <(ls ..)
  ```

## 1.3 Example File

```bash
#!/bin/bash

echo "Starting program at $(date)" # Date will be substituted

echo "Running program $0 with $# arguments with pid $$"

for file in "$@"; do
    grep foobar "$file" > /dev/null 2> /dev/null
    # When pattern is not found, grep has exit status 1
    # We redirect STDOUT and STDERR to a null register since we do not care about them
    
    # using [[]] and comparisions -ne 
    if [[ $? -ne 0 ]]; then
        echo "File $file does not have any foobar, adding one"
        echo "# foobar" >> "$file"
    fi
done
```

## 1.4 Other languages

```python
#!/usr/local/bin/python
import sys
for arg in reversed(sys.argv[1:]):
    print(arg)
```

- the first line could also be `#!/user/bin/env python`, since some system don't have python in bin folder

### Directly

`python script.py a b c`

### By Shell

`./script.py a b c`

## 1.5 Debug 

Shellcheck: it can detect potential bugs and warnings

- `shellcheck mcd.sh`

## 1.6 Differences

Some differences between shell functions and scripts that you should keep in mind are:

- Functions have to be in the same language as the shell, while scripts can be written in any language. This is why including a shebang for scripts is important.
- Functions are loaded once when their definition is read. Scripts are loaded every time they are executed. This makes functions slightly faster to load, but whenever you change them you will have to reload their definition.
- Functions are executed in the current shell environment whereas scripts execute in their own process. Thus, functions can modify environment variables, e.g. change your current directory, whereas scripts can’t. Scripts will be passed by value environment variables that have been exported using [`export`](https://www.man7.org/linux/man-pages/man1/export.1p.html)
- As with any programming language, functions are a powerful construct to achieve modularity, code reuse, and clarity of shell code. Often shell scripts will include their own function definitions.

# 2. Shell Tools

## 2.1 Finding how to use commands

1. `CMD -h` or `CMD --help`

2. `man CMD`

3. `tldr CMD`
   - with explanatory examples

## 2.2 Finding files

1. `find`

   - ```bash
     # Find all directories named src
     find . -name src -type d
     # Find all python files that have a folder named test in their path
     find . -path '*/test/*.py' -type f
     # Find all files modified in the last day
     find . -mtime -1
     # Find all zip files with size in range 500k to 10M
     find . -size +500k -size -10M -name '*.tar.gz'
     ```

   - `find . -name "*.tmp" -exec rm {} \;` find all tmp file and then rm each of them 

     ==what is the last {} \ ; part doing?==

2. `fd`
3. `locate`
   - it build indexes so it's much faster
   - but the databases sometimes is updated daily, so speed vs freshness tradeoff

## 2.3 Finding code

1. `grep`

   - `grep foobar mcd.sh`: find "foobar" in file mcd.sh
   - `grep -R foobar .`: find "foobar" from current directory recursively

2. `rg`

   - Installation for ubuntu `sudo apt-get install ripgrep`

   - more advanced than grep
   - `rg "import requests" -t py -C 5 --stats ~/scratch` : find that string in all python files inside the directory, show before and following 5 lines, with some statistics print to terminal
   - `rg -u --files-without-match "^#\!" -t sh` : don't ignore hidden files, find files that don't match the expression, only look for .sh files

3. `ack`

4. `ag`

## 2.4 Finding shell commands

- up or down arrow key
- `history`
  - `history 1 | grep convert`
- Ctrl + r
  - Backward search
- fzf
  - interactive search
  - `man cat | fzf`
- history-based autosuggestions

## 2.5 Directory navigation

- `fasd`
  - `z cool`

- `autojump`
  - `j cool`

- `ls -R`
- `tree`
- `broot`
- `nnn`
- `ranger`

# # Exercises

1. `ls -a -G -h -l -t`

2. ```bash
    #!/bin/bash
    marco(){
        echo "$(pwd)" > $HOME/marco_history.log
        echo "save pwd $(pwd)"
    }
    polo(){
        cd "$(cat "$HOME/marco_history.log")"
    }
    
   #OR
   
   #!/bin/bash
    marco() {
        export MARCO=$(pwd)
    }
    polo() {
        cd "$MARCO"
    }
   ```

3. ```bash
   #!/usr/bin/env bash
   
   count=0
   
   while true
   do
   	((count++))
   	./missing3-3 >> out.log
   	
   	if [[ $? -ne 0 ]]; then
   		cat out.log
   		echo "failed after $count times"
   		break
       fi
   done
   ```

4. `find . -type f -name "*.html" | xargs -d '\n'  tar -cvzf html.zip`
   -  [`xargs`](https://www.man7.org/linux/man-pages/man1/xargs.1.html) command which will execute a command using STDIN as arguments.

5. `find . -type f -print0 | xargs -0 ls -lt | head -1`

Solution: https://missing-semester-cn.github.io/missing-notes-and-solutions/2020/solutions/shell-tools-solution/