# **Linux Administration – Complete Interview Preparation & Revision Notes**

INTERVIEW-FOCUSED LEARNING MATERIAL • LINUX SYSTEM ADMINISTRATION • BEGINNER TO PRACTICAL LEVEL

I have used your mindmap as the foundation and refined it into proper Linux learning notes.

The objective is not just to memorize commands. You should understand:

1. What a particular command does.
2. Why and where we use it in real-world Linux administration.
3. How to use it with practical examples.
4. What interview questions can be asked from that topic.
5. How to troubleshoot common Linux issues.

I have also included ACL under Linux permissions, along with some additional concepts that are important for a Linux Administrator or DevOps Engineer interview.

# **1. Linux Command-Line Operations**

## **1.1 File and Directory Management**

This is one of the most fundamental topics in Linux administration. A Linux administrator regularly works with files, directories, configuration files, application files, and logs.

### **A. Navigation Commands**

| Command  | Description                                  | Example   |
| -------- | -------------------------------------------- | --------- |
| `pwd`    | Displays the current working directory       | `pwd`     |
| `cd`     | Changes the directory                        | `cd /etc` |
| `cd ..`  | Moves one directory back                     | `cd ..`   |
| `cd ~`   | Moves to the user's home directory           | `cd ~`    |
| `cd -`   | Returns to the previous directory            | `cd -`    |
| `ls`     | Lists files and directories                  | `ls`      |
| `ls -l`  | Displays detailed information                | `ls -l`   |
| `ls -a`  | Displays hidden files                        | `ls -a`   |
| `ls -lh` | Displays human-readable file sizes           | `ls -lh`  |
| `ls -la` | Displays all files with detailed information | `ls -la`  |

**Important interview question:**

What is the difference between `ls -l` and `ls -la`?

- `ls -l` displays files and directories in long format.
- `ls -la` displays all files, including hidden files, in long format.

### **B. File and Directory Creation**

| Command    | Description                            | Example                   |
| ---------- | -------------------------------------- | ------------------------- |
| `touch`    | Creates an empty file                  | `touch file.txt`          |
| `mkdir`    | Creates a directory                    | `mkdir data`              |
| `mkdir -p` | Creates parent directories if required | `mkdir -p /data/app/logs` |

**Practical example:**

```
mkdir project
cd project
touch app.log
mkdir logs
```

### **C. File and Directory Deletion**

| Command  | Description                                       | Example           |
| -------- | ------------------------------------------------- | ----------------- |
| `rm`     | Removes a file                                    | `rm file.txt`     |
| `rm -r`  | Removes a directory recursively                   | `rm -r project`   |
| `rm -f`  | Forces file deletion without confirmation         | `rm -f file.txt`  |
| `rm -rf` | Forcefully removes directories and their contents | `rm -rf project`  |
| `rmdir`  | Removes an empty directory                        | `rmdir empty_dir` |

**Important:** Be extremely careful with `rm -rf`, especially when using root privileges. Always verify the target path before executing it.

### **D. Copying and Moving Files**

| Command | Description                    | Example                     |
| ------- | ------------------------------ | --------------------------- |
| `cp`    | Copies a file                  | `cp file.txt backup.txt`    |
| `cp -r` | Copies a directory recursively | `cp -r app backup/`         |
| `cp -p` | Preserves file attributes      | `cp -p file.txt backup.txt` |
| `mv`    | Moves a file or directory      | `mv file.txt /tmp/`         |
| `mv`    | Renames a file                 | `mv old.txt new.txt`        |

### **E. Finding Files and Directories**

The `find` command is particularly useful for system administration and troubleshooting.

```
find /etc -name "ssh_config"
find /var/log -type f
find /home -type d
find /var/log -name "*.log"
```

Find files based on size:

```
find /var/log -type f -size +100M
```

Find files modified within the last 24 hours:

```
find /var/log -type f -mtime -1
```

Find and delete files older than seven days:

```
find /tmp -type f -mtime +7 -delete
```

**Interview question:** How do you find a particular file in Linux?

Answer: We can use the `find` command with the directory path, filename, and other conditions.

## **1.2 Viewing and Filtering Text Files**

Linux administrators frequently work with configuration files, application logs, and system logs.

### **A. Reading Files**

| Command      | Description                           | Example               |
| ------------ | ------------------------------------- | --------------------- |
| `cat`        | Displays complete file content        | `cat file.txt`        |
| `less`       | Reads large files page by page        | `less app.log`        |
| `more`       | Displays file content page by page    | `more file.txt`       |
| `head`       | Displays the first 10 lines           | `head file.txt`       |
| `head -n 20` | Displays the first 20 lines           | `head -n 20 file.txt` |
| `tail`       | Displays the last 10 lines            | `tail app.log`        |
| `tail -n 50` | Displays the last 50 lines            | `tail -n 50 app.log`  |
| `tail -f`    | Continuously monitors new log entries | `tail -f app.log`     |

