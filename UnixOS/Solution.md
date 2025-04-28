# UNIX Exam Questions and Answers

*Source Material: Provided PDF files - "Initial Course Notes" [Notes] and "TutorialsPoint Unix Tutorial" [TP].*

---

## Unit 1: Introduction to OS & UNIX

### 1. OS & UNIX Definition and Architecture

**Operating System (OS) Definition:**
An Operating System is system software that manages computer hardware and software resources, and provides common services for computer programs. It acts as an interface between the computer hardware and the user, managing tasks like process execution, memory allocation, file systems, and input/output operations. The core component interacting directly with hardware is the kernel.

**UNIX Definition:**
UNIX is a computer Operating System initially developed around 1969 at AT&T Bell Labs. It is characterized as a portable, multitasking (allowing multiple programs to run concurrently), and multiuser (allowing multiple users to access the system simultaneously) time-sharing operating system. Linux is a widely-used, independently developed, Unix-like operating system kernel and the basis for many popular OS distributions.

**UNIX Architecture:**
The conceptual architecture of a UNIX system generally consists of:

1.  **Hardware:** The underlying physical computer components.
2.  **Kernel:** The core of the OS. It manages the hardware resources (CPU scheduling, memory management, device drivers), executes system calls, and controls file management. It isolates hardware from the user and applications.
3.  **Shell:** The command-line interpreter (CLI) that acts as the interface between the user and the kernel. It reads user commands, interprets them (handling metacharacters, variables, etc.), finds and executes the corresponding programs, and manages job control. Common shells include `sh`, `bash`, `csh`, `ksh`, `tcsh`.
4.  **Application Programs / Commands & Utilities:** User-level programs and standard UNIX utilities (`ls`, `grep`, `vi`, compilers, databases, etc.) that perform specific tasks. These programs interact with the shell and make system calls to the kernel to perform operations.

**Diagram: UNIX System Structure**

<img src="https://github.com/43H1-BOI/4th_End_Sem/blob/main/UnixOS/images/placeholder_unix_architecture.png" width="400" height="400">

**Diagram: UNIX Kernel Architecture**

<img src="https://github.com/43H1-BOI/4th_End_Sem/blob/main/UnixOS/images/placeholder_kernel_architecture.png" width="500" height="300">

*(This diagram shows internal kernel components like the file subsystem, process control subsystem, scheduler, memory management, device drivers, hardware interface, and system call interface).*

### 2. UNIX Features & Advantages

UNIX offers several key features and advantages:

*   **Multiuser:** Supports multiple users accessing the system concurrently.
*   **Multitasking:** Allows multiple processes (programs) to run simultaneously.
*   **Portability:** Designed to be relatively easily adaptable to run on different hardware platforms, largely due to being written in C.
*   **Hierarchical File System:** A structured, tree-like organization for files and directories, simplifying data management.
*   **Powerful Shell Interface:** Provides a flexible and scriptable command-line interface for complex tasks and automation.
*   **Rich Set of Utilities:** Includes a vast collection of small, specialized command-line tools that can be combined effectively.
*   **Pipes and Filters:** Enables chaining commands together, using the output of one as input for the next.
*   **Security Model:** Provides file permissions and user/group management for access control.
*   **Networking Capabilities:** Strong, integrated support for network communication.
*   **Machine Independence:** Aims to abstract hardware details from applications.

### 3. UNIX vs. Windows

| Feature           | UNIX (Typical/Linux)                   | Windows                                  |
| :---------------- | :------------------------------------- | :--------------------------------------- |
| **Source Code**   | Often open source (free)               | Proprietary (paid license)               |
| **User Interface**| Primarily CLI (Shell), GUI available   | Primarily GUI, CLI available           |
| **Security**      | Generally high, fine-grained control | Historically lower, improved over time |
| **Tasking**       | Multitasking                           | Multitasking                             |
| **Users**         | Multiuser native                       | Multiuser (esp. Server), desktop often single |
| **Case Sensitive**| Yes (filenames, commands)              | No (filenames)                           |
| **Primary Use**   | Servers, development, embedded         | Desktops, servers, gaming                |
| **Customization** | Highly customizable                  | Less customizable                        |
| **File System**   | Single Hierarchical Tree (`/`)         | Multiple Drives (C:, D:), hierarchical   |
| **Portability**   | High                                   | Limited                                  |

### 4. Command Execution Flow

The typical flow when a command is executed in the shell:

