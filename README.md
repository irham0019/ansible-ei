# WSO2 EI 7.1.0 Ansible scripts

This repository contains the Ansible scripts for installing and configuring WSO2 EI.

## Supported Operating Systems

- CentOS 7

## Supported Ansible Versions

- Ansible 2.9.7

![WSO2 EI 7.1.0 and ActiveMQ 2 deployment architecture ](https://github.com/irham0019/ansible-ei/blob/main/stuller-architecture.jpg)

## Directory Structure
```
.
├── README.md
├── ansible-ei.iml
├── ansible.cfg
├── docs
│   ├── Pattern1.md
│   └── images
│       └── Deployment-pattern-1-diagram.png
├── environments
│   ├── dev
│   │   ├── group_vars
│   │   │   ├── activemq.yml
│   │   │   └── ei.yml
│   │   ├── host_vars
│   │   │   ├── activemq_1.yml
│   │   │   ├── ei_1.yml
│   │   │   └── ei_2.yml
│   │   └── inventory
│   ├── local
│   │   ├── group_vars
│   │   │   ├── activemq.yml
│   │   │   └── ei.yml
│   │   ├── host_vars
│   │   │   ├── activemq_1.yml
│   │   │   ├── ei_1.yml
│   │   │   └── ei_2.yml
│   │   └── inventory
│   ├── prod
│   │   ├── group_vars
│   │   │   ├── activemq.yml
│   │   │   └── ei.yml
│   │   ├── host_vars
│   │   │   ├── activemq_1.yml
│   │   │   ├── ei_1.yml
│   │   │   └── ei_2.yml
│   │   └── inventory
│   └── test
│       ├── group_vars
│       │   ├── activemq.yml
│       │   └── ei.yml
│       ├── host_vars
│       │   ├── ei_1.yml
│       │   └── ei_2.yml
│       └── inventory
├── files
│   ├── carbonapps
│   │   ├── SSAWLEBSCycleCountConfirmationCAR_1.0.0.car
│   │   ├── SSAWLEBSPickConfirmCAR_1.0.0.car
│   │   ├── SSAWLEBSPutAwayConfirmCAR_1.0.0.car
│   │   ├── SSEBSAMZNCreateShipmentCAR_1.0.0.car
│   │   ├── SSEBSAWLCycleCountDownloadCAR_1.0.0.car
│   │   ├── SSEBSAWLDelCycleCntDownloadCAR_1.0.0.car
│   │   ├── SSEBSAWLDeletePutAwayCAR_1.0.0.car
│   │   ├── SSEBSAWLInductionCAR_1.0.0.car
│   │   ├── SSEBSAWLInventoryAdjustmentCAR_1.0.0.car
│   │   ├── SSEBSAWLItemOnHandLocationCAR_1.0.0.car
│   │   ├── SSEBSAWLPartMasterAliasCAR_1.0.0.car
│   │   ├── SSEBSAWLPartMasterCAR_1.0.0.car
│   │   ├── SSEBSAWLPickDOwnloadCAR_1.0.0.car
│   │   ├── SSGVEBSGetItemPriceAPI_CAR_1.0.0.car
│   │   └── StullerSharedResources-car_1.0.0.car
│   ├── db
│   │   └── mysql.sql
│   ├── lib
│   │   ├── TCPDispatchMediator-1.0.0.jar
│   │   ├── activeio-core-3.1.4.jar
│   │   ├── activemq-broker-5.15.14.jar
│   │   ├── activemq-client-5.15.14.jar
│   │   ├── activemq-kahadb-store-5.15.14.jar
│   │   ├── geronimo-j2ee-management_1.1_spec-1.0.1.jar
│   │   ├── geronimo-jms_1.1_spec-1.1.1.jar
│   │   ├── geronimo-jta_1.1_spec-1.1.1.jar
│   │   ├── hawtbuf-1.11.jar
│   │   ├── mysql-connector-java-8.0.22.jar
│   │   ├── ojdbc7.jar
│   │   └── slf4j-api-1.7.30.jar
│   ├── packs
│   │   ├── amazon-corretto-8.282.08.1-linux-x64.tar.gz
│   │   ├── apache-activemq-5.15.14-bin.tar.gz
│   │   └── wso2ei-7.1.0.zip
│   ├── security
│   │   ├── client-truststore.jks
│   │   └── wso2carbon.jks
│   └── system
│       └── etc
│           ├── security
│           │   └── limits.conf
│           └── sysctl.conf
├── issue_template.md
├── pull_request_template.md
├── roles
│   ├── activemq
│   │   ├── handlers
│   │   │   └── main.yml
│   │   ├── tasks
│   │   │   ├── hawtio.yml
│   │   │   └── main.yml
│   │   └── templates
│   │       ├── activemq.j2
│   │       ├── activemq.service.j2
│   │       ├── activemq.xml.j2
│   │       ├── jetty-realm.properties.j2
│   │       ├── jetty.xml.j2
│   │       └── login.config.j2
│   ├── common
│   │   └── tasks
│   │       ├── custom.yml
│   │       └── main.yml
│   ├── ei
│   │   ├── tasks
│   │   │   ├── createdb.yml
│   │   │   ├── custom.yml
│   │   │   └── main.yml
│   │   └── templates
│   │       ├── micro_integrator_dashboard_home
│   │       │   ├── bin
│   │       │   │   └── dashboard.sh.j2
│   │       │   ├── repository
│   │       │   │   └── conf
│   │       │   │       └── deployment.yaml.j2
│   │       │   └── wso2ei-dashboard.service.j2
│   │       └── micro_integrator_home
│   │           ├── bin
│   │           │   └── micro-integrator.sh.j2
│   │           ├── repository
│   │           │   └── conf
│   │           │       └── deployment.toml.j2
│   │           └── wso2ei.service.j2
│   └── start
│       ├── tasks
│       │   └── main.yml
│       └── templates
│           ├── carbon-home
│           │   ├── bin
│           │   │   └── wso2server.sh.j2
│           │   └── repository
│           │       └── conf
│           │           └── deployment.toml.j2
│           └── wso2is.service.j2
├── site.yml
└── stuller-architecture.jpg
```

Packs could be either copied to a local directory, or downloaded from a remote location.

## Packs to be Copied

Copy the following files to `files/packs` directory.

1. [WSO2 EI 7.1.0 package](https://wso2.com/integration/#)
2. [ActiveMQ 5.15.14](https://activemq.apache.org/activemq-5015014-release)
3. [Amazon Coretto for Linux x64 JDK](https://docs.aws.amazon.com/corretto/latest/corretto-8-ug/downloads-list.html)

Copy the following files to `files/lib` directory.

1. [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/5.1.html)
2. Copy the following client libraries from the ACTIVEMQ_HOME/lib directory to the MI_HOME/lib directory.
```
activemq-broker-5.8.0.jar
activemq-client-5.8.0.jar
activemq-kahadb-store-5.8.0.jar
geronimo-jms_1.1_spec-1.1.1.jar
geronimo-j2ee-management_1.1_spec-1.0.1.jar
geronimo-jta_1.0.1B_spec-1.0.1.jar
hawtbuf-1.9.jar
Slf4j-api-1.6.6.jar
activeio-core-3.1.4.jar (available in the ACTIVEMQ_HOME/lib/optional directory)
```

## Downloading from remote location

In **group_vars**, change the values of the following variables in all groups:
1. The value of `pack_location` should be changed from "local" to "remote"

## Running WSO2 EI Ansible scripts

### 1. Run the existing scripts without customization
The existing Ansible scripts contain the configurations to set-up a HA WSO2 EI pattern. In order to deploy the pattern, you need to replace the `[ip_address]` given in the `inventory` file under `dev` folder by the IP of the location where you need to host the EI. An example is given below.
```
[ei]
ei_1 ansible_host=34.121.29.75 ansible_user=user
ei_2 ansible_host=35.202.118.190 ansible_user=user

[activemq]
activemq_1 ansible_host=35.184.193.49 ansible_user=user
```

Run the following command to run the scripts.

`ansible-playbook -i environments/dev site.yml`

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
