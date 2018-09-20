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
2. Create or configure tablespaces directories (this is a mandatory before run the playbook).
3. Open firewall port or add firewall services.



## How to

1. Clone <repo>
2. configure hosts (inventory) file
3. Execute playbook
4. Go to http://<your_ip>/zabbix and finish Zabbix installation

### keep in mind



## Pending and completed tasks

- [ ] Add tasks for Debian based distributions.
- [ ] Add tasks for install and configure NTP/Chrony services.
- [ ] Add tasks for deal with SELinux installations.
- [ ] Add tasks for Open firewall ports/services.



