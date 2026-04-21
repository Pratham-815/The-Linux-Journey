# 📁 Linux File System Structure (FHS)

This document explains:

* The Linux directory structure
* Purpose of each major directory
* Hidden system behavior (what beginners usually miss)
* Useful commands to explore the filesystem

---

## 🧠 What is the Linux File System?

Unlike Windows (C:, D:, E: drives), Linux follows a **single-root hierarchical structure**:

```
/   (root)
├── bin
├── etc
├── home
├── var
├── usr
└── ...
```

👉 Everything starts from `/` (root)

### 🧠 Insight

Initially, it felt strange not having drives like `C:` or `D:`.
But Linux treats **everything as a file inside a single tree**, even:

* USB drives
* Hard disks
* Running processes

---

## 🔗 Symbolic Links (Modern Linux Design)

Many directories today are actually **symbolic links**:

| Link    | Points To   | Purpose         |
| ------- | ----------- | --------------- |
| `/bin`  | `/usr/bin`  | User binaries   |
| `/sbin` | `/usr/sbin` | System binaries |
| `/lib`  | `/usr/lib`  | Libraries       |

### Why this exists?

* Older Linux had separation between `/` and `/usr`
* Modern systems unify everything under `/usr`

### 🧠 Insight

These aren’t real folders—they’re shortcuts (like Windows shortcuts but more powerful).

---

## ⚙️ Important System Directories

### 📦 `/boot`

* Contains files required to boot the system
* Includes:

  * Kernel (`vmlinuz`)
  * Bootloader (GRUB)

👉 Not relevant much in containers, but critical in real systems

---

### 📦 `/usr` (User System Resources)

* Contains most installed software and libraries
* Subdirectories:

  * `/usr/bin` → user commands
  * `/usr/lib` → libraries
  * `/usr/share` → shared data

### 🧠 Insight

Despite the name, `/usr` is **not for users**—it’s for system-wide programs.

---

### 📦 `/var` (Variable Data)

* Stores frequently changing data:

  * Logs → `/var/log`
  * Cache → `/var/cache`
  * Databases → `/var/lib`

### Real Example:

```bash
/var/log/syslog
```

### 🧠 Insight

If something breaks → logs are here. This is your debugging goldmine.

---

### 📦 `/etc` (Configuration Files)

* Stores system-wide config files
* Examples:

  * `/etc/passwd` → user info
  * `/etc/hosts` → hostname mapping
  * `/etc/nginx/nginx.conf`

### 🧠 Insight

If you want to **configure anything in Linux**, you’ll probably touch `/etc`.

---

## 👤 User & Application Directories

### 🏠 `/home`

* Contains personal directories for users:

  ```bash
  /home/pratham
  ```

* Stores:

  * Documents
  * Downloads
  * Config files (hidden `.files`)

---

### 👑 `/root`

* Home directory for **root (admin)** user
* Separate from `/home`

---

### 📦 `/opt`

* Used for installing third-party software
* Example:

  ```bash
  /opt/google/chrome
  ```

---

### 🌐 `/srv`

* Stores data for services (like web servers)
* Rarely used in modern setups

---

## ⚡ Temporary & Virtual Directories

### 🧪 `/tmp`

* Stores temporary files
* Cleared on reboot

---

### ⚙️ `/run`

* Stores runtime process data
* Exists only during system uptime

---

### 🔍 `/proc` (Process Info)

* Virtual filesystem
* Contains info about running processes

Example:

```bash
cat /proc/cpuinfo
cat /proc/meminfo
```

### 🧠 Insight

These aren’t real files—they’re **live system data exposed as files**.

---

### 🧠 `/sys` (System & Hardware Info)

* Provides kernel and hardware-level information
* Used for low-level system tuning

---

### 🔌 `/dev` (Devices)

* Represents hardware as files:

  * `/dev/sda` → hard disk
  * `/dev/null` → black hole (discards data)

### 🧠 Insight

In Linux: **everything is a file—even hardware**.

---

## 💽 Mount Points

### 📂 `/mnt`

* Temporary mount location

---

### 📂 `/media`

* Used for USB drives, CDs

---

### 📂 `/data`

* Custom mount point (e.g., Windows WSL storage)

---

## 🛠️ Essential Commands

### 📁 Navigation & Exploration

```bash
pwd              # Show current directory
ls -la           # List all files (including hidden)
tree             # Show directory structure (install required)
```

---

### 🔍 File & Directory Info

```bash
stat file.txt    # Detailed file info
file file.txt    # File type detection
du -sh *         # Disk usage per file/folder
df -h            # Disk usage of system
```

---

### 🔎 Searching (VERY IMPORTANT)

```bash
find / -name file.txt        # Search file
find / -type d -name logs    # Search directory
locate file.txt              # Fast search (needs indexing)
```

---

### 🔗 Symbolic Links

```bash
ln -s target link_name   # Create symlink
ls -l                    # View symlink
```

---

### 📦 Viewing File Content

```bash
cat file.txt
less file.txt
head -n 10 file.txt
tail -n 10 file.txt
```

---

### 🔥 Hidden but Powerful Commands

```bash
which nginx        # Location of binary
whereis nginx      # Binary + source + man page
history            # Command history
alias ll='ls -la'  # Create shortcut
```

---

## 🚀 Real-World Understanding

* `/etc` → configuration
* `/var/log` → debugging
* `/home` → user work
* `/usr/bin` → commands
* `/dev` → hardware
* `/proc` → live system data

👉 Together, they form a **fully transparent and controllable OS**

---

## ✅ Key Takeaways

* Linux uses a **single-root file system**
* Everything is treated as a file (even devices & processes)
* `/etc`, `/var`, `/usr` are the most important directories
* Understanding filesystem = understanding Linux itself

---
