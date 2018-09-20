# Ansible playbook for zabbix-partition-tables project

## Description

This simple playbook is aimed to automate the process of creating partition tables using [this scripts](https://github.com/jorgesanchez-e/zabbix-partition-tables), after all tasks done you only have to point your browser to http://<Your_Ip>/zabbix/ and complet the installation.



## What this playbook does?

The playbook does all needed tasks to install Zabbix project within partitioned PostgreSQL database and that involves things like install install packages, download scripts and modify configuration files, a detailed list of tasks could by as follow:

1. Deactivate SELinux.
2. Install PostgreSQL yum repo (version 9.3, 9.4, 9.5 or 10).
3. Install Zabbix yum repo (version 3.2 or 3.4).
4. Install Zabbix repo keys.
5. Install all needed packages from yum repositories.
6. Install Perl module dependencies.
7. Initialize PostgreSQL cluster directory
8. Configure postgresql.conf and pg_hba.conf files.
9. Start PostgreSQL service.
10. Create Zabbix database and Zabbix user.
11. Create partition tables for Zabbix data and zabbix indexes.
12. Create/modify all scripts to get ready PostgreSQL with partition tables
13. Configure and start Zabbix server service.
14. Configure and start Zabbix client.
15. Configure and start Zabbix web portal service.



## What this playbook doesn't do?

This script won't do following tasks:

1. Install and configure NTP or Chrony service or timezones (you have to have this service configured before).
2. Create or configure tablespace directories (this is a mandatory before run the playbook).
3. Open firewall port or add firewall services.



## How to

1. Clone repo:

   ```shell
   git clone https://github.com/jorgesanchez-e/ansible-zabbix-partition-tables
   ```

2. configure hosts (inventory) file.

   ```shell
   [db_servers]
   192.168.100.10
   
   [zabbix_servers]
   192.168.100.10
   ```

   For this example we will use same server for both hosts, Database host and Zabbix web portal host

3. Execute playbook

   ```shell
   ansible-playbook -i hosts install.yml --extra-vars='postgres_ip=192.168.100.10 pgsql_data_tb=/postgresql/zabbix/data pgsql_index_tb=/postgresql/zabbix/index'
   ```

   We can control playbook behavior using extra-vars parameter, valid variable names and values are:

   - **postgres_ip**: set ip where PostgreSQL engine will listen to, default is 127.0.0.1.
   - __postgres_port__: set ip port where PostgreSQL engine will listen to, default is 5431 __*NOT* 5432__ this because if you plan to have lot of monitored systems you have to configure a proxy for PostgreSQL connections like pgbouncer.
   - **postgres_sql_version**: Set version for PostgreSQL engine, valid values are 10, 9.6, 9.5, 9.4 and 9.3, default value is 9.5.
   - **zabbix_version**: Set version for Zabbix software, valid values are 3,2 and 3.4, default is 3.2.
   - **pgsql_data_tb**: Set tablespace directory for data, default is /postgresql/zabbix/data.
   - **pgsql_index_tb**: Set tablespace directory for indexes, default is /postgresql/zabbix/index.



   Following and example of how ansible looks like executing this playbook, be patient when it install packages it takes a time.



   ![asciicast](https://asciinema.org/a/hGsJt9MJIdlTHJHsrE7OiVXQu.png)

4. Go to **http://<your_ip>/zabbix** and finish Zabbix installation

   - When you reach **"Configure DB connection"** steep ensure you that you put same ip in **"Database host"** field that you put with **postgres_ip** ansible var and same port in **"Database port"** field than **postgres_port** ansible var, if you didn't set it you have to put **5431**



### keep in mind

__postgres_ip__ variable has to be a database host ip because it will be used to config __postgresql.conf__ file and __pg_hba.conf__ file, ansible will try to parse that ip and use network part to put it into __pg_hba.conf__ file, then you have to keep the host for Zabbix server inside same network, furthermore that IP has to be configured into database host 



## Pending and future completed tasks

### May be it will be never implemented

- [ ] Add tasks for Debian based distributions.
- [ ] Add tasks for install and configure NTP/Chrony services.
- [ ] Add tasks for install and configure pgbouncer.
- [ ] Add tasks for deal with SELinux installations.
- [ ] Add tasks for Open firewall ports/services.



