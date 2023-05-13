Original Source: https://missing.csail.mit.edu/2020/course-shell/

# 1. Using the shell

The shell command is divided by spaces, if you want to include space, use "" , '', or \ for escaping

​	`echo Hello\ World`


Environment variable

​	are set when starting the shell: home directory, user names, path	

- `echo $PATH`: all path the shell will search for programs
  - when you specify a program name, the shell will search that name in those pathes
- `which echo`: the path where the function 'echo' exists

# 2. Navigating in the shell

- `pwd`: print working directory
- `tee`: print it out and also write into a file
- `ls` : print all file in current path
  - `ls {path}`: print  all file in that path
- `~` :home directory
- `/` : root directory
  - absolute path start with /
- `cd ..` go to the parent directory
- `cd -`  back to previous directory [the one you are at previously]
- `mv` 
  - mv file directory: move
  - mv old_directory new_directory: rename directory
  - mv old_file new_file: rename file
- `cp copy_from copy_to`: copy
- `mkdir` : create a new directory
- `rm`
  - rm file: remove file
  - rm -r directory: recursivly delete all file and direcotry inside 
  - rmdir directory: remove directory if this directory and all its children are empty
- `man CMD` : for menu, like help, use q to quit
  - e.g.: man ls
- ctrl + l / `clear`: clear the window and go back to the top
- `ls --help`: help page for 'ls'

## 2.1 Flag [no parameter further needed] / Option [some paramters needed]

e.g. `ls -l` list all files but much more information like permissions
read(r), write(w), excute(x)
---(ower of the file)---(the owner groups)---(everyone else)

- for directory
  - r: allow to see what files are in that directory
  - w: rename, create, move etc. files in that directory
    - if you have w permission to a file but not its directory, then you can only empty its cotent but cannot delete it
  - x: search that directory, allowed to go to that directory [must have the directory x permission to execute a file inside]

# 3. Coonecting programs

- `CMD < a > b`: redirect input to a and output to b 

- `\>>` append 

- `>` overwrite
- `|` : pipe
  - `ls -l | tail -n1 > ls.txt`: the output of ls -l is the input of tail -n1 and then write the result to ls.txt
  - `curl --head --silent google.com | grep -i content-length | cut --delimiter = ' ' -f2` : get content length

# 4. Versatile and powerful tool  

root user / super user, userID=0, can do everything in the computer. can access the file that no one has the permission

- `sudo CMD` : do sth as superuser 
  - /sys: a special system file
    - on mac : `cd /System`
  - many kernel parameters inside the 'sys' directory
- `# CMD`: run cmd as root 
- `sudo su `  make the shell as the super user, change the current user to root, and $ --> #
- `exit`  exit the su
- `xdg-open FILE`  : open a file OR `open` in MacOS

examples

- `sudo find -L /sys/class/backlight -maxdepth 2 -name '*brightness*'`: find the path of brightness
- `echo 500 | sudo tee brightness`

# # Exercises

Can be found on ubaton virtual machine

1) echo $SHELL [check the shell]
2) DONE
3) touch [change file timestamps]
4) touch semester [create a file called semester]
     ==what is the difference between 'semester' and 'semester.txt', why I can run the first one but not the second one?==
5) It’s helpful to know that `#` starts a comment in Bash, and `!` has a special meaning even within double-quoted (`"`) strings. Bash treats single-quoted strings (`'`) differently: they will do the trick in this case. See the Bash [quoting](https://www.gnu.org/software/bash/manual/html_node/Quoting.html) manual page for more information.
6) DONE
7) sh semester
     ==what does sh did?==
     - "Run the command by explicitly starting the `sh` interpreter, and giving it the file `semester` as the first argument, i.e. `sh semester`. Why does this work, while `./semester` didn’t?"
8) man chmod
     chmod [change file mod bits]
9) chmod +x semester
10) ./semester | grep last-modified > ~/last-modified.txt
11) cat /sys/class/power_supply/BAT1/capacity

Solution: https://missing-semester-cn.github.io/missing-notes-and-solutions/2020/solutions/course-shell-solution/