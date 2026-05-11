## Shell Script: Disk Usage Alert — In-Depth Explanation + Full Lab Setup

```bash id="m8x2qv"
#!/bin/bash

# Get root partition usage
usage=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')

# Check usage
if [ "$usage" -gt 80 ]; then
    echo "Warning: Root partition usage is ${usage}%" | mail -s "Disk Alert" admin@example.com
fi
```

---

# Part 1: In-Depth Script Explanation

---

# Line 1

```bash id="s1k2m3"
#!/bin/bash
```

## Meaning

This is called **shebang**.

It tells Linux:

> Execute this file using Bash shell.

When you run:

```bash id="r4t5y6"
./disk_alert.sh
```

Linux reads the first line and uses:

```bash id="u7i8o9"
/bin/bash
```

to interpret the script.

---

# Line 2 Comment

```bash id="c1v2b3"
# Get root partition usage
```

Comment line. Used for readability.

---

# Line 3

```bash id="x4z5a6"
usage=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')
```

This stores root disk usage inside variable `usage`.

---

## Step-by-Step Breakdown

---

## `df -h /`

Means:

* `df` = disk filesystem usage
* `-h` = human readable (GB, MB)
* `/` = check root partition only

Example output:

```text id="d1f2g3"
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda1       20G   17G   3G   85% /
```

---

## Pipe `|`

Pass output to next command.

---

## `awk 'NR==2 {print $5}'`

### Meaning:

* `NR` = line number
* `==2` = only second line
* `print $5` = print fifth column

From:

```text id="h4j5k6"
/dev/xvda1 20G 17G 3G 85% /
```

prints:

```text id="l7m8n9"
85%
```

---

## Pipe to `sed`

```bash id="q1w2e3"
sed 's/%//'
```

Removes `%`

Result:

```text id="r4t5y6"
85
```

---

## `$()`

Command substitution.

Stores command output into variable.

So:

```bash id="y7u8i9"
usage=85
```

---

# Next Block

```bash id="p0o9i8"
if [ "$usage" -gt 80 ]; then
```

---

## Meaning

If usage is greater than 80.

### `[ ]`

Test condition.

### `-gt`

Numeric greater than.

---

## Examples

```bash id="a1s2d3"
85 -gt 80   TRUE
70 -gt 80   FALSE
```

---

# Alert Line

```bash id="f4g5h6"
echo "Warning: Root partition usage is ${usage}%" | mail -s "Disk Alert" admin@example.com
```

---

## echo

Creates message:

```text id="j7k8l9"
Warning: Root partition usage is 85%
```

---

## Pipe to mail

```bash id="z1x2c3"
mail -s "Disk Alert" admin@example.com
```

### `-s`

Subject:

```text id="v4b5n6"
Disk Alert
```

### Recipient:

```text id="m7q8w9"
admin@example.com
```

---

# fi

Ends if block.

```bash id="e1r2t3"
fi
```

---

# Full Logic

```text id="f1l2o3"
Check root usage
   ↓
If usage >80
   ↓
Send email alert
```

---

## Disk Alert Script Lab Setup for **Amazon Linux** and **Ubuntu**

We’ll cover:

1. Create the shell script
2. Configure mail service
3. Test email sending
4. Run script manually
5. Automate with cron

---

# The Script

```bash id="sc1a2b"
#!/bin/bash

usage=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')

if [ "$usage" -gt 80 ]; then
    echo "Warning: Root partition usage is ${usage}%" | mail -s "Disk Alert" admin@example.com
fi
```

Replace:

```text id="em3c4d"
admin@example.com
```

with your real email.

---

# PART A — Ubuntu / Debian

---

# Step 1: Connect to Server

```bash id="ub1a2c"
ssh ubuntu@your-server-ip
```

---

# Step 2: Install Mail Packages

```bash id="ub3d4e"
sudo apt update
sudo apt install mailutils postfix -y
```

---

# Step 3: During Postfix Setup

