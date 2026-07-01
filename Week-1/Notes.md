##1. File \& Directory Management

```
ls          # List files
cd          # Change directory
pwd         # Show current directory
mkdir       # Create directory
rm          # Remove files/directories
cp          # Copy files
mv          # Move/rename files
touch       # Create empty file
```

2. File Viewing \& Text Processing

cat         # View file content
less        # Scroll through file
head        # First few lines
tail        # Last few lines
tail -f     # Follow logs in real-time
grep        # Search text
awk         # Data processing
sed         # Stream editing
cut         # Extract columns


3. System Monitoring Commands


top         # Real-time processes
htop        # Better version of top
free -m     # Memory usage
df -h       # Disk usage
du -sh      # Folder size
uptime      # System uptime
ps aux      # Running processes

4. Process Management

kill        # Kill a process
kill -9     # Force kill
pkill       # Kill by name
bg          # Resume in background
fg          # Resume in foreground
jobs        # Show background jobs

5. Networking Commands

ping        # Check connectivity
curl        # Call APIs
wget        # Download files
netstat     # Network status
ss          # Socket statistics
ifconfig    # Network config (older)
ip addr     # New network command
nslookup    # DNS lookup


6. Package Management (Installation)


Ubuntu/Debian:
  apt update
  apt install nginx
  apt upgrade

RHEL/CentOS:
  yum install nginx
  dnf install nginx


7. User & Permission Management

whoami      #check current user
chmod       # Change permissions
chown       # Change ownership
useradd     # Add user
usermod     # Modify user
passwd      # Change password


8. Log & Debugging Commands

journalctl      # View system logs
dmesg           # Kernel logs
tail -f /var/log/syslog


9. Archiving & Compression

tar -cvf file.tar dir/
tar -xvf file.tar
gzip file
gunzip file.gz
zip / unzip


File Search and I/O Redirection
10. File Search Commands 

find /path -name "file.txt"     # search for a file by name in a given path
find . -type f                 # find all files in current directory
find /var/log -name "\*.log"    # find all .log files in /var/log
find . -size +100M             # find files larger than 100MB

locate filename                # quickly search files using database (faster than find)

updatedb                       # update locate database (required for latest results)

grep "error" file.txt          # search for word "error" inside file
grep -i "error" file.txt       # case-insensitive search
grep -r "error" /logs          # search recursively inside directory

which python                   # show path of executable (where command is located)
whereis nginx                  # show binary, source, and manual location of a command

11. I/O Redirection Commands

ls > files.txt                 # save output of ls into file (overwrites file)
echo "Hello" >> file.txt       # append "Hello" to file (does not overwrite)
wc -l < file.txt               # use file.txt as input to count number of lines
ls invalidfile 2> error.txt    # redirect error output (stderr) into error.txt

command > output.txt 2>\&1      # redirect both output and errors into same file

cat file.txt | grep "error"    # send output of cat to grep (pipe)
ps aux | grep nginx           # filter running processes for nginx

echo "Hello" | tee file.txt    # write output to file AND display on screen

echo "data" | tee -a file.txt  # append output to file and display

**Quick Understanding:**

find → locate files
grep → search inside files
> → overwrite output
>> → append output
2> → redirect errors
| → pass output to another command
tee → display + save output


12. Useful Shortcuts & Tricks

history         # Show command history
clear           # Clear screen
alias           # Create shortcut
echo            # Print output
export          # Set environment variable

Vi Editor: Modes and Shortcuts

13. Vi/Vim Editor Modes

Basic Command List:

:i    # insert before cursor
:w        # save file
:q        # quit
:wq       # save and quit
:q!       # quit without saving
dd       # delete entire line
yy       # copy (yank) line
/word        # search forward
?word        # search backward
n            # next match


Exhaustive commands list:


1. Normal Mode (Default Mode)
This is the starting mode
Used for navigation and commands
You cannot type text directly