**Very important practical command:**

```
tail -f /var/log/messages
```

This helps monitor log entries in real time.

To stop monitoring, press `Ctrl + C`.

### **B. Searching Text Using grep**

The `grep` command searches for specific words or patterns inside files.

```
grep "ERROR" app.log
```

Frequently used options:

| Option | Description                           |
| ------ | ------------------------------------- |
| `-i`   | Case-insensitive search               |
| `-v`   | Displays lines that do not match      |
| `-r`   | Searches recursively                  |
| `-n`   | Displays line numbers                 |
| `-c`   | Counts matching lines                 |
| `-w`   | Matches complete words                |
| `-E`   | Supports extended regular expressions |

Examples:

```
grep -i "error" app.log
grep -n "failed" app.log
grep -v "INFO" app.log
grep -r "Listen" /etc/httpd/
grep -c "ERROR" app.log
```

### **C. Other Text Processing Commands**

| Command   | Description                           | Example                      |
| --------- | ------------------------------------- | ---------------------------- |
| `wc -l`   | Counts lines                          | `wc -l app.log`              |
| `wc -w`   | Counts words                          | `wc -w file.txt`             |
| `sort`    | Sorts lines                           | `sort names.txt`             |
| `uniq`    | Removes consecutive duplicate lines   | `uniq names.txt`             |
| `sort -u` | Sorts and removes duplicates          | `sort -u names.txt`          |
| `cut`     | Extracts specific fields              | `cut -d: -f1 /etc/passwd`    |
| `awk`     | Processes structured text             | `awk '{print $1}' file.txt`  |
| `sed`     | Performs text replacement and editing | `sed 's/old/new/g' file.txt` |

**Practical example:**

Count how many times ERROR appears in an application log:

```
grep -i "error" app.log | wc -l
```

Find the top 10 most frequently occurring IP addresses in an access log:

```
awk '{print $1}' access.log | sort | uniq -c | sort -nr | head
```

## **1.3 Basic File Editing – vi/vim and nano**

A Linux administrator should know how to edit configuration files.

### **Vim Editor**

Important modes:

1. Normal Mode – Used for navigation and commands.
2. Insert Mode – Used to write or modify text.
3. Command Mode – Used to save or exit.

Important commands:

| Command | Description            |
| ------- | ---------------------- |
| `i`     | Enters Insert Mode     |
| `Esc`   | Returns to Normal Mode |
| `:w`    | Saves the file         |
| `:q`    | Quits the editor       |
| `:wq`   | Saves and exits        |
| `:q!`   | Exits without saving   |
| `dd`    | Deletes a line         |
| `yy`    | Copies a line          |
| `p`     | Pastes copied content  |
| `/word` | Searches for a word    |
| `u`     | Undo                   |

Example:

```
vim /etc/ssh/sshd_config
```

### **Nano Editor**

```
nano file.txt
```

Important shortcuts:

- `Ctrl + O` – Save.
- `Ctrl + X` – Exit.
- `Ctrl + W` – Search.

## **1.4 Input/Output Redirection and Pipes**

This is an important topic for Linux administration and shell scripting.

### **A. Standard Input, Output and Error**

Linux has three standard streams:

| Stream | Number | Description     |
| ------ | ------ | --------------- |
| STDIN  | 0      | Standard Input  |
| STDOUT | 1      | Standard Output |
| STDERR | 2      | Standard Error  |

### **B. Redirection Operators**

| Operator      | Description                                               |
| ------------- | --------------------------------------------------------- |
| `>`           | Redirects output and overwrites existing content          |
| `>>`          | Appends output to a file                                  |
| `<`           | Takes input from a file                                   |
| `2>`          | Redirects error output                                    |
| `2>>`         | Appends error output                                      |
| `&>`          | Redirects both standard output and standard error in Bash |
| `2>/dev/null` | Discards error messages                                   |

Examples:

Overwrite a file:

```
echo "Hello Linux" > file.txt
```

Append content:

```
echo "Welcome" >> file.txt
```

Redirect errors:

```
ls /invalid_path 2> error.log
```

Ignore errors:

```
ls /invalid_path 2>/dev/null
```

Redirect both output and errors:

```
command > output.log 2>&1
```

### **C. Pipes ( | )**

A pipe passes the output of one command as input to another command.

Example:

```
ps aux | grep nginx
```

Another example:

```
cat app.log | grep ERROR | wc -l
```

**Interview question: What is the difference between redirection and piping?**

- Redirection sends command output to or receives input from a file.
- Piping sends the output of one command directly to another command.

