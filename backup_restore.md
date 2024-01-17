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

    1. Establish SSH connection to the host, where you have MySQL in Read/Write (Primary) mode and issue the following command:
    
    sudo -u backup duplicity --no-encryption restore rsync://kovalArt@backup.infocare.io/mysql /home/backup/restore/mysql

    2. After the backup has downloaded - issue this command to use the backup. This action should be done as root user!
        
        1. sudo su

        2. mysql agama < /home/backup/restore/mysql/agama.sql

    3. Check the result. MySQL should now have fresh data from backup and agama database available

# Restore InfluxDB data from the backup:

    1. Establish SSH connection to the host, where you have influxdb (kovalart-3) and issue the following command:

    sudo -u backup duplicity --no-encryption restore rsync://kovalArt@backup.infocare.io/influxdb /home/backup/restore/influxdb

    2. After the backup has downloaded - issue this command to use the backup. This action should be done as root user! Before the restoring from the backup - make sure you stopped the "telegraf" service and dropped the telegraf database in influxdb.  

        1. sudo su 
        2. service telegraf stop
        3. influx -execute 'DROP DATABASE telegraf'
        4. influxd restore -portable -database telegraf /home/backup/restore/influxdb

            (On this step you may face an error "error updating meta: DB metadata not changed. database may already exist restore: DB metadata not changed. database may already exist". It's a known issue with InfluxDB restore, you can ignore these. Just make sure that telegraf database is restored correctly.)

        5. After succesfully restored backup - start the telegraf service by one of these commands:
            - ansible-playbook infra.yaml
            - ansible-playbook infra.yaml -ti 

    3. Check the result. InfluxDB telegraf should now have fresh data from backup and telegraf database and service available
