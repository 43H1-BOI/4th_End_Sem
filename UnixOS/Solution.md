# UNIX Operating System Q&A

*Source Material: Based on questions from provided exam papers and answers derived from `unix_notes.pdf` and `unix_tutorial.pdf` within the repository.*

---

## Unit 1: Introduction to OS & UNIX

### 1. OS & UNIX Definition and Architecture

**Operating System (OS) Definition:**
An Operating System is fundamental system software that manages a computer's hardware and software resources. It acts as an intermediary between the user/applications and the physical hardware, providing essential services like process management, memory management, file systems, and device control. The core component is the **kernel**.
*(Source: UnixOS/unix_notes.pdf Pg 1; UnixOS/unix_tutorial.pdf Pg 9)*

**UNIX Definition:**
UNIX is a highly influential operating system family, known for being portable, multitasking, and multiuser. Developed at Bell Labs starting in 1969, it allows multiple users to run multiple programs concurrently. Linux is a popular, open-source Unix-like operating system kernel.
*(Source: UnixOS/unix_notes.pdf Pg 1, 2; UnixOS/unix_tutorial.pdf Pg 2, 9)*

**UNIX Architecture:**
The typical layered architecture includes:

1.  **Hardware:** The physical machine components.
2.  **Kernel:** The core of the OS, directly managing hardware, scheduling tasks, handling memory, and providing system calls.
3.  **Shell:** The command-line interpreter (CLI) acting as the user's interface to the kernel. It parses commands, manages jobs, and executes programs. Examples: `sh`, `bash`, `csh`, `ksh`.
4.  **Application Programs / Commands & Utilities:** User-level software tools (`ls`, `vi`, `cc`, etc.) and applications that utilize the shell and kernel services.

*(Source: UnixOS/unix_notes.pdf Pg 3, 4; UnixOS/unix_tutorial.pdf Pg 2, 10, 11)*
*Diagram Reference: UnixOS/unix_notes.pdf Pg 3; UnixOS/unix_tutorial.pdf Pg 11*

### 2. UNIX Features & Advantages

Key characteristics and benefits of UNIX:

*   **Multiuser:** Allows simultaneous access for multiple users. *(Source: UnixOS/unix_notes.pdf Pg 1, 4; UnixOS/unix_tutorial.pdf Pg 9)*
*   **Multitasking:** Supports concurrent execution of multiple programs/processes. *(Source: UnixOS/unix_notes.pdf Pg 1, 4; UnixOS/unix_tutorial.pdf Pg 9)*
*   **Portability:** Designed to be relatively easily moved to different hardware platforms. *(Source: UnixOS/unix_notes.pdf Pg 4; UnixOS/unix_tutorial.pdf Pg 2)*
*   **Hierarchical File System:** Organizes data in a logical tree structure (`/`). *(Source: UnixOS/unix_notes.pdf Pg 4; UnixOS/unix_tutorial.pdf Pg 10, 16, 24)*
*   **Powerful Shell:** Offers versatile CLI for interaction and scripting. *(Source: UnixOS/unix_notes.pdf Pg 4; UnixOS/unix_tutorial.pdf Pg 11, 64)*
*   **Rich Utilities:** Provides numerous small, focused command-line tools. *(Source: UnixOS/unix_notes.pdf Pg 4; UnixOS/unix_tutorial.pdf Pg 11, 131)*
*   **Pipes and Filters:** Allows chaining commands for complex data processing. *(Source: UnixOS/unix_notes.pdf Pg 4; UnixOS/unix_tutorial.pdf Pg 47)*
*   **Security:** Features user/group-based permissions for access control. *(Source: UnixOS/unix_notes.pdf Pg 1, 4; UnixOS/unix_tutorial.pdf Pg 20, 30)*
*   **Networking:** Strong built-in networking support. *(Source: UnixOS/unix_notes.pdf Pg 2; UnixOS/unix_tutorial.pdf Pg 46, 135)*