## **1.5 Archive and Compression Management**

Linux administrators frequently create backups, transfer files, and compress application directories.

### **TAR Commands**

Create a compressed archive:

```
tar -czvf backup.tar.gz /data
```

Extract an archive:

```
tar -xzvf backup.tar.gz
```

List archive contents:

```
tar -tzvf backup.tar.gz
```

Extract into a specific directory:

```
tar -xzvf backup.tar.gz -C /tmp/
```

Important TAR options:

- `c` – Create archive.
- `x` – Extract archive.
- `z` – gzip compression.
- `v` – Verbose output.
- `f` – Archive filename.

### **ZIP and UNZIP**

```
zip backup.zip file1.txt file2.txt
zip -r backup.zip project/
unzip backup.zip
unzip backup.zip -d /tmp/
```

## **1.6 Disk and Memory Management**

These commands are frequently used during production troubleshooting.

### **A. Disk Usage – df**

Displays filesystem disk usage.

```
df -h
```

- `-h` – Human-readable format.
- `-T` – Displays filesystem type.
- `-i` – Displays inode usage.

Example:

```
df -hT
df -i
```

### **B. Directory Size – du**

Displays directory and file space consumption.

```
du -sh /var/log
du -sh /home/*
du -ah /var/log
```

- `-s` – Summary.
- `-h` – Human-readable.
- `-a` – Includes files.

### **C. Memory Usage – free**

```
free -h
free -m
```

Displays RAM and swap memory usage.

### **D. CPU Information**

```
lscpu
```

Displays CPU architecture and processor information.

```
uptime
```

Displays system uptime and load averages.

**Important interview scenario:**

Your Linux server is running out of disk space. How will you troubleshoot?

1. Check filesystem usage using `df -h`.
2. Check inode usage using `df -i`.
3. Identify large directories using `du -sh`.
4. Find large files using `find`.
5. Check log files and old backups.
6. Clean up unnecessary files after verification.

# **2. Linux File Permissions and Ownership**

Very important interview topic

Linux provides file permissions to control who can read, modify, and execute files or directories.

## **2.1 Understanding Linux Permissions**

Run:

```
ls -l
```

Example output:

```
-rwxr-xr-- 1 rakesh devops 1024 Nov 13 script.sh
```

Understanding the permission string:

```
-    rwx    r-x    r--
|     |      |      |
|   Owner   Group  Others
|
File Type
```

### **Permission Types**

| Permission | Symbol | Numeric Value | Meaning             |
| ---------- | ------ | ------------- | ------------------- |
| Read       | r      | 4             | Read file content   |
| Write      | w      | 2             | Modify file content |
| Execute    | x      | 1             | Execute a file      |

### **Understanding 755**

```
755 = 7 + 5 + 5

Owner  = 7 = rwx
Group  = 5 = r-x
Others = 5 = r-x
```

Similarly:

- `777` – Everyone has full permissions.
- `755` – Owner has full permissions; group and others have read and execute.
- `644` – Owner has read/write; group and others have read.
- `600` – Only owner has read/write.
- `700` – Only owner has full permissions.

## **2.2 Changing Permissions – chmod**

The `chmod` command changes file and directory permissions.

### **A. Numeric Method**

```
chmod 755 script.sh
chmod 644 file.txt
chmod 600 id_rsa
chmod 700 private_dir
```

### **B. Symbolic Method**

```
chmod u+x script.sh
chmod g-w file.txt
chmod o=r file.txt
chmod a+r file.txt
```

Here:

- `u` – User/Owner.
- `g` – Group.
- `o` – Others.
- `a` – All users.

Operators:

- `+` – Add permission.
- `-` – Remove permission.
- `=` – Set permission.

## **2.3 Changing Ownership – chown and chgrp**

### **chown**

Changes file ownership.

```
chown rakesh file.txt
```

Changes both user and group:

```
chown rakesh:devops file.txt
```

Changes ownership recursively:

```
chown -R rakesh:devops /data
```

### **chgrp**

Changes group ownership.

```
chgrp devops file.txt
```

## **2.4 Access Control Lists (ACL)**

ACL provides more granular permission management than traditional Linux permissions.

It allows administrators to assign permissions to specific users or groups without changing the file's primary owner or group.

### **Important ACL Commands**

| Command        | Description                      |
| -------------- | -------------------------------- |
| `getfacl file` | Displays ACL permissions         |
| `setfacl -m`   | Modifies ACL permissions         |
| `setfacl -x`   | Removes a specific ACL entry     |
| `setfacl -b`   | Removes all extended ACL entries |
| `setfacl -R`   | Applies ACL recursively          |
| `setfacl -d`   | Sets default ACL on a directory  |

