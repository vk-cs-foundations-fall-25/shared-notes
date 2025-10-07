# Shell

![alt text](../media/42806128185_fcb7e34927_c.jpg)[^1]

## What is the Shell?
 > A command-line interpreter that allows users to access an operating system's services

e.g. list directory contents:
```shell
$ ls
```

- Intermediary between user and OS kernel
- Common shells by OS

    | OS      | Default Shell  |
    | ------- | -------------- |
    | Linux   | **bash**       |
    | macOS   | **zsh**        |
    | Windows | **PowerShell** |

- Terminology
  - **Terminal**: the program that provides the window/interface
  - **Shell**: the program that interprets and executes commands on the terminal
  - **Command Prompt**: the text indicator showing the shell is ready for input

- Control path: user -> terminal -> shell -> kernel -> hardware

## Why Learn Shell Commands?

1. **Automation**: Repetitive tasks can be scripted
2. **Efficiency**: Often faster than GUI (graphical user interface) for many tasks
3. **Remote Access**: Essential for managing servers
4. **Power**: Access to system features not available in GUI
5. **Universal**: Works on minimal systems without graphical interface

## Basic Navigation Commands

- File system tree hierarchy
  - **Directory** and **File**

    ```shell
    /                       # root directory
    /dir1/                  # 1st level directory
    /dir1/dir2/             # 2nd level directory
    /dir1/dir2/file1.md     # File

- Path types
  - **Absolute**: starts from root e.g. `/home/user/documents`
  - **Relative**: starts from current dir e.g. `./documents`
  - Special paths:
    - `~`: user home dir
    - `.`: current dir
    - `..`: parent dir
    - `-`: previous dir

- Commands

    | Command | Purpose                 | Example         |
    | ------- | ----------------------- | --------------- |
    | `pwd`   | print working directory | `pwd`           |
    | `ls`    | list dir contents       | `ls -al`        |
    | `cd`    | change dir              | `cd /home/user` |

- Common `ls` options (can be combined)

    ```
    ls -l    # Long format with details
    ls -a    # Show hidden files (starting with .)
    ls -h    # Human-readable file sizes
    ls -t    # Sort by modification time
    ls -r    # reverse sort
    ls -R    # Recursive listing
    ```
- RTFM
  
  `man ls`

## File/Dir Manipulation

- Creating and deleting

    | Command | Purpose                               | Example                |
    | ------- | ------------------------------------- | ---------------------- |
    | `mkdir` | make dir                              | `mkdir -p path/to/dir` |
    | `touch` | create empty file or update timestamp | `touch file.txt`       |
    | `rm`    | remove files/directories              | rm -rf dir1/           |
    | `rmdir` | remove empty dir                      | `rmdir dir2`           |

- Copying and moving

    ```shell
    cp source.txt dest.txt           # Copy source to dest
    cp -r source_dir/ dest_dir/      # Copy directory recursively
    mv oldname.txt newname.txt       # Rename/move file
    mv file.txt /new/location/       # Move to different directory
    ```

- Pattern matching
  - **Wildcards**

    ```shell
    *        # Matches zero or more characters
    ?        # Matches exactly one character
    [abc]    # Matches any one of a, b, or c
    [0-9]    # Matches any digit
    [!abc]   # Matches any character except a, b, or c

    # Examples:
    ls *.txt           # All .txt files
    rm file?.pdf       # Remove file1.pdf, file2.pdf, etc.
    cp [A-Z]*.doc ~/   # Copy all .doc files starting with uppercase
    ```
  -  **Globbing**: process by which shell expands wildcards into a list of matching pathnames and then executes the shell command on the expanded filenames

## File Content and Text Processing

- Viewing file contents

    | Command | Purpose                                            | Example               |
    | ------- | -------------------------------------------------- | --------------------- |
    | `cat`   | Concatenate and display (small files)              | `cat file.txt`        |
    | `less`  | Page through large files                           | `less large_file.log` |
    | `head`  | Show first lines for a quick preview               | `head -n 20 file.txt` |
    | `tail`  | Show last lines e.g. to see the latest log entries | `tail -f logfile.txt` |

- Text processing

    | Command | Purpose                         | Example                      |
    | ------- | ------------------------------- | ---------------------------- |
    | `⁠grep` | Search text patterns            | `grep "error" logfile.txt`   |
    | `⁠sed`  | Stream editor                   | `sed 's/old/new/g' file.txt` |
    | `awk`   | Pattern scanning and processing | `awk '{print $1}' data.txt`  |
    | `⁠sort` | Sort lines                      | `sort -n numbers.txt`        |
    | `⁠uniq` | Report or filter unique lines   | `uniq -c file.txt`           |
    | `cut`   | Extract columns                 | `cut -d',' -f2 data.csv`     |
    | `wc`    | Word, line, character count     | `wc -l file.txt`             |

### Grep and Regular Expressions

> **Connection**: DFA/NFA/Regular-Expression equivalently specify a Regular Language

```
# Search for "error" in file
grep "error" logfile.txt

