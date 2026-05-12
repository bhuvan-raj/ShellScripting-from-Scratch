<img src="https://github.com/bhuvan-raj/ShellScripting-from-Scratch/blob/main/assets/banner.png" alt="Shell Scripting Banner" />

<div align="center">

![Shell](https://img.shields.io/badge/Shell-Bash-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white)
![Level](https://img.shields.io/badge/Level-Beginner%20to%20Advanced-purple?style=for-the-badge)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Automation](https://img.shields.io/badge/Automation-Scripts-blue?style=for-the-badge)
![DevOps](https://img.shields.io/badge/DevOps-Ready-orange?style=for-the-badge)
![Contributions](https://img.shields.io/badge/Contributions-Welcome-brightgreen?style=for-the-badge)

# ShellScripting — From Scratch

### 🐚 From basic commands to advanced automation — comprehensive explanations, hands-on examples, and real-world scripting scenarios.

</div>

---

## 📖 About This Repository

**ShellScripting-from-Scratch** is a structured, example-based learning repository designed to take you from understanding the basics of shell scripting all the way through building automated system administration and DevOps workflows using Bash.

Every section is organized into its own folder with a dedicated `README.md` covering in-depth explanations, syntax breakdowns, practical examples, and hands-on labs. The content progresses logically — from foundational shell concepts to advanced automation scripts.

By the end of this course, you will be able to:

- ✅ Understand shell scripting fundamentals and write your first scripts
- ✅ Master conditional logic, operators, and decision-making structures
- ✅ Implement loops for iterative tasks and bulk operations
- ✅ Create reusable functions and modular script libraries
- ✅ Build production-ready automation for log management, backups, and monitoring
- ✅ Automate disk usage alerts and system health checks

---

## 📚 Table of Contents

## 1. Introduction to Shell and Basics

This section introduces the fundamentals of shell scripting — what a shell is, types of shells available in Linux/Unix systems, and how shell scripting differs from regular shell usage. It covers foundational concepts like variables, user input, comments, and command-line arguments that form the building blocks for all scripting tasks.

📂 **[Explore → Introduction to Shell and Basics](./Introduction-to-shell-and-basics/)**

---

## 2. Conditional Testing and Operators

This section explains how to perform tests and comparisons in shell scripts. It covers test commands, file test operators, string comparisons, numeric comparisons, logical operators (AND, OR, NOT), and understanding exit status codes — essential skills for writing intelligent, decision-making scripts.

📂 **[Explore → Conditional Testing and Operators](./Conditional-Testing-and-Operators/)**

---

## 3. Conditional Statements

This section provides a detailed understanding of conditional logic in shell scripting — how to make decisions based on conditions. It covers if, if-else, if-elif-else ladders, nested conditionals, case statements, and real-world examples demonstrating when and how to use each control structure.

📂 **[Explore → Conditional Statements](./conditional-statements/)**

---

## 4. Looping Statements

This section covers iteration and repetition in shell scripts — how to automate repetitive tasks using loops. It includes for loops, while loops, until loops, loop control mechanisms (break and continue), nested loops, and practical examples for processing files, arrays, and command outputs.

📂 **[Explore → Looping Statements](./Looping-Statements/)**

---

## 5. Shellscripting (Functions and Advanced Concepts)

This section provides a detailed understanding of functions in shell scripting — how to write reusable, modular code. It covers function declaration, parameters and arguments, local vs global variables, return values, recursive functions, and sourcing external script libraries.

📂 **[Explore → Advanced Shell Scripting](./Shellscripting/)**

---

## 6. Log Backup Automation

This section demonstrates real-world automation for log file management. You'll learn how to create automated log rotation scripts, implement backup strategies, compress old logs, schedule tasks using cron, and manage log retention policies — essential skills for system administration.

📂 **[Explore → Log Backup Automation](./Log-Backup/)**

---

## 7. Disk Usage Alert System

This section covers building a production-ready disk monitoring script. You'll learn how to check disk space usage, set alert thresholds, send email notifications when limits are exceeded, log monitoring events, and schedule automated health checks — critical for maintaining system reliability.

📂 **[Explore → Disk Usage Alert System](./Disk-Usage-Alert/)**

---

## 8. Service Status Check

This section covers building a production-ready disk service monitoring script where it checks whether a particular service is running or not, if it is not running, the script will automatically restarts that particular service using systemctl.

📂 **[Explore → Service Status Check](./Service-Status-Check/)**

---
## 9. CPU Monitoring and Alert

this script covers the logic of monitoring CPU and sends alert if the cpu usage is exceeding the target value.

📂 **[Explore → CPU Monitoring and Alert](./CPU-Monitoring-And-Alert/)**

## 🛠️ Prerequisites

Before diving in, make sure you have:

| Requirement | Details |
|-------------|---------|
| Linux/Unix Environment | Ubuntu, CentOS, macOS, or WSL on Windows |
| Bash Shell | Version 4.0 or higher (check with `bash --version`) |
| Text Editor | vim, nano, VS Code, or any editor of your choice |
| Basic Command Line | Comfortable with `cd`, `ls`, `cat`, and file navigation |
| Terminal Access | Ability to run commands and scripts |

---

## 🚦 Getting Started

```bash
# Clone this repository
git clone https://github.com/bhuvan-raj/ShellScripting-from-Scratch.git

# Navigate into the project
cd ShellScripting-from-Scratch

# Start with the first section
cd Introduction-to-shell-and-basics

# Make any script executable
chmod +x script-name.sh

# Run the script
./script-name.sh
```

Each folder contains its own `README.md` with step-by-step explanations, syntax examples, and practical scripts. Work through the topics in order for the best learning experience.

---

## 🎯 Learning Path

### **Week 1-2: Foundations**
- Introduction to Shell and Basics
- Conditional Testing and Operators
- Conditional Statements

### **Week 3-4: Control Flow**
- Looping Statements
- Advanced Shell Scripting (Functions)
- String Manipulation and Arrays

### **Week 5-6: Real-World Automation**
- Log Backup Automation
- Disk Usage Alert System
- Building Custom Automation Scripts

---

## 📂 Repository Structure

```
ShellScripting-from-Scratch/
│
├── Introduction-to-shell-and-basics/
│   ├── README.md
│   └── examples/
│
├── Conditional-Testing-and-Operators/
│   ├── README.md
│   └── examples/
│
├── conditional-statements/
│   ├── README.md
│   └── examples/
│
├── Looping-Statements/
│   ├── README.md
│   └── examples/
│
├── Shellscripting/
│   ├── README.md
│   └── examples/
│
├── Log-Backup/
│   ├── README.md
│   └── scripts/
│
├── Disk-Usage-Alert/
│   ├── README.md
│   └── scripts/
│
└── README.md (this file)
```

---

## 💡 Key Concepts Covered

<table>
<tr>
<td width="50%">

### **Fundamentals**
- Shell vs Shell Scripting
- Variables and Data Types
- User Input and Arguments
- Comments and Documentation
- Command Substitution
- Quoting and Escaping

</td>
<td width="50%">

### **Control Structures**
- if/else Conditionals
- case Statements
- for Loops
- while/until Loops
- Loop Control (break/continue)
- Nested Structures

</td>
</tr>
<tr>
<td width="50%">

### **Advanced Topics**
- Functions and Parameters
- Local/Global Scope
- Return Values
- Recursive Functions
- Script Libraries
- Error Handling

</td>
<td width="50%">

### **Practical Applications**
- Log Rotation
- Automated Backups
- Disk Monitoring
- Email Notifications
- Cron Scheduling
- System Health Checks

</td>
</tr>
</table>

---

## 🔧 Tools and Utilities

Throughout this repository, you'll work with essential Linux/Unix tools:

- **File Operations**: `cat`, `grep`, `sed`, `awk`, `find`
- **Text Processing**: `cut`, `sort`, `uniq`, `tr`, `wc`
- **System Monitoring**: `df`, `du`, `top`, `ps`, `free`
- **Networking**: `curl`, `wget`, `nc`, `ping`
- **Scheduling**: `cron`, `at`, `systemd timers`
- **Debugging**: `set -x`, `set -e`, `trap`, `shellcheck`

---

## 📚 Resources

### **Official Documentation**
- [Bash Reference Manual](https://www.gnu.org/software/bash/manual/) — Complete Bash documentation
- [Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/) — In-depth guide to advanced scripting
- [POSIX Shell Specification](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html) — Portable shell scripting standard

### **Recommended Tools**
- [ShellCheck](https://www.shellcheck.net/) — Static analysis tool for shell scripts
- [Bash-it](https://github.com/Bash-it/bash-it) — Community Bash framework
- [explainshell.com](https://explainshell.com/) — Visual breakdown of shell commands

### **Best Practices**
- [Google Shell Style Guide](https://google.github.io/styleguide/shellguide.html) — Industry-standard style guide
- [Bash Pitfalls](https://mywiki.wooledge.org/BashPitfalls) — Common mistakes to avoid
- [Defensive Bash Programming](https://dev.to/thiht/shell-scripts-matter) — Writing robust scripts

### **Practice Platforms**
- [HackerRank Shell](https://www.hackerrank.com/domains/shell) — Shell scripting challenges
- [LeetCode Shell](https://leetcode.com/problemset/shell/) — Database shell problems
- [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/) — Security-focused shell exercises

---

## 🎓 What You'll Build

By completing this repository, you'll have built:

| Project | Description | Skills Covered |
|---------|-------------|----------------|
| **User Management Script** | Automate user creation and permission assignment | Variables, conditionals, functions |
| **Log Rotation System** | Automated log backup with compression and retention | Loops, file operations, cron |
| **Disk Monitor** | Alert system for disk space thresholds | System commands, email notifications |
| **Backup Automation** | Scheduled backups with versioning | Functions, error handling, scheduling |
| **Health Check Dashboard** | System monitoring and reporting | Arrays, text processing, output formatting |

---

## 🤝 Contributing

Contributions are welcome! If you have suggestions for improvements, new examples, bug fixes, or additional topics, feel free to:

1. **Fork** this repository
2. **Create** a new branch (`git checkout -b feature/new-topic`)
3. **Commit** your changes (`git commit -m 'Add new shell scripting example'`)
4. **Push** to the branch (`git push origin feature/new-topic`)
5. **Open** a Pull Request

Please ensure your scripts:
- Follow the [Google Shell Style Guide](https://google.github.io/styleguide/shellguide.html)
- Pass [ShellCheck](https://www.shellcheck.net/) validation
- Include clear comments and documentation
- Provide practical, working examples

---

## ⭐ Show Your Support

If this repository helped you learn shell scripting or build automation workflows, please consider giving it a ⭐ star!

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**Bhuvan Raj**

- GitHub: [@bhuvan-raj](https://github.com/bhuvan-raj)
- Repository: [ShellScripting-from-Scratch](https://github.com/bhuvan-raj/ShellScripting-from-Scratch)

---

## 📞 Contact & Support

For questions, suggestions, or feedback:
- **Open an Issue**: [GitHub Issues](https://github.com/bhuvan-raj/ShellScripting-from-Scratch/issues)
- **Start a Discussion**: [GitHub Discussions](https://github.com/bhuvan-raj/ShellScripting-from-Scratch/discussions)

---

<div align="center">

**Happy Scripting! 🚀**

*Master the shell, automate everything!*

</div>
