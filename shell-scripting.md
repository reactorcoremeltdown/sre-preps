# **30 Common Shell Scripting Questions for SRE/DevOps Interviews (With Answers)**  

Shell scripting is a key skill for **SRE/DevOps** engineers as it automates system tasks, manages deployments, and handles configuration. Below are **30 commonly asked** shell scripting questions with detailed answers.  

---

## **Basic Shell Scripting Questions**  

### **1. What is a shell script?**  
A shell script is a text file containing shell commands, executed in sequence. It automates tasks such as backups, system monitoring, and deployments.  

**Example:**  
```sh
#!/bin/bash
echo "Hello, World!"
```
Run it using:  
```sh
chmod +x script.sh
./script.sh
```

---

### **2. What are different types of shells in Linux?**  
- **Bash (`/bin/bash`)** – Most common  
- **Sh (`/bin/sh`)** – POSIX-compliant  
- **Zsh (`/bin/zsh`)** – Advanced shell with plugins  
- **Ksh (`/bin/ksh`)** – Korn Shell  

Check default shell:  
```sh
echo $SHELL
```

---

### **3. How do you pass arguments to a shell script?**  
Use **positional parameters** (`$1`, `$2`, etc.).  

**Example (`args.sh`)**:  
```sh
#!/bin/bash
echo "First argument: $1"
echo "Second argument: $2"
```
Run:  
```sh
./args.sh arg1 arg2
```

---

### **4. How to read user input in a script?**  
Use `read` command.  
```sh
#!/bin/bash
echo "Enter your name:"
read name
echo "Hello, $name!"
```

---

### **5. How to check if a variable is empty?**  
```sh
if [ -z "$var" ]; then
    echo "Variable is empty"
fi
```

---

## **Control Flow & Loops**  

### **6. What is the difference between `if` and `case` statements?**  
- **`if`** is used for numeric and string comparisons.  
- **`case`** is better for pattern matching.  

**Example (`case.sh`)**:  
```sh
#!/bin/bash
read -p "Enter a number: " num
case $num in
  1) echo "One" ;;
  2) echo "Two" ;;
  *) echo "Other number" ;;
esac
```

---

### **7. How do you use a `for` loop in Bash?**  
```sh
for i in {1..5}; do
  echo "Iteration $i"
done
```

---

### **8. How to loop through files in a directory?**  
```sh
for file in /path/to/dir/*; do
  echo "Processing $file"
done
```

---

### **9. How to use a `while` loop?**  
```sh
i=1
while [ $i -le 5 ]; do
  echo "Count: $i"
  ((i++))
done
```

---

### **10. What does `set -e` do in a script?**  
It makes the script **exit immediately** if any command fails.  

```sh
#!/bin/bash
set -e
cp nonexistentfile /tmp  # Script will exit here
echo "This will not be executed"
```

---

## **File & String Operations**  

### **11. How do you check if a file exists?**  
```sh
if [ -f "file.txt" ]; then
  echo "File exists"
fi
```

---

### **12. How to check if a directory exists?**  
```sh
if [ -d "/path/to/dir" ]; then
  echo "Directory exists"
fi
```

---

### **13. How to append text to a file?**  
```sh
echo "New line" >> file.txt
```

---

### **14. How do you replace a string in a file?**  
Use `sed`:  
```sh
sed -i 's/oldtext/newtext/g' file.txt
```

---

### **15. How to count lines in a file?**  
```sh
wc -l < file.txt
```

---

## **Process Management & Signals**  

### **16. How to run a script in the background?**  
```sh
./script.sh &
```
Check running jobs:  
```sh
jobs
```

---

### **17. How to terminate a running process?**  
Find the process ID (PID):  
```sh
ps aux | grep myscript.sh
kill <PID>
```

---

### **18. What is the difference between `&`, `nohup`, and `screen`?**  
- **`&`** runs a process in the background.  
- **`nohup`** prevents termination when logging out.  
- **`screen`** allows resuming a session.  

Example:  
```sh
nohup myscript.sh &
```

---

### **19. How do you trap a signal in a shell script?**  
```sh
trap "echo 'Process interrupted'; exit" SIGINT SIGTERM
while true; do
  sleep 1
done
```

---

### **20. How do you find the exit code of the last command?**  
```sh
echo $?
```

---

## **Text Processing**  

### **21. How do you extract the first column from a file?**  
```sh
awk '{print $1}' file.txt
```

---

### **22. How to sort a file?**  
```sh
sort file.txt
```

---

### **23. How do you remove duplicate lines from a file?**  
```sh
sort file.txt | uniq
```

---

### **24. How do you filter lines matching a pattern?**  
```sh
grep "error" logfile.txt
```

---

### **25. How to check disk usage of a directory?**  
```sh
du -sh /path/to/dir
```

---

## **Advanced Topics**  

### **26. How to create and use a Bash function?**  
```sh
my_function() {
  echo "Hello, $1!"
}
my_function "User"
```

---

### **27. How to use `cron` jobs for automation?**  
Edit crontab:  
```sh
crontab -e
```
Example cron job (runs every minute):  
```sh
* * * * * /path/to/script.sh
```

---

### **28. How do you debug a Bash script?**  
Use `-x` to enable debug mode:  
```sh
bash -x script.sh
```

---

### **29. How to run multiple commands in one line?**  
```sh
command1 && command2  # Runs command2 only if command1 succeeds
command1 || command2  # Runs command2 only if command1 fails
```

---

### **30. How to store command output in a variable?**  
```sh
output=$(ls -l)
echo "$output"
```

---

## **Final Thoughts**  
These **30 shell scripting questions** will help you **ace SRE/DevOps interviews**! 🚀