1.  **Prompt:** The shell displays a prompt (e.g., `$`), indicating readiness.
2.  **Input:** The user types a command line (command name, options, arguments) and presses Enter.
3.  **Parsing:** The shell reads and parses the command line, breaking it into words and interpreting special characters (wildcards, quotes, redirection, pipes).
4.  **Expansion:** The shell performs expansions (variable substitution like `$HOME`, command substitution like `$(pwd), filename expansion like `*.txt`).
5.  **Command Search:** The shell determines if the command is built-in or external. For external commands, it searches the directories listed in the `$PATH` environment variable to locate the executable file.
6.  **Execution Setup:** The shell prepares for execution, often involving:
    *   **`fork():** Creating a child process that is a copy of the shell.
    *   **Redirection/Piping Setup:** Setting up file descriptors for input/output redirection or pipes if specified.
    *   **`exec():** In the child process, replacing the shell's program image with the program to be executed.
7.  **Kernel Invocation:** The `exec() system call asks the kernel to run the new program.
8.  **Process Execution:** The kernel schedules and runs the command's process.
9.  **Output Handling:** The process sends its standard output and standard error, which the shell directs to the terminal (or files/pipes as redirected).
10. **Waiting (Foreground):** If the command runs in the foreground, the shell waits for it to complete.
11. **Completion & Prompt:** Once the command finishes, the shell typically regains control and displays the prompt again.

---

## Unit 2: UNIX File System & Management

### 5. File System Structure & Hierarchy

**File System Concept:**
In UNIX, the file system provides a structured way to store, retrieve, and manage data. Almost everything is represented as a file, including documents, programs, directories, and even hardware devices. It organizes these files on storage media like hard disks.

**Hierarchical Structure:**
The UNIX file system uses a single, unified, hierarchical tree structure.
*   Starts at the **root directory**, denoted by a single slash (`/`).
*   Contains directories (folders) that can hold files and other directories (subdirectories).
*   Files and directories are located using **pathnames**, which are sequences of directory names separated by `/`.
    *   **Absolute Path:** Starts from the root directory (`/`). E.g., `/home/user/docs/report.txt`.
    *   **Relative Path:** Starts from the current working directory. E.g., `docs/report.txt`.

**Diagram: UNIX Directory Structure**

<img src="https://github.com/43H1-BOI/4th_End_Sem/blob/main/UnixOS/images/placeholder_directory_structure.png" width="500" height="300">

**Key Predefined Directories:**

*   `/`: Root directory.
*   `/bin`: Essential user command binaries (like `ls`, `cp`, `cat`).
*   `/sbin`: Essential system binaries (like `fdisk`, `init`).
*   `/etc`: System configuration files (like `passwd`, `fstab`, `profile`).
*   `/dev`: Device files representing hardware (like `/dev/sda`, `/dev/tty1`).
*   `/home`: User home directories (e.g., `/home/student`).
*   `/usr`: Secondary hierarchy containing user programs (`/usr/bin`), libraries (`/usr/lib`), documentation, etc.
*   `/lib`: Essential shared libraries needed by programs in `/bin` and `/sbin`.
*   `/tmp`: Temporary file storage.
*   `/var`: Variable data files like logs (`/var/log`), mail spools (`/var/mail`).

### 6. File Types & Attributes

**File Attributes:**
Displayed by `ls -l`, key attributes include:
*   File Type & Permissions
*   Number of Hard Links
*   Owner (User)
*   Group
*   Size (in bytes)
*   Last Modification Timestamp
*   Filename

**File Types:**
The first character in the `ls -l` output indicates the type:

| Char | Type                 | Description                                      |
| :--- | :------------------- | :----------------------------------------------- |
| `-`  | Ordinary File        | Contains data, text, or program code.          |
| `d`  | Directory            | Contains other files and directories.            |
| `l`  | Symbolic Link        | Pointer to another file or directory.          |
| `b`  | Block Special File   | Represents a block device (e.g., hard disk).   |
| `c`  | Character Special File| Represents a character device (e.g., terminal). |
| `p`  | Named Pipe (FIFO)    | For inter-process communication.                 |
| `s`  | Socket               | For inter-process or network communication.    |

**Ordinary File Subtypes:**
*   **Text Files:** Contain human-readable characters (ASCII, UTF-8).
*   **Binary Files:** Contain non-printable characters, executable code, or structured data.

**Hidden Files:**
Files or directories whose names start with a dot (`.`). Not shown by `ls` by default; use `ls -a`. Often used for configuration (e.g., `.profile`, `.bashrc`).

### 7. Permissions & Modes

**Permission Categories:**
*   **User (u):** The owner of the file.
*   **Group (g):** The group associated with the file.
*   **Other (o):** All users not in the first two categories.
*   **All (a):** Refers to user, group, and other collectively.

**Permission Types:**

| Type      | File Effect                     | Directory Effect                               | Value (Octal) |
| :-------- | :------------------------------ | :--------------------------------------------- | :------------ |
| **Read (r)** | View contents                   | List contents (filenames)                      | 4             |
| **Write (w)**| Modify/delete contents          | Create/delete/rename files within it           | 2             |
| **Execute (x)**| Run as a program              | Enter (cd into) / traverse                     | 1             |

**Viewing Permissions (`ls -l`):**
Displays a 10-character string: `[type][user-rwx][group-rwx][other-rwx]`.
Example: `drwxr-x---` (Directory: owner=rwx, group=rx, other=no access).

**Changing Permissions (`chmod`):**

*   **Symbolic Mode:** Uses `u, g, o, a` and `+, -, =` with `r, w, x`.
    *   `chmod u+x file` (Add execute for user)
    *   `chmod go-w file` (Remove write for group and other)
    *   `chmod a=r file` (Set permissions to read-only for all)
*   **Absolute (Octal) Mode:** Uses 3 octal digits (0-7) representing permissions for user, group, and other. Each digit is the sum of values (r=4, w=2, x=1).
    *   `chmod 755 script.sh` (Owner=rwx, Group=r-x, Other=r-x)
    *   `chmod 640 data.txt` (Owner=rw-, Group=r--, Other=---)

**SUID/SGID:**
Special permissions:
*   **SUID (Set User ID):** If set on an executable, the process runs with the file *owner's* privileges. Shown as `s` instead of `x` in the user execute position (`rwsr-xr-x`). Useful for commands needing temporary root access (e.g., `passwd`).
*   **SGID (Set Group ID):** If set on an executable, the process runs with the file *group's* privileges (`rwxr-sr-x`). If set on a directory (`drwxrwsr-x`), new files/dirs created inside inherit the directory's group.

### 8. Ownership

**Concept:**
Every file/directory has one owner (user) and one group owner. These determine which permission set (user, group, other) applies to a user trying to access the file.

**Changing Ownership (`chown`):**
Changes the user owner of a file/directory. Requires appropriate privileges (usually root, or file owner under specific system policies).
*   **Syntax:** `chown <new_owner> <file(s)>`
*   **Example:** `chown alice report.txt`

**Changing Group Ownership (`chgrp`):**
Changes the group owner of a file/directory. Requires appropriate privileges (usually file owner belonging to the target group, or root).
*   **Syntax:** `chgrp <new_group> <file(s)>`
*   **Example:** `chgrp project-a report.txt`

### 9. Basic File/Directory Commands

*   **`ls`**: Lists directory contents. Options: `-l` (long), `-a` (all/hidden).
*   **`cat`**: Concatenate and display files. Options: `-b` (number non-blank lines). Used also for creation (`>`) and appending (`>>`).
*   **`cp`**: Copy files/directories. Option: `-r` (recursive for directories).
*   **`mv`**: Move or rename files/directories.
*   **`rm`**: Remove files. Options: `-i` (interactive prompt), `-r` (recursive for directories - **CAUTION**).
*   **`mkdir`**: Make directories. Option: `-p` (create parent directories as needed).
*   **`rmdir`**: Remove empty directories.
*   **`pwd`**: Print Working Directory (show current location).
*   **`cd`**: Change Directory. Special args: `~` (home), `.` (current), `..` (parent), `-` (previous).

### 10. File Content Commands (`wc`)

*   **`wc`**: Word Count. Counts lines, words, and bytes/characters.
    *   `wc file.txt`: Shows lines, words, bytes, filename.
    *   `wc -l file.txt`: Count lines only.
    *   `wc -w file.txt`: Count words only.
    *   `wc -c file.txt`: Count bytes only.

### 11. Mounting/Unmounting

*   **`mount`**: Attaches a filesystem (e.g., from a device like `/dev/sdb1`) to a specified directory (mount point, e.g., `/mnt/usb`), making its contents accessible. Running `mount` without arguments lists currently mounted filesystems.
*   **`umount`**: Detaches a mounted filesystem. Specify either the device or the mount point. (Note: it's `umount`, not `unmount`).

### 12. Utility Commands

*   **`tty`**: Display terminal name connected to standard input.
*   **`cal`**: Display calendar (current month, specific month/year, or full year).
*   **`date`**: Display or set system date and time.
*   **`who`**: Show who is logged on (username, terminal, time).
*   **`whoami`**: Print effective user ID (current username).
*   **`users`**: Print usernames of currently logged-in users.
*   **`w`**: Show who is logged on and what they are doing (more detail than `who`).
*   **`finger`**: Display information about users (local or remote).

---

## Unit 3: Pipes, Filters & Redirection

### 13. Filters

**Definition & Purpose:**
A filter is a command that reads data from standard input, processes it (e.g., transforms, selects, counts), and writes the result to standard output. They are designed to be used in pipelines to perform complex data manipulation by chaining simple tools.

**Examples:** `grep`, `sort`, `head`, `tail`, `wc`, `cut`, `paste`, `uniq`, `tr`, `sed`, `awk`, `more`, `less`.

### 14. Piping

**Concept:**
Piping uses the vertical bar (`|`) symbol to connect the standard output of one command directly to the standard input of the next command, creating a data processing pipeline.

**Example:** `ls -l | grep 'Aug' | sort -k 5n | head -n 5` (List files -> Filter for 'Aug' -> Sort by size (field 5, numeric) -> Show top 5 largest).

### 15. Redirection

**Concept:**
Changing the default source of standard input or the default destination of standard output/error.

**Operators:**
*   `< file`: Redirect standard input from `file`.
*   `> file`: Redirect standard output to `file` (overwrites).
*   `>> file`: Redirect standard output to `file` (appends).
*   `2> file`: Redirect standard error (fd 2) to `file`.
*   `&> file` or `> file 2>&1`: Redirect both stdout and stderr to `file`.
*   `<< DELIMITER`: "Here Document". Redirects lines following the command (until `DELIMITER`) as stdin.

**Diagram: I/O Redirection Concept**

<img src="https://github.com/43H1-BOI/4th_End_Sem/blob/main/UnixOS/images/placeholder_io_redirection.png" width="500" height="300">

*(Illustrates keyboard as default stdin, monitor as default stdout/stderr, and redirection to/from files).*

### 16. `grep` Command

**Purpose:** Searches input for lines matching a pattern (regular expression).

**Syntax:** `grep [options] pattern [file...]`

**Options:**
*   `-i`: Ignore case.
*   `-n`: Show line numbers.
*   `-v`: Invert match (show non-matching lines).
*   `-c`: Count matching lines.
*   `-l`: List filenames with matches.
*   `-r`, `-R`: Recursive search.
*   `-E`: Use Extended Regular Expressions (`egrep`).
*   `-F`: Use Fixed strings (`fgrep`).

**`egrep` vs `fgrep`:**
*   `egrep` (`grep -E`): Faster for complex patterns using ERE metacharacters (`+`, `?`, `|`, `()).
*   `fgrep` (`grep -F`): Fastest for literal string searches, treats all characters literally.

### 17. `head`/`tail` Commands

*   **`head`**: Display first N lines (default 10). Option `-n N` or `-N`.
*   **`tail`**: Display last N lines (default 10). Option `-n N` or `-N`. Option `-f` to follow file changes.

### 18. `sort` Command

**Purpose:** Sorts lines of text.

**Options:**
*   `-n`: Numeric sort.
*   `-r`: Reverse order.
*   `-f`: Fold case (ignore case).
*   `-u`: Unique (output only first of identical lines).
*   `-k N`: Sort on field N (fields separated by whitespace).
*   `-t CHAR`: Use CHAR as field separator (with `-k`).

### 19. `pg`/`more` Commands

**Purpose:** Display output one screenful at a time (pagers). `more` is common, `less` is often preferred.

**Usage:** `command | more` or `more filename`. Navigate with Spacebar (page), Enter (line), `q` (quit).

---

## Unit 4: Process Management

### 20. Process Concepts

*   **Process:** A running instance of a program, with its own PID, memory space, and resources.
*   **Parent/Child:** A process that creates another (`fork()) is the parent; the new one is the child.
*   **Process States:** Processes transition between various states during their lifecycle. Key states include:
    *   **New/Created:** Process is being created.
    *   **Ready:** Waiting to be assigned to a processor.
    *   **Running:** Instructions are being executed.
    *   **Waiting/Blocked/Asleep:** Waiting for some event (e.g., I/O completion).
    *   **Terminated:** Process has finished execution.
    *   **Zombie:** Terminated, but waiting for parent to collect exit status.

    **Diagram: Process State Model**

    <img src="https://github.com/43H1-BOI/4th_End_Sem/blob/main/UnixOS/images/placeholder_process_states.jpg" width="500" height="300">

    *(Illustrates transitions between New, Ready, Running, Waiting, Terminated states).*

*   **Zombie Process:** A terminated process whose parent hasn't read its exit status yet; shown as `<defunct>` or `Z`.
*   **Orphan Process:** A process whose parent terminated; adopted by `init` (PID 1).
*   **Daemon Process:** A system background process, no controlling terminal (`tty` is `?`), often runs as root, provides services.

### 21. Process Creation & Management

**Creation:** Typically via `fork() (create copy) followed by `exec() (replace program image). The parent can `wait() for the child to finish.

**Diagram: Process Creation (Fork/Exec)**

<img src="https://github.com/43H1-BOI/4th_End_Sem/blob/main/UnixOS/images/placeholder_process_creation.jpg" width="500" height="300">

*(Shows shell -> fork -> child -> exec -> new program -> exit -> parent potentially waiting).*

**Management:** Kernel handles scheduling (CPU time), memory allocation, tracking state (PID, PPID, status), IPC, termination.

### 22. Foreground/Background Processes

*   **Foreground:** Runs interactively, attached to terminal, shell waits. Default execution.
*   **Background:** Runs detached from terminal, shell returns prompt immediately. Started with `&`.

### 23. Process Status (`ps`) Command

**Purpose:** Display information about active processes.

**Options:**
*   (No options): User's processes on current terminal.
*   `-f`: Full format listing (UID, PID, PPID, C, STIME, TTY, TIME, CMD).
*   `-e`: All processes system-wide.
*   `-a`: All users' processes, including those without terminals (BSD style often `aux`).
*   `-u user`: Processes for specific user.
*   `-l`: Long format (more details like state S, priority PRI).

### 24. Stopping Processes (`kill`) Command

**Purpose:** Send signals to processes, usually to terminate them.

**Syntax:** `kill [-signal] PID|%JobId`
*   `kill PID`: Send default SIGTERM (15) - polite request to terminate.
*   `kill -9 PID`: Send SIGKILL (9) - forceful termination.
*   `kill %JobId`: Send signal to background job number.

**Job ID vs PID:**
*   PID: Unique System-wide Process ID.
*   Job ID: Shell-specific number (`%1`, `%2`) for background/stopped jobs in that shell.

### 25. Process Monitoring (`top`) Command

**Purpose:** Dynamic real-time view of running processes, sorted by usage (CPU default). Interactive.

**Usage:** Type `top`, use keys like `q` (quit), `k` (kill), `M` (sort memory), `P` (sort CPU).

---

## Unit 5: Shell Programming & Environment

### 26. Shell Basics

*   **Shell:** Command-line interpreter, interface to kernel.
*   **Types:** `sh`, `bash` (common Linux default), `csh`, `ksh`, `tcsh`.
*   **Prompt:** PS1 (primary, e.g., `$`), PS2 (secondary, e.g., `>`).
*   **Comments:** `#` denotes a comment (except for `#!` shebang).

### 27. Shell Scripts

*   **Definition:** Text file with shell commands, executed sequentially.
*   **Shebang:** First line `#!/path/to/shell` specifies interpreter.
*   **Execution:** `chmod +x script.sh` then `./script.sh` OR `sh script.sh`.

### 28. Shell Variables

*   **Environment Vars:** System/Shell defined, UPPERCASE convention, inherited. `HOME`, `PATH`, `USER`, `PS1`, `TERM`.
*   **User-Defined Vars:** Script/User defined, lowercase/mixed convention.
*   **Define:** `VARNAME="value"` (no spaces around `=`).
*   **Access:** `$VARNAME` or `${VARNAME}`.
*   **Read-only:** `readonly VARNAME`.
*   **Unset:** `unset VARNAME`.

### 29. Input (`read`) Command

**Purpose:** Read user input from stdin into variable(s).
**Syntax:** `read var1 [var2...]`

### 30. Shell Operators

*   **Arithmetic:** `` `expr OP1 + OP2` `` or `$((OP1 + OP2)). Operators: `+ - \* / %`. (`*` needs escaping in `expr`).
*   **Relational (Numeric):** Within `[ ]`: `-eq`, `-ne`, `-gt`, `-lt`, `-ge`, `-le`.
*   **Boolean:** Within `[ ]`: `!` (not), `-a` (and), `-o` (or).
*   **String:** Within `[ ]`: `=` (equal), `!=` (not equal), `-z` (zero length), `-n` (non-zero length). Use quotes: `[ "$a" = "$b" ]`.
*   **File Test:** Within `[ ]`: `-e` (exists), `-f` (is file), `-d` (is directory), `-r` (readable), `-w` (writable), `-x` (executable), `-s` (size > 0), `-L` (is link), `f1 -nt f2` (newer than), `f1 -ot f2` (older than).

### 31. Shell Control Flow

*   **`if` Statements:**
    *   `if [ cond ]; then ... fi`
    *   `if [ cond ]; then ... else ... fi`
    *   `if [ cond1 ]; then ... elif [ cond2 ]; then ... else ... fi`
*   **`case` Statement:** Matches variable against patterns.
    ```bash
    case "$var" in
      pat1) cmd ;;
      pat2) cmd ;;
      *) default_cmd ;;
    esac
    ```
*   **`while` Loop:** Repeats while condition is true (tests before loop).
    ```bash
    while [ cond ]; do ... done
    ```
*   **`for` Loop:** Iterates over a list of items.
    ```bash
    for i in item1 item2 ...; do ... done
    for f in *.txt; do ... done
    ```
*   **`until` Loop:** Repeats while condition is false (tests before loop).
    ```bash
    until [ cond ]; do ... done
    ```
*   **Loop Control:** `break` (exit loop), `continue` (next iteration).

### 32. Metacharacters (Wildcards) & Quoting

*   **Metacharacters (Globbing):** `*` (0+ chars), `?` (1 char), `[...]` (any char in set). For filename expansion.
*   **Quoting:**
    *   `'...'` (Single Quotes): Literal. No substitutions. Strongest.
    *   `"..."` (Double Quotes): Allows `$var`, `` `cmd` ``, `$(cmd), `\`. Weak.
    *   `\` (Backslash): Escape next character.
    *   `` `cmd` `` or `$(cmd) (Command Substitution): Replace with command output.

