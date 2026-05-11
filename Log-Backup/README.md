# Real-Time Log Backup to S3 + Cleanup Script

```bash id="lg1a2b"
#!/bin/bash

#############################################
# Real-Time Log Backup to S3 + Cleanup
#############################################

DATE=$(date +%Y-%m-%d_%H-%M-%S)
HOSTNAME=$(hostname)

LOG_SOURCE="/var/log/myapp"
BACKUP_DIR="/tmp/log_backup"
ARCHIVE_NAME="${HOSTNAME}_logs_${DATE}.tar.gz"
S3_BUCKET="s3://your-log-backup-bucket"

mkdir -p $BACKUP_DIR

echo "Starting log backup..."

cp -r $LOG_SOURCE/* $BACKUP_DIR/

tar -czf /tmp/$ARCHIVE_NAME -C $BACKUP_DIR .

aws s3 cp /tmp/$ARCHIVE_NAME $S3_BUCKET/

if [ $? -eq 0 ]; then
    echo "Backup uploaded successfully to S3"
    rm -rf $BACKUP_DIR
    rm -f /tmp/$ARCHIVE_NAME
    echo "Local backup cleaned successfully"
else
    echo "S3 Upload Failed! Backup not deleted."
fi
```

---

# What This Script Does (High-Level)

This is a common DevOps backup automation workflow:

```text id="flow1a2b"
Application Logs
      ↓
Copy logs to temp backup folder
      ↓
Compress into .tar.gz
      ↓
Upload archive to AWS S3
      ↓
If upload successful:
   Delete local temp files
Else:
   Keep backup for retry/debug
```

Used for:

* Application log archival
* Saving disk space
* Centralized log retention
* Disaster recovery
* Compliance backups

---

# Line-by-Line Deep Explanation

---

# 1. Shebang

```bash id="sh1a2b"
#!/bin/bash
```

## Meaning

Tells Linux to run this file using Bash shell.

When you execute:

```bash id="sh3c4d"
./backup.sh
```

Linux uses:

```bash id="sh5e6f"
/bin/bash backup.sh
```

---

# 2. Comment Block

```bash id="cm1a2b"
#############################################
# Real-Time Log Backup to S3 + Cleanup
#############################################
```

For readability/documentation only.

No execution.

---

# 3. Date Variable

```bash id="dt1a2b"
DATE=$(date +%Y-%m-%d_%H-%M-%S)
```

## Meaning

Stores current timestamp.

Example:

```text id="dt3c4d"
2026-05-11_10-45-22
```

## Why Needed?

Used in filename to avoid overwrite and track backup time.

---

# 4. Hostname Variable

```bash id="hn1a2b"
HOSTNAME=$(hostname)
```

Gets server hostname.

Example:

```text id="hn3c4d"
webserver01
```

## Why Needed?

If many servers upload to same bucket:

```text id="hn5e6f"
webserver01_logs...
dbserver01_logs...
```

Easy identification.

---

# 5. Log Source Path

```bash id="lg3a4b"
LOG_SOURCE="/var/log/myapp"
```

Folder containing logs to back up.

Example:

```text id="lg5c6d"
/var/log/myapp/app.log
/var/log/myapp/error.log
```

---

# 6. Temporary Backup Directory

```bash id="bk1a2b"
BACKUP_DIR="/tmp/log_backup"
```

Used as staging area before compression.

---

# 7. Archive Name

```bash id="ar1a2b"
ARCHIVE_NAME="${HOSTNAME}_logs_${DATE}.tar.gz"
```

Creates dynamic filename.

Example:

```text id="ar3c4d"
webserver01_logs_2026-05-11_10-45-22.tar.gz
```

---

# 8. S3 Bucket

```bash id="s31a2b"
S3_BUCKET="s3://your-log-backup-bucket"
```

Destination cloud storage bucket.

---

# 9. Create Backup Folder

```bash id="mk1a2b"
mkdir -p $BACKUP_DIR
```

## Meaning

Create directory if missing.

`-p` avoids error if already exists.

---

# 10. Print Status

```bash id="ec1a2b"
echo "Starting log backup..."
```

Displays progress.

---

# 11. Copy Logs

```bash id="cp1a2b"
cp -r $LOG_SOURCE/* $BACKUP_DIR/
```

## Meaning

Copy all logs recursively into temp folder.

### Example

From:

