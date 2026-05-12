# Study Note: Service Restart Script

This shell script is a **real-world DevOps / Linux administration automation script** used to monitor a service and automatically restart it if it stops.

It is commonly used for:

* Web servers (`nginx`, `apache`)
* Databases (`mysql`, `postgresql`)
* CI/CD tools (`jenkins`)
* Containers (`docker`)
* Custom applications

---

# Full Script

```bash id="s1a2b3"
#!/bin/bash

#########################################
# Service Restart Script
# Checks if service is running
# If stopped, restart automatically
#########################################

SERVICE="nginx"

# Check service status
systemctl is-active --quiet $SERVICE

if [ $? -ne 0 ]; then
    echo "$SERVICE is down. Restarting..."

    systemctl restart $SERVICE

    if [ $? -eq 0 ]; then
        echo "$SERVICE restarted successfully."
    else
        echo "Failed to restart $SERVICE."
    fi
else
    echo "$SERVICE is running normally."
fi
```

---

# 1. Purpose of This Script

The script checks whether a Linux service is active.

If the service has stopped or failed:

* Restart automatically
* Print success/failure message

If running:

* Print healthy status

---

# Real Production Use Case

Suppose your website uses **Nginx**.

If Nginx crashes:

```text id="s4c5d6"
Website Down
Users Cannot Access App
Revenue Loss
```

This script can detect the issue and restart it automatically.

---

# 2. Shebang Line

```bash id="s7e8f9"
#!/bin/bash
```

## Meaning

Tells Linux:

> Execute this script using Bash shell.

Without it, Linux may use another shell.

---

# 3. Comment Block

```bash id="s0g1h2"
#########################################
# Service Restart Script
# Checks if service is running
# If stopped, restart automatically
#########################################
```

Used for documentation.

Comments are ignored by Bash.

---

# 4. Variable Declaration

```bash id="s3i4j5"
SERVICE="nginx"
```

Stores service name in a variable.

## Why Use Variable?

Instead of writing:

```bash id="s6k7l8"
systemctl restart nginx
systemctl status nginx
```

Use:

```bash id="s9m0n1"
$SERVICE
```

Easy to change later.

## Example

To monitor Apache:

```bash id="s2o3p4"
SERVICE="httpd"
```

Ubuntu Apache:

```bash id="s5q6r7"
SERVICE="apache2"
```

---

# 5. Check Service Status

```bash id="s8s9t0"
systemctl is-active --quiet $SERVICE
```

---

# What is systemctl?

`systemctl` manages Linux services using **systemd**.

Examples:

```bash id="s1u2v3"
systemctl start nginx
systemctl stop nginx
systemctl restart nginx
systemctl status nginx
```

---

# What does is-active do?

Checks if service is currently running.

---

# What does --quiet do?

Suppresses output.

Normally:

```bash id="s4w5x6"
systemctl is-active nginx
```

Output:

```text id="s7y8z9"
active
```

With `--quiet`, nothing is printed.

Instead, script checks exit code.

---

# 6. Exit Status `$?`

```bash id="s0a1b2"
$?
```

Stores status of previous command.

## Rules:

| Exit Code | Meaning |
| --------- | ------- |
| `0`       | Success |
| Non-zero  | Failure |

---

# Here:

```bash id="s3c4d5"
systemctl is-active --quiet nginx
```

Returns:

* `0` if running
* non-zero if stopped/failed

---

# 7. First if Condition

```bash id="s6e7f8"
if [ $? -ne 0 ]; then
```

---

# Breakdown

## `[ ]`

Test condition.

## `$?`

Previous command result.

## `-ne`

Not equal.

## Means:

If service status is **not success**, then service is down.

---

# Equivalent Meaning

```text id="s9g0h1"
If nginx is NOT active
```

---

# 8. Down Message

```bash id="s2i3j4"
echo "$SERVICE is down. Restarting..."
```

