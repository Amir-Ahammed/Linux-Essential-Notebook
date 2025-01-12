# Table of Contents | Basic Linux Commands in Ubuntu 24.04
1. [File and Directory Management](#file-and-directory-management)
2. [File Permissions and Ownership](#fpo)
3. [File Manipulation](#fm)
4. [Search and Find](#sf) 
5. [Process Management](#pm) 
6. [Disk and Filesystem Management](#dfm)
7. [Networking](#n)
8. [Package Management](#pam)
9. [Archiving and Compression](#ac)
10. [System Monitoring](#sm)
11. [User Management](#um)
12. [Scheduling Tasks](#st)
13. [Copy Files from Local Machine to Remote Machine](#ctrpc)

---

### 1. File and Directory Management <a name="file-and-directory-management"></a>
- **List files and directories**
  ```bash
  ls           # Basic list
  ls -l        # Detailed view
  ls -lh       # Human-readable file sizes
  ls -a        # Show hidden files
  ```

- **Create directories**
  ```bash
  mkdir new_directory
  mkdir -p parent/child_directory # Create nested directories
  ```

- **Remove files or directories**
  ```bash
  rm file.txt                 # Delete a file
  rm -r directory/            # Delete a directory recursively
  rm -i file.txt              # Prompt before deleting
  ```

- **Copy and move files**
  ```bash
  cp source_file target_file  # Copy a file
  cp -r source_dir target_dir # Copy a directory recursively
  mv old_name new_name        # Rename or move files/directories
  ```

---

### 2. File Permissions and Ownership <a name="fpo"></a>
- **Check file permissions**
  ```bash
  ls -l filename
  ```

- **Change file permissions**  
  ```bash
  chmod 644 file.txt          # rw-r--r--
  chmod 755 script.sh         # rwxr-xr-x
  ```

- **Change file ownership**  
  ```bash
  sudo chown user:group file.txt
  sudo chown -R user:group directory/ # Recursive ownership change
  ```

---

### 3. File Manipulation  <a name="fm"></a>
- **View file contents**  
  ```bash
  cat file.txt                # Display contents
  less file.txt               # Scroll through file
  head -n 10 file.txt         # First 10 lines
  tail -n 10 file.txt         # Last 10 lines
  ```

- **Edit files (Command-line editors)**  
  ```bash
  nano file.txt               # Easy-to-use editor
  vim file.txt                # Advanced editor
  ```

---

### 4. Search and Find <a name="sf"></a>
- **Search for text in files**  
  ```bash
  grep "search_text" file.txt       # Search specific text
  grep -r "search_text" directory/ # Search recursively
  ```

- **Find files and directories**  
  ```bash
  find /path -name "file.txt"       # By name
  find /path -type d -name "dir_name" # By directory name
  ```

---

### 5. Process Management  <a name="pm"></a>
- **Check running processes**  
  ```bash
  ps aux                         # Show all processes
  top                            # Interactive process viewer
  htop                           # Enhanced top (if installed)
  ```

- **Kill a process**  
  ```bash
  kill PID                       # Kill process by PID
  killall process_name           # Kill all processes by name
  ```

- **Background and foreground jobs**  
  ```bash
  command &                      # Run command in the background
  jobs                           # List background jobs
  fg %1                          # Bring job 1 to the foreground
  ```

---

### 6. Disk and Filesystem Management <a name="dfm"></a>
- **Disk usage and free space**  
  ```bash
  df -h                          # Disk usage
  du -sh file_or_directory       # Size of file or directory
  ```

- **Mount and unmount drives**  
  ```bash
  sudo mount /dev/sdX /mnt
  sudo umount /mnt
  ```

- **Check filesystem**  
  ```bash
  fsck /dev/sdX                  # Filesystem check
  ```

---

### 7. Networking <a name="n"></a>
- **Check network information**  
  ```bash
  ip a                           # Show IP addresses
  ```

- **Test network connectivity**  
  ```bash
  ping google.com
  ```

- **Download files**  
  ```bash
  wget http://example.com/file
  curl -O http://example.com/file
  ```

---

### 8. Package Management  <a name="pam"></a>
- **Update and upgrade system**  
  ```bash
  sudo apt update                # Update package list
  sudo apt upgrade               # Upgrade installed packages
  ```

- **Install and remove packages**  
  ```bash
  sudo apt install package_name
  sudo apt remove package_name
  ```

- **Search for packages**  
  ```bash
  apt search package_name
  ```

---

### 9. Archiving and Compression  <a name="ac"></a>
- **Create and extract tar archives**  
  ```bash
  tar -cvf archive.tar file1 file2
  tar -xvf archive.tar           # Extract archive
  tar -czvf archive.tar.gz file  # Compress with gzip
  tar -xzvf archive.tar.gz       # Extract gzip archive
  ```

---

### 10. System Monitoring  <a name="sm"></a>
- **Check system information**  
  ```bash
  uname -a                       # System info
  lsb_release -a                 # Ubuntu version
  ```

- **Memory and CPU usage**  
  ```bash
  free -h                        # Memory usage
  uptime                         # System uptime and load
  ```

---

### 11. User Management  <a name="um"></a>
- **Add a new user**  
  ```bash
  sudo adduser username
  ```
- **Add the user to the sudo group**
  ```bash
  sudo usermod -aG sudo <username>
  ``` 

- **Switch user**  
  ```bash
  su - username
  ```

- **Check logged-in users**  
  ```bash
  who
  ```

---

### 12. Scheduling Tasks  <a name="st"></a>
- **View cron jobs**  
  ```bash
  crontab -l
  ```

- **Edit cron jobs**  
  ```bash
  crontab -e
  ```

- **Schedule a one-time task**  
  ```bash
  at 2pm
  ```

---

### 13. Copy Files from Local Machine to Remote Machine <a name="ctrpc"></a>

To copy files from your **local** Ubuntu machine to a **remote** machine, use the **SCP (Secure Copy Protocol)** tool:

#### **Syntax for SCP**:
```bash
scp [options] user@source_host:/path/to/source_file /path/to/destination
```
- `user`: The username on the remote machine.
- `source_host`: The IP address or hostname of the remote machine.
- `/path/to/source_file`: The file or directory you want to copy.
- `/path/to/destination`: The location where you want to copy the file on your local machine.

#### **Example: Copy a file to a remote machine**
```bash
scp /home/youruser/file.txt user@192.168.1.100:/home/user/
```
This command will copy `file.txt` from your local machine to the `/home/user/` directory on the remote machine.

#### **Example: Copy a directory to the remote machine**
```bash
scp -P 8181 /home/amir/Downloads/donate.tar amir@192.168.1.81:/home/amir/
```
This will copy the `directory` and its contents from your local machine to the remote machine.