Examples:

Give a particular user read and write permissions:

```
setfacl -m u:john:rw file.txt
```

Give a group read and write permissions:

```
setfacl -m g:devops:rw file.txt
```

View ACL:

```
getfacl file.txt
```

Remove a user's ACL entry:

```
setfacl -x u:john file.txt
```

Remove all extended ACL entries:

```
setfacl -b file.txt
```

**Default ACL:**

A default ACL on a directory provides default permission entries for newly created files and subdirectories within it, subject to normal permission and application behavior.

```
setfacl -d -m u:john:rwx /data
```

### **Important Interview Question**

What is the difference between chmod and ACL?

- `chmod` manages traditional owner, group, and others permissions.
- ACL allows additional permissions for specific users and groups.

**Important:** ACL permissions can also be restricted by the ACL mask. Therefore, an ACL entry showing `rwx` does not always mean all three permissions are effective.

## **2.5 Special Permissions**

Three special Linux permissions are important:

| Permission | Numeric Value | Purpose                                                                                                               |
| ---------- | ------------- | --------------------------------------------------------------------------------------------------------------------- |
| SUID       | 4             | Executes a file with the file owner's effective privileges                                                            |
| SGID       | 2             | Executes a file with the file group's effective privileges; on directories, new entries inherit the directory's group |
| Sticky Bit | 1             | Restricts deletion of files in a shared directory                                                                     |

Examples:

```
chmod 4755 file
chmod 2755 directory
chmod 1777 /shared
```

Common real-world example:

```
ls -ld /tmp
```

The `/tmp` directory normally has sticky-bit permission:

```
drwxrwxrwt
```

This allows users to create files but generally prevents them from deleting other users' files.

## **2.6 sudo and Important Linux Files**

### **sudo**

Allows an authorized user to execute commands with elevated privileges.

```
sudo systemctl restart nginx
sudo -i
```

### **Important Linux Files**

| File              | Purpose                                               |
| ----------------- | ----------------------------------------------------- |
| `/etc/passwd`     | Stores user account information                       |
| `/etc/shadow`     | Stores password hashes and password aging information |
| `/etc/group`      | Stores group information                              |
| `/etc/sudoers`    | Defines sudo privileges                               |
| `/etc/sudoers.d/` | Contains additional sudo configuration files          |

**Interview question:** Where are Linux user passwords stored?

Answer: Password hashes are stored in `/etc/shadow`, not in `/etc/passwd`.

# **3. Process and Service Management**

Very important interview topic

## **3.1 Understanding Processes**

A process is an instance of a running program.

Whenever you execute a command or start an application, the Linux operating system creates a process.

Each process has a unique Process ID (PID).

Important process information:

- PID – Process ID.
- PPID – Parent Process ID.
- USER – Process owner.
- CPU% – CPU consumption.
- MEM% – Memory consumption.
- STAT – Process state.

## **3.2 Process Monitoring Commands**

### **A. ps**

Displays currently running processes.

```
ps aux
```

Another format:

```
ps -ef
```

Find a particular process:

```
ps aux | grep nginx
```

Understand the difference:

- `ps aux` – BSD-style process listing.
- `ps -ef` – Full-format process listing.

### **B. top**

Displays real-time system and process information.

```
top
```

Important information:

- CPU utilization.
- Memory utilization.
- Running processes.
- Load average.
- Process IDs.

### **C. htop**

Provides an interactive and user-friendly process monitoring interface.

```
htop
```

It may need to be installed separately.

### **D. pgrep**

Finds processes using their names.

```
pgrep nginx
pgrep -a nginx
```

### **E. pidof**

Displays the PID of a running program.

```
pidof nginx
```

## **3.3 Process Control**

Sometimes a process becomes unresponsive or consumes excessive resources. Linux provides signals to manage processes.

### **kill**

Terminates a process using its PID.

```
kill 1234
```

By default, `kill` sends SIGTERM (signal 15).

### **Important Signals**

| Signal  | Number | Description                                                                  |
| ------- | ------ | ---------------------------------------------------------------------------- |
| SIGTERM | 15     | Requests graceful termination                                                |
| SIGKILL | 9      | Forcefully terminates a process                                              |
| SIGHUP  | 1      | Traditionally indicates hangup; some services use it to reload configuration |
| SIGSTOP | 19     | Stops a process                                                              |
| SIGCONT | 18     | Resumes a stopped process                                                    |

Examples:

```
kill -15 1234
kill -9 1234
kill -STOP 1234
kill -CONT 1234
```

**Important interview question:**

What is the difference between `kill -15` and `kill -9`?

- `kill -15` sends SIGTERM and allows the process to shut down gracefully.
- `kill -9` sends SIGKILL and immediately terminates the process without allowing cleanup handlers to run.