# Case-insensitive search
grep -i "error" logfile.txt

# Search in multiple files
grep "TODO" *.py

# Recursive search
grep -r "function" ./src/

# Show line numbers
grep -n "warning" logfile.txt

# Count matches
grep -c "failed" logfile.txt
```

```
# Essential options
grep -i    # Case-insensitive
grep -v    # Invert match
grep -n    # Line numbers
grep -c    # Count matches
grep -r    # Recursive
grep -E    # Extended regex
grep -F    # Fixed strings
grep -w    # Word match
grep -A/-B/-C # Context lines

# Basic patterns
.          # Any character
*          # Zero or more of preceding
^          # Start of line
$          # End of line
[abc]      # Character class
[^abc]     # Negated class
\          # Escape special character
```

#### Common Examples


- Email Addresses (Simplified)
    
    ```
    # Basic email pattern
    grep -E "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" emails.txt
    ```

- IP Addresses

    ```
    # Simple pattern (not perfect)
    grep -E "[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}" file.txt
    ```

- Phone Numbers

    ```
    # US phone number formats
    grep -E "([0-9]{3})-[0-9]{3}-[0-9]{4}" file.txt           # 555-123-4567
    grep -E "\([0-9]{3}\) [0-9]{3}-[0-9]{4}" file.txt         # (555) 123-4567
    ```

- URLs

    ```
    # Basic HTTP/HTTPS URLs
    grep -E "https?://[[:alnum:].-]+" file.txt
    ```

- Dates

    ```
    # MM/DD/YYYY or MM-DD-YYYY
    grep -E "[0-9]{2}[/-][0-9]{2}[/-][0-9]{4}" file.txt
    ```

#### Debugging

- Testing patterns

    ```
    # Test with echo
    echo "test string" | grep "pattern"

    # Verbose matching with -o
    echo "test123 ab456" | grep -o "[0-9]+"
    # Output: 123
    #         456

    # Use online regex testers
    # - regex101.com
    # - regexpal.com
    ```

- Building complex patterns

    ```
    # Start simple
    grep "[0-9]" file.txt           # Any digit

    # Add complexity gradually
    grep "[0-9]+" file.txt          # One or more digits
    grep "^[0-9]+" file.txt         # Start with digits
    grep "^[0-9]+\." file.txt      # Start with digits, then period
    grep "^[0-9]+\.[0-9]+" file.txt # Decimal number at line start
    ```

## Redirection and Pipes

- Standard streams
  
  - **stdin (0)**: standard input
  - **stdout (1)**: standard output
  - **stderr (2)**: standard error

- Redirection operators

    ```
    >   # Redirect stdout (overwrite)
    >>  # Redirect stdout (append)
    <   # Redirect stdin
    2>  # Redirect stderr
    &>  # Redirect both stdout and stderr

    # Examples:
    ls > file_list.txt              # Save ls output to file
    echo "text" >> log.txt          # Append to file
    sort < unsorted.txt > sorted.txt # Input from file, output to file
    command 2> errors.log           # Redirect only errors
    command &> all_output.log       # Redirect everything
    ```

- Pipes: send output of one command as input to another

    ```
    ls -l | grep ".txt"              # List only .txt files
    cat file.txt | sort | uniq      # Sort and remove duplicates
    ps aux | grep python             # Find Python processes
    history | tail -20               # Show last 20 commands
    df -h | grep /dev/sda            # Check specific disk usage
    ```

- Command substitution

    ```
    echo "Today is $(date)"         # Modern syntax
    echo "Files: `ls | wc -l`"      # Backtick syntax (older)
    ```

## Process and System Management

- Process commands

    | Command | Purpose | Example |
    | --- | --- | --- |
    | `⁠ps` | List processes | `ps aux` |
    | `⁠top` | Interactive process viewer | `⁠top` |
    | `⁠kill` | Terminate process| `⁠kill -9 1234` |
    | `⁠jobs` | List background jobs | `jobs` |
    | `⁠bg` | Resume job in background | `⁠bg %1` |
    | `⁠fg` | Bring job to foreground | `⁠fg %1` |

- Background execution

    ```
    command &                        # Run in background
    Ctrl+Z                          # Suspend current process
    nohup command &                 # Run immune to hangups
    ```

- System information

    ```
    uname -a                        # System information
    df -h                          # Disk usage
    du -sh *                       # Directory sizes
    free -h                        # Memory usage
    uptime                         # System uptime and load
    ```

## File Permissions

- Understanding Permissions

    ```
    -rwxr-xr-- 1 user group 1024 Jan 1 12:00 file.txt
    │││││││││
    │││││││└─ Other: Read only (4)
    ││││││└── Group: Execute (1)
    │││││└─── Group: No write (0)
    ││││└──── Group: Read (4)
    │││└───── Owner/user: Execute (1)
    ││└────── Owner/user: Write (2)
    │└─────── Owner/user: Read (4)
    └──────── File type (- = regular file)
    ```

- Permission Commands

    ```
    chmod 755 script.sh             # rwxr-xr-x
    chmod u+x file.sh              # Add execute for user
    chmod -R 644 documents/        # Recursive permission change
    chown user:group file.txt      # Change ownership
    ```

- Octal Notation
  - Read (r) = 4
  - Write (w) = 2
  - Execute (x) = 1

## Scripting

- Creating a Simple Script

    ```
    #!/bin/bash
    # This is a comment

    echo "Hello, World!"
    NAME="Student"
    echo "Welcome, $NAME"

    # Conditionals
    if [ -f "file.txt" ]; then
        echo "File exists"
    fi

    # Loops
    for i in {1..5}; do
        echo "Number: $i"
    done
    ```

- Making Scripts Executable

    ```
    chmod +x script.sh
    ./script.sh
    ```

- Command Line Arguments

    ```
    #!/bin/bash
    echo "Script name: $0"
    echo "First argument: $1"
    echo "All arguments: $@"
    echo "Number of arguments: $#"
    ```

## Tips

- Safety Tips
  
  1. Use ⁠`rm -i` for interactive deletion
  2. Test with `⁠echo` before running destructive commands
  3. Use `⁠--dry-run` when available
  4. Keep backups before bulk operations	
   
- Efficiency Tips

  1. Tab completion: Press Tab to auto-complete
  2. History search: Ctrl+R for reverse search
  3. Aliases: Create shortcuts for common commands

        ```
        alias ll='ls -la'
        alias ..='cd ..'
        ```

  4. Learn keyboard shortcuts:
     1. Ctrl+A: Beginning of line
     2. Ctrl+E: End of line
     3. Ctrl+K: Delete to end of line
     4. Ctrl+U: Delete to beginning of line

- Getting Help

    ```
    man command        # Manual pages
    command --help     # Built-in help
    which command      # Find command location
    type command       # Show command type
    apropos keyword    # Search manual pages
    ```

[^1]: <p class="attribution">"<a rel="noopener noreferrer" href="https://www.flickr.com/photos/114240786@N08/42806128185">Shell</a>" by <a rel="noopener noreferrer" href="https://www.flickr.com/photos/114240786@N08">ako_law</a> is licensed under <a rel="noopener noreferrer" href="https://creativecommons.org/licenses/by-sa/2.0/?ref=openverse">CC BY-SA 2.0 <img src="https://mirrors.creativecommons.org/presskit/icons/cc.svg" style="height: 1em; margin-right: 0.125em; display: inline;" /><img src="https://mirrors.creativecommons.org/presskit/icons/by.svg" style="height: 1em; margin-right: 0.125em; display: inline;" /><img src="https://mirrors.creativecommons.org/presskit/icons/sa.svg" style="height: 1em; margin-right: 0.125em; display: inline;" /></a>.</p>