# Ansible Role: MySQL

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-mysql.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-mysql)

Installs and configures MySQL or MariaDB server on RHEL/CentOS or Debian/Ubuntu servers.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `vars/main.yml`):

    mysql_user_home: /root

The home directory inside which Python MySQL settings will be stored, which Ansible will use when connecting to MySQL. This should be the home directory of the user which runs this Ansible role.

    mysql_root_password: root

The MySQL root user account password.

    mysql_root_password_update: no

Whether to force update the MySQL root user's password. By default, this role will only change the root user's password when MySQL is first configured. You can force an update by setting this to `yes`.

    mysql_enabled_on_startup: yes

Whether MySQL should be enabled on startup.

    overwrite_global_mycnf: yes

Whether the global my.cnf should be overwritten each time this role is run. Setting this to `no` tells Ansible to only create the `my.cnf` file if it doesn't exist. This should be left at its default value (`yes`) if you'd like to use this role's variables to configure MySQL.

    mysql_config_include_files: []

A list of files that should override the default global my.cnf. Each item in the array requires a "src" parameter which is a path to a file. An optional "force" parameter can force the file to be updated each time ansible runs.

    mysql_databases: []

The MySQL databases to create. A database has the values `name`, `encoding` (defaults to `utf8`), `collation` (defaults to `utf8_general_ci`)). The formats of these are the same as in the `mysql_db` module.

    mysql_users: []

The MySQL users and their privileges. A user has the values `name`, `host` (defaults to `localhost`), `password`, `priv` (defaults to `*.*:USAGE`), and `append_privs` (defaults to `no`). The formats of these are the same as in the `mysql_user` module.

    mysql_packages:
      - mysql
      - mysql-server

(OS-specific, RedHat/CentOS defaults listed here) Packages to be installed. In some situations, you may need to add additional packages, like `mysql-devel`.

    mysql_enablerepo: ""

(RedHat/CentOS only) If you have enabled any additional repositories (might I suggest geerlingguy.repo-epel or geerlingguy.repo-remi), those repositories can be listed under this variable (e.g. `remi,epel`). This can be handy, as an example, if you want to install later versions of MySQL.

    mysql_port: "3306"
    mysql_bind_address: '0.0.0.0'
    mysql_datadir: /var/lib/mysql

Slow query log settings. Note that the log file will be created by this role, but if you're running on a server with SELinux or AppArmor, you may need to add this path to the allowed paths for MySQL, or disable the mysql profile. For example, on Debian/Ubuntu, you can run `sudo ln -s /etc/apparmor.d/usr.sbin.mysqld /etc/apparmor.d/disable/usr.sbin.mysqld && sudo service apparmor restart`.

    mysql_key_buffer_size: "256M"
    mysql_max_allowed_packet: "64M"
    mysql_table_open_cache: "256"
    [...]

The rest of the settings in `defaults/main.yml` control MySQL's memory usage. The default values are tuned for a server where MySQL can consume ~512 MB RAM, so you should consider adjusting them to suit your particular server better.

    mysql_server_id: "1"

## Dependencies

None.

## Example Playbook

    - hosts: db-servers
      vars_files:
        - vars/main.yml
      roles:
        - { role: geerlingguy.mysql }

*Inside `vars/main.yml`*:

    mysql_root_password: super-secure-password
    mysql_databases:
      - name: example_db
        encoding: latin1
        collation: latin1_general_ci
    mysql_users:
      - name: example_user
        host: "%"
        password: similarly-secure-password
        priv: "example_db.*:ALL"

## License

MIT / BSD

## Author Information

This role was created in 2014 by [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/).
