![hdd-prep](title.png)

# hdd-prep

A safe, user-friendly Bash script to wipe, partition, format, mount, and permanently configure new HDDs/SSDs under `/mnt/`.

Created for Chia users who frequently add large storage drives.

---

## Features

- Safe by default with multiple guardrails and confirmation prompts  
- Automatically handles device unmounting and stale fstab entries  
- Uses GPT + ext4 optimized for large files (`largefile4`)  
- Adds proper fstab entry using UUID with `defaults,noatime,nodiratime`  
- Creates timestamped backups of `/etc/fstab` before changes  
- Full logging to `/var/log/hdd-prep.log`  
- `--list` mode to view all mounted drives and fstab status  
- Dry-run mode for testing  
- Colorful, clear output  

---

## Quick Start

```
# View current drives
sudo ./hdd-prep --list

# Prepare a new drive
sudo ./hdd-prep sdn hdd-13
```

---

## Installation

1. **Download the script**

```
# Download latest version
curl -O https://raw.githubusercontent.com/yourusername/hdd-prep/main/hdd-prep

# Or using wget
wget https://raw.githubusercontent.com/yourusername/hdd-prep/main/hdd-prep
```

2. **Make it executable**

```
chmod +x hdd-prep
```

3. **Move to a directory in your PATH** (recommended)

```
sudo mv hdd-prep /usr/local/bin/
```

Now you can run it from anywhere with:
```
sudo hdd-prep --list
```

---

## Usage

```
sudo hdd-prep <DEVICE> <MOUNT_NAME> [OPTIONS]
```

**Example:**
```
sudo hdd-prep sde hdd-04
```

`DEVICE`     → Block device name **without** `/dev/` (e.g. `sde`, `sdm`, `nvme1n1`)  
`MOUNT_NAME` → Desired folder name under `/mnt/` (e.g. `hdd-04`, `backup`, `media`)

---

## Options

| Option           | Description                                      |
|------------------|--------------------------------------------------|
| `-h`, `--help`   | Show help message                                |
| `--list`         | Show all `/mnt/` mounts and relevant fstab entries |
| `-n`, `--dry-run`| Simulate the process without making any changes  |
| `-f`, `--force`  | Skip most confirmation prompts (use with caution)|

---

## Logging

Every run is automatically logged to:

```
/var/log/hdd-prep.log
```

View recent activity with:

```
tail -n 50 /var/log/hdd-prep.log
```

---

## ⚠️ Important Warnings

**This script is destructive.**

- It will **permanently erase all data** on the target device.  
- Always double-check the device name before running.  
- The script includes multiple safety checks, but **you are responsible** for choosing the correct device.

### Disclaimer

**Use at your own risk.**  
This script comes with **no warranty**. The author is not liable for any data loss, system damage, or boot issues that may occur.

**Always**:
- Verify your device with `lsblk` first
- Keep backups of important data
- Know how to edit `/etc/fstab` in recovery mode if needed

---

## Requirements

- Root privileges (`sudo`)
- Standard tools: `wipefs`, `parted`, `mkfs.ext4`, `blkid`, `lsblk`, `tput`
- Tested on Ubuntu / Debian-based systems

---

## License

[Apache License 2.0](LICENSE)

---

**Made with 💚 for Chia enthusiasts.**