Always try SIGTERM first. Use SIGKILL only when necessary.

## **3.4 Background and Foreground Processes**

Linux allows commands to run in the foreground or background.

### **Background Execution**

```
sleep 100 &
```

The `&` symbol starts the command in the background.

### **jobs**

Displays background jobs in the current shell.

```
jobs
```

### **fg**

Brings a background job into the foreground.

```
fg %1
```

### **bg**

Resumes a stopped job in the background.

```
bg %1
```

### **nohup**

Runs a command so it can continue after the terminal session ends.

```
nohup ./script.sh &
```

By default, output is written to `nohup.out` unless redirected.

**Interview question:** What is the difference between `&` and `nohup`?

- `&` runs a command in the background.
- `nohup` makes a command ignore the hangup signal, allowing it to continue after terminal disconnection in typical usage.

# **4. Linux Service Management – systemd**

Must prepare

## **4.1 What is systemd?**

systemd is a system and service manager used by many modern Linux distributions.

It manages:

- System services.
- Startup processes.
- Service dependencies.
- Mount points.
- System targets.
- System initialization.

`systemctl` is the command-line utility used to interact with systemd.

## **4.2 Service Management Commands**

| Command                               | Description                        |
| ------------------------------------- | ---------------------------------- |
| `systemctl status nginx`              | Checks service status              |
| `systemctl start nginx`               | Starts service                     |
| `systemctl stop nginx`                | Stops service                      |
| `systemctl restart nginx`             | Restarts service                   |
| `systemctl reload nginx`              | Reloads configuration if supported |
| `systemctl enable nginx`              | Enables service at boot            |
| `systemctl disable nginx`             | Disables automatic startup         |
| `systemctl is-active nginx`           | Checks whether service is active   |
| `systemctl is-enabled nginx`          | Checks whether service is enabled  |
| `systemctl list-units --type=service` | Lists loaded service units         |
| `systemctl daemon-reload`             | Reloads systemd unit definitions   |

### **Important Difference: enable vs start**

**start:**

Starts a service immediately.

```
systemctl start nginx
```

**enable:**

Configures a service to start automatically during system boot.

```
systemctl enable nginx
```

To do both:

```
systemctl enable --now nginx
```

## **4.3 Checking Service Logs – journalctl**

systemd stores service and system logs in its journal.

Important commands:

```
journalctl
journalctl -u nginx
journalctl -u nginx -n 50
journalctl -u nginx -f
journalctl -xe
journalctl -b
```

Descriptions:

- `-u` – Filters logs for a particular service.
- `-n 50` – Displays the last 50 lines.
- `-f` – Follows logs in real time.
- `-xe` – Displays recent logs with additional explanatory information.
- `-b` – Displays logs from the current boot.

## **4.4 Practical Service Troubleshooting**

**Scenario: Nginx service is not starting. What will you do?**

Step 1: Check service status.

```
systemctl status nginx
```

Step 2: Check service logs.

```
journalctl -u nginx -n 50
```

Step 3: Check configuration syntax.

```
nginx -t
```

Step 4: Check whether the required port is already occupied.

```
ss -tulnp
```

Step 5: Check file permissions and configuration files.

Step 6: Fix the issue and restart the service.

```
systemctl restart nginx
```

Step 7: Verify the service.

```
systemctl status nginx
```

# **5. Linux Shell Scripting – Bash**

Important for DevOps interviews

Shell scripting is used to automate repetitive Linux administration tasks.

For example:

- Checking disk utilization.
- Monitoring services.
- Creating backups.
- Cleaning old log files.
- Checking whether a file exists.
- Automating routine administrative activities.

## **5.1 Basic Shell Script Structure**

A Bash script generally starts with a shebang.

```
#!/bin/bash

echo "Hello Linux"
```

Save the file:

```
vim hello.sh
```

Give execution permission:

```
chmod +x hello.sh
```

Execute:

```
./hello.sh
```

Alternatively:

```
bash hello.sh
```

## **5.2 Variables**

Variables store values that can be reused in a script.

```
#!/bin/bash

NAME="Rakesh"

echo "Welcome $NAME"
```

Important:

There should be no spaces around the `=` sign when assigning a shell variable.

Correct:

```
NAME="Rakesh"
```

Incorrect:

```
NAME = "Rakesh"
```

## **5.3 Command-Line Arguments**

Shell scripts can accept values from the command line.

Example:

```
#!/bin/bash

echo "First argument: $1"
echo "Second argument: $2"
echo "All arguments: $@"
echo "Number of arguments: $#"
```

Execute:

```
bash script.sh Linux DevOps
```

Important variables:

