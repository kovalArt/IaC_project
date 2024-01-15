# Backup SLA Document

## === Database (MySQL) Servers ===

### Backup Coverage
- What is backed up: Database contents (Agama database)
- What is not backed up: System binaries, temporary files, configurations

### RPO (Recovery Point Objective)
- Acceptable data loss: Up to 1 day

### Versioning and Retention
- Number of Full Backup Versions Stored: 3
    
- Number of Incremental Backup Versions Stored: 1

- Retention Period for Full and Incremental Backups: 40 days (On Sunday we have a New Full backup, On Monday we delete old backups)

### Usability Checks
- "Alpha" Team of Infrastructure Engineers are resposible to periodically check the usability of backups
- Each Monday of a week, team should test the backups 
- Periodic restores to a sandbox environment.

### Restoration Criteria
- Database corruption.
- Accidental data deletion.
- Database encryption by ransomware

### RTO (Recovery Time Objective)
- Target recovery time: Within 8 hours.

### When backups are created and deleted

Full backup - each Sunday at 20:30 (8:30 PM) UTC
Incremental backups - from Monday to Saturday at 20:31 (8:31 PM) UTC
Delete old backups (40D) - each Monday at 20:27 (8:27 PM) UTC

## === InfluxDB ===

### Backup Coverage
- What is backed up: InfluxDB data, telegraf database
- What is not backed up: Temporary files, Bind, nginx, agama, haproxy, keepalived

### RPO (Recovery Point Objective)
- Acceptable data loss: Up to 1 day

### Versioning and Retention
- Number of Full Backup Versions Stored: 2
    
- Number of Incremental Backup Versions Stored: 1

- Retention Period for Full and Incremental Backups: 40 days (On Sunday we have a New Full backup, On Monday we delete old backups)

### Usability Checks
- "Beta" Team of Infrastructure Engineers are resposible to periodically check the usability of backups
- Each Monday of a week, team should test the backups 
- Regular backups checks.
- Periodic test restores to a separate instance.
- Periodic test restores to a sandbox environment.

### Restoration Criteria
- Database corruption.
- Accidental data deletion.

### RTO (Recovery Time Objective)
- Target recovery time: Within 8 hours.

Full backup - each Sunday at 20:08 (8:08 PM) UTC
Incremental backups - from Monday to Saturday at 20:09 (8:09 PM) UTC
Delete old backups (40D) - each Monday at 20:30 (8:30 PM) UTC

## === Ansible Repository ===

### Backup Coverage
- What is backed up: Playbooks, roles, inventory files.
- What is not backed up: Temporary files, build artifacts.

### RPO (Recovery Point Objective)
- Acceptable data loss: Up to 2 day.

### Versioning and Retention
- Number of backup versions stored: 40
- Retention period: 6 months.

### Usability Checks
- Regular backup checks.
- Periodic test restores to a separate directory.

### Restoration Criteria
- Critical playbook or role deletion.
- Repository corruption.

### RTO (Recovery Time Objective)
- Target recovery time: Within 8 hours.

---