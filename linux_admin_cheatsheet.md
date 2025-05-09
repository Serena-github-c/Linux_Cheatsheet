
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
