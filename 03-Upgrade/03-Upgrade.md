# Upgrades
 You can check the current version using the API command:

```bash
# curl -u $USER:$PASSWORD -X GET http://localhost:9200/_logserver/license
```

## Upgrade from version 7.6.0

### Preferred Upgrade steps

1. Run upgrade script:
   - ./install.sh -u

#### Required post upgrade from version 7.6.0

**Breaking and major changes**

- Archive: Changed the default archives location to `/usr/share/kibana/data/archive/archives/` - please adjust external storage resource to this path [if used]. To customize the `archive.archivefolderpath` directive edit the `/etc/logserver-gui/kibana.yml` file and restart the kibana service.

- Network-Probe: Move required directives from `/opt/license-service/license-service.conf` to `/opt/license-service/license-service.conf.rpmnew` and replace `license-service.conf` then restart the license-service.

- User "logserver" will no longer be able to log into GUI. Use "admin" user instead. Update process will print generated password for this new user.

    In case you have missed it you can run the following command on your main client node to recover the password:
    \# /usr/share/elasticsearch/utils/logserver-password-util.sh get_password -u admin -q


## Upgrade from version 7.5.0

### Preferred Upgrade steps

1. Run upgrade script:
```bash
# ./install.sh -u
```

#### Required post upgrade from version 7.5.0

**Breaking and major changes**

- User "logserver" will no longer be able to log into GUI. Use "admin" user instead. Update process will print generated password for this new user.
  In case you have missed it you can run the following command on your main client node to recover the password:
```bash
# /usr/share/elasticsearch/utils/logserver-password-util.sh get_password -u admin -q
```


## Upgrade from version 7.4.3

### Preferred Upgrade steps

1. Run upgrade script:
   - ./install.sh -u

#### Required post upgrade from version 7.4.3

**Breaking and major changes**

- Network-Probe replaces Logstash: follow the steps below.

**LOGSTASH:**

- Backup `/etc/logstash`
- Uninstall old version: `# yum versionlock delete logstash-oss-7.17.11-1 && yum remove logstash-oss && rm -rf /etc/logstash /var/lib/logstash /usr/share/logstash`
- Install current Input Layer from fresh `# ./install.sh -i` - Network-Probe Section
- Restore from backup custom pipelines to `/etc/logstash/conf.d`

**ELASTICSEARCH**

- `./install.sh` checks indexes compatibility before upgrading, if any problem exist please contact product support to guide you through the upgrade process.
- Move required directives from `/etc/elasticsearch/elasticsearch.yml` to `/etc/elasticsearch/elasticsearch.yml.rpmnew` and replace `elasticsearch.yml`.

**KIBANA**

- Move required directives from `/etc/kibana/kibana.yml` to `/etc/kibana/kibana.yml.rpmnew` and replace `kibana.yml`.
- Clear browser cache on client side.

**LICENSE-SERVICE**

- If required, configure `elasticsearch_connection` in `/opt/license-service/license-service.conf`.
- Old configuration should be in `/opt/license-service/license-service.conf.rpmsave`. Do not replace `license-service.conf` with `license-service.conf.rpmsave`

**EMPOWERED-AI**

- Backup `.intelligence_models`, `.intelligence_rule_configuration` indices - if needed
- Stop services: `# systemctl stop intelligence intelligence-scheduler`
- Delete old indices: `# curl -XDELETE '127.0.0.1:9200/.intelligence_rule_configuration,.intelligence_models,.intelligence_results' -u logserver`
- Start services: `# systemctl start intelligence intelligence-scheduler`


## Upgrade from version 7.4.2

### Preferred Upgrade steps

1. Run upgrade script:
   - ./install.sh -u

#### Required post upgrade from version 7.4.2

**Breaking and major changes**

- Network-Probe replaces Logstash: follow the steps below.

**LOGSTASH:**

- Backup `/etc/logstash`
- Uninstall old version: `# yum versionlock delete logstash-oss-7.17.11-1 && yum remove logstash-oss && rm -rf /etc/logstash /var/lib/logstash /usr/share/logstash`
- Install current Input Layer from fresh `./install.sh -i` - Network-Probe Section.
- Restore from backup custom pipelines to `/etc/logstash/conf.d`

**ELASTICSEARCH**

- `./install.sh` checks indexes compatibility before upgrading, if any problem exist please contact product support to guide you through the upgrade process.
- Move required directives from `/etc/elasticsearch/elasticsearch.yml` to `/etc/elasticsearch/elasticsearch.yml.rpmnew` and replace `elasticsearch.yml`.

**KIBANA**

- Move required directives from `/etc/kibana/kibana.yml` to `/etc/kibana/kibana.yml.rpmnew` and replace `kibana.yml`.
- Clear browser cache on client side.

**LICENSE-SERVICE**

- If required, configure `elasticsearch_connection` in `/opt/license-service/license-service.conf`.
- Old configuration should be in `/opt/license-service/license-service.conf.rpmsave`. Do not replace `license-service.conf` with `license-service.conf.rpmsave`

## Upgrade from version 7.4.1

### Preferred Upgrade steps

1. Run upgrade script:
   - ./install.sh -u

## Upgrade from version 7.4.0

### Preferred Upgrade steps

1. Run upgrade script:
   - ./install.sh -u

## Upgrade from version 7.3.0

### **Breaking and major changes**