### 3. UNIX vs. Windows

| Feature           | UNIX (Typical/Linux)             | Windows                            | Source Ref ([Notes]) |
| :---------------- | :------------------------------- | :--------------------------------- | :------------------- |
| **Source**        | Often Open Source (Free)         | Proprietary (Paid)                 | Pg 2, 3              |
| **UI**            | CLI (Shell) primary, GUI optional| GUI primary, CLI available       | Pg 2, 3              |
| **Security**      | High, granular control         | Lower (historically), improving  | Pg 2, 3              |
| **Tasking**       | Multitasking                     | Multitasking                       | Pg 2                 |
| **Users**         | Multiuser native                 | Multiuser (Server), often single   | Pg 2                 |
| **Case Sensitive**| Yes                              | No (filenames)                     | Pg 2                 |
| **File System**   | Single Root Hierarchy (`/`)      | Drive-based Hierarchy (C:, D:)   | Pg 3                 |
| **Customization** | High                             | Lower                              | Pg 3                 |
| **Portability**   | High                             | Limited                            | Pg 2                 |

### 4. Command Execution Flow

1.  **Prompt:** Shell signals readiness (`$`, `%`, etc.).
2.  **Input:** User types command + arguments, presses Enter.
3.  **Parsing:** Shell reads line, separates command/args, interprets special chars (`*`, `|`, `>`, `$`, `` ` ``).
4.  **Expansion:** Shell performs variable (`$VAR`), command (`$(cmd)`), filename (`*.txt`) expansions.
5.  **Search:** Shell checks if command is built-in. If not, searches directories in `$PATH` for the executable.
6.  **Fork:** Shell creates a child process (copy of itself).
7.  **Setup:** Child process sets up I/O redirection/pipes as needed.
8.  **Exec:** Child process replaces itself with the command's program code.
9.  **Execution:** Kernel runs the command process.
10. **Output:** Command sends output/errors (usually to terminal via shell, unless redirected).
11. **Wait:** Shell waits for foreground command completion.
12. **Return:** Shell displays prompt again.

*(Source: UnixOS/unix_notes.pdf Pg 4; UnixOS/unix_tutorial.pdf Pg 11, 64, command execution principles)*

---

## Unit 2: UNIX File System & Management

### 5. File System Structure & Hierarchy

**Concept:**
The UNIX file system organizes all data (files, directories, devices) in a unified structure, typically starting from a single root. Everything is treated as a file.
*(Source: UnixOS/unix_notes.pdf Pg 7; UnixOS/unix_tutorial.pdf Pg 10, 16, 154)*

**Structure:**
A hierarchical tree:
*   **Root (`/`):** The top-level directory.
*   **Directories:** Containers for files and other directories.
*   **Pathnames:** Unique addresses for files/directories.
    *   *Absolute:* Start from `/` (e.g., `/usr/bin/ls`).
    *   *Relative:* Start from the current directory (e.g., `../docs/file.txt`).

*(Source: UnixOS/unix_notes.pdf Pg 10; UnixOS/unix_tutorial.pdf Pg 10, 16, 24, 154)*

**Key Directories:** See list in previous answer.
*(Source: UnixOS/unix_notes.pdf Pg 10; UnixOS/unix_tutorial.pdf Pg 154)*

### 6. File Types & Attributes

**Attributes (`ls -l` output):**
File Type, Permissions, Link Count, Owner, Group, Size, Modification Time, Name.
*(Source: UnixOS/unix_notes.pdf Pg 8, 11, 37; UnixOS/unix_tutorial.pdf Pg 17, 18, 30)*

**Types (First char of `ls -l`):**
*   `-`: Ordinary File (Text or Binary)
*   `d`: Directory
*   `l`: Symbolic Link
*   `b`: Block Special File (Device)
*   `c`: Character Special File (Device)
*   `p`: Named Pipe (FIFO)
*   `s`: Socket
*(Source: UnixOS/unix_notes.pdf Pg 9; UnixOS/unix_tutorial.pdf Pg 18)*

**Hidden Files:** Names start with `.`, use `ls -a` to view. For configuration.
*(Source: UnixOS/unix_notes.pdf Pg 9, 11; UnixOS/unix_tutorial.pdf Pg 19)*

### 7. Permissions & Modes

**Categories:** User (`u`), Group (`g`), Other (`o`), All (`a`).
*(Source: UnixOS/unix_notes.pdf Pg 8, 10, 37; UnixOS/unix_tutorial.pdf Pg 20, 30)*

**Types:** Read (`r`/4), Write (`w`/2), Execute (`x`/1). Meaning differs slightly for files vs. directories.
*(Source: UnixOS/unix_notes.pdf Pg 8, 37; UnixOS/unix_tutorial.pdf Pg 20, 30, 31)*

**Viewing:** `ls -l` (shows `rwx` for u, g, o).
*(Source: UnixOS/unix_notes.pdf Pg 11, 37, 38; UnixOS/unix_tutorial.pdf Pg 17, 30)*

**Changing (`chmod`):**
*   **Symbolic:** `chmod [ugoa][+-=][rwx] file` (e.g., `chmod g+w data.txt`).
    *(Source: UnixOS/unix_notes.pdf Pg 38; UnixOS/unix_tutorial.pdf Pg 21, 31)*
*   **Octal (Absolute):** `chmod NNN file` where N is sum of r=4, w=2, x=1 for user, group, other (e.g., `chmod 755 script.sh`).
    *(Source: UnixOS/unix_notes.pdf Pg 38; UnixOS/unix_tutorial.pdf Pg 22, 32)*

**SUID/SGID:** Special permissions (`s` in execute field) allowing temporary privilege escalation based on file owner/group.
*(Source: UnixOS/unix_tutorial.pdf Pg 24, 34, 35)*

### 8. Ownership

**Concept:** Each file/directory belongs to one user (owner) and one group.
*(Source: UnixOS/unix_tutorial.pdf Pg 23, 33)*

**Changing:**
*   `chown <new_owner> <file>`: Change user owner (usually needs root).
*   `chgrp <new_group> <file>`: Change group owner (usually needs owner permission & group membership, or root).
*(Source: UnixOS/unix_tutorial.pdf Pg 23, 24, 33, 34)*

### 9. Basic File/Directory Commands

*   **`ls`**: List contents (`-l`, `-a`). *(Source: UnixOS/unix_notes.pdf Pg 11; UnixOS/unix_tutorial.pdf Pg 16, 17, 19)*
*   **`cat`**: Display/Combine/Create files (`>`, `>>`, `-b`). *(Source: UnixOS/unix_notes.pdf Pg 11-13; UnixOS/unix_tutorial.pdf Pg 20, 21)*
*   **`cp`**: Copy (`-r` for directories). *(Source: UnixOS/unix_tutorial.pdf Pg 13, 21)*
*   **`mv`**: Move/Rename. *(Source: UnixOS/unix_tutorial.pdf Pg 13, 22, 28)*
*   **`rm`**: Remove files (`-i` prompt, `-r` recursive - **CAUTION**). *(Source: UnixOS/unix_tutorial.pdf Pg 13, 22)*
*   **`mkdir`**: Make directory (`-p` parents). *(Source: UnixOS/unix_notes.pdf Pg 18; UnixOS/unix_tutorial.pdf Pg 16, 26, 27)*
*   **`rmdir`**: Remove *empty* directory. *(Source: UnixOS/unix_notes.pdf Pg 18; UnixOS/unix_tutorial.pdf Pg 18, 27)*
*   **`pwd`**: Print Working Directory. *(Source: UnixOS/unix_notes.pdf Pg 17; UnixOS/unix_tutorial.pdf Pg 25)*
*   **`cd`**: Change Directory (`~`, `.`, `..`, `-`). *(Source: UnixOS/unix_notes.pdf Pg 18; UnixOS/unix_tutorial.pdf Pg 18, 24, 25, 27)*

### 10. File Content Commands (`wc`)

*   **`wc`**: Counts lines (`-l`), words (`-w`), bytes (`-c`).
*(Source: UnixOS/unix_notes.pdf Pg 39; UnixOS/unix_tutorial.pdf Pg 12, 21)*

### 11. Mounting/Unmounting

*   **`mount`**: Attach a filesystem to a mount point directory. *(Source: UnixOS/unix_tutorial.pdf Pg 158)*
*   **`umount`**: Detach a filesystem. *(Source: UnixOS/unix_tutorial.pdf Pg 159)*

### 12. Utility Commands

*   **`tty`**: Show terminal device name. *(Source: UnixOS/unix_notes.pdf Pg 14)*
*   **`cal`**: Show calendar. *(Source: UnixOS/unix_notes.pdf Pg 13; UnixOS/unix_tutorial.pdf Pg 11)*
*   **`date`**: Show/set date and time. *(Source: UnixOS/unix_notes.pdf Pg 13)*
*   **`whoami`**: Show current username. *(Source: UnixOS/unix_notes.pdf Pg 14; UnixOS/unix_tutorial.pdf Pg 13)*
*   **`who`**: Show logged-in users, terminal, time. *(Source: UnixOS/unix_notes.pdf Pg 14; UnixOS/unix_tutorial.pdf Pg 14)*
*   **`users`**: List logged-in usernames. *(Source: UnixOS/unix_tutorial.pdf Pg 13)*
*   **`w`**: Show who is logged on and what they're doing. *(Source: UnixOS/unix_tutorial.pdf Pg 14)*
*   **`finger`**: Show user information (local/remote). *(Source: UnixOS/unix_tutorial.pdf Pg 50, 62)*

---

## Unit 3: Pipes, Filters & Redirection

### 13. Filters

**Definition:** Commands reading from stdin, processing, and writing to stdout. Used in pipelines.
*(Source: UnixOS/unix_notes.pdf Pg 20; UnixOS/unix_tutorial.pdf Pg 37, 47)*
**Examples:** `grep`, `sort`, `wc`, `head`, `tail`, `tr`, `cut`, `paste`, `uniq`, `sed`, `awk`, `more`.

### 14. Piping

**Concept:** Use `|` to send stdout of `cmd1` to stdin of `cmd2`.
*(Source: UnixOS/unix_notes.pdf Pg 20; UnixOS/unix_tutorial.pdf Pg 37, 47)*
**Example:** `ls -l | grep ".sh"`

### 15. Redirection

**Concept:** Change default input/output streams.
*(Source: UnixOS/unix_notes.pdf Pg 19; UnixOS/unix_tutorial.pdf Pg 23, 121)*
**Operators:**
*   `< file`: Stdin from file. *(Source: UnixOS/unix_tutorial.pdf Pg 122)*
*   `> file`: Stdout to file (overwrite). *(Source: UnixOS/unix_tutorial.pdf Pg 121)*
*   `>> file`: Stdout to file (append). *(Source: UnixOS/unix_tutorial.pdf Pg 121)*
*   `2> file`: Stderr to file. *(Source: UnixOS/unix_tutorial.pdf Pg 125)*
*   `&> file` or `> file 2>&1`: Stdout & Stderr to file. *(Source: UnixOS/unix_tutorial.pdf Pg 125)*
*   `<< DELIM`: Here Document (stdin from script lines until DELIM). *(Source: UnixOS/unix_tutorial.pdf Pg 122)*

### 16. `grep` Command

**Purpose:** Search input for pattern matches.
*(Source: UnixOS/unix_notes.pdf Pg 41; UnixOS/unix_tutorial.pdf Pg 37, 47)*
**Options:** `-i` (ignore case), `-n` (line numbers), `-v` (invert), `-c` (count), `-l` (filenames), `-r`/`-R` (recursive), `-E` (egrep), `-F` (fgrep).
*(Source: UnixOS/unix_notes.pdf Pg 41; UnixOS/unix_tutorial.pdf Pg 48)*
**`egrep` vs `fgrep`:** `egrep` uses extended regex (faster complex), `fgrep` uses fixed strings (fastest literal).
*(Source: UnixOS/unix_notes.pdf Pg 23, 24)*

### 17. `head`/`tail` Commands

*   **`head [-n N]`**: Show first N lines (default 10). *(Source: UnixOS/unix_notes.pdf Pg 38)*
*   **`tail [-n N] [-f]`**: Show last N lines (default 10); `-f` follows updates. *(Source: UnixOS/unix_notes.pdf Pg 39)*

### 18. `sort` Command

**Purpose:** Sort lines alphanumerically.
*(Source: UnixOS/unix_notes.pdf Pg 40; UnixOS/unix_tutorial.pdf Pg 38, 49)*
**Options:** `-n` (numeric), `-r` (reverse), `-f` (ignore case), `-u` (unique), `-k N` (sort key field N), `-t C` (field separator C).
*(Source: UnixOS/unix_notes.pdf Pg 41; UnixOS/unix_tutorial.pdf Pg 49)*

### 19. `pg`/`more` Commands

**Purpose:** Paginate output (view screen by screen).
*(Source: UnixOS/unix_tutorial.pdf Pg 39, 50)*
**Usage:** `command | more` or `more file`. Navigate: Spacebar, Enter, `q`.

---

## Unit 4: Process Management

### 20. Process Concepts

*   **Process:** Running program instance (PID, memory). *(Source: UnixOS/unix_notes.pdf Pg 27; UnixOS/unix_tutorial.pdf Pg 41, 51)*
*   **Parent/Child:** Creator/Created process (PPID). *(Source: UnixOS/unix_notes.pdf Pg 27; UnixOS/unix_tutorial.pdf Pg 44, 55)*
*   **Zombie:** Terminated but not 'reaped' by parent (`<defunct>`). *(Source: UnixOS/unix_notes.pdf Pg 29; UnixOS/unix_tutorial.pdf Pg 44, 55)*
*   **Orphan:** Parent terminated first; adopted by `init`. *(Source: UnixOS/unix_tutorial.pdf Pg 44, 55)*
*   **Daemon:** System background service (no terminal). *(Source: UnixOS/unix_notes.pdf Pg 32; UnixOS/unix_tutorial.pdf Pg 45, 55)*

### 21. Process Creation & Management

**Creation:** `fork()` (creates copy) + `exec()` (replaces image). *(Source: UnixOS/unix_notes.pdf Pg 30)*
**Management:** Kernel handles scheduling, memory, state tracking (PID, PPID, status), IPC, termination. *(Source: UnixOS/unix_notes.pdf Pg 1; UnixOS/unix_tutorial.pdf Pg 10)*

### 22. Foreground/Background Processes

*   **Foreground:** Interactive, attached to terminal, shell waits. *(Source: UnixOS/unix_notes.pdf Pg 31; UnixOS/unix_tutorial.pdf Pg 41, 52)*
*   **Background:** Detached, non-interactive input, shell continues. Use `&`. *(Source: UnixOS/unix_notes.pdf Pg 31; UnixOS/unix_tutorial.pdf Pg 42, 52)*

### 23. Process Status (`ps`) Command

**Purpose:** Show running processes.
*(Source: UnixOS/unix_notes.pdf Pg 30; UnixOS/unix_tutorial.pdf Pg 42, 53)*
**Options:** `-f` (full), `-e` (all), `-l` (long), `-u user`, `aux` (BSD style).
*(Source: UnixOS/unix_tutorial.pdf Pg 53, 54)*

### 24. Stopping Processes (`kill`) Command

**Purpose:** Send signals (default SIGTERM 15) to terminate.
*(Source: UnixOS/unix_notes.pdf Pg 34; UnixOS/unix_tutorial.pdf Pg 44, 54)*
**Usage:** `kill PID` (terminate), `kill -9 PID` (force kill), `kill %JobId`.
**Job ID vs PID:** Job ID is shell-local (`%1`), PID is system-wide. *(Source: UnixOS/unix_tutorial.pdf Pg 45, 56)*

### 25. Process Monitoring (`top`) Command

**Purpose:** Real-time interactive process viewer (CPU/Mem usage).
*(Source: UnixOS/unix_tutorial.pdf Pg 45, 55)*
**Usage:** `top`. Interactive keys: `q`, `k`, `M`, `P`.

---

## Unit 5: Shell Programming & Environment

### 26. Shell Basics

*   **Shell:** CLI, interface to kernel. *(Source: UnixOS/unix_notes.pdf Pg 3, 47; UnixOS/unix_tutorial.pdf Pg 10, 64)*
*   **Types:** `sh`, `bash`, `csh`, `ksh`. *(Source: UnixOS/unix_notes.pdf Pg 4, 47; UnixOS/unix_tutorial.pdf Pg 11, 64)*
*   **Prompt:** PS1 (main), PS2 (continuation). *(Source: UnixOS/unix_notes.pdf Pg 50; UnixOS/unix_tutorial.pdf Pg 28, 38, 64)*
*   **Comments:** `#` ignored (except `#!`). *(Source: UnixOS/unix_notes.pdf Pg 49; UnixOS/unix_tutorial.pdf Pg 66)*

### 27. Shell Scripts

*   **Definition:** File with shell commands. *(Source: UnixOS/unix_notes.pdf Pg 48; UnixOS/unix_tutorial.pdf Pg 65)*
*   **Shebang:** `#!/bin/sh` (or other shell) on first line. *(Source: UnixOS/unix_notes.pdf Pg 48; UnixOS/unix_tutorial.pdf Pg 65)*
*   **Execution:** Make executable (`chmod +x`) then `./script` OR `sh script`. *(Source: UnixOS/unix_notes.pdf Pg 49; UnixOS/unix_tutorial.pdf Pg 65)*

### 28. Shell Variables

*   **Environment:** System-wide/inherited (`PATH`, `HOME`). UPPERCASE. *(Source: UnixOS/unix_notes.pdf Pg 50; UnixOS/unix_tutorial.pdf Pg 30, 41, 68)*
*   **User-Defined:** Local to script/shell. *(Source: UnixOS/unix_notes.pdf Pg 50; UnixOS/unix_tutorial.pdf Pg 68)*
*   **Define:** `NAME="Value"`. *(Source: UnixOS/unix_notes.pdf Pg 50; UnixOS/unix_tutorial.pdf Pg 68)*
*   **Access:** `$NAME` or `${NAME}`. *(Source: UnixOS/unix_notes.pdf Pg 51; UnixOS/unix_tutorial.pdf Pg 37, 69)*
*   **Read-only:** `readonly NAME`. *(Source: UnixOS/unix_notes.pdf Pg 51; UnixOS/unix_tutorial.pdf Pg 69)*
*   **Unset:** `unset NAME`. *(Source: UnixOS/unix_notes.pdf Pg 51; UnixOS/unix_tutorial.pdf Pg 70)*

### 29. Input (`read`) Command

**Purpose:** Read user input into variables.
*(Source: UnixOS/unix_notes.pdf Pg 52)*
**Syntax:** `read var1 [var2...]`

### 30. Shell Operators

*(Source: UnixOS/unix_notes.pdf Pg 53-55; UnixOS/unix_tutorial.pdf Pg 77-93)*
*   **Arithmetic:** `expr ...` or `$((...))`. Ops: `+ - \* / %`.
*   **Relational (Num):** `[ $a -eq $b ]`, `-ne`, `-gt`, `-lt`, `-ge`, `-le`.
*   **Boolean:** `[ ! expr ]`, `[ expr1 -a expr2 ]`, `[ expr1 -o expr2 ]`.
*   **String:** `[ "$a" = "$b" ]`, `!=`, `-z` (empty), `-n` (not empty).
*   **File Test:** `[ -f file ]` (file), `[ -d dir ]` (directory), `[ -r file ]` (readable), `[ -w file ]` (writable), `[ -x file ]` (executable), `[ -s file ]` (not empty), `[ -e file ]` (exists).

### 31. Shell Control Flow

*(Source: UnixOS/unix_notes.pdf Pg 56-60; UnixOS/unix_tutorial.pdf Pg 94-112)*
*   **`if`:** `if [ cond ]; then ... fi`, `if...else...fi`, `if...elif...else...fi`.
*   **`case`:** `case "$var" in pat1) ... ;; pat2) ... ;; *) ... ;; esac`.
*   **`while`:** `while [ cond ]; do ... done`.
*   **`for`:** `for var in list; do ... done`.
*   **`until`:** `until [ cond ]; do ... done`.
*   **Control:** `break` (exit loop), `continue` (next iteration).

### 32. Metacharacters (Wildcards) & Quoting

*   **Wildcards (Globbing):** `*` (any string), `?` (any char), `[...]` (char set/range). For filename expansion. *(Source: UnixOS/unix_notes.pdf Pg 9-metachar context; UnixOS/unix_tutorial.pdf Pg 10, 19, 117)*
*   **Quoting:** Controls interpretation.
    *   `'...'`: Literal (strong).
    *   `"..."`: Allows `$var`, `$(cmd)`, `` `cmd` ``, `\` escapes (weak).
    *   `\`: Escapes next character.
    *   `` `cmd` `` or `$(cmd)`: Command substitution (replace with output).
*(Source: UnixOS/unix_tutorial.pdf Pg 118-120)*

### 33. Unix Environment

*   **Concept:** Session settings via environment variables. *(Source: UnixOS/unix_tutorial.pdf Pg 26, 37)*
*   **Initialization Files:** `/etc/profile` (global), `~/.profile` or `~/.bash_profile` (user login). *(Source: UnixOS/unix_tutorial.pdf Pg 27, 37)*
*   **`PATH` Variable:** Directories searched for commands. `echo $PATH`, `export PATH="$PATH:/new"`. *(Source: UnixOS/unix_notes.pdf Pg 50; UnixOS/unix_tutorial.pdf Pg 27, 38, 41)*

---

## Unit 6: `vi` Editor

### 34. `vi` Editor Basics

*(Source: UnixOS/unix_notes.pdf Pg 20-21; UnixOS/unix_tutorial.pdf Pg 52-62)*
*   **Modes:** Command (default, `Esc`), Insert (`i, a, o, O`), Last Line/Ex (`:`).
*   **Navigation:** `h, j, k, l` (arrows often work), `w, b, 0, $`, `G, gg`.
*   **Saving/Quitting:** `:w`, `:q`, `:q!`, `:wq`, `:x`, `ZZ`.
*   **Editing:** `x` (del char), `dd` (del line), `dw` (del word), `yy` (copy line), `yw` (copy word), `p/P` (paste).
*   **Searching:** `/pattern` (forward), `?pattern` (backward), `n/N` (next/prev).

---

## Unit 7: User Administration

### 35. User/Group Management

*(Source: UnixOS/unix_tutorial.pdf Pg 161-165)*
*   **Users:** Accounts (`/etc/passwd`, `/etc/shadow`). UID.
*   **Groups:** Collections of users (`/etc/group`). GID.
*   **Commands (Root often needed):**
    *   `groupadd`, `groupdel`
    *   `useradd`, `userdel` (use `passwd` after `useradd`)
    *   `usermod`, `groupmod` (modify existing)

---

**Topics Mentioned in Exams but NOT Covered by Provided Source PDFs:**

*   `man -k` command
*   `apropos` command
*   `sudo` command details (configuration, granting/checking specific rights).