| Variable | Description                     |
| -------- | ------------------------------- |
| `$0`     | Script name                     |
| `$1`     | First argument                  |
| `$2`     | Second argument                 |
| `$@`     | All arguments                   |
| `$#`     | Number of arguments             |
| `$?`     | Exit status of the last command |
| `$$`     | Current shell process PID       |

## **5.4 Conditional Statements**

The `if` statement is used to execute commands based on conditions.

Example:

```
#!/bin/bash

if [ -f "/etc/passwd" ]; then
    echo "File exists"
else
    echo "File does not exist"
fi
```

Important file conditions:

| Condition | Meaning                              |
| --------- | ------------------------------------ |
| `-f`      | Checks whether a regular file exists |
| `-d`      | Checks whether a directory exists    |
| `-e`      | Checks whether a path exists         |
| `-r`      | Checks read permission               |
| `-w`      | Checks write permission              |
| `-x`      | Checks execute permission            |

Numeric comparisons:

| Operator | Meaning               |
| -------- | --------------------- |
| `-eq`    | Equal                 |
| `-ne`    | Not equal             |
| `-gt`    | Greater than          |
| `-lt`    | Less than             |
| `-ge`    | Greater than or equal |
| `-le`    | Less than or equal    |

Example:

```
#!/bin/bash

AGE=25

if [ "$AGE" -ge 18 ]; then
    echo "Adult"
else
    echo "Minor"
fi
```

## **5.5 Loops**

Loops are used to execute commands repeatedly.

### **For Loop**

```
#!/bin/bash

for i in 1 2 3 4 5
do
    echo "Number: $i"
done
```

### **While Loop**

```
#!/bin/bash

COUNT=1

while [ "$COUNT" -le 5 ]
do
    echo "$COUNT"
    COUNT=$((COUNT + 1))
done
```

## **5.6 Functions**

Functions allow us to reuse a block of commands.

```
#!/bin/bash

welcome() {
    echo "Welcome to Linux"
}

welcome
```

## **5.7 Exit Status**

Every Linux command returns an exit status.

- `0` – Success.
- Non-zero – Failure or another condition.

Example:

```
mkdir test

echo $?
```

If the directory is created successfully, the exit status will generally be `0`.

This is particularly useful in automation scripts.

# **6. Python Scripting – Basic Knowledge**

For a DevOps Engineer, basic Python knowledge is useful for automation, API interactions, infrastructure management, and log processing.

You do not need to become an advanced Python developer for a basic Linux administration interview, but you should understand the following concepts.

## **6.1 Variables and Data Types**

```
name = "Rakesh"
age = 30
salary = 70000
is_active = True
```

Common data types:

- String
- Integer
- Float
- Boolean
- List
- Tuple
- Dictionary
- Set

## **6.2 Lists and Dictionaries**

List:

```
servers = ["server1", "server2", "server3"]

print(servers)
```

Dictionary:

```
server = {
    "name": "server1",
    "ip": "192.168.1.10",
    "status": "running"
}

print(server["name"])
```

## **6.3 Conditional Statements**

```
disk_usage = 85

if disk_usage > 80:
    print("Warning: Disk usage is high")
else:
    print("Disk usage is normal")
```

## **6.4 Loops**

```
servers = ["server1", "server2", "server3"]

for server in servers:
    print(server)
```

## **6.5 Functions**

```
def welcome(name):
    print("Welcome", name)

welcome("Rakesh")
```

## **6.6 Exception Handling**

Used to handle errors without unexpectedly terminating a program.

```
try:
    file = open("app.log", "r")
    print(file.read())
    file.close()

except FileNotFoundError:
    print("File not found")
```

## **6.7 File Handling**

A better way to open and close files automatically:

```
with open("app.log", "r") as file:
    content = file.read()
    print(content)
```

## **6.8 OS and Subprocess Modules**

The `os` module is used to interact with the operating system.

```
import os

if os.path.exists("/etc/passwd"):
    print("File exists")
```

The `subprocess` module is used to execute external commands.

```
import subprocess

result = subprocess.run(
    ["df", "-h"],
    capture_output=True,
    text=True
)

print(result.stdout)
```

# **7. Practical Linux Troubleshooting Scenarios**

High interview value

The interviewer may not simply ask you to define commands. They may give you a real-world situation and ask how you would troubleshoot it.

Prepare the following scenarios carefully.

## **Scenario 1: Disk Usage Is 95%**

**Question:** Your Linux server is running out of disk space. How will you troubleshoot?

Commands:

```
df -h
df -i
du -sh /*
du -sh /var/log/*
find /var/log -type f -size +100M
```

Approach:

1. Identify the filesystem with high usage.
2. Check inode utilization.
3. Identify directories consuming space.
4. Find large log files and old backups.
5. Check whether deleted files are still held open by running processes using `lsof +L1`.
6. Clean up unnecessary data safely.
7. Verify disk utilization again.