- Complete database redefinition
- Complete user interface redefinition
- Complete SIEM Engine redefinition
- Input layer uses Logstash-OSS 7.17.11
- Support for Beats-OSS Agents => 7.17.11

### Preferred Upgrade steps

1. Run upgrade script:
   - ./install.sh -u

### Required post upgrade from version 7.3.0

**ELASTICSEARCH**

- `./install.sh` checks indexes compatibility before upgrading, if any problem exist please contact product support to guide you through the upgrade process.
- Move required directives from `/etc/elasticsearch/elasticsearch.yml` to `/etc/elasticsearch/elasticsearch.yml.rpmnew` and replace `elasticsearch.yml`.
- Move required directives from `/etc/sysconfig/elasticsearch` to `/etc/sysconfig/elasticsearch.rpmnew` and replace `/etc/sysconfig/elasticsearch`.
- Elasticsearch keystore must be recreated if it is used.

**KIBANA**

- Move required directives from `/etc/kibana/kibana.yml` to `/etc/kibana/kibana.yml.rpmnew` and replace `kibana.yml`.
- Clear browser cache on client side.
- Kibana keystore must be recreated if it is used.

**SIEM ENGINE**

- Update automatically migrates connected agents [manager-site].
- Connected agents can be updated at any time [client-site].
- Move required directives from `/usr/share/kibana/plugins/wazuh/wazuh.yml.rpmsave` to `/usr/share/kibana/data/wazuh/config/wazuh.yml`.

**LOGSTASH:**

- No need to upgrade, if interested then:
  - Backup `/etc/logstash`
  - Uninstall old version: `# yum versionlock delete logstash-oss-7.17.11-1 && yum remove logstash-oss && rm -rf /etc/logstash /var/lib/logstash /usr/share/logstash`
  - Install from fresh `./install.sh -i` - logstash section.

- After updating logstash change in `/etc/logstash/conf.d/*`:
  - `input-elasticsearch` => `input-logserver`
  - `filter-elasticsearch` => `filter-logserver`
  - `output-elasticsearch` => `output-logserver`

**TRANSLATIONS**

- Move `/usr/share/kibana/.i18nrc.json` to `/usr/share/kibana/translations/`.

## Upgrade from version 7.2.0

### Preferred Upgrade steps

1. Run upgrade script:
   - ./install.sh -u

### Required post upgrade

- Recreate bundles/cache: ```rm -rf /usr/share/kibana/optimize/bundles/* && systemctl restart kibana```

## Upgrade from version 7.1.3

### **Breaking and major changes**

- Wiki portal renamed to E-Doc

### Preferred Upgrade steps

1. Run upgrade script:
   - ./install.sh -u

### Required post upgrade

- Recreate bundles/cache: ```rm -rf /usr/share/kibana/optimize/bundles/* && systemctl restart kibana```

### Required post upgrade from version 7.1.3

In this version, the name "wiki" has been replace by "e-doc".
Due to this change user have to check if there are differences in config.yml and database.sqlite files.
If the user made his own changes to one of these files before update after the update, the files with .rpmsave extension
will appear in the /opt/wiki folder.

1. In case there is config.yml.rpmsave file in /opt/wiki directory, follow the steps below:
   - Rename config.yml to config.yml.new: # mv /opt/e-doc/config.yml /opt/e-doc/config.yml.new
   - Move config.yml.rpmsave to e-doc directory: # mv /opt/wiki/config.yml.rpmsave /opt/e-doc/config.yml
   - Compare files config.yml/config.yml.new and apply changes from config.yml.new to config.yml:
      a. new default path to db storage: "/opt/e-doc/database.sqlite"
      b. new default kibanaCredentials: "e-doc:e-doc"
2. In case there is database.sqlite.rpmsave file in /opt/wiki directory, follow the steps below:
   - Stop kibana service: # systemctl stop kibana
   - Stop e-doc service: # systemctl stop e-doc
   - Replace database file: # mv /opt/wiki/database.sqlite.rpmsave /opt/e-doc/database.sqlite
   - Change permissions to the e-doc: # chown e-doc:e-doc /opt/e-doc/database.sqlite
   - Start e-doc service: # systemctl start e-doc
   - Start kibana service: # systemctl start kibana

## Upgrade from version 7.1.0

### Preferred Upgrade steps

Run upgrade script:

   ```bash
   ./install.sh -u
   ```

### Required post upgrade

- (SIEM only) Update user in license-service to `license`,
- Update logtrail pipeline in Logstash configuration,
- Migrate logtrail-* indices to new format (the next call will display the current status of the task):

   ```bash
   for index in logtrail-kibana logtrail-alert logtrail-elasticsearch logtrail-logstash; do curl -XPOST "127.0.0.1:9200/_logserver/prepareindex/$index" -u logserver;done
   ```

## Upgrade from version 7.0.6

### **Breaking and major changes**

