# Ansible deployment for JIRA

Based on https://github.com/fauzigo/ansible-jira

Role jira
=========

Role to deploy Jira on RedHat 7.0 linux servers.


Requirements
------------

Ansible 2.2 must be installed in the host where the playbook will be executed.


Recommended install Ansible via pip (http://docs.ansible.com/ansible/intro_installation.html#latest-releases-via-pip)

Role Variables
--------------

- **jira_user_group**: Unix group for user which execute Jira service.
- **jira_user**: Unix user which execute Jira service.
- **jira_user_home_dir**: Top level directory where jira will be installed.
- **jira_home**: Jira home directory, Jira will set its workspace in this directory.
- **jira_download_link**: Link to download the .tar.gz file.
- **jira_version**: Jira version to install.
- **jira_version_file_sha256sum**: SHA 256 hash to validate the donwloaded file.
- **set_db**: If set to true will configure Jira for use an existent database
- **jira_db_host**: Database hostname or IP address
- **jira_db_name**: Jira database name
- **jira_db_user**: Jira database user name
- **jira_db_password**: Jira database password

Dependencies
------------

- overdrive3000.java8

Example Playbook
----------------

main.yml playbook
```
    - hosts: localhost
      become: true
      vars_files:
        - vars/variables.yml
      roles:
         - overdrive3000.java
         - overdrive3000.jira
```

vars/variables.yml file for a brand new jira installation
```
jira_user_group: jira
jira_user: jira
jira_user_home_dir: "/opt"
jira_home: "/var/jira"
jira_download_link: "http://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-software"
jira_version: "7.2.4"
jira_version_file_sha256sum: 0a57714dc5cf8d136a5ecf9156c6875f5547ce6c2b7aac9acc94695ea2d4b529
```

vars/variables.yml file for installing jira using an existent database
```
jira_user_group: jira
jira_user: jira
jira_user_home_dir: "/opt"
jira_home: "/var/jira"
jira_download_link: "http://www.atlassian.com/software/jira/downloads/binary"
jira_filename: "atlassian-jira-software"
jira_extracted: "{{ jira_filename }}" 
jira_version: "7.2.4"
jira_version_file_sha256sum: 0a57714dc5cf8d136a5ecf9156c6875f5547ce6c2b7aac9acc94695ea2d4b529

# database variables
set_db: true
jira_db_host: localhost
jira_db_name: jiradb
jira_db_user: jira
jira_db_password: verylongsecurepassword
```

License
-------

BSD

Author Information
------------------

Juan Mesa - linuxven@gmail.com
