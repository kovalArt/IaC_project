# Backup SLA Document

## Database (MySQL) Servers

### Backup Coverage
- What is backed up: Database contents
- What is not backed up: System binaries, temporary files, configurations

### RPO (Recovery Point Objective)
- Acceptable data loss: Up to 1 day

### Versioning and Retention
-  Number of Full Backup Versions Stored: 4 (assuming one full backup each Friday for a month).
    
- Number of Incremental Backup Versions Stored: 25 (assuming one incremental backup each day for the remaining  days of the month, excluding Sunday when full backups are done, 29 days in month as for example).

- Retention Period for Full and Incremental Backups: 40 days

### Usability Checks
- "Alpha" Team of Infrastructure Engineers are resposible to periodically check the usability of backups
- Each Monday of a week, team should test backups 
- Periodic restores to a sandbox environment.

### Restoration Criteria
- Database corruption.
- Accidental data deletion.
- Database encryption by ransomware

### RTO (Recovery Time Objective)
- Target recovery time: Within 2 hours.

## InfluxDB

### Backup Coverage
- What is backed up: InfluxDB data 
- What is not backed up: Temporary files, Bind, nginx, agama, haproxy, keepalived

### RPO (Recovery Point Objective)
- Acceptable data loss: Up to 1 day

### Versioning and Retention
-  Number of Full Backup Versions Stored: 4 (assuming one full backup each Friday for a month).
    
- Number of Incremental Backup Versions Stored: 25 (assuming one incremental backup each day for the remaining  days of the month, excluding Sunday when full backups are done, 29 days in month as for example).

- Retention Period for Full and Incremental Backups: 40 days

### Usability Checks
- "Beta" Team of Infrastructure Engineers are resposible to periodically check the usability of backups
- Regular automated backups checks.
- Periodic test restores to a separate instance.
- Periodic test restores to a sandbox environment.

### Restoration Criteria
- Database corruption.
- Accidental data deletion.

### RTO (Recovery Time Objective)
- Target recovery time: Within 2 hours.

## Ansible Repository

### Backup Coverage
- What is backed up: Playbooks, roles, inventory files.
- What is not backed up: Temporary files, build artifacts.

### RPO (Recovery Point Objective)
- Acceptable data loss: Up to 1 day.

### Versioning and Retention
- Number of backup versions stored: 20
- Retention period: 6 months.

### Usability Checks
- Regular automated backup checks.
- Periodic test restores to a separate directory.

### Restoration Criteria
- Critical playbook or role deletion.
- Repository corruption.

### RTO (Recovery Time Objective)
- Target recovery time: Within 2 hours.

---