### **30 Common Linux Internal Mechanisms, Process, and Memory Management Interview Questions for SRE/DevOps**  

Understanding **Linux internals** is crucial for **SRE/DevOps** engineers, especially when troubleshooting performance issues, optimizing resource usage, and debugging processes. Below are **30 commonly asked** questions along with detailed answers.

---

## **1. What happens when you execute a command in a Linux shell?**  
When you type a command (e.g., `ls`) and press Enter:  
1. The shell searches for the executable in `$PATH`.  
2. A **new process is created** using `fork()`.  
3. The child process is replaced with `exec()` to run the command.  
4. The process runs, produces output, and exits with a status code.  

---

## **2. What are the different types of process states in Linux?**  
A process can be in the following states:  
- **R (Running)**: Actively executing or ready to run.  
- **S (Sleeping)**: Waiting for an event (I/O, network, etc.).  
- **D (Uninterruptible Sleep)**: Waiting for non-interruptible I/O.  
- **T (Stopped)**: Stopped manually (e.g., `SIGSTOP`).  
- **Z (Zombie)**: Process completed, but parent hasn’t collected exit status.  

Check process states using:  
```sh
ps aux
```

---

## **3. What is a zombie process?**  
A **zombie process** is a process that has completed execution but its parent hasn't collected its exit status.  

To find zombies:  
```sh
ps aux | grep Z
```

To eliminate zombies, **kill the parent process**:  
```sh
kill -9 <parent_pid>
```

---

## **4. What is the difference between `fork()` and `exec()`?**  
- **`fork()`**: Creates a new process (child process) that is a copy of the parent.  
- **`exec()`**: Replaces the current process image with a new program.  

Example:  
```c
pid_t pid = fork();
if (pid == 0) {
    execlp("/bin/ls", "ls", NULL);
}
```

---

## **5. How does Linux handle memory allocation?**  
Linux uses:  
- **Heap & Stack**: Managed by `malloc()`, `free()`, and automatic allocations.  
- **Paging & Swapping**: Moves unused memory to disk (swap).  
- **Virtual Memory**: Processes see a continuous memory space, mapped to physical RAM.  

Check memory usage:  
```sh
free -m
```

---

## **6. What is a memory leak?**  
A **memory leak** occurs when allocated memory is not freed, leading to excessive RAM usage.

Detect with:  
```sh
valgrind --leak-check=full ./my_program
```

---

## **7. What are `ulimit` settings?**  
`ulimit` defines resource limits for user processes.

Check limits:  
```sh
ulimit -a
```

Set max open files:  
```sh
ulimit -n 100000
```

---

## **8. How does Linux handle process scheduling?**  
Linux uses the **Completely Fair Scheduler (CFS)** with priorities defined by:  
- **Nice value (-20 to 19)** (Lower = higher priority).  
- **Real-time scheduling policies** (`SCHED_FIFO`, `SCHED_RR`).  

Check scheduling:  
```sh
ps -eo pid,pri,nice,comm
```

---

## **9. What is `OOM Killer` in Linux?**  
The **Out-of-Memory (OOM) Killer** terminates processes when the system is out of RAM.

Check OOM logs:  
```sh
dmesg | grep -i "oom"
```

---

## **10. What is Swappiness?**  
Swappiness (0-100) controls how aggressively the kernel swaps memory to disk.  

Check swappiness:  
```sh
cat /proc/sys/vm/swappiness
```

Set swappiness:  
```sh
sysctl -w vm.swappiness=10
```

---

## **11. What is the difference between soft and hard limits in `ulimit`?**  
- **Soft limit**: Can be increased by user.  
- **Hard limit**: Can only be increased by root.

Check limits:  
```sh
ulimit -a
```

---

## **12. What is HugePages in Linux?**  
HugePages optimize memory access by allocating large pages instead of small ones.  

Enable HugePages:  
```sh
echo 512 > /proc/sys/vm/nr_hugepages
```

---

## **13. What is `strace` used for?**  
`strace` traces **system calls** made by a process.

Example:  
```sh
strace -p <pid>
```

---

## **14. What is `lsof` used for?**  
`lsof` lists open files.

Check open files by a process:  
```sh
lsof -p <pid>
```

---

## **15. What is a file descriptor in Linux?**  
A **file descriptor (FD)** is an integer representing an open file.

Common FDs:  
- **0** → stdin  
- **1** → stdout  
- **2** → stderr  

List file descriptors:  
```sh
ls -l /proc/<pid>/fd
```

---

## **16. What is the difference between `nice` and `renice`?**  
- **`nice`** sets priority when launching a process.  
- **`renice`** changes priority of a running process.  

Example:  
```sh
nice -n -10 ./my_program
renice -5 -p <pid>
```

---

## **17. What are shared memory and IPC mechanisms in Linux?**  
- **Pipes** (`|`)  
- **Shared Memory (`shmget`, `shmat`)**  
- **Message Queues (`msgget`, `msgsnd`)**  
- **Sockets**  

---

## **18. How do you list running processes with resource usage?**  
```sh
top
htop
ps aux --sort=-%mem
```

---

## **19. How does the kernel manage process execution?**  
Using **context switching**, the kernel:  
1. Saves process state (registers, stack).  
2. Switches to another process.  
3. Restores the state when resuming.  

---

## **20. How to measure CPU load in Linux?**  
```sh
uptime
top
mpstat
```

---

## **21. What is a Runqueue in Linux?**  
The **Runqueue** holds runnable processes waiting for CPU.

Check queue size:  
```sh
cat /proc/loadavg
```

---

## **22. What is Kernel Space vs. User Space?**  
- **User Space**: Where applications run.  
- **Kernel Space**: Where system processes and drivers run.  

---

## **23. How to find which process is using most memory?**  
```sh
ps aux --sort=-%mem | head
```

---

## **24. What is Transparent Huge Pages (THP)?**  
THP dynamically manages large memory pages to improve performance.

Disable THP:  
```sh
echo never > /sys/kernel/mm/transparent_hugepage/enabled
```

---

## **25. What is Dirty Memory in Linux?**  
Dirty memory contains modified data **not yet written to disk**.

Flush dirty pages:  
```sh
sync
```

---

## **26. How does `malloc()` work internally?**  
- Allocates memory from the **heap**.  
- Uses `sbrk()` or `mmap()` to request memory from the OS.  

---

## **27. How to detect a memory leak in a running process?**  
```sh
pmap <pid> | tail -n 1
```

---

## **28. What is a Coredump?**  
A **coredump** is a snapshot of a crashed process for debugging.

Enable core dumps:  
```sh
ulimit -c unlimited
```

---

## **29. How does Linux handle file caching?**  
Linux caches files in RAM and writes them lazily.

Clear cache:  
```sh
echo 3 > /proc/sys/vm/drop_caches
```

---

## **30. How to tune kernel parameters at runtime?**  
```sh
sysctl -w vm.dirty_ratio=20
```

---

### **Final Thoughts**  
These **30 Linux internals questions** will help you **ace SRE/DevOps** interviews. 🚀