2. Insert Mode: Used to insert/edit text

i    # insert before cursor
I    # insert at beginning of line
a    # insert after cursor
A    # insert at end of line
o    # new line below
O    # new line above

3. Visual Mode: Used to select text
v    # character selection
V    # line selection
Ctrl + v   # block selection

4. Command Mode (Last Line Mode)
:
`

File Operations
:w        # save file
:q        # quit
:wq       # save and quit
:q!       # quit without saving
:x        # save and exit

Editing Shortcuts:
x        # delete character
dd       # delete entire line
dw       # delete word
d$       # delete till end of line
yy       # copy (yank) line
yw       # copy word
p        # paste after cursor
P        # paste before cursor
u        # undo last action
Ctrl + r # redo

Search & Replace:
/word        # search forward
?word        # search backward
n            # next match
N            # previous match

Useful DevOps Shortcuts:
:set number      # show line numbers
:set nonumber    # hide line numbers
:set ignorecase  # case-insensitive search

Users, Groups, and File Permissions
What is a Cron Job?
A cron job is a scheduled task that runs automatically at a specified time or interval in Linux.
Cron job = automate tasks like scripts, backups, monitoring, etc.

Why Cron Jobs are Important (DevOps Usage)

✅ Automate backups
✅ Clean logs regularly
✅ Run scripts/tasks periodically
✅ Monitor systems
✅ Schedule deployments

📂 Cron Job Syntax

* * * * * 
│ │ │ │ │
│ │ │ │ └── Day of week (0–7) (Sunday = 0 or 7)
│ │ │ └──── Month (1–12)
│ │ └────── Day of month (1–31)
│ └──────── Hour (0–23)
└────────── Minute (0–59)




* * * * * command 👉 Runs every minute
0 * * * * command 👉 Runs every hour
0 2 * * * command 👉 Runs daily at 2 AM
0 0 * * 0 command 👉 Runs every Sunday at midnight
*/5 * * * * command 👉 Runs every 5 minutes


crontab -e  	#Edit Cron Jobs
crontab -l	#List Cron Jobs
crontab -r	#Remove Cron Jobs

Real DevOps Examples:

🔹 1. Backup script daily

0 1 * * * /home/user/backup.sh

# runs backup script every day at 1 AM

🔹 2. Delete old logs

0 3 * * * find /var/log -name "\*.log" -mtime +7 -delete

# deletes logs older than 7 days at 3 AM

🔹 3. Monitor server every 5 mins

*/5 * * * * /home/user/check\_server.sh

# runs monitoring script every 5 minutes

🔹 4. Save output to log file

0 * * * * /script.sh >> /var/log/script.log 2>&1

# run script every hour and log output \& errors


Important Files

/etc/crontab	# system-wide cron jobs
/etc/cron.d/	# additional cron jobs
/etc/cron.daily
/etc/cron.hourly
/etc/cron.weekly

# predefined job directories

Basic Networking and Iptables:

🌐 PART 1: Basic Networking (Linux)

✅ What is Networking?

Networking = communication between systems using IP addresses.

🔹 Important Concepts

✅ 1. IP Address

Unique address of a system in a network

Example: 192.168.1.10


✅ 2. Types of IP
Private IP → inside network (e.g., 192.168.x.x)
Public IP → internet-facing

✅ 3. Ports
Used to identify services:
22 → SSH
80 → HTTP
443 → HTTPS
3306 → MySQL

✅ 4. Protocols
TCP → reliable (used by web, SSH)
UDP → faster, no guarantee (used by streaming, DNS)



🛠️ Basic Networking Commands

ip addr               # show IP address
ip route              # show routing table
ping google.com       # test connectivity
ss -tuln              # list open ports
netstat -tuln         # older version of above
curl http://example.com   # test HTTP request
wget http://file.com      # download file
nslookup google.com   # DNS lookup


🔥 PART 2: IPTables (Firewall):

✅ What is IPTables?
👉 IPTables is a Linux firewall tool used to: 
Allow or block traffic
Filter packets
Secure servers

🔹 Key Idea

👉 IPTables works using rules applied to network traffic.

📌 IPTables Structure
✅ Tables
filter → default (allow/block traffic)
nat → network address translation
mangle → modify packets

✅ Chains (Flow of Traffic)
INPUT → incoming traffic
OUTPUT → outgoing traffic
FORWARD → traffic passing through server

✅ Actions (Targets)
ACCEPT → allow
DROP → block silently
REJECT → block with response

🛠️ Basic IPTables Commands

iptables -L		# list all firewall rules
iptables -L -n -v	# show detailed rules with IPs and packet count	
iptables -A INPUT -p tcp --dport 22 -j ACCEPT	# allow SSH (port 22)
iptables -A INPUT -s 192.168.1.10 -j DROP	# block specific IP
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp --dport 443 -j ACCEPT	# allow web traffic
iptables -A INPUT -j DROP	# block everything (use carefully!)
iptables -D INPUT -p tcp --dport 80 -j ACCEPT	# remove HTTP rule
iptables -F	# delete all rules
iptables-save > /etc/iptables.rules	#Save rules
iptables-restore < /etc/iptables.rules	#Restore rules


🔐 Common Use Cases in DevOps
✅ Secure server access
✅ Allow only required ports
✅ Block malicious IPs
✅ Protect production systems

👉 Networking helps systems communicate; IPTables controls and secures that communication.


💾 What are Linux Storage Fundamentals?
Linux storage fundamentals explain how data is stored, managed, and accessed in Linux systems.

👉 This includes:
Disks
Partitions
File systems
Mounting
Logical volumes

🧱 1. Storage Components Hierarchy: Disk → Partition → Filesystem → Mount Point → Files
🔹 1. Disk (Physical Storage)
A disk is a physical storage device
Examples:	HDD / SSD
Cloud disks (AWS EBS, Azure Disk)
lsblk          # show disks \& partitions
fdisk -l       # list disk details

🔹 2. Partitions
A partition divides a disk into sections
Each partition can hold its own filesystem
👉 Example:
/dev/sda1
/dev/sda2
👉 Manage partitions:
fdisk /dev/sda   # create/manage partitions

🔹 3. File System

A filesystem organizes how data is stored
Without it → data cannot be used
Common types:
ext4 (most common in Linux)
xfs (used in enterprise)
vfat (for USB drives)

👉 Create filesystem: mkfs.ext4 /dev/sda1

🔹 4. Mounting

Mounting = making storage accessible in Linux
👉 Example: mount /dev/sda1 /mnt
👉 Check mounted filesystems:
df -h
mount

🔹 5. Mount Points

A directory where a filesystem is attached
👉 Example:
/mnt
/home
/var

🔹 Permanent Mount
/etc/fstab
/dev/sda1  /data  ext4  defaults  0 0

🔹 6. Logical Volume Manager (LVM)
LVM = flexible storage management (very important for DevOps)
✅ Why use LVM?

Resize storage easily
Combine multiple disks
Better management


🧩 LVM Structure:

Physical Volume (PV)
      ↓

Volume Group (VG)

      ↓

Logical Volume (LV)


✅ LVM Commands
pvcreate /dev/sdb            # create physical volume
vgcreate myvg /dev/sdb      # create volume group
lvcreate -L 5G -n mylv myvg # create logical volume

👉 Format and mount:
mkfs.ext4 /dev/myvg/mylv
mount /dev/myvg/mylv /data

🔹 7. Disk Usage Monitoring
df -h      # show disk space
du -sh \*   # folder size

🔹 8. Swap Memory: Used when RAM is full: free -m

🔹 9. Important Directories

/home → user data
/var → logs, applications
/etc → config files
/tmp → temporary files



👉 Linux storage fundamentals describe how disks are organized, formatted, and made accessible for data storage and management.
