# Backup SLA Document

## Database Servers

### Backup Coverage
- What is backed up: Database contents, configuration files.
- What is not backed up: System binaries, temporary files.

### RPO (Recovery Point Objective)
- Acceptable data loss: Up to 1 hour.

### Versioning and Retention
- Number of backup versions stored: 7.
- Retention period: 30 days.

### Usability Checks
- Regular automated integrity checks.
- Periodic test restores to a sandbox environment.

### Restoration Criteria
- Database corruption.
- Accidental data deletion.

### RTO (Recovery Time Objective)
- Target recovery time: Within 4 hours.

## InfluxDB

### Backup Coverage
- What is backed up: InfluxDB data directory, MySQL data
- What is not backed up: Temporary files, Bind, nginx, agama

### RPO (Recovery Point Objective)
- Acceptable data loss: Up to 1 hour.

### Versioning and Retention
- Number of backup versions stored: 0.
- Retention period: 14 days.

### Usability Checks
- Regular automated backups checks.
- Periodic test restores to a separate instance.

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
- Number of backup versions stored: 3.
- Retention period: 7 days.

### Usability Checks
- Regular automated backup checks.
- Periodic test restores to a separate directory.

### Restoration Criteria
- Critical playbook or role deletion.
- Repository corruption.

### RTO (Recovery Time Objective)
- Target recovery time: Within 6 hours.

---