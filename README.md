# WSO2 Identity Server Ansible scripts

This repository contains the Ansible scripts for installing and configuring WSO2 EI.

## Supported Operating Systems

- Ubuntu 16.04 or higher
- CentOS 7

## Supported Ansible Versions

- Ansible 2.6.2

## Directory Structure
```
.
├── README.md
├── ansible-is.iml
├── dev
│   ├── group_vars
│   │   ├── ei-migration.yml
│   │   └── ei.yml
│   ├── host_vars
│   │   └── ei_1.yml
│   └── inventory
├── docs
│   ├── Pattern1.md
│   ├── Pattern2.md
│   └── images
│       ├── Deployment-pattern-1-diagram.png
│       └── Deployment-pattern-2-diagram.png
├── files
│   ├── lib
│   │   ├── amazon-corretto-8.242.08.1-linux-x64.tar.gz
│   │   └── mysql-connector-java-5.1.48-bin.jar
│   ├── migration-scripts
│   │   ├── migration-resources.zip
│   │   └── org.wso2.carbon.ei.migration-1.0.101.jar
│   ├── packs
│   │   └── wso2ei-5.9.0.zip
│   ├── security
│   │   ├── client-truststore.jks
│   │   └── wso2carbon.jks
│   ├── security-old
│   │   └── wso2carbon-old.jks
│   ├── system
│   │   └── etc
│   │       ├── security
│   │       │   └── limits.conf
│   │       └── sysctl.conf
│   └── tenants
│       └── tenants.zip
├── issue_template.md
├── pull_request_template.md
├── roles
│   ├── common
│   │   └── tasks
│   │       ├── custom.yml
│   │       └── main.yml
│   ├── ei
│   │   ├── tasks
│   │   │   ├── custom.yml
│   │   │   └── main.yml
│   │   └── templates
│   │       ├── carbon-home
│   │       │   ├── bin
│   │       │   │   └── wso2server.sh.j2
│   │       │   └── repository
│   │       │       ├── conf
│   │       │       │   ├── deployment.toml.j2
│   │       └── wso2ei.service.j2
│   └── ei-migration
│       └── tasks
│           ├── custom.yml
│           └── main.yml
├── scripts
│   ├── update.sh
│   └── update_README.md
└── site.yml
```

Packs could be either copied to a local directory, or downloaded from a remote location.

## Packs to be Copied

Copy the following files to `files/packs` directory.

1. [WSO2 Identity Server 5.9.0 package](https://wso2.com/identity-and-access-management/install)
Copy the following files to `files/lib` directory.

1. [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/5.1.html)
2. [Amazon Coretto for Linux x64 JDK](https://docs.aws.amazon.com/corretto/latest/corretto-8-ug/downloads-list.html)

## Downloading from remote location

In **group_vars**, change the values of the following variables in all groups:
1. The value of `pack_location` should be changed from "local" to "remote"
2. The value of `remote_jdk` should be changed to the URL in which the JDK should be downloaded from, and remove it as a comment.
3. The value of `remote_pack` should be changed to the URL in which the package should be downloaded from, and remove it as a comment.

## Running WSO2 Identity Server Ansible scripts

### 1. Run the existing scripts without customization
The existing Ansible scripts contain the configurations to set-up a single node WSO2 Identity Server pattern. In order to deploy the pattern, you need to replace the `[ip_address]` given in the `inventory` file under `dev` folder by the IP of the location where you need to host the Identity Server. An example is given below.
```
[ei]
wso2ei ansible_host=172.28.128.4
```

Run the following command to run the scripts.

`ansible-playbook -i dev site.yml`

If you need to alter the configurations given, please change the parameterized values in the yaml files under `group_vars` and `host_vars`.

### 2. Customize the WSO2 Ansible scripts

The templates that are used by the Ansible scripts are in j2 format in-order to enable parameterization.

The `axis2.xml.j2` file is added under `roles/wso2ei/templates/carbon-home/repositoy/conf/axis2/`, in order to enable customizations. You can add any other customizations to `custom.yml` under tasks of each role as well.

#### Step 1
Uncomment the following line in `main.yml` under the role you want to customize.
```
- import_tasks: custom.yml
```

#### Step 2
Add the configurations to the `custom.yml`. A sample is given below.

```
- name: "Copy custom file"
  template:
    src: path/to/example/file/example.xml.j2
    dest: destination/example.xml.j2
  when: "(inventory_hostname in groups['ei'])"
```

Follow the steps mentioned under `docs` directory to customize/create new Ansible scripts and deploy the recommended patterns.

## Performance Tuning

System configurations can be changed through Ansible to optimize OS level performance. Performance tuning can be enabled by changing `enable_performance_tuning` in `dev/group_vars/ei.yml` to `true`.

System files that will be updated when performance tuning are enabled is available in `files/system`. Update the configuration values according to the requirements of your deployment.