- During the update, the "kibana" role will be removed and replaced by "gui-access", "gui-objects", "report". The three will automatically be assigned to all users that prior had the "kibana" role. If you had a custom role that allowed users to log in to the GUI this WILL STOP WORKING and you will have to manually enable the access for users.
- The above is also true for LDAP users. If role mapping has been set for role kibana this will have to be manually updated to "gui-access" and if required "gui-objects" and "report" roles.
- If any changes have been made to the "kibana" role paths, those will be moved to "gui-objects". GUI objects permissions also will be moved to "gui-objects" for "gui-access" cannot be used as a default role.
- The "gui-access" is a read-only role and cannot be modified. By default, it will allow users to access all GUI apps; to constrain user access, assign user a role with limited apps permissions.
- "small_backup.sh" script changed name to "configuration-backup.sh" - this might break existing cron jobs
- SIEM plan is now a separate add-on package (requires an additional license)
- Network-Probe is now a separate add-on package (requires an additional license)
- (SIEM) Verify rpmsave files for alert and restore them if needed for following:
  - /opt/alert/config.yaml
  - /opt/alert/op5_auth_file.yml
  - /opt/alert/smtp_auth_file.yml

### Preferred Upgrade steps

1. Run upgrade script:
   - ./install.sh -u

#### Required post upgrade

- Full restart of the cluster is necessary when upgrading from 7.0.6 or below.
- Role "wiki" has to be modified to contain only path: ".wiki" and all methods,
- Configure the License Service according to the *Configuration* section.

## Upgrade from version 7.0.5

### General note

1. Indices *.agents, audit, alert* indices currently uses rollover for rotation, after upgrade please use dedicated API for migration:

```bash
curl -u $USER:$PASSWORD -X POST http://localhost:9200/_logserver/prepareindex/$indexname
```

1. Wiki plugin require open port *tcp/5603*

1. Update alert role to include index-paths: *".alert", "alert_status", "alert_error", ".alertrules_", ".risks", ".riskcategories", ".playbooks"*

### Preferred Upgrade steps

1. Run upgrade script:

   ```bash
   ./install.sh -u
   ```

2. Restart services:

   ```bash
   systemctl restart elasticsearch alert kibana cerebro wiki
   ```

3. Migrate Audit index to new format (the next call will display the current status of the task):

   ```bash
   curl -XPOST '127.0.0.1:9200/_logserver/prepareindex/audit' -u logserver
   ```

4. Migrate Alert index to new format (the next call will display the current status of the task):

   ```bash
   curl -XPOST '127.0.0.1:9200/_logserver/prepareindex/alert' -u logserver
   ```

5. Migrate Agents index to new format (the next call will display the current status of the task):

   ```bash
   curl -XPOST '127.0.0.1:9200/_logserver/prepareindex/.agents' -u logserver
   ```

6. Open tcp/5603 port for wiki plugin:

   ```bash
   firewall-cmd --zone=public --add-port=5603/tcp --permanent
   firewall-cmd --reload
   ```

### Alternative Upgrade steps (without install.sh script)

1. Stop services:

   ```bash
   systemctl stop elasticsearch alert kibana cerebro
   ```

2. Upgrade client-node (includes alert engine):

   ```bash
   yum update ./itrs-log-analytics-client-node-7.0.6-1.el7.x86_64.rpm
   ```

3. Upgrade data-node:

   ```bash
   yum update ./itrs-log-analytics-data-node-7.0.6-1.el7.x86_64.rpm
   ```

4. Start services:

   ```bash
   systemctl start elasticsearch alert kibana cerebro wiki 
   ```

5. Migrate Audit index to new format (the next call will display the current status of the task):

   ```bash
   curl -XPOST '127.0.0.1:9200/_logserver/prepareindex/audit' -u logserver
   ```

6. Migrate Alert index to new format (the next call will display the current status of the task):

   ```bash
   curl -XPOST '127.0.0.1:9200/_logserver/prepareindex/alert' -u logserver
   ```

7. Migrate Agents index to new format (the next call will display the current status of the task):

   ```bash
   curl -XPOST '127.0.0.1:9200/_logserver/prepareindex/.agents' -u logserver
   ```

8. Open tcp/5603 port for wiki plugin:

   ```bash
   firewall-cmd --zone=public --add-port=5603/tcp --permanent
   firewall-cmd --reload
   ```

## Upgrade from version 7.0.4

### General note

1. The following indices `.agents`, `audit`, `alert` currently uses rollover for rotation, after upgrade please use dedicated AIP for migration:

   ```bash
   curl -u $USER:$PASSWORD -X POST http://localhost:9200/_logserver/prepareindex/$indexname
   ```

2. The Wiki plugin require open port `tcp/5603`

### Preferred Upgrade steps

1. Run upgrade script:

   ```bash
   ./install.sh -u
   ```

2. Restart services:

   ```bash
    systemctl restart elasticsearch alert kibana cerebro wiki
   ```

3. Migrate Audit index to new format (the next call will display the current status of the task):

   ```bash
   curl -X POST 'http://localhost:9200/_logserver/prepareindex/audit' -u $USER:$PASSWORD
   ```

4. Migrate Alert index to new format (the next call will display the current status of the task):

   ```bash
   curl -XPOST 'http://localhost:9200/_logserver/prepareindex/alert' -u $USER:$PASSWORD
   ```

5. Migrate Agents index to new format (the next call will display the current status of the task):

   ```bash
    curl -XPOST 'http://localhost:9200/_logserver/prepareindex/.agents' -u $USER:$PASSWORD
   ```

6. Open `tcp/5603` port for Wikipedia plugin:

   ```bash
   firewall-cmd --zone=public --add-port=5603/tcp --permanent
   ```

   ```bash
   firewall-cmd --reload
   ```

### Alternative Upgrade steps (without install.sh script)

