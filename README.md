# ica0002
Repo for the university course - IT Infrastructure Services

The main objectice is to create the IaaC project, that would deploy a secure and sustainable infrastructure by using a one command (ansible-playbook infra.yaml). 

### Infrastructure deployed:

##### 2 client side machines:
- 3 docker containers per machine with application (agama)
- 1 mysql per machine (with a functionality of replication (1 master - 1 slave))
- 1 haproxy per machine
- 1 keepalived per machine
- docker
- dns (slave) per machine 

##### Server side machine: 
- nginx (with reverse proxying) 
- influxdb
- grafana (in container)
- docker
- dns (primary)
- prometheus
- pinger (latency measurments)

### How does it work 
##### Overall info
The whole infrastructure is deployed through the Ansible Repo and establishing connection through SSH. To succesfully pass the course - it was needed to create the high-available and secure infra, that would be used by imaginatory small startup and their application. 

##### Deep dive 
There were 3 machines - two for client services and one for internal services. Every piece of infra is monitored by Grafana with a source of Prometheus and InfluxDB. To keep startup application available all time - we used Keepalived and Haproxy, that allowed to serve application 24/7. The appliction is served in docker containers that significantly helped with availability. For high availablity we also used MySQL replication that allowed not to loose data in case of MySQL corruption, change the master mysql host by one variable and backup all data from Slave host to backup host. 

##### Backups (InfluxDB and MySQL) 
Backups were made each day from Monday-Saturday (incremental) and Full Backup on Sunday. Retention period 40 days. 

:)
