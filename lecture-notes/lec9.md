## Introduction to Using the Shell

The Shell
- a program that takes commands from the keyboard and gives them to the operating system to perform
- a.k.a command line, terminal

Shell Location
- a shell is considered to be working in a single location in the file system

File Systems
- a file system is an OS component for managing files
- what is a file?
    - a file is an abstraction for a cluster of user data
    - has contents, size, owner, last read/write time, protection, etc.
    - files can have types which are understood by the file system
- file systems have a tree hierarchical structure
    - you can have files with the same name if the context is different

Directories
- a directory is a cluster of space for storing files
- provides structured organization for users

Relative vs absolute naming
- `/home/faculty/sarwar/personal/letter`
- we normally type letter
- this is implicitly `./letter`
    - `.` means current directory
- this is a relative path name
- the full name is an absolute path name

Important directory names
- `~` the home directory
- `.` the current directory
- `..` the parent directory
- `/` the root directory

- `pwd` tells you what directory you are currently in
- `cd` lets you change to a different directory

Command Flags
- most commands have many different options for what they do
- choosing between options is done with flags
- usually done as `command -f`

Accessing other machines
- `ssh username@machine.address`

Commands for managing files
- `ls` lists the files in the directory
- `touch` creates files
- `cp` copies files
- `mv` moves fikes
- `rm` removes files

Hidden Files
- `-a` flag will show all files (even hidden ones)

Dangers of `rm`
- `rm -rf` is especially dangerous because it will recursively remove everything in a directory without asking you if you actually want to remove each file
- `rm -rf/` will delete the entire file system on a computer (bricks your computer)
- `rm -rf*` will delete everything
- `mc /home/user/* /dev/null` deletes the entire user folder

Compressing Files
- use the `tar` command
- `tar -cf` will create a zip file with a specified name

Text Processing
- `sort` sorts lines of text file
- `cat` concatenates inputs and prints on the screen
- `head` and `tail` print the first (or last) lines of a file

File permissions
- 3 types of permissions (read, write, execute)
- permissions are defined for 3 groups (owner, group, others)
- check permissions with `ls -l`

Wildcards for files names
- `*` matches any characers
- `?` matches any single character
- `[characters]` matches any character that is a member of the set characters
- ex: `rm g*` will remove any file in the current directory that starts with a g
- ex: `[[:upper:]]*` references any file beginning with an upper case character

I/O Redirection
- can redirect input and output of commands
- `command < file` (reads the stdin of "command" from "file")
- `command > file` sends the stdout of "command" to "file", overwriting its contents
- `command >> file` appends the stdout of "command" to the end of "file"
- `command 2> file` sends the stderr of "command" to "file", overwriting its contents
- Pipes can chain one command's output to the input of another
    - to create a pipe we use the unix pipe character `|`
    - using pipes effectively can reduce some incredibly hard problems into single lines of code

Processes
- a process is an instance of a running program 
- a process is a currently executing command (or program) sometimes refered to as a job

Foreground vs Background
- jobs can be run in:
    - foreground job: a job that occupies the terminal until it is computed
    - background job: a job that executes in the background and does not occupy the terminal (run one by adding `&` to the end of the line)
    - only one job can be run in the foreground but multiple can be run in the background

Version Control
- a practice of tracking and managing changes to code
- provides shared copies of projects
- allows for concurrent development
- tracking changes

Git
- a version control system















