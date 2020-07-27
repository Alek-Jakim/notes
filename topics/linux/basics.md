# Terminal

`/` - Root directory  
`~` - Home directory

`^` - Control key.  
`M` - Alt key.

`CTRL` + `C` - Stop running command.  
`CTRL` + `D` - Close current shell session.  
`CTRL` + `L` - Clear screen. (Scrolls you down in reality)

`CTRL` + `A` - Go to beginning of line.  
`CTRL` + `E` - Go to end of line.  
`CTRL` + `F` - Next word.  
`CTRL` + `B` - Previous word.

`ALT` + `Backspace` - Delete last word.  
`ALT` + `Left` / `Right` - Go to previous / next word.  
`CTRL` + `U` - Delete whole line.

`man COMMAND` - Command help.  
`history` - Lists all the commands used.  
`CTRL` + `R` - Search command history. Hit again for previous command.

## Basic Navigation

`pwd ` - print working directory

`ls ` -  list computer files

`ls -a ` - list all computer files(hidden and not hidden)

`ls /` - list computer files from root directory

`cd / `  - go to root directory

`cd ~ ` - go to home directory

`mkdir directory_name` - create new directory

`touch file_name ` - create new file

`cat file_name ` - read the file

`mv file_name directory_name` - move the file to the specified directory 

`mv file_name  new_file_name ` - rename a file

### Removing Files
`rm file_name ` - remove the specified file

`rmdir directory_name ` - remove the specified directory

`rm -r directory_name ` - **Use this** for removing directories

`rm -rf / ` - **NEVER** use this, it brings the end of days for your entire system

`cd ../..` - Return two directories backwards

# Information


```bash
cat /etc/os-release     # Linux version
df -h                   # Show disk space in readable format
```

One of the keys to becoming good at Linux is **using the command line for everything!**

Root directory is the base of the file tree, everything else, including the OS system files, is in it. Home directory is within the root directory, and contains user files, contained in a sub directory for each user. ... There is one root directory for the computer's entire filesystem.


## Text Editors

### Nano/Vim/Emacs

Use nano for simple edits, vim or emacs for programming

[Vim](vim.md)




 