### 33. Unix Environment

*   **Concept:** Set of variables defining user session settings.
*   **Initialization:** `/etc/profile` (system-wide), `~/.profile` (user-specific) read at login (for Bourne-type shells).
*   **`PATH` Variable:** Colon-separated list of directories searched for commands. View with `echo $PATH`. Set with `export PATH="$PATH:/new/path"`.

---

## Unit 6: `vi` Editor

### 34. `vi` Editor Basics

*   **Modes:**
    *   **Command (Normal):** Default. Navigation, commands (`Esc` to enter).
    *   **Insert:** Enter text (`i, a, o, O` to enter).
    *   **Last Line (Ex):** Commands at bottom (`:` to enter).
*   **Navigation:** `h, j, k, l`, `w`, `b`, `0`, `$`, `G`, `gg`.
*   **Saving/Quitting:** `:w` (save), `:q` (quit), `:q!` (force quit), `:wq` or `:x` or `ZZ` (save & quit).
*   **Editing:** `x` (delete char), `dd` (delete line), `dw` (delete word), `yy` (copy line), `yw` (copy word), `p`/`P` (paste after/before).
*   **Searching:** `/pattern` (forward), `?pattern` (backward), `n`/`N` (next/prev match).

---

## Unit 7: User Administration

### 35. User/Group Management

*   **Users:** Accounts identified by username and UID (`/etc/passwd`, `/etc/shadow`).
*   **Groups:** Collections of users identified by group name and GID (`/etc/group`).
*   **Commands (require root):**
    *   `groupadd <group>`: Create group.
    *   `groupdel <group>`: Delete group.
    *   `useradd [options] <user>`: Create user (use `passwd <user>` after).
    *   `userdel [-r] <user>`: Delete user (`-r` removes home dir).
    *   `usermod`, `groupmod`: Modify existing users/groups.

---

**Topics Not Covered by Provided PDFs:**

*   `man -k`, `apropos` commands.
*   `sudo` command details (configuration, privilege checking).
