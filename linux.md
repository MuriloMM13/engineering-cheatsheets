# Linux Terminal Cheat Sheet

Quick reference for basic, intermediate, and advanced Linux terminal commands, with focus on server access and file transfer.

---

# Basic Commands

## Show current directory

Print the current working directory.

```bash
pwd
```

---

## List files

List files and folders in the current directory.

```bash
ls
```

---

## List files with details

Show permissions, owner, size, and date.

```bash
ls -l
```

---

## List hidden files

Show hidden files too.

```bash
ls -la
```

---

## Change directory

Move to another folder.

```bash
cd folder_name
```

---

## Go up one level

Move to parent directory.

```bash
cd ..
```

---

## Go to home directory

Jump to your home folder.

```bash
cd ~
```

---

## Create a folder

Make a new directory.

```bash
mkdir new_folder
```

---

## Create nested folders

Make full directory path at once.

```bash
mkdir -p project/data/results
```

---

## Create an empty file

Create a new file.

```bash
touch file.txt
```

---

## Copy file

Copy one file to another location.

```bash
cp file.txt backup.txt
```

---

## Copy folder

Copy a directory recursively.

```bash
cp -r source_folder destination_folder
```

---

## Move or rename file

Move a file or rename it.

```bash
mv old_name.txt new_name.txt
```

---

## Remove file

Delete a file.

```bash
rm file.txt
```

---

## Remove folder recursively

Delete a folder and everything inside it.

```bash
rm -r folder_name
```

---

## Remove forcefully

Delete without confirmation.

```bash
rm -rf folder_name
```

---

## Show file content

Print file content in terminal.

```bash
cat file.txt
```

---

## Read file page by page

Useful for long files.

```bash
less file.txt
```

---

## Show first lines

Print first 10 lines of a file.

```bash
head file.txt
```

---

## Show last lines

Print last 10 lines of a file.

```bash
tail file.txt
```

---

## Follow file in real time

Useful for logs.

```bash
tail -f log.txt
```

---

# Intermediate Commands

## Search text inside files

Find a word or pattern in a file.

```bash
grep "pattern" file.txt
```

---

## Search recursively in folders

Search inside all files under a directory.

```bash
grep -r "pattern" folder_name
```

---

## Search with line numbers

Show matching line numbers.

```bash
grep -n "pattern" file.txt
```

---

## Find files by name

Search for files in a directory tree.

```bash
find . -name "file.txt"
```

---

## Find all Python files

Example of wildcard search.

```bash
find . -name "*.py"
```

---

## Show file size

Display file or folder size.

```bash
du -sh folder_name
```

---

## Show disk usage

Display storage usage of mounted disks.

```bash
df -h
```

---

## Show calendar date and time

Useful for timestamps and remote sessions.

```bash
date
```

---

## Show command history

Display recently used commands.

```bash
history
```

---

## Re-run a command from history

Run command number 123 again.

```bash
!123
```

---

## Clear terminal

Clean the terminal screen.

```bash
clear
```

---

## Edit a file with nano

Simple terminal text editor.

```bash
nano file.txt
```

---

## Edit a file with vim

More advanced terminal text editor.

```bash
vim file.txt
```

---

## Count lines, words, characters

Useful for checking file size quickly.

```bash
wc file.txt
```

---

## Sort lines

Sort file content alphabetically.

```bash
sort file.txt
```

---

## Remove duplicate lines

Often used after sorting.

```bash
sort file.txt | uniq
```

---

## Redirect output to file

Save command output into a file.

```bash
ls -l > files.txt
```

---

## Append output to file

Add command output to end of a file.

```bash
ls -l >> files.txt
```

---

## Pipe output

Send output of one command into another.

```bash
cat file.txt | grep "pattern"
```

---

## Show environment variables

Print environment variables.

```bash
env
```

---

## Show one environment variable

Display one variable value.

```bash
echo $HOME
```

---

## Export an environment variable

Set a variable for current shell session.

```bash
export MY_VAR="value"
```

---

# Permissions

## Show permissions

Display detailed file permissions.

```bash
ls -l
```

---

## Make file executable

Allow a script to be executed.

```bash
chmod +x script.sh
```

---

## Change permissions numerically

Example: owner rwx, group rx, others rx.

```bash
chmod 755 script.sh
```

---

## Change file owner

Change file ownership.

```bash
sudo chown user:user file.txt
```

---

# Processes and Monitoring

## Show running processes

List current processes.

```bash
ps aux
```

---

## Search for a process

Find a specific running process.

```bash
ps aux | grep python
```

---

## Interactive process viewer

Monitor CPU and memory usage live.

```bash
top
```

---

## Better process viewer

More user-friendly than top, if installed.

```bash
htop
```

---

## Kill a process by PID

Stop a process using its process ID.

```bash
kill 12345
```

---

## Force kill a process

Terminate immediately.

```bash
kill -9 12345
```

---

## Kill by name

Stop processes by name.

```bash
pkill python
```

---

## Run command in background

Start a process in background.

```bash
python script.py &
```

---

## Show background jobs

List jobs in current shell.

```bash
jobs
```

---

## Bring job to foreground

Resume a background job in terminal.

```bash
fg %1
```

---

# Compression

## Create tar.gz archive

Compress folder or files.

```bash
tar -czvf archive.tar.gz folder_name
```

---

## Extract tar.gz archive

Uncompress archive.

```bash
tar -xzvf archive.tar.gz
```

---

## Create zip archive

Compress into zip format.

```bash
zip -r archive.zip folder_name
```

---

## Extract zip archive

Unzip a file.

```bash
unzip archive.zip
```

---

# SSH and Remote Access

## Connect to a server with SSH

