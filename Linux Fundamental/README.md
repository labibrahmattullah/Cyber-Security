# 🐧 Linux Debian — Command Fundamentals

<div align="center">

![Debian](https://img.shields.io/badge/Debian-Linux-A81D33?style=for-the-badge&logo=debian&logoColor=white)
![Shell](https://img.shields.io/badge/Shell-Bash-4EAA25?style=for-the-badge&logo=gnubash&logoColor=white)
![Level](https://img.shields.io/badge/Level-Beginner%20→%20Intermediate-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)

<br/>

> *"The command line is the single most important tool for a Linux user — master it, and the system is yours."*

<br/>

A comprehensive guide to basic and intermediate commands on the **Debian Linux** operating system, systematically structured to build a solid foundation in terminal utilization.

</div>

---

## 📋 Table of Contents

- [Introduction to Debian Linux](#-introduction-to-debian-linux)
- [Linux Filesystem Structure](#-linux-filesystem-structure)
- [Directory Navigation](#-directory-navigation)
- [File & Directory Management](#-file--directory-management)
- [Viewing & Editing Files](#-viewing--editing-files)
- [User & Group Management](#-user--group-management)
- [Permission & Ownership](#-permission--ownership)
- [Process Management](#-process-management)
- [Package Management (APT)](#-package-management-apt)
- [Networking Commands](#-networking-commands)
- [Disk & Storage Management](#-disk--storage-management)
- [System Information & Monitoring](#-system-information--monitoring)
- [Archiving & Compression](#-archiving--compression)
- [Searching & Filtering](#-searching--filtering)
- [Shell & Environment](#-shell--environment)
- [Systemd & Service Management](#-systemd--service-management)
- [Firewall (UFW & iptables)](#-firewall-ufw--iptables)
- [SSH & Remote Access](#-ssh--remote-access)
- [Shell Scripting Basics](#-shell-scripting-basics)
- [Useful Shortcuts & Tips](#-useful-shortcuts--tips)

---

## 🔍 Introduction to Debian Linux

**Debian** is one of the oldest and most stable Linux distributions, first released in 1993 by Ian Murdock. Debian serves as the upstream foundation for many popular distributions such as Ubuntu, Kali Linux, and Parrot OS.

**Key Advantages of Debian:**
- Exceptionally stable and reliable (ideal for server environments)
- Features one of the largest package repositories (~59,000+ packages)
- Implements the powerful APT package management system
- Extensive community support and comprehensive documentation
- Highly versatile for production servers, desktops, and embedded systems

**Debian Releases:**

| Codename | Status | Description |
|----------|--------|-------------|
| Bookworm (12) | Stable | Current stable release |
| Bullseye (11) | Oldstable | Still supported |
| Trixie (13) | Testing | Next upcoming stable release |
| Sid | Unstable | Rolling release, primarily for developers |

---

## 📁 Linux Filesystem Structure

```
/  (root — the top-level directory of the entire filesystem)
│
├── bin/        → Essential command binaries (ls, cp, mv, cat)
├── boot/       → Bootloader files (GRUB, kernel)
├── dev/        → Hardware device nodes (disks, USBs, terminals)
├── etc/        → Host-specific system-wide configuration files (hosts, fstab, apt)
│   ├── apt/        → APT package manager configurations
│   ├── network/    → Network configuration parameters
│   └── ssh/        → SSH server/client configuration files
├── home/       → Personal home directories for regular users (/home/username)
├── lib/        → Shared system libraries required by binaries in /bin and /sbin
├── media/      → Mount points for auto-mounted removable devices
├── mnt/        → Mount points for temporary manually-mounted filesystems
├── opt/        → Optional add-on third-party application packages
├── proc/       → Virtual filesystem providing process and kernel information
├── root/       → Dedicated home directory for the superuser (root)
├── run/        → Volatile runtime data describing the system since last boot
├── sbin/       → Essential system administration binaries
├── srv/        → Data for site-specific services provided by the system (web, ftp)
├── sys/        → Virtual filesystem providing device and hardware information
├── tmp/        → Temporary files (automatically cleared upon reboot)
├── usr/        → User programs, libraries, and secondary hierarchy data
│   ├── bin/        → Non-essential user binaries (python3, vim, git)
│   ├── lib/        → Libraries for binaries within /usr/bin
│   ├── local/      → Secondary hierarchy for locally compiled/installed programs
│   └── share/      → Architecture-independent static shareable data (documentation, icons)
└── var/        → Variable data files (logs, databases, administrative caches)
├── log/        → System log files
├── www/        → Default web server root directory
└── cache/      → Volatile application cache data    
```

---

## 🧭 Directory Navigation

```bash
# Print working directory: Displays the current absolute path
pwd
# Output: /home/user

# Change directory
cd /var/log            # Navigate to an absolute path
cd Documents           # Navigate to a relative subdirectory
cd ..                  # Move up one level to the parent directory
cd ../..               # Move up two levels in the hierarchy
cd ~                   # Navigate directly to the current user's home directory
cd -                   # Switch back to the previous working directory

# List directory contents
ls                     # Lists files and folders in the current location
ls -l                  # Long listing format (displays permissions, size, owner)
ls -a                  # Reveals hidden files (files prefixed with a dot, e.g., .bashrc)
ls -la                 # Combined: Detailed view including hidden files
ls -lh                 # Displays file sizes in human-readable format (KB, MB, GB)
ls -lt                 # Sorts entries by modification time (newest first)
ls -lR                 # Recursive listing: Displays all subdirectories and their contents
ls /etc                # Lists contents of a specified target directory

# Visualizing directory structure as a tree
tree                   # Displays a graphical directory tree from the current location
tree -L 2              # Restricts the tree depth to 2 levels
tree -a                # Includes hidden files in the tree display
# Installation: apt install tree
```

---

## 📂 File & Directory Management

### Creating Files & Directories

```# Creating empty files
touch filename.txt
touch file1.txt file2.txt file3.txt    # Create multiple files simultaneously

# Creating directories
mkdir mydirectory
mkdir -p /path/to/nested/dir           # Create nested parent directories recursively
mkdir -m 755 mydirectory               # Create a directory with specific inline permissions

# Creating files with immediate content
echo "Hello, Debian!" > file.txt       # Write/overwrite string to a file
echo "Additional line" >> file.txt      # Append string to the end of a file
cat > file.txt << EOF
First line
Second line
Third line
EOF
```

### Copying, Moving, & Renaming

```bash
# Copying files and directories (copy)
cp source.txt destination.txt          # Copy a file
cp -r source_dir/ destination_dir/    # Copy a directory recursively
cp -i file.txt /path/                  # Interactive: Prompt before overwriting an existing file
cp -v file.txt /path/                  # Verbose: Display progress output
cp -p file.txt /backup/                # Preserve file attributes (timestamp, permissions)
cp -u source dest                      # Update: Copy only if source is newer than destination

# Moving & Renaming (move)
mv oldname.txt newname.txt             # Rename a file
mv file.txt /path/to/destination/      # Move a file to another directory
mv -i source dest                      # Interactive prompt on overwrite
mv -v source dest                      # Verbose output mode

# Deleting (remove)
rm filename.txt                        # Delete a file permanently
rm -i filename.txt                     # Interactive: Prompt prior to deletion
rm -f filename.txt                     # Force deletion without prompting or warnings
rm -r mydirectory/                     # Delete a directory and its contents recursively
rm -rf mydirectory/                    # Force recursive deletion of a directory (Use with extreme caution!)
rmdir mydirectory/                     # Delete empty directories only

# Creating links
ln -s /path/to/original /path/to/link # Create a symbolic link (symlink)
ln /path/to/original /path/to/link    # Create a hard link
```

---

## 📄 Viewing & Editing Files

### Displaying File Contents

```bash
# Display entire file contents
cat filename.txt
cat -n filename.txt                    # Display contents with line numbers
cat -A filename.txt                    # Show all hidden non-printing characters

# Pagination (for reading long files)
less filename.txt                      # Interactive navigation: ↑↓ keys, 'q' to exit
more filename.txt                      # Simple pagination: scroll down line-by-line or page-by-page

# Display specific portions of a file
head filename.txt                      # Output the first 10 lines (default)
head -n 20 filename.txt                # Output the first 20 lines
tail filename.txt                      # Output the last 10 lines
tail -n 20 filename.txt                # Output the last 20 lines
tail -f /var/log/syslog                # Follow: Monitor file additions in real-time (ideal for logs)

# Inspecting file properties
file filename.txt                      # Determine and identify file type
wc filename.txt                        # Count lines, words, and characters
wc -l filename.txt                     # Count lines only
wc -w filename.txt                     # Count words only
stat filename.txt                      # Display comprehensive file metadata status

# Comparing file modifications
diff file1.txt file2.txt               # Display differences between files
diff -u file1.txt file2.txt            # Unified format output (more readable)
```

### Text Editors

```bash
# nano — straightforward, lightweight text editor ideal for beginners
nano filename.txt
# Essential nano shortcuts:
#   Ctrl+O  → Save changes
#   Ctrl+X  → Exit editor
#   Ctrl+K  → Cut line
#   Ctrl+U  → Paste line
#   Ctrl+W  → Search text

# vim — advanced, highly efficient and powerful modal text editor
vim filename.txt
# Vim operation modes:
#   i       → Insert mode (start typing text)
#   Esc     → Return to Normal mode
#   :w      → Save changes (write)
#   :q      → Exit editor (quit)
#   :wq     → Save changes and exit
#   :q!     → Exit forcefully without saving changes
#   /keyword→ Search for text matching the keyword

# Inline text modification using sed (stream editor)
sed -i 's/old_word/new_word/g' file.txt     # Replace all string occurrences inside file
sed -n '5,10p' file.txt                     # Output lines 5 through 10 explicitly
sed '/^#/d' file.txt                        # Delete and filter out all comment lines
```

---

## 👥 User & Group Management

```bash
# ── USER INFORMATION ────────────────────────────────────────
whoami                          # Display the username of the current active session
id                              # Display current UID, GID, and effective groups
id username                     # Display user information for a specific account
who                             # Show a list of users currently logged into the system
w                               # Show logged-in users alongside their current active processes
last                            # Display a historical log of recent user logins
finger username                 # Display detailed biographical info about a user (if installed)
cat /etc/passwd                 # View the comprehensive system user registry database

# ── CREATING & MANAGING USERS ───────────────────────────────
sudo adduser username           # Create a new user (Interactive shell script, recommended)
sudo useradd username           # Low-level utility to add a user (Non-interactive, manual setup required)
sudo useradd -m -s /bin/bash -G sudo username  # Create user with home directory + bash shell + sudo group

sudo passwd username            # Modify or set the password for a specific user
sudo passwd -l username         # Lock (suspend) a specific user account password
sudo passwd -u username         # Unlock a suspended user account password
sudo passwd -e username         # Force user to change password on their next login attempt

sudo usermod -aG sudo username  # Append Group: Add an existing user to the secondary 'sudo' group
sudo usermod -aG group1,group2 user  # Add a user to multiple secondary groups simultaneously
sudo usermod -s /bin/zsh user   # Change the default login shell for a user
sudo usermod -l newname oldname # Modify a user account login name (username)
sudo usermod -d /new/home user  # Define a new absolute path for a user's home directory

sudo deluser username           # Delete a user account (preserves the home directory)
sudo deluser --remove-home username  # Delete a user account along with their home directory
sudo userdel -r username        # Alternative command to completely remove user + home directory

# ── GROUP MANAGEMENT ────────────────────────────────────────
cat /etc/group                  # View the system group definition registry
groups username                 # List all group associations for a specific user
sudo groupadd groupname         # Create a new system group
sudo groupdel groupname         # Delete an existing system group
sudo gpasswd -d user group      # Remove a specific user from a defined group

# ── SWITCHING USER SESSIONS ─────────────────────────────────
su - username                   # Switch user to another account session with environment variables
sudo su -                       # Elevate privileges to a root user environment shell
sudo -i                         # Invoke an interactive root login shell session
sudo command                    # Execute a single administrative command with root privileges
sudo -u username command        # Execute a command as a specifically designated user
exit / logout                   # Terminate the current user shell session
```

---

## 🔐 Permission & Ownership

### Understanding Linux Permissions

```
Contoh output: -rwxr-xr--  1  user  group  4096  Jan 01  file.txt

Karakter 1   : Tipe (-=file, d=direktori, l=symlink, b=block, c=char)
Karakter 2-4 : Permission Owner  (rwx = read+write+execute)
Karakter 5-7 : Permission Group  (r-x = read+execute)
Karakter 8-10: Permission Others (r-- = read only)

Nilai Oktal:
  r (read)    = 4
  w (write)   = 2
  x (execute) = 1
  - (none)    = 0

Contoh kombinasi:
  7 = rwx (4+2+1) → Full permission
  6 = rw- (4+2+0) → Read & Write
  5 = r-x (4+0+1) → Read & Execute
  4 = r-- (4+0+0) → Read only
  0 = --- (0+0+0) → No permission
```

### Change Permission (chmod)

```bash
# Octal Notation (Absolute Mode)
chmod 755 filename      # rwxr-xr-x  (owner=7, group=5, others=5)
chmod 644 filename      # rw-r--r--  (Standard configuration for regular files)
chmod 600 filename      # rw-------  (Private access configuration for sensitive files)
chmod 777 filename      # rwxrwxrwx  (Global open permission configuration — avoid using!)
chmod 400 filename      # r--------  (Read-only restricted strictly to the file owner)
chmod -R 755 directory/ # Apply permissions recursively across an entire directory tree

# Symbolic Notation (Relative Mode)
chmod u+x filename      # Grant execute permission to the user (owner)
chmod g-w filename      # Revoke write permission from the group
chmod o+r filename      # Grant read permission to others
chmod a+x filename      # Grant execute permission universally to all tiers (all)
chmod u=rwx,g=rx,o=r filename  # Define explicit granular controls simultaneously

# Special Access Permissions
chmod +t directory/     # Sticky bit (restricts deletion within directory strictly to the file owner)
chmod u+s filename      # SUID (executable runs utilizing the privileges of the file owner)
chmod g+s directory/    # SGID (newly created items inherit the parent directory's group ownership)
chmod 1755 directory/   # Sticky bit application utilizing octal syntax representation
```

### Adjusting Ownerwhip (chown & chgrp)

```bash
# Modifying ownership parameters
chown username filename                 # Modify the owner of a file
chown username:groupname filename       # Modify both owner and group attributes simultaneously
chown -R username:groupname directory/  # Apply ownership changes recursively to a directory tree
chown :groupname filename               # Modify group association exclusively

# Modifying group parameters exclusively
chgrp groupname filename
chgrp -R groupname directory/

# Auditing file system security contexts
ls -la                  # View comprehensive file permission parameters
stat filename           # Review absolute breakdown including numerical octal representations
getfacl filename        # Retrieve the Access Control Lists (ACLs) configuration
setfacl -m u:user:rwx file  # Assign custom external granular ACL privileges to a specified user
```

---

## ⚙️ Process Management

```bash
# ── PROCESS AUDITING ────────────────────────────────────────
ps                              # Display running processes associated with the current terminal session
ps aux                          # Display all running system processes from all users (BSD syntax style)
ps -ef                          # Display all running processes across the system (UNIX syntax style)
ps -ef | grep nginx             # Search and filter out a specific active process by name
ps -u username                  # List active processes belonging exclusively to a designated user
pstree                          # Display running processes represented as a hierarchical tree structure
top                             # Dynamic, interactive real-time process and system resource monitor
htop                            # Enhanced interactive process and resource visualization tool
                                # (requires installation: apt install htop)

# ── INTERACTIVE CONTROLS ────────────────────────────────────
# Operations within top/htop interfaces:
#   q → Exit interface session
#   k → Send process termination signal (requires target PID)
#   r → Renice: adjust process priority scheduling execution
#   P → Sort processes based on CPU usage metrics
#   M → Sort processes based on Memory allocation metrics
#   / → Initiate process lookup query filter

# ── SIGNALS & PROCESS TERMINATION ───────────────────────────
kill PID                        # Send SIGTERM (15) — Request a clean, graceful process shutdown
kill -9 PID                     # Send SIGKILL (9) — Force an immediate kernel process termination
kill -15 PID                    # Send SIGTERM (default execution standard)
kill -HUP PID                   # Send SIGHUP (1) — Instruct a daemon to reload its configuration files
killall process_name            # Terminate all running processes matching the exact string name
pkill -f "process_name"         # Terminate running processes utilizing a pattern-matching filter
pkill -u username               # Terminate all active running processes belonging to a specific user

# ── BACKGROUND & FOREGROUND OPERATIONS ──────────────────────
command &                      # Append an ampersand to initiate a process immediately in the background
jobs                            # List active background jobs started from the current terminal session
fg                              # Bring the most recent background job forward to the active foreground
fg %1                           # Bring background job ID number 1 to the active foreground session
bg %1                           # Resume a suspended or paused job background execution state
Ctrl+Z                          # Suspend Job: Freeze and pause the current active foreground process
Ctrl+C                          # Abort Job: Terminate the current foreground process execution state

# ── PERSISTENT PROCESS EXECUTION ────────────────────────────
nohup command &                # Run command immune to hangups, allowing background execution after logout
nohup command > output.log &   # Persistent background execution redirecting standard output logs to file
screen                          # Invoke a virtual terminal multiplexer session (apt install screen)
tmux                            # Modern terminal multiplexer tool for session persistence (apt install tmux)

# ── SCHEDULING PRIORITIES ───────────────────────────────────
nice -n 10 command             # Launch a command running on low scheduling priority (value 10)
nice -n -5 command             # Launch a command running on high scheduling priority (Requires root/sudo)
renice 10 -p PID                # Dynamically alter the priority value of an actively running process
```

---

## 📦 Package Management (APT)

APT (Advanced Package Tool) adalah sistem manajemen paket resmi Debian dan turunannya.

```bash
# ── INDEX UPDATES & UPGRADES ────────────────────────────────
sudo apt update                     # Synchronize local package registries with upstream repositories
sudo apt upgrade                    # Safely upgrade all outdated installed software packages
sudo apt full-upgrade               # Perform upgrades handling complex changing dependency structures
sudo apt dist-upgrade               # Legacy distribution upgrade tool version
sudo apt-get update && sudo apt-get upgrade -y  # Automated package maintenance (non-interactive auto-yes)

# ── INSTALLATION ARTIFACTS ──────────────────────────────────
sudo apt install packagename          # Download and install a package from configured repositories
sudo apt install pkg1 pkg2          # Supply multiple package parameters for simultaneous installation
sudo apt install -y packagename       # Auto-confirm installation steps avoiding interactive validation prompts
sudo apt install --no-install-recommends packagename  # Suppress optional recommended dependency packages
sudo apt install ./packagename.deb    # Handle installation from a local .deb file package using APT
sudo dpkg -i packagename.deb          # Use low-level dpkg utility to install a local binary package file
sudo apt install -f                 # Fix broken dependencies: Resolve unmet architectural package rules

# ── PACKAGE REMOVAL ─────────────────────────────────────────
sudo apt remove packagename           # Uninstall software package binary binaries but preserve configuration logs
sudo apt purge packagename            # Completely purge a software package along with all configuration modifications
sudo apt autoremove                 # Clean up orphaned packages originally installed as necessary dependencies
sudo apt autoclean                  # Purge obsolete downloaded archive files from local cache
sudo apt clean                      # Wipe out the local repository directory of cached package files

# ── SEARCHING & DIAGNOSTICS ─────────────────────────────────
apt search packagename                # Query repositories looking for package records matching a keyword
apt show packagename                  # Retrieve an absolute metadata summary record of a targeted package
apt list --installed                # Return a comprehensive list of all software packages installed on system
apt list --upgradable               # Isolate and list all available installable package upgrades
dpkg -l                             # Generate a comprehensive list of tracked package states via dpkg
dpkg -l | grep packagename            # Validate if a specific package is registered as installed
dpkg -L packagename                   # Map and print out every asset path provisioned by a specific package
dpkg -S /path/to/file               # Reverse-lookup: Find which package provisioned a specific absolute file path
which programname                   # Locate and return the path pointing to an executable's binary destination

# ── REPOSITORY SOURCES ──────────────────────────────────────
cat /etc/apt/sources.list           # View the upstream package archive connection endpoints configuration file
ls /etc/apt/sources.list.d/         # List internal repository configurations provisioned by independent vendors
sudo add-apt-repository ppa:name/ppa  # Bind an external Personal Package Archive endpoint (Ubuntu ecosystems)
sudo apt-key adv --keyserver ...    # Authenticate external archives by registering cryptographic GPG keys
```

---

## 🌐 Networking Commands

```bash
# ── NETWORK INTERFACE RECONNAISSANCE ────────────────────────
ip addr                         # Display all physical and virtual network interfaces alongside IP allocations
ip addr show eth0               # Display attributes exclusively for network interface 'eth0'
ifconfig                        # Legacy interface diagnostics tracking (requires package: apt install net-tools)
ip link show                    # Map operational connection state variables across link layer interfaces
ip route                        # Review active IP routing table configurations
ip route show default           # Identify the system default gateway path configuration
hostname                        # Return the alphanumeric identifier assigned to system host
hostname -I                     # Isolate and display all valid assigned IP addresses belonging to host
cat /etc/hosts                  # Inspect static host definition lookup files
cat /etc/resolv.conf            # Verify upstream DNS nameserver allocation paths
cat /etc/network/interfaces     # Review core interfaces mapping files (classic Debian network engine)

# ── CONNECTIVITY DIAGNOSTICS ────────────────────────────────
ping google.com                 # Send ICMP ECHO_REQUEST packets to verify external network reachability
ping -c 4 google.com            # Restrict network diagnostic echo sequence to 4 packet attempts
ping -i 2 google.com            # Enforce a 2-second delay window spacing between individual ICMP packets
traceroute google.com           # Map out transit route hops across gateway path segments (apt install traceroute)
tracepath google.com            # Trace network path attributes omitting privileged permissions
mtr google.com                  # Invoke an interactive real-time combined ping/traceroute diagnostic tool (apt install mtr)

# ── DNS RECORD RESOLUTION ───────────────────────────────────
nslookup domain.com             # Execute a basic interactive nameserver diagnostic query
dig domain.com                  # Perform an extensive structural domain nameserver validation probe
dig domain.com MX               # Target domain records focusing exclusively on mail exchange entries
dig +short domain.com           # Extract bare IP configuration values omitting informational metadata
host domain.com                 # Quick standard resolution utility mapping names to target IP endpoints
whois domain.com                # Query global databases to audit registration records for a domain

# ── SOCKET & PORT AUDITING ──────────────────────────────────
ss -tulnp                       # Map open listening sockets displaying underlying process targets (modern standard)
netstat -tulnp                  # Audit network sockets (Legacy alternative; requires package: apt install net-tools)
ss -s                           # Generate a statistical summary tracking active socket connections
lsof -i :80                     # Audit processes binding and asserting ownership on network Port 80
lsof -i TCP                     # Isolate active system resource links to TCP communication vectors
nmap localhost                  # Port scanner: Audit local interface connection exposures (apt install nmap)
nmap -p 22,80,443 target_ip     # Run port validation targeting specific core communication vectors

# ── FILE TRANSFER PROTOCOLS ─────────────────────────────────
wget https://url/file           # Network downloader: Retrieve an asset from an external endpoint URL
wget -O output.zip https://url  # Retrieve a remote asset mapping output to a custom file parameter destination
wget -c https://url             # Direct downloader engine to resume broken or disconnected asset transfers
wget -r https://website         # Initiate a recursive mirror sequence downing web layout architectures
curl https://url                # Evaluate HTTP connections rendering output contents to standard output stream
curl -O https://url/file        # Download file saving artifact under its original remote file string name
curl -L https://url             # Configure execution variables to follow upstream HTTP redirect paths
curl -u user:pass https://url   # Pass string credentials to evaluate basic HTTP authentication challenges
curl -X POST -d "data" https://url  # Construct and submit an explicit HTTP POST data transaction request

# SCP (Secure Copy Protocol via SSH Layer)
scp file.txt user@host:/path/             # Upload an asset directly to a remote host destination path
scp user@host:/path/file.txt ./           # Download a remote asset extracting it to the current path
scp -r directory/ user@host:/path/        # Recursively execute file layer sync operations for directories
scp -P 2222 file.txt user@host:/path/     # Inject parameter flags to target non-standard SSH port bounds

# Rsync (Optimized File Synchronization Engine)
rsync -avz source/ dest/                  # Sync assets locally archiving meta settings applying compression
rsync -avz -e ssh source/ user@host:dest/ # Securely sync localized datasets across remote nodes via SSH tunnels
rsync -avz --delete source/ dest/         # Synchronize folders executing mirror deletes on orphaned targets
rsync --progress source dest              # Enable active diagnostic metrics tracking block sync states
```

---

## 💾 Disk & Storage Management

```bash
# ── DISK UTILIZATION ANALYSIS ───────────────────────────────
df -h                           # Display disk capacity across mounted filesystems in human-readable notation
df -hT                          # Append filesystem definition classification parameters to capacity summary
du -sh /path/                   # Calculate total cumulative data consumption metrics for a specific folder
du -sh * # Evaluate consumption metrics formatting individual entries across current path
du -sh /* | sort -rh | head -10 # Isolate and list the top 10 most space-consuming systems folders off Root
ncdu /                          # Open an interactive curse-based system disk consumption analyzer (apt install ncdu)

# ── HARDWARE TRACKING ───────────────────────────────────────
lsblk                           # Map and list storage block devices displaying partition bounds
lsblk -f                        # Append operational configuration data tracking UUID markers and filesystem tags
fdisk -l                        # List low-level structural partition layouts across tracked drives (Requires root)
sudo fdisk -l /dev/sda          # Isolate partition tables mapping parameters specifically for a target disk drive
blkid                           # Output specific block device attributes tracing validation UUID indicators
cat /proc/partitions            # Interrogate kernel layer metrics mapping system partition allocations

# ── DRIVE PARTITION PROCEDURES ──────────────────────────────
sudo fdisk /dev/sdb             # Open an interactive menu engine to build MBR/GPT partition labels
sudo parted /dev/sdb            # Execute advanced structural storage tier provisioning processes
sudo cfdisk /dev/sdb            # Invoke a user-friendly graphical terminal partition management interface

# ── FILESYSTEM INITIALIZATION ───────────────────────────────
sudo mkfs.ext4 /dev/sdb1        # Initialize an EXT4 filesystem structure on a targeted drive block
sudo mkfs.xfs /dev/sdb1         # Initialize a high-performance corporate XFS filesystem layout layer
sudo mkswap /dev/sdb2           # Initialize low-level operational structural bounds for system Swap allocations

# ── MOUNT POINT OPERATIONS ──────────────────────────────────
sudo mount /dev/sdb1 /mnt/data         # Bind a storage hardware partition directly onto a target directory node
sudo mount -t ext4 /dev/sdb1 /mnt/     # Force a mount mapping asserting an explicit filesystem classification rule
sudo umount /mnt/data                  # Sever hardware mounting mappings resolving system connection locks
sudo umount -l /mnt/data               # Execute a lazy unmount immediately decoupling references during operations
mount                                  # Summary list capturing every active storage tier mount point mapping
cat /etc/fstab                         # Review persistent drive mount rule matrices mapped during boot procedures

# ── SWAP MANAGEMENT ─────────────────────────────────────────
free -h                         # Summary log tracking active memory distribution matching physical RAM and Swap spaces
swapon --show                   # Map out attributes defining currently engaged memory virtualization spaces
sudo swapon /dev/sdb2           # Activate an isolated storage layer allocation to join system Swap pools
sudo swapoff /dev/sdb2          # Decouple and suspend swap assignments on a targeted storage block node

# Provisions for building a custom file-based Swap configuration
sudo fallocate -l 2G /swapfile  # Allocate a rigid unfragmented data block boundary sizing 2 Gigabytes
sudo chmod 600 /swapfile        # Assert tight access permissions locking out unprivileged reading access
sudo mkswap /swapfile           # Direct formatting engine to transform the asset space into a swap layer block
sudo swapon /swapfile           # Dynamically loop and register the local swap asset file into active memory maps
```

---

## 📊 System Information & Monitoring

```bash
# ── SYSTEM METRICS RECONNAISSANCE ───────────────────────────
uname -a                        # Generate a complete data string summarizing kernel and host architectures
uname -r                        # Output operational classification tracking current active kernel release
cat /etc/os-release             # Query structural data describing current active OS distribution properties
lsb_release -a                  # Audit Linux Standard Base metrics clarifying distro configurations (apt install lsb-release)
hostnamectl                     # Interface managing persistent host settings displaying core platform specs
uptime                          # Summary reporting how long the platform has executed alongside system load averages
uptime -p                       # Simplify platform uptime logging applying a readable time formatting syntax
date                            # View system chronological logs displaying current date and time calculations
timedatectl                     # Comprehensive time interface logging active time zones and network sync status

# ── HARDWARE SPECS INVENTORY ────────────────────────────────
lscpu                           # Generate a modular architecture breakdown tracking central processing specs
lsmem                           # Audit physical storage structures tracking capacity boundaries for memory units
lspci                           # Inventory peripheral component infrastructure bridges (Graphics chips, Network interface cards)
lsusb                           # Map structural data outlining items binding to universal serial bus slots
lshw                            # Deep inventory utility detailing general underlying hardware configurations (apt install lshw)
lshw -short                     # Generate a highly dense structural summary indexing key system hardware paths
dmidecode                       # Extract hardware configuration details raw out of BIOS/DMI tables (Requires root)
cat /proc/cpuinfo               # Interrogate the kernel file engine to parse system microarchitecture configurations
cat /proc/meminfo               # Interrogate active system file buffers tracking runtime memory parameters

# ── REAL-TIME ENVIRONMENT PERFORMANCE MONITORING ────────────
top                             # Invoke standard dynamic monitoring mapping processes against continuous CPU and RAM traces
htop                            # Launch an advanced interactive multi-color analytical panel rendering real-time performance
vmstat 1                        # Run looping traces tracking virtual memory usage steps sampled every second
iostat 1                        # Log operational statistics tracking throughput metrics for drive input/output arrays
iotop                           # Map storage execution costs identifying read/write operations per process (apt install iotop)
iftop                           # Monitor communication interface utilization tracking connection bandwidth (apt install iftop)
nload                           # Launch structural graphics monitoring incoming and outgoing network traffic vectors (apt install nload)
glances                         # Open an extensive monitoring control panel dashboard capturing global specs (apt install glances)
watch -n 2 'df -h'              # Command looper: Execute a script pattern repeatedly capturing differences every 2 seconds

# ── KERNEL & SYSTEM JOURNAL DIAGNOSTICS ─────────────────────
journalctl                      # Access the comprehensive historical system journal registry managed by systemd
journalctl -b                   # Filter target log views isolating events tracking only the current boot cycle
journalctl -f                   # Engaged log tracking: Keep stream open printing new system events in real-time
journalctl -u nginx             # Restrict diagnostic data trace windows tracking a specific system service target
journalctl --since "1 hour ago" # Construct a time-bounded search constraint focusing on recent operational windows
journalctl -p err               # Implement filter parameters isolating critical diagnostic indicators (err, warning, info)
tail -f /var/log/syslog         # Continuously tail general operating logs processing standard system updates
tail -f /var/log/auth.log       # Monitor authentication records auditing local system access procedures
less /var/log/dpkg.log          # Read through package layer modification logs tracking platform installations
```

---

## 🗜️ Archiving & Compression

```bash
# ── TAR (Tape Archive Framework) ────────────────────────────
# Packing assets into archives
tar -cvf archive.tar directory/          # Assemble an uncompressed archive container file
tar -czvf archive.tar.gz directory/      # Pack a folder compressing it utilizing the Gzip algorithm
tar -cjvf archive.tar.bz2 directory/    # Pack a folder compressing it utilizing the Bzip2 algorithm
tar -cJvf archive.tar.xz directory/     # Pack a folder compressing it utilizing the high-efficiency XZ algorithm

# Unpacking archive containers
tar -xvf archive.tar                     # Unpack standard tape archive container contents to current path
tar -xzvf archive.tar.gz                 # Unpack a compressed Gzip archive block asset file
tar -xjvf archive.tar.bz2               # Unpack a compressed Bzip2 archive block asset file
tar -xJvf archive.tar.xz                # Unpack a compressed XZ archive block asset file
tar -xvf archive.tar -C /target/path/   # Decompress target data extracting outputs straight to a remote folder destination

# Previewing structural indices omitting unpack writes
tar -tvf archive.tar                     # Parse and display directory contents mapped inside an archive file
tar -tzvf archive.tar.gz                 # Inspect internal folder maps bound within a Gzip container file

# Summary index referencing key flag operations:
#   -c → Create a brand-new archive file target
#   -x → Extract data containers rewriting targets locally
#   -t → Tabulate: output structural components mapping inside asset
#   -v → Verbose: output file strings actively processing during runtime
#   -f → Enforce command focus mapping targets directly onto a file name variable
#   -z → Route processing pipeline layers to process Gzip encryption adjustments
#   -j → Route processing pipeline layers to process Bzip2 encryption adjustments
#   -J → Route processing pipeline layers to process XZ encryption adjustments
#   -C → Redirect target directory output paths to a defined location

# ── ZIP UTILIZATION ARTIFACTS ───────────────────────────────
zip -r archive.zip directory/            # Build an archived dataset mapping folder components recursively
zip archive.zip file1 file2             # Target independent multi-file items packing them to a common zip target
unzip archive.zip                        # Decompress a generic zip data package rendering assets to active path
unzip archive.zip -d /target/path/       # Route decompression engines writing extracted data to a precise folder destination
unzip -l archive.zip                     # Run indexing functions listing file contents embedded inside zip without extraction
unzip -p archive.zip file.txt            # Stream a specific nested asset string file out to standard output directly

# ── GZIP & BZIP2 ENGINES ────────────────────────────────────
gzip file.txt                          # Compress a single targeted file transforming asset to file.txt.gz format
gzip -d file.txt.gz                    # Execute a reverse decompression routine stripping away .gz attributes
gunzip file.txt.gz                     # Functional equivalent command execution managing Gzip expansion states
gzip -k file.txt                       # Force compression processing loops while maintaining original base uncompressed files
bzip2 file.txt                         # Compress a targeted data asset creating a file.txt.bz2 payload
bunzip2 file.txt.bz2                   # Execute extraction routines stripping away .bz2 data block parameters
```

---

## 🔍 Searching & Filtering

```bash
# ── FIND (File System Discovery Operations) ──────────────────
find /path -name "filename"            # Locate files matching precise structural string terms (Case-sensitive)
find /path -iname "filename"           # Run a flexible file discovery query ignoring character casing properties
find /path -name "*.log"              # Apply wildcard parameters filtering system elements by custom extension types
find /path -type f                     # Restrict file validation scans exclusively to standard physical files
find /path -type d                     # Restrict searching functions exclusively to directory paths
find /path -type l                     # Scan system layouts tracking exposed symbolic links exclusively
find /path -size +100M                 # Locate files displaying space footprints exceeding 100 Megabytes
find /path -size -1k                   # Locate sparse small files tracking storage metrics under 1 Kilobyte
find /path -mtime -7                   # Identify components displaying active modifications within the last week
find /path -mtime +30                  # Filter structures showing ancient usage states modified over a month ago
find /path -user username              # Isolate files owned exclusively by a specific system identity descriptor
find /path -group groupname            # Isolate files holding explicit administrative group assignments
find /path -perm 777                   # Scan network storage looking for files matching dangerous 777 permissions
find /path -perm -o+w                  # Audit security positions hunting for items giving write permission to global users (others)
find /path -empty                      # Locate vacant zero-byte files or empty system directory paths

# Compounding Find Operations with Action Triggers
find /path -name "*.log" -delete       # Automated purge: Locate all logs matching parameters and delete them
find /path -name "*.txt" -exec chmod 644 {} \;  # Execute inline configuration adjustments across discovered files
find /tmp -mtime +7 -exec rm -f {} \; # Locate ancient cache elements inside temp files older than 7 days and clear them

# ── GREP (Regular Expression Content Analysis) ──────────────
grep "keyword" filename.txt               # Parse a target document printing rows containing the exact text sequence
grep -i "keyword" filename.txt            # Execute content scanning passes ignoring upper/lowercase constraints
grep -r "keyword" /path/                  # Run recursive parsing passes traversing entire directory file layers
grep -n "keyword" filename.txt            # Trace text matches rendering respective structural file line numbers
grep -v "keyword" filename.txt            # Inverse Filter: Print only the lines that DO NOT match the search string
grep -c "keyword" filename.txt            # Aggregate computational counting logging matching string line events
grep -l "keyword" /path/* # Suppress raw match rows returning only the names of matching files
grep -A 3 "keyword" filename.txt          # Context parsing: Output a matching string row plus the subsequent 3 lines
grep -B 3 "keyword" filename.txt          # Context parsing: Output a matching string row plus the preceding 3 lines
grep -E "pattern1|pattern2" filename.txt   # Activate extended regular expression matching parsing boolean OR behaviors
grep -w "keyword" filename.txt            # Restrict match processing patterns ensuring assertions fit absolute standalone words
grep "^keyword" filename.txt              # Anchor query targeting lines initializing explicitly with the search text
grep "keyword$" filename.txt              # Anchor query targeting lines ending explicitly with the search text

# Advanced Multi-tier Processing using Pipes
ps aux | grep nginx                    # Inspect active process tables passing logs to parse running web daemons
cat /var/log/auth.log | grep "Failed"  # Interrogate access control logs isolating failed authentication attempts
dmesg | grep -i error                  # Scan system kernel rings tracking critical initialization errors

# ── SORT, UNIQ, CUT, AWK (Stream Data Transformation) ───────
sort file.txt                          # Arrange file document line strings following alphabetical order rules
sort -r file.txt                       # Reorder document text tracking sequences in reverse sorting order
sort -n file.txt                       # Direct parsing routines to follow absolute numerical sorting hierarchies
sort -k 2 file.txt                     # Force file text lines to sort processing attributes found on column 2
uniq file.txt                          # Deduplicate consecutive matching repeating strings inside a text document
sort file.txt | uniq                   # Process complete string sorting loops before stripping all document duplicates
sort file.txt | uniq -c                # Track line frequencies printing out computational instance repeat counts
cut -d':' -f1 /etc/passwd              # Parse character fields extracting user field index 1 utilizing a colon separator
cut -c1-10 file.txt                    # Strip data lines extracting raw strings resting within character bounds 1-10
awk '{print $1}' file.txt              # Execute layout parsing parsing and rendering the first data column parameters
awk -F':' '{print $1,$3}' /etc/passwd  # Interrogate text systems mapping column indices 1 and 3 via a defined delimiter
awk 'NR==5' file.txt                   # Advance text line index pointers directly to extract line number 5 exclusively
```

---

## 🖥️ Shell & Environment

```bash
# ── ENVIRONMENT LAYER VARIABLES ─────────────────────────────
env                             # Print out a summary recording all active system environment variables
printenv                        # Core validation tool mapping out configuration states across environments
echo $PATH                      # Display absolute filesystem directories registered to handle native command lookup
echo $HOME                      # Output the absolute file path pointing to current active user home location
echo $USER                      # Display system identity tracking string assigned to active operational shell
echo $SHELL                     # Verify the identity of active default shell translation parsing framework
echo $HOSTNAME                  # Output network alphanumeric identification string representing local system host

# Establishing local scope tracking runtime settings (Session-locked)
NAME="Debian"
echo $NAME

# Elevating variable contexts (Exporting settings to downstream child processes)
export NAME="Debian"
export PATH=$PATH:/usr/local/myapp/bin    # Inject an appended folder destination rule to active path maps

# Making modifications persistent → Append declarations directly to shell profile files (~/.bashrc)
echo 'export MYVAR="value"' >> ~/.bashrc
source ~/.bashrc                          # Re-evaluate shell settings loading changed configurations immediately

# ── COMMAND CONTEXT ALIASING ────────────────────────────────
alias ll='ls -la'              # Build a temporary shortcut parameter shorthand link to map complex operations
alias update='sudo apt update && sudo apt upgrade'
unalias ll                     # Unbind a custom shorthand shortcut definition linkage rule
alias                          # Review every shortcut abstraction tracking active command aliases

# Making aliases persistent → Append definitions directly onto target shell configurations (~/.bashrc)
echo "alias ll='ls -la'" >> ~/.bashrc

# ── COMMAND HISTORY DATA TRACES ─────────────────────────────
history                         # Dump the comprehensive command history list recording past console executions
history 20                      # Restrict historical tracking logs outputting the final 20 shell commands
!n                              # Re-execute a historical command by calling its numeric history list marker index
!!                              # Command loopback shorthand: Re-execute the immediate preceding command step
!string                         # Re-execute the most recent historical command initialization starting with targeted text
Ctrl+R                          # Initiate interactive reverse-search functions scanning shell tracking history logs
history -c                      # Flush history records erasing active session logs completely

# ── I/O REDIRECTIONS & TERMINAL STREAM PIPES ────────────────
command > file.txt             # Intercept standard output stream printing records to file (Destructive overwrite)
command >> file.txt            # Intercept standard output stream appending entries onto end of target file
command 2> error.txt           # Isolate standard error tracking streams routing error messages out to separate file
command &> all.txt             # Capture standard output and error logging streams writing all logs to single target
command < input.txt            # Modify execution context forcing standard input streams to read text out of a file
command1 | command2           # Invoke stream piping: Pass standard output metrics from one program straight into input of next

# Practical Compounded Data Modification Sequences
ls -la | grep ".txt" | sort     # Read directory mappings → Filter for text artifacts → Apply alphabetical sort rules
cat file | sort | uniq | wc -l  # Parse a dataset → Order lines → Clean out duplicate rows → Count unique entries
cat /var/log/auth.log | grep "Failed" | tail -20
```

---

## 🔧 Systemd & Service Management

```bash
# ── DAEMON DIAGNOSTICS & SYSTEM STATUS ──────────────────────
systemctl status                        # Review operational parameters tracing active and failed resource components
systemctl status nginx                  # Query configuration and logging properties for a target system daemon
systemctl status nginx.service          # Canonical interface lookup querying services using fully-qualified nomenclature
systemctl list-units --type=service     # Generate a complete listing tracking every active runtime software service
systemctl list-units --state=failed     # Run diagnostics to filter out damaged daemon processes that failed loading
systemctl list-unit-files               # Audit the system initialization script registry mapping active boot capabilities

# ── INTERFACE SERVICE CONTROL METRIC FIELDS ─────────────────
sudo systemctl start nginx              # Trigger systemd orchestration layers to launch a specific system service
sudo systemctl stop nginx               # Send shutdown instructions processing safe software daemon suspension routines
sudo systemctl restart nginx            # Force a service execution break cycling a daemon through a complete shutdown and restart
sudo systemctl reload nginx             # Instruct an active service to ingest modified configuration files omitting state reset
sudo systemctl enable nginx             # Update system startup links configuring a service to auto-start during system boot
sudo systemctl disable nginx            # Revoke boot orchestration rules stopping a service from launching at startup
sudo systemctl enable --now nginx       # Complex compounding instruction: Enable service persistence and launch target immediately
sudo systemctl mask nginx               # Deep-lock a service creating system links blocking manual or automatic execution attempts
sudo systemctl unmask nginx             # Clear structural mask overrides unlocking service management interactions

# ── POWER MANAGEMENT ARCHITECTURES ──────────────────────────
sudo systemctl reboot                   # Terminate all active operations triggering a hard platform system restart
sudo systemctl poweroff                 # Securely step down active system layers cutting physical unit motherboard power
sudo systemctl halt                     # Suspend central processing functions bringing system states to a frozen stop
sudo shutdown -h now                    # Issue an immediate platform terminal destruction command turning off the system
sudo shutdown -r now                    # Issue an immediate platform command instruction forcing system reboot routines
sudo shutdown -h +10                    # Schedule a delayed system shutdown queue ticking down for 10 minutes
sudo shutdown -c                        # Terminate an active scheduled platform shutdown countdown sequence

# ── SYSTEM TARGET RUNLEVEL ENVIRONMENT CONTEXTS ──────────────
systemctl get-default                   # Review the active operational target classification runlevel environment
sudo systemctl set-default multi-user.target  # Set system defaults to load bare console shells omitting graphical interfaces
sudo systemctl set-default graphical.target   # Set system defaults to initialize full desktop window manager environments (GUI)
sudo systemctl isolate rescue.target    # Strip active processes down shifting terminal scope into a safe single-user rescue mode

# ── RESOURCE LOG REPORT AUDITING ────────────────────────────
journalctl -u nginx                     # Isolate logging data traces capturing events tied strictly to a designated daemon
journalctl -u nginx -f                  # Engaged diagnostic logging tracking changes streaming daemon outputs in real-time
journalctl -u nginx --since "1 hour ago"
journalctl -xe                          # Open extended system event traces matching system failures to debug issues
```

---

## 🛡️ Firewall (UFW & iptables)

```bash
# ── UFW (Uncomplicated Firewall Layer Abstraction) ──────────
# Deployment installation mapping
sudo apt install ufw

# Operational States & Toggling
sudo ufw status                 # Query firewall configuration reviewing active/inactive status parameters
sudo ufw status verbose         # Request granular diagnostics showing deep rule parameters and logging properties
sudo ufw enable                 # Engage network packet filtering engines activating tracking rules across interfaces
sudo ufw disable                # Suspend firewall interactions passing packets unfiltered across interfaces
sudo ufw reset                  # Flush database settings restoring firewall state definitions back to stock factory settings

# Defining Communication Rules (Allow & Deny Matrices)
sudo ufw allow 22               # Unblock communication routes managing Port 22 handling both TCP and UDP packets
sudo ufw allow 22/tcp           # Open network interface access on Port 22 restricting scope strictly to TCP traffic
sudo ufw allow 80/tcp           # Open standard unencrypted HTTP transmission routes on Port 80
sudo ufw allow 443/tcp          # Open secure encrypted HTTPS transmission routes on Port 443
sudo ufw allow ssh              # Provision interface access permissions using canonical network profile service strings
sudo ufw allow http
sudo ufw allow https
sudo ufw deny 23                # Build drop filters blockading cleartext network connections directed on Port 23 (Telnet)
sudo ufw deny from 192.168.1.100  # Explicitly blacklist network connection requests coming out of a target host IP

# Setting Advanced Fine-Grained Rules
sudo ufw allow from 192.168.1.0/24         # Authorize network data packet transmissions originating from an entire local subnet
sudo ufw allow from 10.0.0.1 to any port 22  # Map strict security pipelines routing a designated host to service Port 22 exclusively
sudo ufw allow in on eth0 to any port 80   # Restrict ingress connections to Port 80, accepting packets strictly via physical interface eth0

# Purging Firewall Rules
sudo ufw delete allow 80        # Locate and drop the explicit firewall policy opening up communication over Port 80
sudo ufw delete deny 23         # Drop a tracking block rule clearing access filters associated with Port 23
sudo ufw status numbered        # Index active network security policies returning entries tied to discrete numeric markers
sudo ufw delete 3               # Purge a specific firewall security rule by calling its index location identifier

# Default Operational Policies
sudo ufw default deny incoming  # Restrict access parameters dropping all unsolicited incoming connections (Secure Default position)
sudo ufw default allow outgoing # Allow outbound packet traffic permitting internal network layers to establish external interfaces

# ── IPTABLES (Low-level Packet Filtering Framework) ─────────
sudo iptables -L                         # Review raw netfilter kernel structural rules running across standard tables
sudo iptables -L -n -v                   # Deep network auditing: Output structural packet logs using absolute numeric layouts
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT   # Append netfilter rule explicitly allowing ingress SSH data packets
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT   # Append netfilter rule explicitly allowing incoming web traffic over HTTP
sudo iptables -A INPUT -j DROP           # Assert global drop rule dumping packet entities failing validation checks
sudo iptables -D INPUT -j DROP           # Locate and strip out standard drop assertions from active tables
sudo iptables-save > /etc/iptables/rules.v4  # Serialize active network rule settings storing configurations to storage file
sudo iptables-restore < /etc/iptables/rules.v4  # Process rule asset configurations loading definitions back into kernel space
```

---

## 🔑 SSH & Remote Access

```bash
# ── REMOTE CONNECTION PROCEDURES ────────────────────────────
ssh user@hostname                       # Initialize a standard cryptographically secured terminal session mapping a host
ssh user@192.168.1.100                  # Command network links establishing shell sessions utilizing explicit IP addresses
ssh -p 2222 user@hostname               # Instruct connection brokers to map target hosts running on alternative non-standard ports
ssh -i ~/.ssh/keyfile.pem user@host     # Bypass password constraints passing private identity keys to process key auth challenges
ssh -v user@host                        # Diagnostic Debug Mode: Enforce verbose connection logging to monitor transaction logs
ssh -X user@host                        # Instruct shell protocols to route graphical window layouts via X11 forwarding rules

# ── SSH KEY ARTIFACT MANAGEMENT ─────────────────────────────
# Creating secure cryptographic key pair units
ssh-keygen -t rsa -b 4096               # Generate a legacy RSA asymmetric system key pair utilizing 4096-bit length rules
ssh-keygen -t ed25519                   # Generate a modern ultra-secure elliptic curve Ed25519 system identity key pair
ssh-keygen -t ed25519 -C "email@example.com"  # Build cryptographically sound access key pairs attaching custom user markers

# Copying localized public access keys over onto a remote target server node
ssh-copy-id user@hostname               # Automated synchronization utility mapping public key tokens onto a remote user profile
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@host  # Direct utility engine to register a precise targeted key file signature

# Manual public cryptographic authentication key deployment fallback mapping sequence:
cat ~/.ssh/id_rsa.pub | ssh user@host "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"

# Core Operational File System Assets (SSH Environment Maps)
~/.ssh/id_rsa                   # Private Access Key Token (KEEP STRICTLY CONFIDENTIAL — ENFORCE LOCKOUT ACCESS RULES)
~/.ssh/id_rsa.pub               # Public Access Key Token (Safe to share out and register across external target platforms)
~/.ssh/authorized_keys          # Public key tokens permitted to establish trusted access links bypassing password triggers
~/.ssh/known_hosts              # Database map keeping cryptographic fingerprints indexing previously validated remote hosts
~/.ssh/config                   # Local user identity profile map configuring remote host connection behavior details

# ── SSH LOCAL PROFILE STRUCTURE MASTERING (~/.ssh/config) ──
# Simplify connection commands by appending profile blocks onto configuration records:
# Host myserver
#     HostName 192.168.1.100
#     User admin
#     Port 2222
#     IdentityFile ~/.ssh/mykey
#
# Once custom configuration blocks are defined, trigger remote connections instantly by executing shorthand parameters:
# ssh myserver

# ── SSH DEPLOYMENT SERVER CONFIGURATION (/etc/ssh/sshd_config)
# Recommended production hardening guidelines to secure remote endpoints:
# Port 2222                       # Shift default communication maps away from standard open port configurations
# PermitRootLogin no              # Rigidly prohibit direct administrative root access logins across network connections
# PasswordAuthentication no       # Suppress cleartext password interfaces requiring absolute key-based cryptographic access
# PubkeyAuthentication yes        # Enforce structural authentication rules validating connections via public key token registries
# MaxAuthTries 3                  # Restrict interactive access attempts down dropping connections after 3 authentication fails
# AllowUsers username             # Restrict system exposure by white-listing specific validated username parameters

sudo systemctl restart ssh        # Cycle remote communication service daemons to activate updated system settings

# ── ADVANCED PORT ENCAPSULATION & TUNNELING ─────────────────
# Local Port Forwarding: Expose remote daemon services pulling routes locally onto client machines
ssh -L 8080:localhost:80 user@host      # Establish local terminal tracking routing client path localhost:8080 → remote node:80

# Remote Port Forwarding: Project localized workspace development configurations outward onto an external remote public platform
ssh -R 8080:localhost:3000 user@host    # Project workspace routes forwarding traffic mapping remote node:8080 → client localhost:3000

# Dynamic SOCKS Proxy Creation
ssh -D 1080 user@host                   # Instantiate an encrypted dynamic SOCKS5 routing proxy tracking data over Port 1080
```

---

## 📝 Shell Scripting Basics

```bash
#!/bin/bash
# ═══════════════════════════════════════════════════════════
#  Script      : sample_script.sh
#  Description : Fundamental shell scripting architecture demonstrating Bash environments
#  Execution   : chmod +x script.sh && ./script.sh
# ═══════════════════════════════════════════════════════════

# ── VARIABLE DECLARATIONS ───────────────────────────────────
DISTRO="Debian"
VERSION=12
WELCOME_MSG="Welcome to $DISTRO $VERSION"
echo $WELCOME_MSG

# Contextual Environment Internal Meta-Variables
echo "Executing script file path : $0"
echo "Supplied argument string 1 : $1"
echo "Supplied argument string 2 : $2"
echo "Total count of arguments   : $#"
echo "Array list of all tokens   : $@"
echo "Runtime Process ID (PID)   : $$"
echo "Most recent exit status code: $?"

# ── INTERACTIVE USER STREAMS INPUTS ──────────────────────────
read -p "Provide user identification string: " USER_INPUT
echo "Session processing parameters initialized for: $USER_INPUT!"
read -s -p "Provide system access password: " PASS    # -s = Suppress echoes blocking terminal UI text feedback
echo ""

# ── CONDITIONALS & LOGICAL MATRIX CHECKPOINTS ───────────────
NUMERIC_VAL=10

if [ $NUMERIC_VAL -gt 5 ]; then
    echo "Stated numerical boundary matches rule: Value is greater than 5"
elif [ $NUMERIC_VAL -eq 5 ]; then
    echo "Stated numerical boundary matches rule: Value is equivalent to 5"
else
    echo "Stated numerical boundary matches rule: Value evaluates to under 5"
fi

# Numerical comparative testing conditional flags: -eq -ne -lt -le -gt -ge
# String comparative testing conditional flags: == != -z (Vacant check) -n (Populated token verification)
# Filesystem comparative testing conditional flags: -f (Regular file verification) -d (Folder confirmation) -e (Existence verification) -r -w -x

# Programmatic evaluation verifying the physical existence of a target tracking log
if [ -f "/etc/passwd" ]; then
    echo "Target identity ledger structure found mapping at: /etc/passwd"
fi

# ── SWITCH EVALUATIONS (CASE EXPRESSIONS) ───────────────────
read -p "Select environment target node configuration option (a/b/c): " SELECTION
case $SELECTION in
    a) echo "User selected workspace branch operational parameter profile: A" ;;
    b) echo "User selected workspace branch operational parameter profile: B" ;;
    c) echo "User selected workspace branch operational parameter profile: C" ;;
    *) echo "Invalid operation option parameter token submitted" ;;
esac

# ── PROGRAMMATIC LOOP SEQUENCES ─────────────────────────────
# Standard numerical iteration using a 'For' layout
for i in 1 2 3 4 5; do
    echo "Active tracking loop iteration processing step index: $i"
done

for i in {1..10}; do
    echo -n "$i "
done
echo ""

# Automated directory looping mapping configurations inside a filesystem folder target
for config_file in /etc/*.conf; do
    echo "Discovered system configuration profile mapping target target: $config_file"
done

# Dynamic conditional validation using a 'While' loop tracking process increments
TRACKER=0
while [ $TRACKER -lt 5 ]; do
    echo "Current counter iteration tracking metrics point: $TRACKER"
    ((TRACKER++))
done

# Dynamic conditional validation executing inverse assertions using an 'Until' layout
TRACKER=0
until [ $TRACKER -ge 5 ]; do
    echo "Evaluating step trace metrics until loop rule conditions break: $TRACKER"
    ((TRACKER++))
done

# ── MODULAR FUNCTIONS ───────────────────────────────────────
greet_user() {
    local USERNAME_TARGET=$1           # Isolate parameter scopes restricting assignments locally inside functions
    echo "Executing automated greeting interface instructions for: $USERNAME_TARGET!"
    return 0                # Dispatch a normal execution exit status verification code marker back to the shell environment
}

greet_user "World"
greet_user "Debian"

calculate_spatial_area() {
    local LENGTH_VAL=$1
    local WIDTH_VAL=$2
    echo $((LENGTH_VAL * WIDTH_VAL))  # Execute standard mathematical tracking arithmetic conversions
}

TOTAL_AREA=$(calculate_spatial_area 5 3)
echo "Evaluated system spatial operational scale boundaries resolve to: $TOTAL_AREA"

# ── EXPLICIT SHELL RUNTIME ERROR HANDLING OVERRIDES ──────────
set -e          # Direct interpreter shell to halt script immediately upon any instruction error failure
set -u          # Trigger script execution crashes if code encounters uninstantiated variable identifiers
set -o pipefail # Force system error tracers to analyze upstream errors dropping out of complex command pipelines

nonexistent_command || echo "Target execution failed, processing alternative fallback scripting path branches"
valid_command && echo "Target execution step completed successfully without tracking errors"

# Implementing structural programmatic cleanup hooks managing resource teardowns
execute_environment_cleanup() {
    echo "Garbage collection hooks engaged: Flushing temporary environment working files..."
    rm -f /tmp/tempfile
}
trap execute_environment_cleanup EXIT    # Direct runtime engine to execute cleanup routines upon native script exit
trap execute_environment_cleanup INT     # Bind cleanup event triggers to process execution abort disruptions (Ctrl+C interrupts)
```

---


## ⌨️ Useful Shortcuts & Tips

Mastering the terminal is not just about knowing the commands; it is about execution speed and environment efficiency. Below is a curated list of essential keyboard shortcuts and advanced scripting tips to maximize your terminal productivity.

### 1. Core Keyboard Shortcuts (Bash / Zsh)

Utilize these shortcuts to navigate the command-line interface efficiently without touching the mouse.

| Shortcut | Functional Action | Category |
| :--- | :--- | :--- |
| `Ctrl + C` | Aborts the currently executing foreground process immediately. | Process Control |
| `Ctrl + Z` | Suspends (pauses) the current process and pushes it to the background. | Process Control |
| `Ctrl + D` | Closes the current terminal session (equivalent to the `exit` command). | Session Management |
| `Ctrl + L` | Clears the entire terminal screen layout (equivalent to the `clear` command). | Screen Management |
| `Ctrl + A` | Moves the text cursor instantly to the **beginning** of the current line. | Navigation |
| `Ctrl + E` | Moves the text cursor instantly to the **end** of the current line. | Navigation |
| `Ctrl + U` | Deletes all characters from the current cursor position back to the beginning of the line. | Text Editing |
| `Ctrl + K` | Deletes all characters from the current cursor position forward to the end of the line. | Text Editing |
| `Ctrl + W` | Erases a single word backward (to the left of the cursor). | Text Editing |
| `Ctrl + R` | Initiates an interactive reverse-search through your execution history. | History Search |
| `Tab` | Autocompletes command names, system paths, and file targets. | Automation |
| `Tab Tab` | Displays all available string possibilities matching the autocomplete prefix. | Automation |

---

### 2. Advanced Chaining & Command Hacks

Combine multiple Linux commands sequentially using logical operators to build powerful automation strings.

```bash
# Re-execute the immediate preceding command elevating privileges via root (Sudo)
sudo !!

# Construct nested folder paths and step into the directory context instantly
mkdir -p /path/to/nested/dir && cd $_

# Redirect terminal output strings straight into your system clipboard (requires xclip)
cat log.txt | xclip -selection clipboard

# Dry-Run Audit: Print complex text commands inside an echo to review syntax safety boundaries
echo rm -rf /path/to/target/

# Time-Tracking: Measure the precise operational runtime duration required by a specific process
time ./backup_script.sh

### Productivity Pro-Tips & Core Terminal Hacks

```bash
# Force the re-execution of the preceding command injection elevating permissions via root/superuser controls
sudo !!

# Compound file system scripting: Construct nested folder paths and step target contexts inside them instantly
mkdir -p /path/to/dir && cd $_

# Redirect terminal print lines directly into system copy-paste clipboards (Requires tool utility: xclip)
command | xclip -selection clipboard

# Dry-Run Audit: Print complex text configurations inside echoes to review execution syntax safety parameters
echo rm -rf /path/

# Time-Tracking: Measure the exact resource execution time duration requirements a specific program process takes
time command

# Mastering Compound Sequential Execution Command Operators
cmd1 ; cmd2 ; cmd3          # Linear Sequencing: Execute tasks one after another, completely ignoring error breaks
cmd1 && cmd2                # Conditional Pathing: Direct system to run cmd2 only if cmd1 completes without tracking errors
cmd1 || cmd2                # Fallback Execution: Route system to process cmd2 only if cmd1 crashes or throws a failure state

# Accessing system application documentation and operational blueprints
man command                # Open the comprehensive authoritative structural system reference manual index for a task
man -k keyword             # Run structural manual lookup sweeps searching index registries for matching descriptors
tldr command               # Fetch practical, community-curated, hyper-dense usage cheat sheets (apt install tldr)
command --help             # Output a brief summary mapping native configuration arguments inline within the console
```

---

<div align="center">

![Debian](https://img.shields.io/badge/Debian-Linux-A81D33?style=flat-square&logo=debian&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-Scripting-4EAA25?style=flat-square&logo=gnubash&logoColor=white)

**Hopefully this documentation is helpful!**
⭐ Star this repo if it helps your learning process!

*"Practice makes perfect — open the terminal and start practicing!"*

</div>