## **Scenario 2: Linux Server Is Running Slowly**

**Question:** Your Linux server is responding slowly. How will you troubleshoot?

Commands:

```
uptime
top
free -h
df -h
vmstat 1
iostat -xz 1
```

Approach:

1. Check CPU utilization.
2. Identify processes consuming high CPU.
3. Check available memory and swap usage.
4. Check disk space and I/O utilization.
5. Check system load average.
6. Investigate network and application issues if required.

## **Scenario 3: Permission Denied While Executing a Script**

**Question:** You created a shell script, but you are getting Permission Denied.

Check:

```
ls -l script.sh
```

Fix:

```
chmod +x script.sh
```

Execute:

```
./script.sh
```

If permission is still denied, investigate directory traversal permissions, ownership, filesystem mount options such as `noexec`, and SELinux policies where applicable.

## **Scenario 4: Service Is Not Running**

Check:

```
systemctl status nginx
journalctl -u nginx -n 50
```

Check configuration:

```
nginx -t
```

Check port:

```
ss -tulnp
```

Fix the underlying issue and restart the service.

## **Scenario 5: Application Port Is Already in Use**

**Question:** Your application is not starting because port 8080 is already in use.

Check:

```
ss -tulnp | grep :8080
```

Alternative:

```
lsof -i :8080
```

Identify the process and determine whether it is safe to stop or whether the application should use another port.

## **Scenario 6: How Will You Monitor Live Application Logs?**

```
tail -f /var/log/app.log
```

Search errors:

```
grep -i "error" /var/log/app.log
```

Count errors:

```
grep -i "error" /var/log/app.log | wc -l
```

# **8. Practical Shell Scripting Programs for Interview Preparation**

These are the scripts I recommend practising yourself rather than simply reading.

## **Program 1: Check Whether a File Exists**

```
#!/bin/bash

FILE="/etc/passwd"

if [ -f "$FILE" ]; then
    echo "File exists"
else
    echo "File does not exist"
fi
```

## **Program 2: Create a Directory If It Does Not Exist**

```
#!/bin/bash

DIR="/data/backup"

if [ ! -d "$DIR" ]; then
    mkdir -p "$DIR"
    echo "Directory created"
else
    echo "Directory already exists"
fi
```

## **Program 3: Check Disk Usage and Generate an Alert**

```
#!/bin/bash

USAGE=$(df -P / | awk 'NR==2 {gsub("%","",$5); print $5}')

if [ "$USAGE" -gt 80 ]; then
    echo "WARNING: Disk usage is above 80%"
else
    echo "Disk usage is normal"
fi
```

## **Program 4: Count ERROR Entries in a Log File**

```
#!/bin/bash

LOG_FILE="/var/log/app.log"

if [ -f "$LOG_FILE" ]; then
    COUNT=$(grep -ic "ERROR" "$LOG_FILE")
    echo "Total errors: $COUNT"
else
    echo "Log file not found"
fi
```

## **Program 5: Check Whether a Service Is Running**

```
#!/bin/bash

SERVICE="nginx"

if systemctl is-active --quiet "$SERVICE"; then
    echo "$SERVICE is running"
else
    echo "$SERVICE is not running"
fi
```

# **9. Additional Linux Topics You Should Revise**

Your mindmap covers the core fundamentals. However, for a Linux Administrator or DevOps Engineer interview, I would also recommend revising these topics.

These are particularly useful because interviewers often move from basic Linux commands to actual system administration.

### **A. User and Group Management**

- `useradd`
- `usermod`
- `userdel`
- `passwd`
- `groupadd`
- `groupdel`
- `id`
- `groups`
- `whoami`
- `who`
- `last`

### **B. Linux Boot Process**

Understand the basic sequence:

```
BIOS / UEFI
    |
    v
GRUB Bootloader
    |
    v
Linux Kernel
    |
    v
initramfs
    |
    v
systemd (PID 1)
    |
    v
System Services
    |
    v
Login
```

Know:

- What is GRUB?
- What is the Linux kernel?
- What is initramfs?
- What is systemd?
- What is the difference between reboot and shutdown?

### **C. Package Management**

For RHEL-based systems:

```
rpm -qa
rpm -ivh package.rpm
dnf install nginx
dnf remove nginx
dnf update
dnf search nginx
dnf info nginx
```

For Debian/Ubuntu:

```
apt update
apt install nginx
apt remove nginx
apt upgrade
dpkg -l
```

### **D. Networking Commands**

