Role Name
=========

A brief description of the role goes here.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.



amq_datasource:
  id: mysql-ds
  class: org.apache.commons.dbcp2.BasicDataSource
  properties:
    driverClassName: com.mysql.jdbc.Driver
    url: "jdbc:mysql://{{ amq_datasource_host }}:{{ amq_datasource_port }}/{{ amq_datasource_database }}?relaxAutoCommit=true&amp;autoReconnect=true"
    username: "{{ amq_datasource_username }}"
    password: "{{ amq_datasource_password }}"
    poolPreparedStatements: true
    testOnBorrow: true
    testWhileIdle: true
    validationQuery: SELECT 1
    timeBetweenEvictionRunsMillis: 30000


OLD: 

amq_datasource_host:     'localhost'
amq_datasource_port:     3306
amq_datasource_database: 'activemq'
amq_datasource_username: 'amq'
amq_datasource_password: 'topsecret'


Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
