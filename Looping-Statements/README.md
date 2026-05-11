# Looping Statements in Shell Script

---

# 1. What are Looping Statements?

Looping statements are used to execute a block of code repeatedly until a condition is met or for a fixed number of times.

## Simple Definition:

> A loop runs the same set of commands multiple times automatically.

---

# Why Use Loops?

Instead of writing:

```bash id="l1a2b3"
echo 1
echo 2
echo 3
echo 4
echo 5
```

Use a loop:

```bash id="l4c5d6"
for i in 1 2 3 4 5
do
    echo $i
done
```

---

# Real-World Uses of Loops

* Create multiple users
* Process files one by one
* Backup many folders
* Monitor services continuously
* Ping multiple servers
* Read file line by line

---

# Types of Loops in Shell Script

1. `for` loop
2. `while` loop
3. `until` loop
4. Nested loops
5. Loop control statements (`break`, `continue`)

---

# 2. for Loop

Used when number of iterations is known.

## Syntax

```bash id="l7e8f9"
for variable in list
do
    commands
done
```

---

# Example 1: Print Numbers

```bash id="l0g1h2"
for i in 1 2 3 4 5
do
    echo $i
done
```

## Output

```text id="l3i4j5"
1
2
3
4
5
```

---

# Example 2: Print Names

```bash id="l6k7l8"
for name in John Bhuvan Alice
do
    echo $name
done
```

---

# Example 3: Range Style (Bash)

```bash id="l9m0n1"
for i in {1..5}
do
    echo $i
done
```

---

# Example 4: C-Style for Loop

```bash id="l2o3p4"
for (( i=1; i<=5; i++ ))
do
    echo $i
done
```

---

# 3. while Loop

Used when loop should run while condition is true.

## Syntax

```bash id="l5q6r7"
while [ condition ]
do
    commands
done
```

---

# Example 1: Count 1 to 5

```bash id="l8s9t0"
count=1

while [ $count -le 5 ]
do
    echo $count
    count=$((count+1))
done
```

## Output

```text id="l1u2v3"
1
2
3
4
5
```

---

# Example 2: Infinite Loop

```bash id="l4w5x6"
while true
do
    echo "Running..."
    sleep 5
done
```

Used in monitoring scripts.

---

# 4. until Loop

Runs until condition becomes true.

## Syntax

```bash id="l7y8z9"
until [ condition ]
do
    commands
done
```

---

# Example

```bash id="l0a1b2"
count=1

until [ $count -gt 5 ]
do
    echo $count
    count=$((count+1))
done
```

## Output

```text id="l3c4d5"
1
2
3
4
5
```

---

# Difference:

* `while` runs while condition is true
* `until` runs while condition is false

---

# 5. Reading File Line by Line with while

Very common real-world use.

## Example

File: `users.txt`

```text id="l6e7f8"
john
alice
bob
```

Script:

```bash id="l9g0h1"
while read user
do
    echo "Creating user: $user"
done < users.txt
```

---

# Output

```text id="l2i3j4"
Creating user: john
Creating user: alice
Creating user: bob
```

---

# 6. Nested Loops

Loop inside another loop.

## Example

```bash id="l5k6l7"
for i in 1 2
do
    for j in A B
    do
        echo "$i $j"
    done
done
```

## Output

```text id="l8m9n0"
1 A
1 B
2 A
2 B
```

---

# 7. break Statement

Stops loop immediately.

## Example

```bash id="l1o2p3"
for i in 1 2 3 4 5
do
    if [ $i -eq 3 ]
    then
        break
    fi
    echo $i
done
```

## Output

```text id="l4q5r6"
1
2
```

---

# 8. continue Statement

Skips current iteration and moves next.

## Example

```bash id="l7s8t9"
for i in 1 2 3 4 5
do
    if [ $i -eq 3 ]
    then
        continue
    fi
    echo $i
done
```

## Output

```text id="l0u1v2"
1
2
4
5
```

---

# 9. Real-World DevOps Examples

---

# Check Multiple Servers

```bash id="l3w4x5"
for server in app1 app2 db1
do
    ping -c 1 $server
done
```

---

# Backup Multiple Directories

```bash id="l6y7z8"
for dir in /etc /var/log /home
do
    tar -czf $dir.tar.gz $dir
done
```

---

# Continuous Disk Monitoring

```bash id="l9a0b1"
while true
do
    df -h /
    sleep 60
done
```

---

# Create Users from File

```bash id="l2c3d4"
while read user
do
    useradd $user
done < users.txt
```

---

# 10. Important Operators Used in Loops

| Operator | Meaning          |
| -------- | ---------------- |
| `-lt`    | less than        |
| `-le`    | less or equal    |
| `-gt`    | greater than     |
| `-ge`    | greater or equal |
| `-eq`    | equal            |

---

# 11. Common Mistakes

Wrong:

```bash id="l5e6f7"
while[$a -lt 5]
```

Correct:

```bash id="l8g9h0"
while [ $a -lt 5 ]
```

---

Wrong increment:

```bash id="l1i2j3"
count=count+1
```

Correct:

```bash id="l4k5l6"
count=$((count+1))
```

---

# 12. When to Use Which Loop?

| Loop         | Use Case         |
| ------------ | ---------------- |
| `for`        | Known count/list |
| `while`      | Condition-based  |
| `until`      | Run until true   |
| `while read` | Read file lines  |

---

# 13. Interview Questions

## What is loop?

A loop repeats commands multiple times.

## Difference between for and while?

* `for` = known iterations
* `while` = depends on condition

## Use of break?

Stops loop.

## Use of continue?

Skips current iteration.

---