Basic remote login.

```bash
ssh user@server_ip
```

---

## Connect using a specific port

Useful if SSH does not use port 22.

```bash
ssh -p 2222 user@server_ip
```

---

## Connect using a private key

Use an SSH key instead of password.

```bash
ssh -i ~/.ssh/id_rsa user@server_ip
```

---

## Generate SSH key

Create a new SSH key pair.

```bash
ssh-keygen -t rsa -b 4096
```

---

## Copy SSH key to server

Enable passwordless login.

```bash
ssh-copy-id user@server_ip
```

---

## Test SSH connectivity

Quick test to confirm remote access.

```bash
ssh user@server_ip "hostname"
```

---

## Show current machine hostname

Useful to confirm if you are local or remote.

```bash
hostname
```

---

## Show current logged user

Useful in local or remote sessions.

```bash
whoami
```

---

# File Transfer: Local <-> Server

## Copy local file to server

Send a file from your machine to the server.

```bash
scp file.txt user@server_ip:/remote/path/
```

---

## Copy server file to local machine

Download a file from server to local machine.

```bash
scp user@server_ip:/remote/path/file.txt .
```

---

## Copy folder to server

Send a folder recursively.

```bash
scp -r local_folder user@server_ip:/remote/path/
```

---

## Copy folder from server

Download a remote folder recursively.

```bash
scp -r user@server_ip:/remote/path/folder .
```

---

## Copy using a specific port

Useful when SSH uses a custom port.

```bash
scp -P 2222 file.txt user@server_ip:/remote/path/
```

---

## Sync local folder to server

Efficient transfer; copies only changes.

```bash
rsync -av local_folder/ user@server_ip:/remote/path/
```

---

## Sync server folder to local

Download only changed files.

```bash
rsync -av user@server_ip:/remote/path/ local_folder/
```

---

## Sync with progress

Show transfer progress.

```bash
rsync -av --progress local_folder/ user@server_ip:/remote/path/
```

---

## Sync using SSH port

Use rsync with custom SSH port.

```bash
rsync -av -e "ssh -p 2222" local_folder/ user@server_ip:/remote/path/
```

---

# Server Workflows

## Log into server and go to a folder

Common one-line remote workflow.

```bash
ssh user@server_ip "cd /remote/path && pwd && ls -la"
```

---

## Run a command remotely

Execute a command on server without opening full session.

```bash
ssh user@server_ip "df -h"
```

---

## Run a remote script

Execute script directly on server.

```bash
ssh user@server_ip "bash /remote/path/script.sh"
```

---

## Download file after remote processing

Typical workflow after running something remotely.

```bash
scp user@server_ip:/remote/path/result.txt .
```

---

## Keep a process running after logout

Useful for long simulations or scripts.

```bash
nohup python script.py > output.log 2>&1 &
```

---

## Open a persistent terminal session

Useful for long remote work.

```bash
tmux
```

---

## Reattach tmux session

Return to an existing tmux session.

```bash
tmux attach
```

---

## List tmux sessions

Show all active tmux sessions.

```bash
tmux ls
```

---

# Network and Connectivity

## Check if a machine responds

Basic network connectivity test.

```bash
ping server_ip
```

---

## Check open ports on a host

Useful for diagnosing remote access issues.

```bash
nc -zv server_ip 22
```

---

## Show local IP addresses

Inspect network interfaces.

```bash
ip a
```

---

## Show active connections

Inspect listening or connected sockets.

```bash
ss -tulpn
```

---

# Advanced Useful Commands

## Search command location

Show where a command is installed.

```bash
which python
```

---

## Show full path and type of command

Useful if aliases are involved.

```bash
type python
```

---

## Show real path

Resolve absolute path.

```bash
realpath file.txt
```

---

## Compare two files

See line differences.

```bash
diff file1.txt file2.txt
```

---

## Watch command output repeatedly

Run a command every few seconds.

```bash
watch -n 2 ls -l
```

---

## Find recently modified files

Useful on servers and project folders.

```bash
find . -type f -mtime -1
```

---

## Find large files

Useful when disk space is low.

```bash
find . -type f -size +100M
```

---

## Show last commands from shell history

Quick review of recent actions.

```bash
history | tail
```

---

## Run command as another user

Useful on managed systems.

```bash
sudo -u username command
```

---

## Download file from URL

Fetch file directly from terminal.

```bash
wget https://example.com/file.zip
```

---

## Alternative download command

Another common downloader.

```bash
curl -O https://example.com/file.zip
```

---

# Very Practical Examples

## Send one local file to server

```bash
scp report.pdf user@server_ip:/home/user/work/
```

---

## Bring one result file from server

```bash
scp user@server_ip:/home/user/work/result.csv .
```

---

## Mirror local project to server

```bash
rsync -av --progress project/ user@server_ip:/home/user/project/
```

---

## Mirror server project to local

```bash
rsync -av --progress user@server_ip:/home/user/project/ project/
```

---

## Login and start work in project folder

```bash
ssh user@server_ip
cd /home/user/project
ls -la
```

---

## Start long remote job safely

```bash
nohup bash run_sim.sh > sim.log 2>&1 &
```

---

## Follow remote log file

```bash
tail -f sim.log
```

---

## Check if remote job is still running

```bash
ps aux | grep run_sim
```

---

## Download results when job is done

```bash
scp user@server_ip:/home/user/project/results.tar.gz .
```

---

# Recommended Minimum Set to Memorize

## Most useful daily commands

```bash
pwd
ls -la
cd
mkdir -p
cp -r
mv
rm -r
cat
less
grep -r
find
chmod +x
ps aux
top
ssh
scp
rsync -av --progress
tail -f
df -h
du -sh
```
