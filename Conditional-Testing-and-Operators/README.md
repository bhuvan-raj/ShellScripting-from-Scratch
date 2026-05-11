# Conditional Testing Methods in Shell Script

Conditional testing methods are used in shell scripts to check conditions and make decisions.

They are commonly used with:

```bash id="t1a2b3"
if
if else
while
until
case
```

---

# 1. What is Conditional Testing?

Conditional testing means checking whether something is true or false.

Examples:

* Is number greater than 10?
* Is file present?
* Is username equal to admin?
* Is directory writable?

---

# Syntax of Test Conditions

## Method 1: Single Brackets

```bash id="t4c5d6"
if [ condition ]
then
    commands
fi
```

## Method 2: Double Brackets (Bash Preferred)

```bash id="t7e8f9"
if [[ condition ]]
then
    commands
fi
```

## Method 3: test command

```bash id="t0g1h2"
if test condition
then
    commands
fi
```

---

# Example

```bash id="t3i4j5"
num=10

if [ $num -gt 5 ]
then
    echo "Greater"
fi
```

---

# 2. Numeric Comparison Operators

Used to compare numbers.

| Operator | Meaning               |
| -------- | --------------------- |
| `-eq`    | Equal to              |
| `-ne`    | Not equal to          |
| `-gt`    | Greater than          |
| `-lt`    | Less than             |
| `-ge`    | Greater than or equal |
| `-le`    | Less than or equal    |

---

# Examples

## Equal

```bash id="t6k7l8"
if [ $a -eq 10 ]
then
    echo "Equal"
fi
```

---

## Greater Than

```bash id="t9m0n1"
if [ $a -gt 5 ]
then
    echo "Greater"
fi
```

---

## Less Than or Equal

```bash id="t2o3p4"
if [ $a -le 100 ]
then
    echo "OK"
fi
```

---

# Real Example

```bash id="t5q6r7"
usage=85

if [ $usage -gt 80 ]
then
    echo "Disk Full"
fi
```

---

# 3. String Comparison Operators

Used to compare text values.

| Operator | Meaning             |
| -------- | ------------------- |
| `=`      | Equal               |
| `==`     | Equal (Bash)        |
| `!=`     | Not equal           |
| `-z`     | String is empty     |
| `-n`     | String is not empty |

---

# Examples

## Equal

```bash id="t8s9t0"
name="Bhuvan"

if [ "$name" = "Bhuvan" ]
then
    echo "Welcome"
fi
```

---

## Not Equal

```bash id="t1u2v3"
if [ "$name" != "Admin" ]
then
    echo "Access Limited"
fi
```

---

## Empty String

```bash id="t4w5x6"
name=""

if [ -z "$name" ]
then
    echo "Empty"
fi
```

---

## Not Empty

```bash id="t7y8z9"
if [ -n "$name" ]
then
    echo "Has Value"
fi
```

---

# Why Use Quotes?

Correct:

```bash id="t0a1b2"
[ "$name" = "John" ]
```

Safer if variable empty or has spaces.

---

# 4. File Test Conditions

Used to check files/directories.

| Operator  | Meaning                      |
| --------- | ---------------------------- |
| `-f file` | File exists and regular file |
| `-d dir`  | Directory exists             |
| `-e file` | Exists (file or dir)         |
| `-r file` | Readable                     |
| `-w file` | Writable                     |
| `-x file` | Executable                   |
| `-s file` | File exists and not empty    |

---

# Examples

## File Exists

```bash id="t3c4d5"
if [ -f report.txt ]
then
    echo "File exists"
fi
```

---

## Directory Exists

```bash id="t6e7f8"
if [ -d /backup ]
then
    echo "Directory found"
fi
```

---

## Writable

```bash id="t9g0h1"
if [ -w data.txt ]
then
    echo "Writable"
fi
```

---

## File Not Empty

```bash id="t2i3j4"
if [ -s log.txt ]
then
    echo "Has content"
fi
```

---

# Real Example

```bash id="t5k6l7"
if [ -f backup.tar.gz ]
then
    echo "Backup ready"
else
    echo "No backup"
fi
```

---

# 5. Logical Operators

Used to combine multiple conditions.

---

# AND Operator

Both conditions must be true.

## Syntax

```bash id="t8m9n0"
if [ condition1 ] && [ condition2 ]
then
    commands
fi
```

---

## Example

```bash id="t1o2p3"
age=25

if [ $age -ge 18 ] && [ $age -le 60 ]
then
    echo "Working Age"
fi
```

---

# OR Operator

Any one condition true.

## Syntax

```bash id="t4q5r6"
if [ condition1 ] || [ condition2 ]
then
    commands
fi
```

---

## Example

```bash id="t7s8t9"
day="Sun"

if [ "$day" = "Sat" ] || [ "$day" = "Sun" ]
then
    echo "Weekend"
fi
```

---

# NOT Operator

Reverse condition.

## Example

```bash id="t0u1v2"
if [ ! -f file.txt ]
then
    echo "File missing"
fi
```

---

# 6. Using Double Brackets `[[ ]]`

Better in Bash.

Supports:

* pattern matching
* safer string tests
* easier logical checks

---

## Example

```bash id="t3w4x5"
name="Bhuvan"

if [[ $name == B* ]]
then
    echo "Starts with B"
fi
```

---

# 7. Real DevOps Examples

---

# Check Disk Usage

```bash id="t6y7z8"
usage=90

if [ $usage -gt 80 ]
then
    echo "Disk Alert"
fi
```

---

# Check Service Config File

```bash id="t9a0b1"
if [ -f /etc/nginx/nginx.conf ]
then
    echo "Nginx Installed"
fi
```

---

# Check Login User

```bash id="t2c3d4"
user="admin"

if [ "$user" = "admin" ]
then
    echo "Full Access"
fi
```

---

# Multiple Conditions

```bash id="t5e6f7"
if [ -f backup.sh ] && [ -x backup.sh ]
then
    echo "Ready to run"
fi
```

---

# 8. Common Mistakes

Wrong:

```bash id="t8g9h0"
if[$a -gt 5]
```

Correct:

```bash id="t1i2j3"
if [ $a -gt 5 ]
```

---

Wrong:

```bash id="t4k5l6"
if [ $name = John ]
```

Better:

```bash id="t7m8n9"
if [ "$name" = "John" ]
```

---

# 9. Interview Questions

## What is conditional testing?

Checking true/false conditions in script.

## Difference between `-eq` and `=`?

* `-eq` numeric comparison
* `=` string comparison

## What does `-f` mean?

Checks regular file exists.

## Difference between `&&` and `||`?

* `&&` = AND
* `||` = OR

---

# 10. Summary Table

| Type    | Examples      |   |    |
| ------- | ------------- | - | -- |
| Numeric | `-eq -gt -lt` |   |    |
| String  | `= != -z -n`  |   |    |
| File    | `-f -d -r -w` |   |    |
| Logical | `&&           |   | !` |

---