| Command       | Purpose                            |
| ------------- | ---------------------------------- |
| `ip addr`     | Displays IP addresses              |
| `ip route`    | Displays routing table             |
| `ping`        | Tests connectivity                 |
| `ss -tulnp`   | Displays listening TCP/UDP sockets |
| `traceroute`  | Traces network path                |
| `nslookup`    | DNS lookup                         |
| `dig`         | Detailed DNS lookup                |
| `curl`        | Tests HTTP/API connectivity        |
| `wget`        | Downloads files                    |
| `hostname`    | Displays system hostname           |
| `hostnamectl` | Manages hostname information       |

### **E. Scheduling Jobs – Cron**

Cron is used to schedule recurring tasks.

Edit cron jobs:

```
crontab -e
```

List cron jobs:

```
crontab -l
```

Cron format:

```
* * * * * command
| | | | |
| | | | +---- Day of week
| | | +------ Month
| | +-------- Day of month
| +---------- Hour
+------------ Minute
```

Example: Execute a script every day at 2 AM.

```
0 2 * * * /scripts/backup.sh
```

### **F. Environment Variables**

```
env
printenv
echo $PATH
export APP_ENV=production
```

Understand:

- What is an environment variable?
- What is PATH?
- Difference between local and exported variables.
- Where are environment variables configured?

### **G. Linux Filesystem and Mount Management**

Important commands:

```
lsblk
blkid
mount
umount
findmnt
df -h
```

Important concepts:

- Filesystem.
- Partition.
- Mount point.
- `/etc/fstab`.
- XFS and ext4.
- LVM basics.

### **H. SELinux Basics**

For RHEL-based environments:

```
getenforce
sestatus
setenforce 0
setenforce 1
restorecon -Rv /var/www/html
```

Understand:

- What is SELinux?
- Enforcing, Permissive, and Disabled modes.
- SELinux contexts.
- Why permission denied can occur even when normal Linux permissions look correct.

Note: `setenforce` changes runtime mode; it does not permanently configure SELinux.

# **10. Most Probable Linux Interview Questions**

Use this section for your final revision.

## **Linux Fundamentals**

1. What is Linux?
2. What is the difference between Linux and Unix?
3. What is the Linux kernel?
4. What is a shell?
5. What is the difference between Bash and the Linux kernel?
6. What is the root user?
7. What is the difference between absolute and relative paths?
8. What are hidden files in Linux?
9. What is the purpose of the `/etc`, `/var`, `/home`, `/tmp`, and `/root` directories?

## **File Management**

10. What is the difference between `cp` and `mv`?
11. What is the difference between `rm` and `rmdir`?
12. How do you find a file in Linux?
13. How do you find files larger than 100 MB?
14. How do you search for a particular word in a log file?
15. What is the difference between `cat`, `less`, and `more`?
16. How do you monitor logs in real time?
17. What is the difference between `>` and `>>`?
18. What is the purpose of a pipe?

## **Permissions and Ownership**

19. Explain Linux file permissions.
20. What is the difference between `chmod` and `chown`?
21. Explain `755`, `644`, and `777`.
22. What is the difference between numeric and symbolic permissions?
23. What is ACL?
24. What is the difference between chmod and ACL?
25. What are SUID, SGID, and Sticky Bit?
26. What is the difference between `/etc/passwd` and `/etc/shadow`?
27. What is sudo?

## **Processes and Services**

28. What is a process in Linux?
29. What is the difference between PID and PPID?
30. What is the difference between `ps aux` and `top`?
31. What is the difference between `kill -15` and `kill -9`?
32. What is a zombie process?
33. What is a defunct process?
34. What is the difference between foreground and background processes?
35. What is nohup?
36. What is systemd?
37. What is the difference between `start` and `enable`?
38. What is the difference between `restart` and `reload`?
39. How do you check service logs?

## **System Administration**

40. How do you check disk utilization?
41. What is the difference between `df` and `du`?
42. How do you check memory utilization?
43. How do you check CPU utilization?
44. What is load average?
45. What is swap memory?
46. How do you check which process is using a particular port?
47. How do you check open network ports?
48. How do you schedule a task in Linux?
49. What is the Linux boot process?
50. What is the difference between hard link and soft link?

## **Shell Scripting**

51. What is shell scripting?
52. What is a shebang?
53. What is the difference between `$1`, `$@`, and `$#`?
54. What is `$?`?
55. What is the difference between `if` and `case`?
56. What is the difference between for and while loops?
57. How do you check whether a file exists?
58. How do you check whether a service is running?
59. How do you create a disk usage monitoring script?
60. How do you automate backup using shell scripting?

nux knowledge. Knowing how to identify a full filesystem, trace the directory consuming space, find deleted-but-open files, and resolve the problem safely demonstrates Linux administration skills.

That practical troubleshooting ability is what you should focus on.