Choose:

```text id="ub5f6g"
Internet Site
```

System mail name:

```text id="ub7h8i"
server.localdomain
```

---

# Step 4: Start Service

```bash id="ub9j0k"
sudo systemctl enable postfix
sudo systemctl start postfix
sudo systemctl status postfix
```

---

# Step 5: Create Script

```bash id="ub1l2m"
nano disk_alert.sh
```

Paste script → Save.

---

# Step 6: Give Permission

```bash id="ub3n4o"
chmod +x disk_alert.sh
```

---

# Step 7: Test Mail

```bash id="ub5p6q"
echo "Ubuntu test mail" | mail -s "Mail Test" yourmail@gmail.com
```

---

# Step 8: Run Script

```bash id="ub7r8s"
./disk_alert.sh
```

---

# Step 9: Force Alert Test

Change:

```bash id="ub9t0u"
if [ "$usage" -gt 1 ]; then
```

Then run again.

---

# Step 10: Mail Logs

```bash id="ub1v2w"
sudo tail -f /var/log/mail.log
```

---

# PART B — Amazon Linux (EC2)

---

# Step 1: Connect to EC2

```bash id="am1a2b"
ssh -i key.pem ec2-user@ec2-public-ip
```

---

# Step 2: Install Mail Packages

## Amazon Linux 2

```bash id="am3c4d"
sudo yum update -y
sudo yum install postfix mailx -y
```

## Amazon Linux 2023

```bash id="am5e6f"
sudo dnf update -y
sudo dnf install postfix mailx -y
```

---

# Step 3: Enable Mail Service

```bash id="am7g8h"
sudo systemctl enable postfix
sudo systemctl start postfix
sudo systemctl status postfix
```

---

# Step 4: Create Script

```bash id="am9i0j"
nano disk_alert.sh
```

Paste script.

---

# Step 5: Give Permission

```bash id="am1k2l"
chmod +x disk_alert.sh
```

---

# Step 6: Test Mail

```bash id="am3m4n"
echo "Amazon Linux test mail" | mail -s "Mail Test" yourmail@gmail.com
```

---

# Step 7: Run Script

```bash id="am5o6p"
./disk_alert.sh
```

---

# Step 8: Mail Logs

```bash id="am7q8r"
sudo tail -f /var/log/maillog
```

---

# IMPORTANT for AWS EC2

Direct outbound SMTP (port 25) may be blocked by AWS.

So mail may fail unless you use:

## Recommended:

* Amazon SES
* Gmail SMTP relay
* SendGrid

---

# Best AWS Method: Amazon SES SMTP

Use SES instead of local postfix sending.

Then configure Postfix relay.

If you'd like, I can give exact SES setup.

---

# Cron Job for Both Ubuntu / Amazon Linux

Run every 5 mins:

```bash id="cr1a2b"
crontab -e
```

Add:

```bash id="cr3c4d"
*/5 * * * * /home/ec2-user/disk_alert.sh
```

Ubuntu user:

```bash id="cr5e6f"
*/5 * * * * /home/ubuntu/disk_alert.sh
```

---

# Verify Cron

```bash id="cr7g8h"
crontab -l
```

---

# Common Problems

---

## mail command not found

Ubuntu:

```bash id="er1a2b"
sudo apt install mailutils -y
```

Amazon Linux:

```bash id="er3c4d"
sudo yum install mailx -y
```

---

## No Email Received

Check:

* Spam folder
* SMTP blocked on AWS
* Postfix logs

---

## Permission denied

```bash id="er5e6f"
chmod +x disk_alert.sh
```

---

# Real DevOps Recommendation

## Ubuntu VM:

Use Gmail SMTP + msmtp

## AWS EC2:

Use Amazon SES SMTP

---

# Interview Answer

> On Ubuntu or Amazon Linux, install `postfix` + `mailx/mailutils`, enable postfix, test sending mail, then schedule the monitoring script through cron.

---
