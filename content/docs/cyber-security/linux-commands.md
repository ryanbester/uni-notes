---
title: "1. Linux Commands and Vim"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 1. Linux Commands and Vim

## Common Commands

| Command | Description | Example |
|:--------|:------------|:--------|
| cd | Changes the current directory | `cd dir1` |
| cat | Outputs the contents of the file | `cat file.txt` |
| echo | Outputs the specified argument (to stdout) | `echo Hello` |
| ls | Lists files in the specified directory | `ls dir1` |
| rm | Removes (deletes) a file or directory | `rm file.txt` |
| man | Shows the manual page for the specified command | `man ping` |
| exit | Exits the current terminal session | `exit` |
| mkdir | Creates a new directory | `mkdir dir2` |
| which | Shows the full path of a command in the $PATH | `which google-chrome` |
| pwd | Prints the current working directory | `pwd` |
| tree | Outputs a list of files and directories in tree form | `tree dir1` |
| ln | Creates a new link | `ln dir1 linktodir` |
| find | Helps find data in file hierarchies (can be used for many advanced things) | `find ./ -name "*.txt" ` |
| ps | Lists processes running on the system | `ps -ef ` |
| grep | Searches a string for matches (basically a Find function) | `grep tofind file.txt` |
| tail | Outputs the last lines of a file | `tail log.txt` |
| head | Outputs the first lines of a file | `head file.txt` |
| touch | Updates the access times for a file, or can just be used to create a blank file | `touch file.txt` |
| mv | Moves or renames a file or directory | `mv file.txt newname.txt` |
| diff | Shows the differences between two files | `diff file-v1.txt file-v2.txt` |
| whoami | Outputs your current username | `whoami` |

Note: folders should be called directories in Linux/Unix.

## Vim

Vim is a highly-configurable text editor for Linux and Unix.

Command: `vi` or `vim`

- Vim operates in 2 modes: **Command** and **Insert**
    - **Command** mode allows you to use your keyboard to enter commands
    - **Insert** mode allows you to enter text and edit a file
- By default Vim opens in **Command** mode
    - You can change to **Insert** mode by hitting `i` (there are more keys to do this)
    - You can go back to **Command** mode by hitting `esc`
- No one appears to know [how to exit Vim](https://stackoverflow.com/questions/11828270/how-do-i-exit-vim)
    - `:wq`: Save (write) and quit
    - `:q!`: Quit without saving

### Common Vim Commands

- **Cursor Movement**
    - `h` `j` `k` `l`: up, down, up, right
    - Most versions allow arrow keys
- **Delete**
    - `dd`: Delete line
    - `x`: Delete at cursor
    - `dw`: Delete word
    - `r`: Replace a character
    - `D`: Delete to end of line
- **Editing**
    - `yy`: Copy (yank) a line
    - `nyy`: Copy `n` lines
    - `p`: Paste above current line
    - `P`: Paste below current line
    - `?string`: Search backwards for `string`
    - `/string`: Search forwards for `string`
    - `.`: Repeat last command
    - `u`: Undo last command

For full commands see [the amazing Vim cheat sheet](https://vim.rtorr.com/).
