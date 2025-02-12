Here are **30 commonly asked Linux questions** in **SRE/DevOps job interviews**, along with detailed answers.

---

## **1. How do you check CPU and memory usage in Linux?**
- **Commands**:
  - `top` / `htop` (interactive system monitoring)
  - `free -m` (memory usage)
  - `vmstat 1 5` (performance stats)
  - `mpstat -P ALL 1` (per-CPU usage)
  - `cat /proc/meminfo` (detailed memory stats)

---

## **2. How do you find the largest files on a Linux system?**
- Use the `find` command:
  ```bash
  find / -type f -exec du -h {} + | sort -rh | head -10
  ```
- Or use `du`:
  ```bash
  du -ah / | sort -rh | head -10
  ```

---

## **3. How do you check which process is using a specific port?**
- Use:
  ```bash
  netstat -tulnp | grep :PORT
  ss -tulnp | grep :PORT
  lsof -i :PORT
  ```

---

## **4. How do you find a process and kill it?**
- **Find process by name**:  
  ```bash
  ps aux | grep process_name
  ```
- **Kill by PID**:  
  ```bash
  kill -9 PID
  ```

---

## **5. How do you count the number of lines in a file?**
- `wc -l filename`

---

## **6. What does `nohup` do in Linux?**
- `nohup` lets a process continue running even after the user logs out.
  ```bash
  nohup myscript.sh &
  ```

---

## **7. How do you create a tar archive and extract it?**
- Create:
  ```bash
  tar -cvf archive.tar files/
  ```
- Extract:
  ```bash
  tar -xvf archive.tar
  ```

---

## **8. How do you monitor logs in real time?**
- `tail -f /var/log/syslog`
- `journalctl -f`

---

## **9. What is the difference between a hard link and a soft link?**
| Feature        | Hard Link       | Soft Link (Symlink) |
|---------------|----------------|----------------------|
| Points to     | File inode      | File path |
| Breaks if original file is deleted | No | Yes |
| Works across filesystems | No | Yes |

- Create:
  ```bash
  ln original.txt hardlink.txt
  ln -s original.txt symlink.txt
  ```

---

## **10. How do you check disk usage?**
- `df -h` (disk space)
- `du -sh /path/` (size of a directory)

---

## **11. How do you change file permissions and ownership?**
- **Change permissions**:
  ```bash
  chmod 644 file
  ```
- **Change ownership**:
  ```bash
  chown user:group file
  ```

---

## **12. How do you find a file in Linux?**
- `find / -name "filename"`
- `locate filename`

---

## **13. How do you restart a service using systemd?**
- `systemctl restart service_name`

---

## **14. How do you check system uptime?**
- `uptime`

---

## **15. How do you check kernel version?**
- `uname -r`

---

## **16. How do you list all installed packages?**
- **Debian-based (Ubuntu, Debian):**
  ```bash
  dpkg -l
  ```
- **RHEL-based (CentOS, Fedora):**
  ```bash
  rpm -qa
  ```
- **Universal (works in most distributions):**
  ```bash
  apt list --installed  # Debian
  yum list installed    # RHEL
  ```

---

## **17. What is the difference between `/dev`, `/proc`, and `/sys`?**
- `/dev` - Contains device files (e.g., `/dev/sda` for disks).
- `/proc` - Virtual filesystem with process and system info (`/proc/cpuinfo`).
- `/sys` - Exposes kernel parameters.

---

## **18. How do you schedule a cron job?**
- Edit crontab with:
  ```bash
  crontab -e
  ```
- Example:
  ```bash
  0 3 * * * /path/to/script.sh  # Runs daily at 3 AM
  ```

---

## **19. How do you list running processes?**
- `ps aux`
- `top` / `htop`

---

## **20. How do you mount and unmount a filesystem?**
- **Mount**:
  ```bash
  mount /dev/sdb1 /mnt
  ```
- **Unmount**:
  ```bash
  umount /mnt
  ```

---

## **21. How do you check free and used memory?**
- `free -m`
- `vmstat -s`

---

## **22. How do you check network connections?**
- `netstat -tulnp`
- `ss -tulnp`
- `lsof -i`

---

## **23. What is `nice` and `renice`?**
- **nice**: Start a process with a lower/higher priority.
  ```bash
  nice -n 10 myscript.sh
  ```
- **renice**: Change priority of a running process.
  ```bash
  renice -n 5 -p PID
  ```

---

## **24. How do you create a new user and add it to a group?**
- Create user:
  ```bash
  useradd -m username
  ```
- Add user to a group:
  ```bash
  usermod -aG groupname username
  ```

---

## **25. How do you lock and unlock a user account?**
- **Lock:**
  ```bash
  passwd -l username
  ```
- **Unlock:**
  ```bash
  passwd -u username
  ```

---

## **26. How do you check available shell interpreters?**
- `cat /etc/shells`

---

## **27. What are `soft` and `hard` limits in Linux?**
- **Soft limit**: User can exceed temporarily.
- **Hard limit**: Maximum enforced by kernel.
- Check:
  ```bash
  ulimit -a
  ```

---

## **28. What are the differences between `ext3` and `ext4`?**
- **ext4** supports larger files, faster performance, and journaling improvements.

---

## **29. How do you change the hostname?**
- **Temporary:**
  ```bash
  hostname new-hostname
  ```
- **Permanent (Ubuntu/Debian):**
  ```bash
  echo "new-hostname" > /etc/hostname
  ```

---

## **30. How do you check system logs?**
- **General logs**:
  ```bash
  journalctl -xe
  ```
- **Authentication logs**:
  ```bash
  cat /var/log/auth.log
  ```

---

### **Final Thoughts**
These **30 Linux interview questions** cover **essential topics** for **SRE/DevOps** roles. The best way to prepare is by **practicing these commands on a real Linux system**. 🚀