1. Stop services:

   ```bash
   systemctl stop elasticsearch alert kibana cerebro
   ```

2. Upgrade client-node (includes alert engine):

   ```bash
   yum update ./itrs-log-analytics-client-node-7.0.5-1.el7.x86_64.rpm
   ```

3. Upgrade data-node:

   ```bash
   yum update ./itrs-log-analytics-data-node-7.0.5-1.el7.x86_64.rpm
   ```

4. Start services:

   ```bash
   systemctl start elasticsearch alert kibana cerebro wiki
   ```

5. Migrate Audit index to new format (the next call will display the current status of the task):

   ```bash
   curl -XPOST 'http://localhost:9200/_logserver/prepareindex/audit' -u $USER:$PASSWORD
   ```

6. Migrate Alert index to new format (the next call will display the current status of the task):

   ```bash
   curl -XPOST 'http://localhost:9200/_logserver/prepareindex/alert' -u $USER:$PASSWORD
   ```

7. Migrate Agents index to new format (the next call will display the current status of the task):

   ```bash
   curl -XPOST 'http://localhost:9200/_logserver/prepareindex/.agents' -u $USER:$PASSWORD
   ```

8. Open `tcp/5603` port for Wikipedia plugin:

   ```bash
   firewall-cmd --zone=public --add-port=5603/tcp --permanent
   ```

   ```bash
   firewall-cmd --reload
   ```

## Upgrade from version 7.0.3

### General note

1. Indicators of compromise (IOCs auto-update) require access to the software provider's servers.

2. GeoIP Databases (auto-update) require access to the software provider's servers.

3. Archive plugin require `ztsd` package to work:

   ```bash
   yum install zstd
   ```

### Upgrade steps

1. Stop services

   ```bash
   systemctl stop elasticsearch alert kibana cerebro
   ```

2. Upgrade client-node (includes alert engine):

   ```bash
   yum update ./itrs-log-analytics-client-node-7.0.4-1.el7.x86_64.rpm
   ```

3. Upgrade data-node:

   ```bash
   yum update ./itrs-log-analytics-data-node-7.0.4-1.el7.x86_64.rpm
   ```

4. Start services:

   ```bash
   systemctl start elasticsearch alert kibana cerebro
   ```

## Upgrade from version 7.0.2

### General note

- Update the `kibana` role to include index-pattern `.kibana*`
- Update the `alert` role to include index-pattern `.alertrules*` and `alert_status*`
- Install `python36` which is required for the Alerting engine on client-node:

    ```bash
    yum install python3
    ```

- AD users should move their saved objects  from the `adrole`.
- Indicators of compromise (IOCs auto-update) require access to the software provider's servers.
- GeoIP Databases (auto-update) require access to the software provider's servers.

### Upgrade steps

- Stop services

    ```bash
    systemctl stop elasticsearch alert kibana
    ```

- Upgrade client-node (includes alert engine)

    ```bash
    yum update ./itrs-log-analytics-client-node-7.0.3-1.el7.x86_64.rpm
    ```

- Login in the GUI ITRS Log Analytics and go to the `Alert List`  on the `Alerts` tab and click `SAVE` button

    ![](/media/media/image143.png)

- Start  `alert` and `kibana` service

    ```bash
    systemctl start alert kibana
    ```

- Upgrade data-node

    ```bash
    yum update ./itrs-log-analytics-data-node-7.0.3-1.el7.x86_64.rpm
    ```

- Start services

    ```bash
    systemctl start elasticsearch alert
    ```

**Extra note**

If the Elasticsearch service has been started on the client-node, then it is necessary to update the **client.rpm** and **data.rpm** packages on the client node.

After update, you need to edit:

```bash
/etc/elasticsearch/elasticsearch.yml
```

and change:

```bash
node.data: false
```

Additionally, check the file:

```bash
elasticsearch.yml.rpmnew
```

and complete the configuration in `elasticsearch.yml` with additional lines.

## Upgrade from version 7.0.1

### General note

- Update the `kibana` role to include index-pattern `.kibana*`
- Update the `alert` role to include index-pattern `.alertrules*` and `alert_status*`
- Install `python36` which is required for the Alerting engine

    ```bash
    yum install python3 on client-node
    ```

- AD users should move their saved objects  from the `adrole`.
- Indicators of compromise (IOCs auto-update) require access to the software provider's servers.
- GeoIP Databases (auto-update) require access to the software provider's servers.

### Upgrade steps

- Stop services

    ```bash
    systemctl stop elasticsearch alert kibana
    ```

- Upgrade client-node (includes alert engine)

    ```bash
    yum update ./itrs-log-analytics-client-node-7.0.2-1.el7.x86_64.rpm
    ```

- Login in the GUI ITRS Log Analytics and go to the `Alert List`  on the `Alerts` tab and click `SAVE` button

    ![](/media/media/image143.png)

- Start  `alert` and `kibana` service

    ```bash
    systemctl start alert kibana
    ```

- Upgrade data-node

    ```bash
    yum update ./itrs-log-analytics-data-node-7.0.2-1.el7.x86_64.rpm
    ```

- Start services

    ```bash
    systemctl start elasticsearch alert
    ```

**Extra note**

If the Elasticsearch service has been started on the client-node, then it is necessary to update the **client.rpm** and **data.rpm** packages on the client node.

After update, you need to edit:

```bash
/etc/elasticsearch/elasticsearch.yml
```

