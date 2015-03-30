# ansible-mysql

This ansible task installs and configures the MySQL database server as well as automatic backups, on any Debian server

## Role variables

* ``packages``: List of [packages](vars/main.yml). Override in order to specify specific versions. When overriding, make sure to include all packages in the list.
* ``root_password``: Password for MySQL's ``root`` user. Mandatory.
* ``database_name``: Name of database to create. Mandatory.
* ``database_username``: MySQL username to be given access to the database. Mandatory.
* ``database_password``: The corresponding password. Mandatory.
* ``backup_hour``: Hour of the day when a database backup should be made. Possible values are ``00-23``. Default is ``00``.

## Examples

A playbook that's going to install the latest versions of all packages

    playbook.yml

    ---
    hosts: all
    remote_user: foo
    sudo: yes
    roles:
     - { role: "ansible-mysql", 
         root_password: pass, 
         database_name: db, 
         database_username: user, 
         database_password: password, 
         backup_hour: 23}

A playbook that's going to install specific versions of packages

    playbook.yml

    ---
    hosts:all
    remote_user: foo
    sudo: yes
    roles: 
     - { role: "ansible-mysql", 
         root_password: pass, 
         database_name: db, 
         database_username: user, 
         database_password: password, 
         backup_hour: 23, 
         packages: [mysql-server=5.5.41-0+wheezy1, mysql-client=5.5.41-0+wheezy1, libmysqlclient-dev=5.5.41-0+wheezy1, python-mysqldb=1.2.3-2, automysqlbackup=2.6+debian.3-1]}
    
Invoke playbook

    ansible-playbook playbook.yml

