# Complete Study Notes: Shell Script, Shell Scripting & Basics

---

# 1. What is a Shell?

A **Shell** is a command-line interpreter that allows users to communicate with the operating system.

It takes commands from the user and passes them to the Linux kernel for execution.

## Simple Architecture

```text id="g1a2b3"
User → Shell → Kernel → Hardware
```

Example:

```bash id="g4c5d6"
ls
pwd
date
```

These commands are interpreted by the shell.

---

# 2. What is a Shell Script?

A **Shell Script** is a file containing a list of Linux commands written in sequence.

Instead of typing commands manually one by one, we save them in a file and run the file.

## Definition:

> A shell script is a text file with shell commands used to automate tasks.

---

# Example

```bash id="g7e8f9"
#!/bin/bash
echo "Hello World"
date
pwd
```

Save as:

```text id="g0h1i2"
hello.sh
```

Run:

```bash id="g3j4k5"
bash hello.sh
```

---

# 3. What is Shell Scripting?

**Shell Scripting** is the process of writing shell scripts to automate system tasks.

## Definition:

> Shell scripting means creating scripts using shell commands, variables, loops, and conditions to perform automation.

---

# Real Examples of Shell Scripting

* Backup files automatically
* Create users in Linux
* Monitor disk space
* Deploy applications
* Rotate logs
* Run scheduled cron jobs

---

# 4. Why Use Shell Scripting?

## Automation

Repeat tasks without manual work.

## Save Time

Do in seconds what takes minutes manually.

## Reduce Human Error

Same task executes consistently.

## Important in DevOps

Used in:

* CI/CD
* Server management
* Cloud automation
* Monitoring

---

# 5. Types of Shells

| Shell        | Command | Description             |
| ------------ | ------- | ----------------------- |
| Bourne Shell | `sh`    | Original shell          |
| Bash         | `bash`  | Most common Linux shell |
| Korn Shell   | `ksh`   | Advanced shell          |
| C Shell      | `csh`   | C-style syntax          |
| Z Shell      | `zsh`   | Powerful modern shell   |

---

# Most Common Today

```bash id="g6l7m8"
bash
```

---

# 6. What is Bash?

**Bash** means:

```text id="g9n0o1"
Bourne Again Shell
```

Default shell in many Linux systems.

Used for commands + scripting.

---

# 7. What is Shebang?

The first line of many scripts:

```bash id="g2p3q4"
#!/bin/bash
```

This is called **Shebang**.

## Meaning:

It tells Linux:

> Run this script using Bash shell.

---

# Example

```bash id="g5r6s7"
#!/bin/bash
echo "Hello"
```

When executed:

```bash id="g8t9u0"
./script.sh
```

Linux uses Bash interpreter.

---

# 8. Comments in Shell Script

Comments are lines ignored by the shell.

Used to explain code.

## Single-Line Comment

```bash id="g1v2w3"
# This is a comment
```

---

# Example

```bash id="g4x5y6"
#!/bin/bash
# Print welcome message
echo "Welcome"
```

---

# Why Comments Important?

* Easy to understand code
* Documentation
* Helpful in teams

---

# 9. Variables in Shell Script

Variables store values.

## Syntax

```bash id="g7z8a9"
name="Bhuvan"
age=25
```

Use variable:

```bash id="g0b1c2"
echo $name
echo $age
```

---

# Output

```text id="g3d4e5"
Bhuvan
25
```

---

# Important Rule

No spaces:

Correct:

```bash id="g6f7g8"
name="John"
```

Wrong:

```bash id="g9h0i1"
name = John
```

---

# 10. User Input

Take input using `read`

```bash id="g2j3k4"
echo "Enter your name:"
read name
echo "Hello $name"
```

---

# 11. Command Substitution

Store command output in variable.

```bash id="g5l6m7"
today=$(date)
echo $today
```

---

# Example

```text id="g8n9o0"
Mon May 11
```

---

# 12. Output Commands

## echo

```bash id="g1p2q3"
echo "Hello"
```

## printf

```bash id="g4r5s6"
printf "Hello\n"
```

---

the process of writing Linux shell commands in a script file to automate tasks efficiently.
