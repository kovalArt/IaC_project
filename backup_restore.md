# This Document Provide Information how to restore Mysql and Influxdb from a backup 

# Install and configure infrastructure with Ansible:

    # All infrustructure: 
    ansible-playbook infra.yaml

    # MySQL and Inflxdb parts of infrustructure:
    ansible-playbook infra.yaml -tdb -ti -ta

    # Explanations:
    -tdb - setting up MySQL
    -ti - setting up Influxdb
    -ta - setting up Agama application (will pickup changes from MySQL)


# Restore MySQL data from the backup:

    1. Establish SSH connection to the host, where you have MySQL in Read/Write mode and issue the following command:
    
    sudo -u backup duplicity --no-encryption restore rsync://kovalArt@backup.infocare.io/mysql /home/backup/restore/mysql

    2. After the backup has downloaded - issue this command to use the backup. This action should be done as root user!

    mysql agama < /home/backup/restore/mysql/agama.sql

    3. Check the result. MySQL should now have fresh data from backup 

# Restore InfluxDB data from the backup:

    1. Establish SSH connection to the host, where you have influxdb and issue the following command:

    sudo -u backup duplicity --no-encryption restore rsync://kovalArt@backup.infocare.io/influxdb /home/backup/restore/influxdb

    2. After the backup has downloaded - issue this command to use the backup. This action should be done as root user!

    influxd restore -portable -database telegraf /home/backup/restore/influxdb

    3. Check the result. InfluxDB should now have fresh data from backup 