and change:

```bash
node.data: false
```

Additionally, check the file:

```bash
elasticsearch.yml.rpmnew
```

and complete the configuration in `elasticsearch.yml` with additional lines.

## Upgrade from 6.x

Before upgrading to ITRS Log Analytics from 6.x  OpenJDK / Oracle JDK  version 11:

```bash
yum -y -q install java-11-openjdk-headless.x86_64
```

And select default command for OpenJDK /Oracle JDK:

```bash
alternatives --config java
```

The update includes packages:

- itrs-log-analytics-data-node
- itrs-log-analytics-client-node

### Pre-upgrade steps for data node

1. Stop the Logstash service

   ```bash
   systemctl stop logstash
   ```

1. Flush sync for indices

   ```bash
   curl -sS -X POST "localhost:9200/_flush/synced?pretty" -u$USER:$PASSWORD
   ```

1. Close all indexes with production data, except system indexes (the name starts with a dot `.`), example of query:

   ```bash
   for i in `curl -u$USER:$PASSWORD "localhost:9200/_cat/indices/winlogbeat*?h=i"` ; do curl -u$USER:$PASSWORD -X POST localhost:9200/$i/_close ; done
   ```

1. Disable shard allocation

   ```bash
   curl -u$USER:$PASSWORD -X PUT "localhost:9200/_cluster/settings?pretty" -H 'Content-Type: application/json' -d' { "persistent": {"cluster.routing.allocation.enable": "none"}}'
   ```

1. Check Cluster Status

    ```bash
    export CREDENTIAL="logserver:logserver"
    
    curl -s -u $CREDENTIAL localhost:9200/_cluster/health?pretty
    ```

      Output:

    ```bash
    {
        "cluster_name" : "elasticsearch",
        "status" : "green",
        "timed_out" : false,
        "number_of_nodes" : 1,
        "number_of_data_nodes" : 1,
        "active_primary_shards" : 25,
        "active_shards" : 25,
        "relocating_shards" : 0,
        "initializing_shards" : 0,
        "unassigned_shards" : 0,
        "delayed_unassigned_shards" : 0,
        "number_of_pending_tasks" : 0,
        "number_of_in_flight_fetch" : 0,
        "task_max_waiting_in_queue_millis" : 0,
        "active_shards_percent_as_number" : 100.0
       }
    ```

1. Stop Elasticsearch service

    ```bash
    systemctl stop elasticsearch
    ```

### Upgrade ITRS Log Analytics Data Node

1. Upload Package

   ```bash
   scp ./itrs-log-analytics-data-node-7.0.1-1.el7.x86_64.rpm root@hostname:~/
   ```

1. Upgrade ITRS Log Analytics Package

   ```bash
   yum update ./itrs-log-analytics-data-node-7.0.1-1.el7.x86_64.rpm
   ```

   Output:

   ```bash
   Loaded plugins: fastestmirror
   Examining ./itrs-log-analytics-data-node-7.0.1-1.el7.x86_64.rpm:       itrs-log-analytics-data-node-7.0.1-1.el7.x86_64
   Marking ./itrs-log-analytics-data-node-7.0.1-1.el7.x86_64.rpm as an    update to itrs-log-analytics-data-node-6.1.8-1.x86_64
   Resolving Dependencies
   --> Running transaction check
   ---> Package itrs-log-analytics-data-node.x86_64 0:6.1.8-1 will be    updated
   ---> Package itrs-log-analytics-data-node.x86_64 0:7.0.1-1.el7 will be an update
   --> Finished Dependency Resolution

   Dependencies Resolved
   =======================================================================================================================================================================================
    Package                                        Arch                          Version                            Repository                                                          Size
   ========================================================================  ========================================================================  =======================================
   Updating:
    itrs-log-analytics-data-node                     x86_64                        7.0.1-1.el7                        /itrs-log-analytics-data-node-   7.0.1-1.el7.x86_64                     117 M

   Transaction Summary
   =======================================================================================================================================================================================
   Upgrade  1 Package

   Total size: 117 M
   Is this ok [y/d/N]: y
   Downloading packages:
   Running transaction check
   Running transaction test
   Transaction test succeeded
   Running transaction
     Updating   : itrs-log-analytics-data-node-7.0.1-1.el7.x86_64                                                                                                                       1/2
   Removed symlink /etc/systemd/system/multi-   user.target.wants/elasticsearch.service.
   Created symlink from /etc/systemd/system/multi-   user.target.wants/elasticsearch.service to    /usr/lib/systemd/system/elasticsearch.service.
     Cleanup    : itrs-log-analytics-data-node-6.1.8-1.x86_64                                                                                                                           2/2
     Verifying  : itrs-log-analytics-data-node-7.0.1-1.el7.x86_64                                                                                                                       1/2
     Verifying  : itrs-log-analytics-data-node-6.1.8-1.x86_64                                                                                                                           2/2

   Updated:
     itrs-log-analytics-data-node.x86_64 0:7.0.1-1.el7

   Complete!
   ```

