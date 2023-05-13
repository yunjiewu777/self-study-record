Original: https://missing.csail.mit.edu/2020/editors/

# 1. Modal editing

## 1. 1 Multiple operating modes

1. normal mode: for moving around a file and making edits
2. insert mode (i): for inserting text
3. replacing mode  (R): for replacing text 
4. Selection: for selecting blocks of text
   1. Visual mode (v)
   2. Visual Line (V)
   3. Visual Block (Ctrl-V)
5. Command Line mode (:): for running a command

## 1.2 Notations

Control V can be expressed in the following 3 ways:

1. ^V
2. Ctrl-V
3. \<C-V\>

# 2. Basics

## 2.1 Inserting Text

`i` get into insert mode

`esc` exit insert mode

## 2.2 Command-line

### Buffers, tabs, and windows

- `:sp`, `:vsp`
- `:tabnew`
- `:open file`

### Exit vim

- `:q` close the current window
- `:qa` quit all
- `:q!` quit and don't save the file
- `:wq` save and quit
- `:w` save
- `:e {name of file}` open file for editing
- `:ls` show open buffers

### Help

- `:help CMD`
  - e.g., `:help :w`

# 3. Vim's Interface

## 3.1 Movement

- Basic movement: `hjkl` (left, down, up, right)
- Words: `w` (next word), `b` (beginning of word), `e` (end of word)
- Lines: `0` (beginning of line), `^` (first non-blank character, same as `0w`), `$` (end of line)
- Screen: `H` (top of screen), `M` (middle of screen), `L` (bottom of screen)
- Scroll: `Ctrl-u` (up), `Ctrl-d` (down)
- File: `gg` (beginning of file), `G` (end of file)
- Line numbers: `:{number}<CR>` or `{number}G` (line {number})
- Misc: `%` (corresponding {} () [])
- Find: `f{character}`, `t{character}`, `F{character}`, `T{character}`
  -  find/to forward/backward {character} on the current line
  - `,` / `;` for navigating matches
- Search: `/{regex}`, `n` / `N` for navigating matches

- `number + jklh{}` go direction with number of line or char
- W,B move with ignorance of punctuation, only cares about space
- {, } go up and down blocks of code

## 3.2 Selection

- Visual: `v`
- Visual Line: `V`
- Visual Block: `Ctrl-v`



- 可以和hjkl{} G gg 组合使用
  - then d, y ...

## 3.3 Edits

- o add a black line below and get into insert mode

- O add a black line above and get into insert mode 
- dd delete the just edited thing, or delete a line; and copy to clipboard
  - number + dd delete number of lines
  - d + hjkl{} %bw  delete that
  - D delete  from cursor to the rest of the line

- x delete one character
- c changing, delete something and get into insert mode
  - C delete from cursor to the rest of the line	
  - ct} change until }
  - cc delete the line ang into insert mode

- s substitute character (equal to cl)
- r replace the cursor letter
  - 3ro replace flowwing 3 letter with o, so 'ooo'

- R replace the follwing letter

- u undo, \<Ctrl-r\> redo
- . redo the thing you just did -- [note everything?]\(d)

- y+ jkhlwb copy coresponding content
- yy copy current line
- p paste down, P paste below
- ~ swap the case, lower to upper or upper to lower

## 3.4 Modifiers

- `a` go to insert mode and move curson 1 right 
  - `A` go the end of the line and insert mode

- `i` inside
  - `ca[` change things inside the [], but also delete the []
  - `ci[` change things inside the []
- `da'` delete a single-quoted string, including the surrounding single quotes

## 3.5 Others

- ; go to the next D with f or t
- zz center your cursor
- esc clear the current command
- \* move between the same word in the file
- x delete the cursor character
- I go to the start at the line and go to insert mode
- .  redose the last thing you do
- < indent
  - can be combine with V
- \> indent
- / find words	
  - n go to other same words

# 4. Demo

Examples: 

d3w : Delete 3 word(s) 

y3w : Yank/Copy 3 word(s) 

3p : Put/Paste 3 (times) 

dt" : Delete To " 

3j : 3 lines down 

di": Delete inside "..." 

dG: Delete to the bottom of the file

# 5. Customizing Vim

stored in ~/.vimrc

# 6. Extending Vim

https://vimawesome.com/

# 7. Vim mode in other programs

## Shell

If you’re a Bash user, use `set -o vi`. If you use Zsh, `bindkey -v`. For Fish, `fish_vi_key_bindings`. Additionally, no matter what shell you use, you can `export EDITOR=vim`. This is the environment variable used to decide which editor is launched when a program wants to start an editor. For example, `git` will use this editor for commit messages.

# 8. Advanced Vim

## 8.1 Search and replace

- `:s` substitute
  - `:%s/foo/bar/g` replace foo with bar globally in file
  - `%s/\[.*\](\(.*\))/\1/g` replace named Markdown links with plain URLs
  - `:%s/new/new/gc` change with a prompt

## 8.2 Macros

- q+charctar +[some code] + q  save the recording to character and press q again to stop the recording
  - call by @ character
  - number @ character, run multiple times

# 9. Resources

- `vimtutor` is a tutorial that comes installed with Vim - if Vim is installed, you should be able to run `vimtutor` from your shell
- [Vim Adventures](https://vim-adventures.com/) is a game to learn Vim
- [Vim Tips Wiki](http://vim.wikia.com/wiki/Vim_Tips_Wiki)
- [Vim Advent Calendar](https://vimways.org/2019/) has various Vim tips
- [Vim Golf](http://www.vimgolf.com/) is [code golf](https://en.wikipedia.org/wiki/Code_golf), but where the programming language is Vim’s UI
- [Vi/Vim Stack Exchange](https://vi.stackexchange.com/)
- [Vim Screencasts](http://vimcasts.org/)
- [Practical Vim](https://pragprog.com/titles/dnvim2/) (book)

# # Exercises

1. Complete `vimtutor`.
2. 
3. a
4. 3
5. 3
6. 3
7. 3
8. 3
9. 3
10. 3

Solution: 













