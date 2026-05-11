# Conditional Statements in Shell Script

---

# 1. What are Conditional Statements?

Conditional statements are used to make decisions in a shell script.

They allow the script to execute different commands based on whether a condition is **true** or **false**.

## Simple Definition:

> Conditional statements control the flow of a script depending on conditions.

---

# Real-Life Example

```text id="c1a2b3"
If age >= 18 → Allow voting
Else → Not eligible
```

---

# Why Use Conditional Statements?

* Check file existence
* Validate user input
* Compare numbers
* Check service status
* Monitor disk usage
* Automate decisions

---

# Main Conditional Statements in Shell Script

1. `if`
2. `if else`
3. `if elif else`
4. Nested if
5. `case`

---

# 2. Basic if Statement

## Syntax

```bash id="c4d5e6"
if [ condition ]
then
    commands
fi
```

---

# Example

```bash id="c7f8g9"
age=20

if [ $age -ge 18 ]
then
    echo "Eligible to vote"
fi
```

---

# Output

```text id="c0h1i2"
Eligible to vote
```

---

# Explanation

If condition is true, commands inside `then` run.

---

# 3. if else Statement

Used when one action for true and another for false.

## Syntax

```bash id="c3j4k5"
if [ condition ]
then
    commands_if_true
else
    commands_if_false
fi
```

---

# Example

```bash id="c6l7m8"
age=16

if [ $age -ge 18 ]
then
    echo "Adult"
else
    echo "Minor"
fi
```

---

# Output

```text id="c9n0o1"
Minor
```

---

# 4. if elif else Statement

Used for multiple conditions.

## Syntax

```bash id="c2p3q4"
if [ condition1 ]
then
    commands
elif [ condition2 ]
then
    commands
else
    commands
fi
```

---

# Example

```bash id="c5r6s7"
marks=75

if [ $marks -ge 90 ]
then
    echo "Grade A"
elif [ $marks -ge 75 ]
then
    echo "Grade B"
else
    echo "Grade C"
fi
```

---

# Output

```text id="c8t9u0"
Grade B
```

---

# 5. Nested if Statement

if inside another if.

## Example

```bash id="c1v2w3"
age=25
citizen=yes

if [ $age -ge 18 ]
then
    if [ $citizen = yes ]
    then
        echo "Can vote"
    fi
fi
```

---

# 6. Comparison Operators

## Numeric Operators

| Operator | Meaning          |
| -------- | ---------------- |
| `-eq`    | equal            |
| `-ne`    | not equal        |
| `-gt`    | greater than     |
| `-lt`    | less than        |
| `-ge`    | greater or equal |
| `-le`    | less or equal    |

---

# Example

```bash id="c4x5y6"
num=10

if [ $num -gt 5 ]
then
    echo "Greater"
fi
```

---

# 7. String Comparison

| Operator | Meaning      |
| -------- | ------------ |
| `=`      | equal        |
| `!=`     | not equal    |
| `-z`     | empty string |
| `-n`     | not empty    |

---

# Example

```bash id="c7z8a9"
name="Bhuvan"

if [ "$name" = "Bhuvan" ]
then
    echo "Welcome"
fi
```

---

# 8. File Condition Checks

| Test      | Meaning          |
| --------- | ---------------- |
| `-f file` | file exists      |
| `-d dir`  | directory exists |
| `-r file` | readable         |
| `-w file` | writable         |
| `-x file` | executable       |
| `-s file` | file not empty   |

---

# Example

```bash id="c0b1c2"
if [ -f data.txt ]
then
    echo "File exists"
fi
```

---

# 9. Logical Operators

## AND

```bash id="c3d4e5"
if [ $age -ge 18 ] && [ $age -le 60 ]
then
    echo "Working age"
fi
```

---

## OR

```bash id="c6f7g8"
if [ $day = "Sat" ] || [ $day = "Sun" ]
then
    echo "Weekend"
fi
```

---

# 10. Using Double Brackets `[[ ]]`

Modern Bash style.

```bash id="c9h0i1"
if [[ $name == B* ]]
then
    echo "Starts with B"
fi
```

Supports pattern matching.

---

# 11. case Statement

Used instead of multiple ifs.

## Syntax

```bash id="c2j3k4"
case $var in
    value1) commands ;;
    value2) commands ;;
    *) default ;;
esac
```

---

# Example

```bash id="c5l6m7"
read choice

case $choice in
1) echo "Create File" ;;
2) echo "Delete File" ;;
3) echo "Exit" ;;
*) echo "Invalid Choice" ;;
esac
```

---

# 12. Important Rules

## Spaces Required

Correct:

```bash id="c8n9o0"
if [ $a -gt 5 ]
```

Wrong:

```bash id="c1p2q3"
if[$a -gt 5]
```

---

## Quote Strings

Correct:

```bash id="c4r5s6"
if [ "$name" = "John" ]
```

---

# 13. Real-World Examples

---

# Disk Usage Alert

```bash id="c7t8u9"
usage=85

if [ $usage -gt 80 ]
then
    echo "Disk Full"
fi
```

---

# Service Check

```bash id="c0v1w2"
if systemctl is-active --quiet nginx
then
    echo "Running"
else
    echo "Stopped"
fi
```

---

# File Backup Check

```bash id="c3x4y5"
if [ -f backup.tar.gz ]
then
    echo "Backup Exists"
fi
```

---

# 14. Common Mistakes

Wrong:

```bash id="c6z7a8"
if [ $a=5 ]
```

Correct:

```bash id="c9b0c1"
if [ $a -eq 5 ]
```

Wrong:

```bash id="c2d3e4"
if [ "$name"=="John" ]
```

Correct:

```bash id="c5f6g7"
if [ "$name" = "John" ]
```

---

# 15. Interview Questions

## What is conditional statement?

Used for decision-making in scripts.

## Difference between if and case?

* `if` for conditions/comparisons
* `case` for matching fixed choices

## Why use `[[ ]]`?

Safer and supports patterns.

---

# 16. Summary

* Conditional statements control script flow.
* Use `if`, `else`, `elif`, `case`.
* Compare numbers, strings, files.
* Used heavily in automation.

---

# Final One-Line Definition

> Conditional statements in shell scripting are used to execute commands based on true or false conditions.