1. Verification of Configuration Files

    Please, verify your Elasticsearch configuration and JVM configuration in files:

        - /etc/elasticsearch/jvm.options – check JVM HEAP settings and another parameters

    ```bash
    grep Xm /etc/elasticsearch/jvm.options <- old configuration file
    ## -Xms4g
    ## -Xmx4g
    # Xms represents the initial size of total heap space
    # Xmx represents the maximum size of total heap space
    -Xms600m
    -Xmx600m
    ```

    ```bash
    cp /etc/elasticsearch/jvm.options.rpmnew /etc/elasticsearch/jvm.options
    cp: overwrite ‘/etc/elasticsearch/jvm.options’? y
    ```

    ```bash
    vim /etc/elasticsearch/jvm.options
    ```

    - /etc/elasticsearch/elasticsearch.yml – verify elasticsearch configuration file

    - compare exiting /etc/elasticsearch/elasticsearch.yml and /etc/elasticsearch/elasticsearch.yml.rpmnew

1. Start and enable Elasticsearch service
    If everything went correctly, we will restart the Elasticsearch instance:

    ```bash
    systemctl restart elasticsearch
    systemctl reenable elasticsearch
    ```

    ```bash
    systemctl status elasticsearch
    ● elasticsearch.service - Elasticsearch
       Loaded: loaded (/usr/lib/systemd/system/elasticsearch.service; enabled; vendor preset: disabled)
       Active: active (running) since Wed 2020-03-18 16:50:15 CET; 57s ago
         Docs: http://www.elastic.co
     Main PID: 17195 (java)
       CGroup: /system.slice/elasticsearch.service
               └─17195 /etc/alternatives/jre/bin/java -Xms512m -Xmx512m -Djava.security.manager -Djava.security.policy=/usr/share/elasticsearch/plugins/elasticsearch_auth/plugin-securi...
    
    Mar 18 16:50:15 migration-01 systemd[1]: Started Elasticsearch.
    Mar 18 16:50:25 migration-01 elasticsearch[17195]: SSL not activated for http and/or transport.
    Mar 18 16:50:33 migration-01 elasticsearch[17195]: SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
    Mar 18 16:50:33 migration-01 elasticsearch[17195]: SLF4J: Defaulting to no-operation (NOP) logger implementation
    Mar 18 16:50:33 migration-01 elasticsearch[17195]: SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
    ```

1. Check cluster/indices status and Elasticsearch version

    Invoke curl command to check the status of Elasticsearch:

    ```bash
    curl -s -u $CREDENTIAL localhost:9200/_cluster/health?pretty
    {
      "cluster_name" : "elasticsearch",
      "status" : "green",
      "timed_out" : false,
      "number_of_nodes" : 1,
      "number_of_data_nodes" : 1,
      "active_primary_shards" : 25,
      "active_shards" : 25,
      "relocating_shards" : 0,
      "initializing_shards" : 0,
      "unassigned_shards" : 0,
      "delayed_unassigned_shards" : 0,
      "number_of_pending_tasks" : 0,
      "number_of_in_flight_fetch" : 0,
      "task_max_waiting_in_queue_millis" : 0,
      "active_shards_percent_as_number" : 100.0
    }
    ```

    ```bash
    curl -s -u $CREDENTIAL localhost:9200
    {
      "name" : "node-1",
      "cluster_name" : "elasticsearch",
      "cluster_uuid" : "igrASEDRRamyQgy-zJRSfg",
      "version" : {
        "number" : "7.3.2",
        "build_flavor" : "oss",
        "build_type" : "rpm",
        "build_hash" : "1c1faf1",
        "build_date" : "2019-09-06T14:40:30.409026Z",
        "build_snapshot" : false,
        "lucene_version" : "8.1.0",
        "minimum_wire_compatibility_version" : "6.8.0",
        "minimum_index_compatibility_version" : "6.0.0-beta1"
      },
      "tagline" : "You Know, for Search"
    }
    ```

1. Install new version of default base template

```bash
curl -k -XPUT -H 'Content-Type: application/json' -u logserver:logserver 'http://127.0.0.1:9200/_template/default-base-template-0' -d@/usr/share/elasticsearch/default-base-template-0.json
```

If everything went correctly, we should see 100% allocated shards in cluster health. However, while connection on port 9200/TCP we  can observe a new version of Elasticsearch.

### Post-upgrade steps for data node

1. Start Elasticsearch service

   ```bash
   systemctl statrt elasticsearch
   ```

1. Delete .auth index

   ```bash
   curl -u$USER:$PASSWORD -X DELETE localhost:9200/.auth
   ```

