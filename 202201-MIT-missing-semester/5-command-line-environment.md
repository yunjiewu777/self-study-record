Original: https://missing.csail.mit.edu/2020/command-line/

# 1. Job Control

- `man signal`
- `jobs`
  - list current jobs
- `bg %1`  recove the process and run in the background
- `kill %1` kill process 1 listed by `jobs`
- `nohup sleep 2000 &`

# 2. Terminal multiplexers

`tmux`

- sessions
- windows
- frame



<Ctrl b> + acv...

# 3. Dot Files

`alias ll="ls -lah"`



# 4. Remote Machines



- ssh
  - ssh keys
  - `ssh-keygen -o -a 100 -t ed25519`
  - `ssh-copy-id ywu449....`

- `scp FILE ywu449@...:FILE_TO`
- `rsync -avP  FOLDER ywu449@...:FOLDER_TO`
  - perserve permission



~/.ssh/config

- 





- you can ssh and start a tmux session
  - 