```text id="cp3c4d"
/var/log/myapp/app.log
/var/log/myapp/archive/old.log
```

To:

```text id="cp5e6f"
/tmp/log_backup/
```

---

# Why Copy First?

Instead of compressing live logs directly:

* safer
* avoids changing active files
* creates snapshot

---

# 12. Compress Backup

```bash id="tr1a2b"
tar -czf /tmp/$ARCHIVE_NAME -C $BACKUP_DIR .
```

---

## Breakdown

### `tar`

Archive tool.

### `-c`

Create archive.

### `-z`

Use gzip compression.

### `-f`

Output filename follows.

### `/tmp/$ARCHIVE_NAME`

Archive path.

### `-C $BACKUP_DIR`

Change into folder before packing.

### `.`

Archive current folder contents.

---

# Output Example

```text id="tr3c4d"
/tmp/webserver01_logs_2026-05-11_10-45-22.tar.gz
```

---

# Why Use tar.gz?

* smaller size
* faster upload
* single file
* preserves structure

---

# 13. Upload to S3

```bash id="aw1a2b"
aws s3 cp /tmp/$ARCHIVE_NAME $S3_BUCKET/
```

Uses AWS CLI.

Copies archive to bucket.

Example:

```text id="aw3c4d"
s3://your-log-backup-bucket/webserver01_logs_2026...
```

---

# Requirement

AWS CLI configured:

```bash id="aw5e6f"
aws configure
```

or IAM Role attached to EC2.

---

# 14. Check Exit Status

```bash id="if1a2b"
if [ $? -eq 0 ]; then
```

## `$?`

Exit code of previous command.

Here previous command is:

```bash id="if3c4d"
aws s3 cp ...
```

### Meaning

* `0` = success
* non-zero = failure

---

# So This Means

If upload succeeded, then run cleanup.

---

# 15. Success Message

```bash id="ok1a2b"
echo "Backup uploaded successfully to S3"
```

---

# 16. Delete Temp Folder

```bash id="rm1a2b"
rm -rf $BACKUP_DIR
```

## Meaning

Remove backup directory recursively.

### `-r`

Recursive.

### `-f`

Force.

---

# Why?

Clean temp staging area for next run.

---

# 17. Delete Tar File

```bash id="rm3c4d"
rm -f /tmp/$ARCHIVE_NAME
```

Deletes compressed archive from local server.

Prevents disk filling.

---

# 18. Cleanup Message

```bash id="cl1a2b"
echo "Local backup cleaned successfully"
```

---

# 19. Failure Case

```bash id="el1a2b"
else
    echo "S3 Upload Failed! Backup not deleted."
fi
```

If upload failed:

* keep temp files
* keep tar archive
* allow retry/debug

Very important production behavior.

---

# Full Runtime Example

```text id="rt1a2b"
Starting log backup...
upload: /tmp/web01_logs_2026... to s3://bucket/...
Backup uploaded successfully to S3
Local backup cleaned successfully
```

---

# Why This Is Real DevOps Style

It includes:

✅ timestamped backups
✅ hostname tagging
✅ compression
✅ cloud upload
✅ success validation
✅ cleanup only on success

---

# Real Risks / Improvements

---

# 1. Spaces in Filenames

Use quotes:

```bash id="im1a2b"
"$BACKUP_DIR"
"$LOG_SOURCE"
```

---

# 2. Empty Source Folder Error

If no logs exist:

```bash id="im3c4d"
cp: cannot stat ...
```

Need checks.

---

# 3. Logging to File

Add:

```bash id="im5e6f"
>> /var/log/backup.log 2>&1
```

---

# 4. Upload to Date Prefix

Better S3 structure:

```bash id="im7g8h"
s3://bucket/logs/$(date +%Y/%m/%d)/
```

---

# 5. Encrypt Archive

Use GPG if sensitive logs.

---

# Cron Automation

Run hourly:

```bash id="cr1a2b"
0 * * * * /home/ec2-user/log_backup.sh
```

---

# Interview Answer

> This script snapshots application logs into a temporary folder, compresses them, uploads the archive to S3 using AWS CLI, and removes local backup files only if upload succeeds.

---

# Enterprise Grade Improvements

Would add:

* retries on upload
* email/slack alert on failure
* checksum validation
* retention cleanup in S3
* incremental backup
* lock file to prevent parallel runs

---