1. Use `elasticdump` to get all templates and load it back

   - get templates

   ```bash
   /usr/share/kibana/elasticdump/elasticdump  --output=http://logserver:logserver@localhost:9200 --input=templates_elasticdump.json --type=template
   ```

   - delete templates

   ```bash
   for i in `curl -ss -ulogserver:logserver http://localhost:9200/_cat/templates | awk '{print $1}'`; do curl -ulogserver:logserver -XDELETE http://localhost:9200/_template/$i ; done
   ```

   - load templates

   ```bash
   /usr/share/kibana/elasticdump/elasticdump  --input=http://logserver:logserver@localhost:9200 --output=templates_elasticdump.json --type=template
   ```

1. Open indexes that were closed before the upgrade, example of query:

   ```bash
   curl -ss -u$USER:$PASSWORD "http://localhost:9200/_cat/indices/winlogbeat*?h=i,s&s=i" |awk '{if ($2 ~ /close/) system("curl -ss -u$USER:$PASSWORD -XPOST http://localhost:9200/"$1"/_open?pretty")}'
   ```

1. Start the Logstash service

   ```bash
   systemctl start logstash
   ```

1. Enable Elasticsearch allocation

   ```bash
   curl -sS -u$USER:$PASSWORD -X PUT "http://localhost:9200/_cluster/settings?pretty" -H 'Content-Type: application/json' -d' { "persistent": {"cluster.routing.allocation.enable": "none"}}'
   ```

1. After starting on GUI remove aliases .kibana* (double version of index patterns)

   ```bash
   curl -u$USER:$PASSWORD "http://localhost:9200/.kibana_1/_alias/_all" -XDELETE
   ```

### Upgrade ITRS Log Analytics Client Node

1. Upload packages

    - Upload new rpm by scp/ftp:

    ```bash
    scp ./itrs-log-analytics-client-node-7.0.1-1.el7.x86_64.rpm root@hostname:~/
    ```

    - Backup report logo file.

1. Uninstall old version ITRS Log Analytics GUI

    - Remove old package:

    ```bash
    systemctl stop kibana alert
    ```

    ```bash
    yum remove itrs-log-analytics-client-node
    Loaded plugins: fastestmirror
    Resolving Dependencies
    --> Running transaction check
    ---> Package itrs-log-analytics-client-node.x86_64 0:6.1.8-1 will be erased
    --> Finished Dependency Resolution

    Dependencies Resolved

    =======================================================================================================================================================================================
     Package                                           Arch                        Version                        Repository                                                          Size
    =======================================================================================================================================================================================
    Removing:
     itrs-log-analytics-client-node                      x86_64                      6.1.8-1                        @/itrs-log-analytics-client-node-6.1.8-1.x86_64                      802 M

    Transaction Summary
    =======================================================================================================================================================================================
    Remove  1 Package

    Installed size: 802 M
    Is this ok [y/N]: y
    Downloading packages:
    Running transaction check
    Running transaction test
    Transaction test succeeded
    Running transaction
      Erasing    : itrs-log-analytics-client-node-6.1.8-1.x86_64                                                                                                                         1/1
    warning: file /usr/share/kibana/plugins/node_modules.tar: remove failed: No such file or directory
    warning: /etc/kibana/kibana.yml saved as /etc/kibana/kibana.yml.rpmsave
      Verifying  : itrs-log-analytics-client-node-6.1.8-1.x86_64                                                                                                                         1/1

    Removed:
      itrs-log-analytics-client-node.x86_64 0:6.1.8-1

    Complete!
    ```

1. Install new version

    - Install dependencies:

      ```bash
      yum install net-tools mailx gtk3 libXScrnSaver ImageMagick ghostscript
      ```

    - Install new package:

      ```bash
      yum install ./itrs-log-analytics-client-node-7.0.1-1.el7.x86_64.rpm
      Loaded plugins: fastestmirror
      Examining ./itrs-log-analytics-client-node-7.0.1-1.el7.x86_64.rpm: itrs-log-analytics-client-node-7.0.1-1.el7.x86_64
      Marking ./itrs-log-analytics-client-node-7.0.1-1.el7.x86_64.rpm to be installed
      Resolving Dependencies
      --> Running transaction check
      ---> Package itrs-log-analytics-client-node.x86_64 0:7.0.1-1.el7 will be installed
      --> Finished Dependency Resolution
      
      Dependencies Resolved
      
      =======================================================================================================================================================================================
       Package                                         Arch                      Version                           Repository                                                           Size
      =======================================================================================================================================================================================
      Installing:
       itrs-log-analytics-client-node                    x86_64                    7.0.1-1.el7                       /itrs-log-analytics-client-node-7.0.1-1.el7.x86_64                    1.2 G
      
      Transaction Summary
      =======================================================================================================================================================================================
      Install  1 Package
      
      Total size: 1.2 G
      Installed size: 1.2 G
      Is this ok [y/d/N]: y
      Downloading packages:
      Running transaction check
      Running transaction test
      Transaction test succeeded
      Running transaction
        Installing : itrs-log-analytics-client-node-7.0.1-1.el7.x86_64                                                                                                                     1/1
      Generating a 2048 bit RSA private key
      ..............................................................................................+++
      ...........................................................................................................+++
      writing new private key to '/etc/kibana/ssl/kibana.key'
      -----
      Removed symlink /etc/systemd/system/multi-user.target.wants/alert.service.
      Created symlink from /etc/systemd/system/multi-user.target.wants/alert.service to /usr/lib/systemd/system/alert.service.
      Removed symlink /etc/systemd/system/multi-user.target.wants/kibana.service.
      Created symlink from /etc/systemd/system/multi-user.target.wants/kibana.service to /usr/lib/systemd/system/kibana.service.
      Removed symlink /etc/systemd/system/multi-user.target.wants/cerebro.service.
      Created symlink from /etc/systemd/system/multi-user.target.wants/cerebro.service to /usr/lib/systemd/system/cerebro.service.
        Verifying  : itrs-log-analytics-client-node-7.0.1-1.el7.x86_64                                                                                                                     1/1
      
      Installed:
        itrs-log-analytics-client-node.x86_64 0:7.0.1-1.el7
      
      Complete!
      ```

1. Start ITRS Log Analytics GUI

    Add service:
    - Kibana
    - Cerebro
    - Alert

    to autostart and add port ( 5602/TCP ) for Cerebro.
    Run them and check status:

    ```bash
    firewall-cmd –permanent –add-port 5602/tcp
    firewall-cmd –reload
    ```

    ```bash
        systemctl enable kibana cerebro alert
        Created symlink from /etc/systemd/system/multi-user.target.wants/kibana.service to /usr/lib/systemd/system/kibana.service.
        Created symlink from /etc/systemd/system/multi-user.target.wants/cerebro.service to /usr/lib/systemd/system/cerebro.service.
        Created symlink from /etc/systemd/system/multi-user.target.wants/alert.service to /usr/lib/systemd/system/alert.service.
    ```

    ```bash
    systemctl start kibana cerebro alert
    systemctl status kibana cerebro alert
    ● kibana.service - Kibana
       Loaded: loaded (/usr/lib/systemd/system/kibana.service; enabled; vendor preset: disabled)
       Active: active (running) since Thu 2020-03-19 14:46:52 CET; 2s ago
     Main PID: 12399 (node)
       CGroup: /system.slice/kibana.service
               └─12399 /usr/share/kibana/bin/../node/bin/node --no-warnings --max-http-header-size=65536 /usr/share/kibana/bin/../src/cli -c /etc/kibana/kibana.yml
    
    Mar 19 14:46:52 migration-01 systemd[1]: Started Kibana.
    
    ● cerebro.service - Cerebro
       Loaded: loaded (/usr/lib/systemd/system/cerebro.service; enabled; vendor preset: disabled)
       Active: active (running) since Thu 2020-03-19 14:46:52 CET; 2s ago
     Main PID: 12400 (java)
       CGroup: /system.slice/cerebro.service
               └─12400 java -Duser.dir=/opt/cerebro -Dconfig.file=/opt/cerebro/conf/application.conf -cp -jar /opt/cerebro/lib/cerebro.cerebro-0.8.4-launcher.jar
    
    Mar 19 14:46:52 migration-01 systemd[1]: Started Cerebro.
    
    ● alert.service - Alert
       Loaded: loaded (/usr/lib/systemd/system/alert.service; enabled; vendor preset: disabled)
       Active: active (running) since Thu 2020-03-19 14:46:52 CET; 2s ago
     Main PID: 12401 (elastalert)
       CGroup: /system.slice/alert.service
               └─12401 /opt/alert/bin/python /opt/alert/bin/elastalert
    
    Mar 19 14:46:52 migration-01 systemd[1]: Started Alert.
    ```

## Downgrade

Follow the steps below:

```bash
systemctl stop elasticsearch kibana logstash wiki cerebro automation intelligence intelligence-scheduler skimmer alert
```

```bash
yum remove itrs-log-analytics-*
```

```bash
yum install old-version.rpm
```

```bash
systemctl start elasticsearch kibana logstash wiki cerebro automation intelligence intelligence-scheduler skimmer alert
```

## Changing OpenJDK version

### Logstash

OpenJDK 11 is supported by Logstash from version 6.8 so if you have an older version of Logstash you must update it.

To update Logstash, follow the steps below:

1. Back up the following files
    - /etc/logstash/logstash.yml
    - /etc/logstash/pipelines.yml
    - /etc/logstash/conf.d

2. Use the command to check custom Logstash plugins:

    ```bash
    /usr/share/bin/logstash-plugin list --verbose
    ```

    and note the result

3. Install a newer version of Logstash according to the instructions:

    https://www.elastic.co/guide/en/logstash/6.8/upgrading-logstash.html

    or

    https://www.elastic.co/guide/en/logstash/current/upgrading-logstash.html

4. Verify installed plugins:

    ```bash
    /usr/share/bin/logstash-plugin list --verbose
    ```

5. Install the missing plugins if necessary:

    ```bash
    /usr/share/bin/logstash-plugin install plugin_name
    ```

6. Run Logstash using the command:

    ```bash
    systemctl start logstash
    ```

### Elasticsearch

ITRS Log Analytics can use OpenJDK version 10 or later.
If you want to use OpenJSK version 10 or later, configure the Elasticsearch service as follows:

1. After installing OpenJDK, select the correct version that Elasticsearch will use:

    ```bash
    alternative --config java
    ```

2. Open the `/etc/elasticsearch/jvm.options` file in a text editor:

    ```bash
    vi /etc/elasticsearch/jvm.options
    ```

3. Disable the OpenJDK version 8 section:

    ```bash
    ## JDK 8 GC logging

    #8:-XX:+PrintGCDetails
    #8:-XX:+PrintGCDateStamps
    #8:-XX:+PrintTenuringDistribution
    #8:-XX:+PrintGCApplicationStoppedTime
    #8:-Xloggc:/var/log/elasticsearch/gc.log
    #8:-XX:+UseGCLogFileRotation
    #8:-XX:NumberOfGCLogFiles=32
    #8:-XX:GCLogFileSize=64m
    ```

4. Enable the OpenJDK version 11 section

    ```bash
    ## G1GC Configuration
    # NOTE: G1GC is only supported on JDK version 10 or later.
    # To use G1GC uncomment the lines below.
    10-:-XX:-UseConcMarkSweepGC
    10-:-XX:-UseCMSInitiatingOccupancyOnly
    10-:-XX:+UseG1GC
    10-:-XX:InitiatingHeapOccupancyPercent=75
    ```

5. Restart the Elasticsearch service

    ```bash
    systemctl restart elasticsearch
    ```
