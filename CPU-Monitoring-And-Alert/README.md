# CPU Monitoring Script (Real-World DevOps Use Case)

This script checks current CPU usage and sends an alert if CPU exceeds a threshold.

Used for:

* Detecting high CPU load
* Preventing application slowdowns
* Capacity monitoring
* Incident response
* Autoscaling signals

---

# Shell Script: CPU Usage Alert Script

```bash id="cpu1a2"
#!/bin/bash

#########################################
# CPU Usage Monitoring Script
# Alerts if CPU usage > 80%
#########################################

THRESHOLD=80

# Get CPU idle %, then calculate usage
CPU_USAGE=$(top -bn1 | grep "Cpu(s)" | awk '{print 100 - $8}' | cut -d. -f1)

echo "Current CPU Usage: ${CPU_USAGE}%"

if [ "$CPU_USAGE" -gt "$THRESHOLD" ]
then
    echo "High CPU Alert! Usage is ${CPU_USAGE}%"
else
    echo "CPU usage is normal."
fi
```

---

# Example Output

## Normal

```text id="cpu2b3"
Current CPU Usage: 34%
CPU usage is normal.
```

## High Usage

```text id="cpu3c4"
Current CPU Usage: 92%
High CPU Alert! Usage is 92%
```

---

# How It Works

## Get CPU Stats

```bash id="cpu4d5"
top -bn1
```

### Flags:

| Flag  | Meaning    |
| ----- | ---------- |
| `-b`  | Batch mode |
| `-n1` | Run once   |

---

## Extract CPU Idle

```bash id="cpu5e6"
grep "Cpu(s)"
```

Then:

```bash id="cpu6f7"
100 - idle%
```

Because:

```text id="cpu7g8"
CPU Usage = 100 - Idle
```

---

# Better Linux Alternative (`mpstat`)

```bash id="cpu8h9"
#!/bin/bash

THRESHOLD=80

CPU_USAGE=$(mpstat 1 1 | awk '/Average/ {print 100 - $NF}' | cut -d. -f1)

echo "CPU Usage: ${CPU_USAGE}%"
```

Install:

## Ubuntu

```bash id="cpu9i0"
sudo apt install sysstat -y
```

## Amazon Linux

```bash id="cpu0j1"
sudo yum install sysstat -y
```

---