Output:

```text id="s5k6l7"
nginx is down. Restarting...
```

---

# 9. Restart Service

```bash id="s8m9n0"
systemctl restart $SERVICE
```

Attempts to restart service.

Equivalent:

```bash id="s1o2p3"
systemctl stop nginx
systemctl start nginx
```

but cleaner.

---

# 10. Second if Condition

```bash id="s4q5r6"
if [ $? -eq 0 ]; then
```

Checks whether restart command succeeded.

---

# Meaning

If restart successful:

```text id="s7s8t9"
Service started correctly
```

---

# 11. Success Message

```bash id="s0u1v2"
echo "$SERVICE restarted successfully."
```

Output:

```text id="s3w4x5"
nginx restarted successfully.
```

---

# 12. Failure Message

```bash id="s6y7z8"
else
    echo "Failed to restart $SERVICE."
```

Output:

```text id="s9a0b1"
Failed to restart nginx.
```

---

# Why Might Restart Fail?

* Bad config file
* Port already used
* Missing permissions
* Broken package
* Dependency failed

---

# 13. Else Block (Healthy Case)

```bash id="s2c3d4"
else
    echo "$SERVICE is running normally."
fi
```

If service already running:

```text id="s5e6f7"
nginx is running normally.
```

---

# Full Logic Flow

```text id="s8g9h0"
Check nginx status
        ↓
Is it running?
 ┌───────────────┐
 Yes             No
 ↓               ↓
Print healthy    Restart service
                 ↓
           Restart successful?
             ↓         ↓
            Yes       No
            ↓         ↓
       Success msg   Failure msg
```

---

# Checking Multiple Services at Once in Shell Script

If you want to monitor **multiple services** instead of just one (`nginx`), the best approach is to use a **loop** with a list/array of service names.

This is common in real DevOps environments where one server may run:

* nginx
* docker
* jenkins
* mysql
* sshd

---

# Multi-Service Restart Script

```bash id="m1a2b3"
#!/bin/bash

#########################################
# Multi Service Monitor & Restart Script
#########################################

SERVICES=("nginx" "docker" "jenkins")

for SERVICE in "${SERVICES[@]}"
do
    systemctl is-active --quiet "$SERVICE"

    if [ $? -ne 0 ]; then
        echo "$SERVICE is down. Restarting..."

        systemctl restart "$SERVICE"

        if [ $? -eq 0 ]; then
            echo "$SERVICE restarted successfully."
        else
            echo "Failed to restart $SERVICE."
        fi
    else
        echo "$SERVICE is running normally."
    fi

done
```

---

# How This Works

---

# 1. Array of Services

```bash id="m4c5d6"
SERVICES=("nginx" "docker" "jenkins")
```

Stores multiple service names.

---

# 2. for Loop

```bash id="m7e8f9"
for SERVICE in "${SERVICES[@]}"
```

Loops through each service one by one.

Execution order:

```text id="m0g1h2"
nginx
docker
jenkins
```

---

# 3. Check Each Service

```bash id="m3i4j5"
systemctl is-active --quiet "$SERVICE"
```

Checks current loop service.

---

# 4. Restart if Down

If stopped:

```bash id="m6k7l8"
systemctl restart "$SERVICE"
```

---

# Example Output

## Scenario:

* nginx running
* docker stopped
* jenkins running

```text id="m9m0n1"
nginx is running normally.
docker is down. Restarting...
docker restarted successfully.
jenkins is running normally.
```

---

# Why This Is Better Than Separate Scripts

Instead of:

```bash id="m2o3p4"
check nginx
check docker
check jenkins
```

One script manages all.

---

# Real Services You Can Monitor

Ubuntu:

```bash id="m5q6r7"
apache2
mysql
ssh
docker
jenkins
```

Amazon Linux / RHEL:

```bash id="m8s9t0"
httpd
mariadb
sshd
docker
nginx
```

---
