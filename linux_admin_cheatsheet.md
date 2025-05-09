
# 🧑‍💻 Linux Admin Cheat Sheet: Users, Groups, Permissions, Processes

---

## 📦 SECTION 1: USERS

### 🧑 Create a New User
```bash
sudo adduser username        # interactive, beginner-friendly
sudo useradd username        # low-level, needs extra options
```

### 🔑 Set or Change a User’s Password
```bash
sudo passwd username
```

### 🛠 Modify a User
```bash
sudo usermod -l newname oldname       # change username
sudo usermod -d /new/home username    # change home directory
sudo usermod -s /bin/bash username    # change default shell
sudo usermod -u 1234 username         # change user ID
```

### 🧺 Delete a User
```bash
sudo deluser username                 # removes user, keeps home
sudo userdel username                 # same, low-level
sudo userdel -r username              # removes user + home
```

### 👥 Add User to a Group
```bash
sudo usermod -aG groupname username   # -aG = append to group
```

### ❌ Remove User from a Group
```bash
sudo gpasswd -d username groupname
```

### 🔄 Change User's Primary Group
```bash
sudo usermod -g newgroup username
```

### 🔎 Show User Info
```bash
id username
groups username
whoami
getent passwd
```

---

## 🧑‍🤝‍🧑 SECTION 2: GROUPS

### ➕ Create Group
```bash
sudo groupadd groupname
```

### 🔧 Modify Group
```bash
sudo groupmod -n newname oldname
sudo groupmod -g 1234 groupname
```

### ❌ Delete Group
```bash
sudo groupdel groupname
```

### 👀 Show Group Info
```bash
getent group
```

---

## 🔐 SECTION 3: FILE PERMISSIONS

### 📁 View File Permissions
```bash
ls -l filename
```

### 🔧 Change Ownership
```bash
sudo chown user file
sudo chown user:group file
```

### 🔄 Change Permissions (numeric)
```bash
chmod 755 file
chmod 644 file
```

### 🔄 Change Permissions (symbolic)
```bash
chmod u+x file
chmod g-w file
chmod o=r file
```

---

## ⚙️ SECTION 4: PROCESSES

### 👀 View Running Processes
```bash
ps aux
ps -ef
top
htop
```

### 🔍 Find Process by Name
```bash
ps aux | grep name
```

### 🔄 Run Process in Background
```bash
some_command &
```

### 🔂 Bring Process to Foreground
```bash
fg %job_number
```

### 🛑 Stop or Kill Process
```bash
kill PID
kill -9 PID
```

### 🧹 Kill All by Name
```bash
killall process_name
```

### ⏸ Suspend a Foreground Job
```bash
Ctrl + Z
```

---

## 📝 BONUS TIPS

- Show currently logged in users:
  ```bash
  who
  w
  ```

- Show user login history:
  ```bash
  last
  ```

- Add a new user with specific UID, GID, shell, home:
  ```bash
  sudo useradd -u 1050 -g mygroup -s /bin/bash -d /home/newuser -m newuser
  ```

- See disk usage:
  ```bash
  df -h
  ```

- Check memory usage:
  ```bash
  free -h
  ```


# Linux Network Administration Exam Guide

## User Management

### Add a User to a Group (Keep Initial Group)

```bash
usermod -aG groupname username
```

**-aG**: Append to supplementary groups without removing the user from others.

### Make a User Admin (Allow User to Add/Remove Users)

```bash
usermod -aG sudo U3
```

This adds `U3` to the `sudo` group, allowing administrative privileges.

### Create a User in a Specific Group

```bash
useradd -G groupname -m username
passwd username
```

**-G**: Supplementary groups
**-m**: Create home directory

## Password Management

### Change Password

```bash
passwd username
```

### Lock/Unlock a Password

```bash
passwd -l username   # Lock
passwd -u username   # Unlock
```

### Add a User to a Group with Expiration

```bash
usermod -aG groupname username
chage -E 2025-06-30 username
```

## Group Management

### Create a Group

```bash
groupadd groupname
```

### Delete a Group

```bash
groupdel groupname
```

### Remove a User from a Group

```bash
gpasswd -d username groupname
```

### Show a User's Groups

```bash
groups username
id username
```

### Change Primary Group

```bash
usermod -g newprimarygroup username
```

### Make a User an Admin of a Group (Without Being a Member)

```bash
gpasswd -A U3 G3
```

This command assigns `U3` as the administrator of group `G3` without adding them as a group member.

## File Permissions

### Show Permissions

```bash
ls -l
```

### Change Permissions

```bash
chmod 755 filename
```

### Change Ownership

```bash
chown user:group filename
```

## Process Management

### Kill Processes by PID

```bash
kill 335 556
```

### Kill Process by Name

```bash
pkill vi
```

### Force Process to Reread Config (Signal HUP)

```bash
kill -HUP 358
```

### Let p2 Start Before p1

```bash
p2 &
sleep 2
p1 &
```

### Display Remaining Processes

```bash
ps -e
```

### Show Active Processes in Real-Time

```bash
top
htop    # If installed
```

### Suspend a Process

Press `Ctrl + Z` in the terminal running the process.

### Reactivate Suspended Process

```bash
fg     # Bring to foreground
bg     # Continue in background
```

## Detailed Explanation of Process Tools

### `top`

* Real-time display of active processes.
* `top`, `q` to quit
* Press `k` in `top` to kill a process

### `ps`

* View current processes.
* `ps`: Current shell only
* `ps -ax`: All processes with terminals
* `ps aux`: All processes with memory and CPU info

### `gedit`

* Opens a graphical text editor (X server must be running).

### `atq`

* List queued jobs for `at` scheduler.

### `atrm`

* Remove a scheduled job: `atrm job_number`

### `kill -HUP PID`

* Tells a process to reinitialize (re-read config).

### `pidof`

* Get PID of a process: `pidof gedit`

### `pstree`

* Visual tree of all processes: `pstree`

### `nice`

* Start process with priority: `nice -n 10 command`

### `renice`

* Change priority of running process: `renice 5 -p 1234`

### `jobs`

* Lists background/suspended jobs in current shell.

### `init`

* Used to change runlevels (older systems). Example: `init 0` (halt)
* Modern systems use `systemctl` instead.

---

✅ Practice these with root or sudo privileges. Try running `man command` for each command to learn more.

Good luck on your exam!
