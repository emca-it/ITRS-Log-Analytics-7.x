# Configuration

## Changing default users for services

### Change Kibana User

Edit file */etc/systemd/system/kibana.service*

```bash
  User=newuser
  Group= newuser
```

Edit */etc/default/kibana*

```bash
  user=" newuser "
  group=" newuser "
```

Add appropriate permission:

```bash
  chown newuser: /usr/share/kibana/ /etc/kibana/ -R
```

### Change Elasticsearch User

Edit **/usr/lib/tmpfiles.d/elasticsearch.conf* and change user name and group:

```bash
  d /var/run/elasticsearch 0755 newuser newuser –
```

Create directory:

```bash
  mkdir /etc/systemd/system/elasticsearch.service.d/
```

Edit */etc/systemd/system/elasticsearch.service.d/01-user.conf*

```bash
  [Service]
  User=newuser
  Group= newuser
```

Add appropriate permission:

```bash
  chown -R newuser: /var/lib/elasticsearch /usr/share/elasticsearch /etc/elasticsearch /var/log/elasticsearch
```

### Change Logstash User

Create directory:

  mkdir /etc/systemd/system/logstash.service.d

Edit */etc/systemd/system/logstash.service.d/01-user.conf*

  [Service]
  User=newuser
  Group=newuser

Add appropriate permission:

  chown -R newuser: /etc/logstash /var/log/logstash

## Plugins Management

### GUI/Kibana

Base installation of the ITRS Log Analytics contains the Agents, Alerts, Archive, Automation, CMDB, Index Management, Intelligence, Network Probe, Reports, SQL  plugins - These add-ons can be disabled or enabled via the configuration file without having to install or uninstall.
You can extend the basic Kibana functionality by installing custom plugins.

After installation, each node must be restarted before the plugin becomes visible.

The Kibana provides three categories of plugins:

- Licenced Plugins - ITRS Log Analytics
- Core Plugins - it is plugins that are part of the Kibana project.
- Community-contributed - it is plugins that are external to the Kibana project

#### Enabling/Disabling Plugins

 **Managing the `Agents` Plugin**:

   - **Disable**:
     - Add `agents.enabled: false` to the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.
   - **Enable**:
     - Remove or comment out the line `agents.enabled: false` in the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.

 **Managing the `Alerts` Plugin**:

   - **Disable**:
     - Change `alerts.enabled: true` to `alerts.enabled: false` in the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.
   - **Enable**:
     - Change `alerts.enabled: false` to `alerts.enabled: true` in the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.

 **Managing the `Archive` Plugin**:

   - **Disable**:
     - Add `archive.enabled: false` to the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.
   - **Enable**:
     - Remove or comment out the line `archive.enabled: false` in the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.

 **Managing the `Automation` Plugin**:

   - **Disable**:
     - Change `automation.enabled: true` to `automation.enabled: false` in the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.
   - **Enable**:
     - Change `automation.enabled: false` to `automation.enabled: true` in the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.

 **Managing the `CMDB` Plugin**:

   - **Disable**:
     - Add `cmdb.enabled: false` to the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.
   - **Enable**:
     - Remove or comment out the line `cmdb.enabled: false` in the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.

 **Managing the `Console` Plugin**:

   - **Disable**:
     - Change `console.enabled: true` to `console.enabled: false` in the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.
   - **Enable**:
     - Change `console.enabled: false` to `console.enabled: true` in the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.

 **Managing the `Index Management` Plugin**:

   - **Disable**:
     - Add `index_management.enabled: false` to the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.
   - **Enable**:
     - Remove or comment out the line `index_management.enabled: false` in the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.

 **Managing the `Intelligence` Plugin**:

   - **Disable**:
     - Add `intelligence.enabled: false` to the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.
   - **Enable**:
     - Remove or comment out the line `intelligence.enabled: false` in the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.

 **Managing the `Network Probe` Plugin**:

   - **Disable**:
     - Add `network-probe.enabled: false` to the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.
   - **Enable**:
     - Remove or comment out the line `network-probe.enabled: false` in the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.

 **Managing the `Reports` Plugin**:

   - **Disable**:
     - Add `reports.enabled: false` to the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.
   - **Enable**:
     - Remove or comment out the line `reports.enabled: false` in the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.

 **Managing the `vis_type_timeline` Plugin**:

   - **Disable**:
     - Change `vis_type_timeline.enabled: true` to `vis_type_timeline.enabled: false` in the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.
   - **Enable**:
     - Change `vis_type_timeline.enabled: false` to `vis_type_timeline.enabled: true` in the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.

 **Managing the `Wazuh` Plugin**:

   - **Disable**:
     - Change `wazuh.enabled: true` to `wazuh.enabled: false` in the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.
   - **Enable**:
     - Change `wazuh.enabled: false` to `wazuh.enabled: true` in the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.

 **Managing the `XLSX Import` Plugin**:

   - **Disable**:
     - Add `xlsx_import.enabled: false` to the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.
   - **Enable**:
     - Remove or comment out the line `xlsx_import.enabled: false` in the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.

 **Managing the `SQL` Plugin**:

   - **Disable**:
     - Add `sql.enabled: false` to the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.
   - **Enable**:
     - Remove or comment out the line `sql.enabled: false` in the file `/etc/kibana/kibana.yml`.
     - Run the command `systemctl restart kibana`.

#### Installing Plugins

Additional GUI/Kibana plugins can be installed as follows:

```bash
 cd /usr/share/kibana/
 bin/opensearch-dashboards-plugin install [plugin_name]
```

Examples: \
Plugins from a custom link or filesystem can be installed as follows:

```bash
 bin/opensearch-dashboards-plugin install file:///path/to/plugin.zip
 bin/opensearch-dashboards-plugin install file:///C:/path/to/plugin.zip
 bin/opensearch-dashboards-plugin install http://some.domain/path/to/plugin.zip
```

#### Listing plugins

Listing currently loaded plugins:

```bash
 bin/opensearch-dashboards-plugin list
```

#### Removing plugins

```bash
 bin/opensearch-dashboards-plugin remove [pluginname]
```

#### Updating plugins

```bash
 bin/opensearch-dashboards-plugin remove [pluginname]
 bin/opensearch-dashboards-plugin install [pluginname]
```

### Database/Elasticsearch

Base installation of the ITRS Log Analytics contains the logserver_auth, join, logserver_quard plugin - These add-ons can be disabled or enabled via the configuration file without having to install or uninstall.
You can extend the basic Elasticsearch functionality by installing custom plugins.

Plugins contain JAR files, but may also contain scripts and config files, and must be installed on every node in the cluster.

After installation, each node must be restarted before the plugin becomes visible.

The Elasticsearch provides three categories of plugins:

- Licenced Plugins - ITRS Log Analytics
- Core Plugins - it is plugins that are part of the Elasticsearch project.
- Community-contributed - it is plugins that are external to the Elasticsearch project

#### Enabling/Disabling Plugins

 **Managing the `logserver_auth` Plugin**:

   - **Disable**:
     - Add `plugins.logserver_auth.enabled: false` to the file `/etc/elasticsearch/elasticsearch.yml`.
     - Run the command `systemctl restart elasticsearch`.
   - **Enable**:
     - Remove or comment out the line `plugins.logserver_auth.enabled: false` in the file `/etc/elasticsearch/elasticsearch.yml`.
     - Run the command `systemctl restart elasticsearch`.

 **Managing the `logserver_guard` Plugin**:

   - **Disable**:
     - Add `logserverguard.ssl.transport.enabled: false` to the file `/etc/elasticsearch/elasticsearch.yml`.
     - Add `logserverguard.ssl.http.enabled: false` to the file `/etc/elasticsearch/elasticsearch.yml`.
     - Run the command `systemctl restart elasticsearch`.
   - **Enable**:
     - Remove or comment out the line `logserverguard.ssl.transport.enabled: false` in the file `/etc/elasticsearch/elasticsearch.yml`.
     - Remove or comment out the line `logserverguard.ssl.http.enabled: false` in the file `/etc/elasticsearch/elasticsearch.yml`.
     - Run the command `systemctl restart elasticsearch`.

 **Managing the `sql` Plugin**:

   - **Disable**:
     - Add `plugins.sql.enabled: false` to the file `/etc/elasticsearch/elasticsearch.yml`.
     - Run the command `systemctl restart elasticsearch`.
   - **Enable**:
     - Remove or comment out the line `plugins.sql.enabled: false` in the file `/etc/elasticsearch/elasticsearch.yml`.
     - Run the command `systemctl restart elasticsearch`.

#### Installing Plugins

Additional Database/Elasticsearch plugins can be installed as follows:

```bash
 cd /usr/share/elasticsearch/
 bin/opensearch-plugin install [plugin_name]
```

Examples: \
Plugins from a custom link or filesystem can be installed as follows:

```bash
 bin/opensearch-plugin install file:///path/to/plugin.zip
 bin/opensearch-plugin install file:///C:/path/to/plugin.zip
 bin/opensearch-plugin install <http://some.domain/path/to/plugin.zip>
```

#### Listing plugins

Listing currently loaded plugins:

```bash
 bin/opensearch-plugin list
```

#### Removing plugins

```bash
 bin/opensearch-plugin remove [pluginname]
```

#### Updating plugins

```bash
 bin/opensearch-plugin remove [pluginname]
 bin/opensearch-plugin install [pluginname]
```

## Transport layer encryption

### Generating Certificates

1. Requirements for certificate configuration:

    - **To encrypt traffic (HTTP and transport layer) of Elasticsearch you have to generate certificate authority which will be used to sign each node certificate of a cluster.**
    - **The Elasticsearch certificate has to be generated in pkcs8 RSA format.**

1. To generate certificates use tlstool.sh script, which can be found in the `/usr/share/elasticsearch/utils/tlstool` directory. \
Example certificate configuration for single node environment (certificates will be valid for 10 years) is listed below:

    ```bash
    ca:
      root:
        dn: CN=mylocal.domain.test,OU=Dev,O=EMCA Software,C=Poland
        keysize: 2048
        validityDays: 3650
        pkPassword: none
        file: rootCA.crt

    defaults:
      validityDays: 3650
      pkPassword: none
      httpsEnabled: true
      reuseTransportCertificatesForHttp: true
      verifyHostnames: true
      resolveHostnames: false

    nodes:
      - name: node1
        dn: CN=mylocal.domain.test,OU=Dev,O=EMCA Software,C=Poland
        ip: 127.0.0.1
    ```

    Other examples can be found in the `config`` directory of the TLS Tool. More details about the TLS Tool and documented options can be found [here.](#offline-tls-tool)

    To use the above configuration run:

    ```bash
    cd /usr/share/elasticsearch/utils/tlstool
    bash tlstool.sh -c config/logserver.yml -ca -crt
    ```

    It will generate the necessary rootCA and server private key together with its certificate.

1. Right now you should have these files:

    ```bash
    ls -1 | sort
    node1.crt
    node1.key
    rootCA.crt
    rootCA.key
    ```

1. Create a directory to store required files (users: elasticsearch, kibana, and logstash have to be able to read these files):

    ```bash
    mkdir /etc/elasticsearch/ssl
    cp out/{node1.*,rootCA.crt} /etc/elasticsearch/ssl
    chown -R elasticsearch:elasticsearch /etc/elasticsearch/ssl
    chmod 755 /etc/elasticsearch/ssl
    chmod 644 /etc/elasticsearch/ssl/*
    ```

#### Setting up configuration files

1. Append or uncomment below lines in `/etc/elasticsearch/elasticsearch.yml` and change paths to proper values (based on past steps):

    - Transport layer encryption

      ```yml
      logserverguard.ssl.transport.enabled: true
      logserverguard.ssl.transport.pemcert_filepath: "/etc/elasticsearch/ssl/node1.crt"
      logserverguard.ssl.transport.pemkey_filepath: "/etc/elasticsearch/ssl/node1.key"
      logserverguard.ssl.transport.pemkey_password: "password_for_pemkey" # If there is no password leave ""
      logserverguard.ssl.transport.pemtrustedcas_filepath: "/etc/elasticsearch/ssl/rootCA.crt"

      logserverguard.ssl.transport.enforce_hostname_verification: true
      logserverguard.ssl.transport.resolve_hostname: true

      logserverguard.ssl.transport.enabled_ciphers:
        - "TLS_DHE_RSA_WITH_AES_128_GCM_SHA256"
        - "TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256"

      logserverguard.ssl.transport.enabled_protocols:
        - "TLSv1.2"
      ```

    - HTTP layer encryption

      ```yaml
      logserverguard.ssl.http.enabled: true
      logserverguard.ssl.http.pemcert_filepath: "/etc/elasticsearch/ssl/node1.crt"
      logserverguard.ssl.http.pemkey_filepath: "/etc/elasticsearch/ssl/node1.key"
      logserverguard.ssl.http.pemkey_password: "password_for_pemkey" # If there is no password leave ""
      logserverguard.ssl.http.pemtrustedcas_filepath: "/etc/elasticsearch/ssl/rootCA.crt"

      logserverguard.ssl.http.clientauth_mode: OPTIONAL
      logserverguard.ssl.http.enabled_ciphers:
        - "TLS_DHE_RSA_WITH_AES_128_GCM_SHA256"
        - "TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256"

      logserverguard.ssl.http.enabled_protocols:
        - "TLSv1.2"
      ```

1. Append or uncomment below lines in `/etc/kibana/kibana.yml` and change paths to proper values:

    ```yaml
    elasticsearch.hosts: ["https://127.0.0.1:8000"]
    ---
    # Elasticsearch trafic encryption
    # There is also an option to use "127.0.0.1/localhost" and to not supply path to CA. Verification Mode should be then changed to "none".
    elasticsearch.ssl.verificationMode: full
    elasticsearch.ssl.certificate: "/etc/elasticsearch/ssl/node1.crt"
    elasticsearch.ssl.key: "/etc/elasticsearch/ssl/node1.key"
    elasticsearch.ssl.keyPassphrase: "password_for_pemkey" # this line is not required if there is no password
    elasticsearch.ssl.certificateAuthorities: "/etc/elasticsearch/ssl/rootCA.crt"
    ```

1. Append or uncomment the below lines in `/opt/alert/config.yaml` and change paths to proper values:

    ```yaml
    # Connect with TLS to Elasticsearch
    use_ssl: True

    # Verify TLS certificates
    verify_certs: True

    # Client certificate
    client_cert: /etc/elasticsearch/ssl/node1.crt
    client_key: /etc/elasticsearch/ssl/node1.key
    ca_certs: /etc/elasticsearch/ssl/rootCA.crt
    ```

1. For CSV/HTML export to work properly rootCA.crt generated in the first step has to be "installed" on the server. Below are example steps for CentOS 7:

    ```bash
    # Copy rootCA.crt and update CA trust store
    cp /etc/elasticsearch/ssl/rootCA.crt /etc/pki/ca-trust/source/anchors/rootCA.crt
    update-ca-trust
    ```

1. Intelligence module. Generate pkcs12 keystore/cert:

    ```bash
    DOMAIN=mylocal.domain.test
    keytool -import -file /etc/elasticsearch/ssl/rootCA.crt -alias root -keystore root.jks
    openssl pkcs12 -export -in /etc/elasticsearch/ssl/${DOMAIN}.crt -inkey /etc/elasticsearch/ssl/${DOMAIN}.key -out ${DOMAIN}.p12 -name "${DOMAIN}" -certfile /etc/elasticsearch/ssl/rootCA.crt
    ```

    ```bash
    # Configure /opt/ai/bin/conf.cfg
    https_keystore=/path/to/pk12/mylocal.domain.test.p12
    https_truststore=/path/to/root.jks
    https_keystore_pass=bla123
    https_truststore_pass=bla123
    ```

#### Logstash/Beats

You can either install CA to allow Logstash and Beats traffic or you can supply the required certificates in config:

1. Logstash:

    ```yml
    output {
      logserver {
        hosts => "https://mylocal.domain.test:9200"
        ssl => true
        index => "winlogbeat-%{+YYYY.MM}"
        user => "logstash"
        password => "logstash"
        cacert => "/path/to/cacert/rootCA.crt"
      }
    }
    ```

2. Beats:

    ```yaml
    output.elasticsearch.hosts: ["https://mylocal.domain.test:9200"]
    output.elasticsearch.protocol: "https"
    output.elasticsearch.ssl.enabled: true
    output.elasticsearch.ssl.certificate_authorities: ["/path/to/cacert/rootCA.crt"]
    ```

Additionally, for any beats program to be able to write to elasticsearch, you will have to make changes to the "enabled_ciphers" directive in "/etc/elasticsearch/elasticsearch.yml". This is done by commenting:
  
  ```yaml
  logserverguard.ssl.http.enabled_ciphers:
  - "TLS_DHE_RSA_WITH_AES_256_GCM_SHA384"
  ```

Otherwise, the beat will not be able to send documents directly and if you want to avoid it you can send a document with Logstash first.

## Offline TLS Tool

The TLS Tool is a program that can be used for:
  
  - Generating Root and Intermediate CA's,
  - Generating Node, Client, and Admin certificates,
  - Generating CSRs,
  - Validating certificates

Besides the actual certificates the tool also generated configuration snippets which you can directly copy and paste into your `elasticsearch.yml`.

### General usage

The tls tool will read the node- and certificate configuration settings from a yaml file, and outputs the generated files in a configurable directory.

You can choose to create the Root CA and (optional) intermediate CAs with your node certificates in one go. Or you can create the Root and intermediate CA first, and generate node certificates as you need them.

You will find the script in:

```bash
<installation directory>/tlstool.sh
```

Default `<installation directory>` is `/usr/share/elasticsearch/utils/tlstool`.

### Command line options

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-lboi{border-color:inherit;text-align:left;vertical-align:middle}
.tg .tg-fymr{border-color:inherit;font-weight:bold;text-align:left;vertical-align:top}
.tg .tg-0pky{border-color:inherit;text-align:left;vertical-align:top}
</style>
<table class="tg" style="undefined;table-layout: fixed; width: 691px">
<colgroup>
<col style="width: 120px">
<col style="width: 471px">
</colgroup>
<thead>
  <tr>
    <th class="tg-fymr">Name</th>
    <th class="tg-fymr">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-lboi">-c,--config</td>
    <td class="tg-lboi">Relative or absolute path to the configuration file. Required.</td>
  </tr>
  <tr>
    <td class="tg-lboi">-t,--target</td>
    <td class="tg-lboi">Relative or absolute path to the output directory. Optional, default: out</td>
  </tr>
  <tr>
    <td class="tg-lboi">-v,--verbose</td>
    <td class="tg-lboi">Enable detailed output, default: false</td>
  </tr>
  <tr>
    <td class="tg-lboi">-f,--force</td>
    <td class="tg-lboi">Force certificate generation despite of validation errors. default: false</td>
  </tr>
  <tr>
    <td class="tg-lboi">-o,--overwrite</td>
    <td class="tg-lboi">Overwrite existing node-, client and admin certificates if they are already present. default: false</td>
  </tr>
  <tr>
    <td class="tg-lboi">-p,--pem</td>
    <td class="tg-lboi">Change certificate file extension from ".crt" to ".pem". default: false</td>
  </tr>
  <tr>
    <td class="tg-lboi">-ca,--create-ca</td>
    <td class="tg-lboi">Create new Root and Intermediate CAs</td>
  </tr>
  <tr>
    <td class="tg-lboi">-crt,--create-cert</td>
    <td class="tg-0pky">Create certificates using an existing or newly created local certificate authority</td>
  </tr>
</tbody>
</table>

### Examples

`<installation directory>/tlstool.sh -c config/tlsconfig.yml -ca -crt`

Reads the configuration from `config/tlsconfig.yml` and generates the configured Root and intermediate CAs and the configured node, admin, and client certificates in one go. The generated files will be written to `out`.

`<installation directory>/tlstool.sh -c config/tlsconfig.yml -ca`

Reads the configuration from `config/tlsconfig.yml` and generates the configured Root and intermediate CAs only.

`<installation directory>/tlstool.sh -c config/tlsconfig.yml -crt`

Reads the configuration from `config/tlsconfig.yml` and generates node, admin, and client certificates only. The Root and (optional) intermediate CA certificates and keys need to be present in the output directory, and their filenames, keys and (optional) passwords have to be configured in `tlsconfig.yml`.

### Root CA

To configure the Root CA for all certificates, add the following lines to your configuration file:

```yml
ca:
   root:
      dn: CN=root.ca.example.com,OU=CA,O=Example Com, Inc.,DC=example,DC=com
      keysize: 2048
      pkPassword: root-ca-password 
      validityDays: 3650
      file: root-ca.crt
```

Generated files:

  - `root-ca.crt` - Root certificate
  - `root-ca.key` - Private key of the Root CA
  - `root-ca.readme` - Auto-generated passwords of the root and intermediate CAs

Options:

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-lboi{border-color:inherit;text-align:left;vertical-align:middle}
.tg .tg-fymr{border-color:inherit;font-weight:bold;text-align:left;vertical-align:top}
</style>
<table class="tg" style="undefined;table-layout: fixed; width: 691px">
<colgroup>
<col style="width: 120px">
<col style="width: 471px">
</colgroup>
<thead>
  <tr>
    <th class="tg-fymr">Name</th>
    <th class="tg-fymr">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-lboi">dn</td>
    <td class="tg-lboi">The complete Distinguished Name of the Root CA. If you have special characters in the DN, you need to quote them correctly. Mandatory.</td>
  </tr>
  <tr>
    <td class="tg-lboi">keysize</td>
    <td class="tg-lboi">The size of the private key. Default: 2048</td>
  </tr>
  <tr>
    <td class="tg-lboi">pkPassword</td>
    <td class="tg-lboi">Password of the private key. One of: "none", "auto" or a self-chosen password. Default: auto</td>
  </tr>
  <tr>
    <td class="tg-lboi">file</td>
    <td class="tg-lboi">File name of the certificate, optional. Default: "root-ca"</td>
  </tr>
</tbody>
</table>

The pkPassword can be one of:

  - **none**: The generated private key will be unencrypted
  - **auto**: A random password is generated automatically. After the certificates have been generated, you can find the password in root-ca.readme file. To use these new passwords again, you must edit the tool config file and set the generated passwords there.
  - **other value**: Values other than none or auto are used as password directly

### Intermediate CA

In addition to the root CA you optionally also specify an intermediate CA. If an intermediate CA is configured, then the node, admin, and client certificates will be signed by the intermediate CA. If you do want to use an intermediate CA, remove the following section from the configuration. The certificates are then signed by the root CA directly.

```yml
ca:
   intermediate:
      dn: CN=signing.ca.example.com,OU=CA,O=Example Com, Inc.,DC=example,DC=com
      keysize: 2048
      validityDays: 3650  
      pkPassword: intermediate-ca-password
      file: intermediate-ca.crt
```

Generated files:

  - `intermediate-ca.crt` - Intermediate certificate
  - `intermediate-ca.key` - Private key of the intermediate certificate
  - `root-ca.readme` - Auto-generated passwords of the root and intermediate CAs

### Node and Client certificates

#### Global and default settings

The default settings are applied to all generated certificates and configuration snippets. All values here are optional.

```yml
defaults:
  validityDays: 730
  pkPassword: auto
  generatedPasswordLength: 12
  nodesDn:
    - "CN=*.example.com,OU=Ops,O=Example Com, Inc.,DC=example,DC=com"
  nodeOid: "1.2.3.4.5.5"
  httpsEnabled: true
  reuseTransportCertificatesForHttp: false
```

Options:

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-cly1{text-align:left;vertical-align:middle}
.tg .tg-lboi{border-color:inherit;text-align:left;vertical-align:middle}
.tg .tg-fymr{border-color:inherit;font-weight:bold;text-align:left;vertical-align:top}
</style>
<table class="tg" style="undefined;table-layout: fixed; width: 691px">
<colgroup>
<col style="width: 120px">
<col style="width: 471px">
</colgroup>
<thead>
  <tr>
    <th class="tg-fymr">Name</th>
    <th class="tg-fymr">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-lboi">validityDays</td>
    <td class="tg-lboi">Validity of the generated certificates, in days. Default: 730. Can be overwritten for each certificate separately.</td>
  </tr>
  <tr>
    <td class="tg-lboi">pkPassword</td>
    <td class="tg-lboi">Password of the private key. One of: "none", "auto" or a self-chosen password. Default: auto. Can be overwritten for each certificate separately.</td>
  </tr>
  <tr>
    <td class="tg-lboi">generatedPasswordLength</td>
    <td class="tg-lboi">Length of the auto-generated password for the private keys. Only takes effect when pkPassword is set to auto. Default: 12. Can be overwritten for each certificate separately.</td>
  </tr>
  <tr>
    <td class="tg-lboi">httpsEnabled</td>
    <td class="tg-lboi">Whether to enable TLS on the REST layer or not. Default: true</td>
  </tr>
  <tr>
    <td class="tg-lboi">reuseTransportCertificatesForHttp</td>
    <td class="tg-lboi">If set to false, individual certificates for REST and Transport are generated. If set to true, the node certificates are also used on the REST layer. Default: false</td>
  </tr>
  <tr>
    <td class="tg-lboi">verifyHostnames</td>
    <td class="tg-lboi">Set this to true to enable hostname verification. Default: false</td>
  </tr>
  <tr>
    <td class="tg-lboi">resolveHostnames</td>
    <td class="tg-lboi">Set this to true to resolve hostnames against DNS. Default: false</td>
  </tr>
  <tr>
    <td class="tg-lboi">signatureAlgorithm</td>
    <td class="tg-lboi">Signature algorithm (for RSA default is SHA256withRSA, for EC its SHA256withECDSA)</td>
  </tr>
  <tr>
    <td class="tg-lboi">useEllipticCurves</td>
    <td class="tg-lboi">If set to true use elliptic curves instead of RSA. Default is false (since 1.7)</td>
  </tr>
  <tr>
    <td class="tg-lboi">ellipticCurve</td>
    <td class="tg-lboi">The curve to be used. Default is: NIST P-384 (since 1.7)</td>
  </tr>
</tbody>
</table>

#### Node certificates

To generate node certificates, add the node name, the Distinguished Name, the hostname(s), and/or the IP address(es) in the `nodes` section:

```yml
nodes:
  - name: node1
    dn: CN=test.example.com,OU=Dev,O=EMCA Software,C=Poland
    dns: test.example.com
    ip: 10.0.2.1
  - name: node2
    dn: CN=node2.example.com,OU=Dev,O=EMCA Software,C=Poland
    dns: 
      - node2.example.com
      - es2.example.com
    ip: 
      - 10.0.2.1
      - 192.168.2.1
  - name: node3
    dn: CN=node3.example.com,OU=Dev,O=EMCA Software,C=Poland
    dns: node3.example.com
```

Generated files:

  - `[nodename].crt` - Node certificate
  - `[nodename].key` - Private key of the node certificate
  - `[nodename]_http.crt` - REST certificate, only generated if reuseTransportCertificatesForHttp is false
  - `[nodename]_logserver_config_snippet.yml` - Logserver Guard configuration snippet for this node, add this to opensearch.yml

Options:

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-lboi{border-color:inherit;text-align:left;vertical-align:middle}
.tg .tg-fymr{border-color:inherit;font-weight:bold;text-align:left;vertical-align:top}
</style>
<table class="tg" style="undefined;table-layout: fixed; width: 691px">
<colgroup>
<col style="width: 120px">
<col style="width: 471px">
</colgroup>
<thead>
  <tr>
    <th class="tg-fymr">Name</th>
    <th class="tg-fymr">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-lboi">name</td>
    <td class="tg-lboi">Name of the node, will become part of the filenames. Mandatory</td>
  </tr>
  <tr>
    <td class="tg-lboi">dn</td>
    <td class="tg-lboi">The Distinguished Name of the certificate. If you have special characters in the DN, you need to quote them correctly. Mandatory</td>
  </tr>
  <tr>
    <td class="tg-lboi">dns</td>
    <td class="tg-lboi">The hostname(s) this certificate is valid for. Should match the hostname of the node. Optional, but recommended.</td>
  </tr>
  <tr>
    <td class="tg-lboi">ip</td>
    <td class="tg-lboi">The IP(s) this certificate is valid for. Optional. Prefer hostnames if possible.</td>
  </tr>
</tbody>
</table>

### Admin and client certificates

To generate admin and client certificates, add the following lines to the configuration file:

```yml
clients:
  - name: spock
    dn: CN=spock.example.com,OU=Dev,O=EMCA Software,C=Poland
  - name: kirk
    dn: CN=kirk.example.com,OU=Dev,O=EMCA Software,C=Poland
    admin: true
```

Generated files:

  - `[name].crt` - Client certificate
  - `[name].key` - Private key of the client certificate
  - `client-certificates.readme` - Contains the auto-generated passwords for the certificates

Options:

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-lboi{border-color:inherit;text-align:left;vertical-align:middle}
.tg .tg-fymr{border-color:inherit;font-weight:bold;text-align:left;vertical-align:top}
</style>
<table class="tg" style="undefined;table-layout: fixed; width: 691px">
<colgroup>
<col style="width: 120px">
<col style="width: 471px">
</colgroup>
<thead>
  <tr>
    <th class="tg-fymr">Name</th>
    <th class="tg-fymr">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-lboi">name</td>
    <td class="tg-lboi">Name of the certificate, will become part of the file name</td>
  </tr>
  <tr>
    <td class="tg-lboi">dn</td>
    <td class="tg-lboi">The complete Distinguished Name of the certificate. If you have special characters in the DN, you need to quote them correctly</td>
  </tr>
  <tr>
    <td class="tg-lboi">admin</td>
    <td class="tg-lboi">If set to true, this certificate will be marked as an admin certificate in the generated configuration snippet.</td>
  </tr>
</tbody>
</table>

Note that you need to mark at least one client certificate as an admin certificate.

### Documentation link

To update the link that is inserted into the generated readme files:

`documentationLink: "https://link-to-docs.com"`

Options:

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-lboi{border-color:inherit;text-align:left;vertical-align:middle}
.tg .tg-fymr{border-color:inherit;font-weight:bold;text-align:left;vertical-align:top}
</style>
<table class="tg" style="undefined;table-layout: fixed; width: 691px">
<colgroup>
<col style="width: 120px">
<col style="width: 471px">
</colgroup>
<thead>
  <tr>
    <th class="tg-fymr">Name</th>
    <th class="tg-fymr">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-lboi">documentationLink</td>
    <td class="tg-lboi">Link to the site. Optional.</td>
  </tr>
</tbody>
</table>

### Adding certificates after the first run

You can always add more node- or admin certificates as you need them after the initial run of the tool. As a precondition

  - the root CA and, if used, the intermediate certificates and keys must be present in the output folder
  - the password of the root CA and, if used, the intermediate CA must be present in the config file

If you use auto-generated passwords, copy them from the generated `root-ca.readme` file to the configuration file.

Certificates that have already been generated in a previous run of the tool will be left untouched unless you run the tool with the `-o,--overwrite` switch. In this case, existing files are overwritten. If you have chosen to auto-generate passwords, new keys with auto-generated passwords are created.

### Creating CSRs

If you just want to create CSRs to submit them to your local CA, you can omit the CA part of the config complete. Just define the `default`, `node`, and `client` section, and run the TLS tool with the `-csr` switch.

### Configuring ciphers for TLS settings

How to enable, disable and/or limit available ciphers for Logserver services.

#### Logserver database

Edit config file `/etc/elasticsearch/elasticsearch.yml`.

Example:

```yaml
logserverguard.ssl.transport.enabled_ciphers:
- TLS_AES_256_GCM_SHA384
- TLS_AES_128_GCM_SHA256
- TLS_CHACHA20_POLY1305_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256
- TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256

logserverguard.ssl.http.enabled_ciphers:
- TLS_AES_256_GCM_SHA384
- TLS_AES_128_GCM_SHA256
- TLS_CHACHA20_POLY1305_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256
- TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
```

After editing restart elasticsearch.service. Note that this settings should be updated on all cluster nodes.

#### Logserver GUI

Edit config file `/etc/kibana/kibana.yml`.

Example:

```yaml
server.ssl.cipherSuites:
- TLS_AES_256_GCM_SHA384
- TLS_AES_128_GCM_SHA256
- TLS_CHACHA20_POLY1305_SHA256
- ECDHE-ECDSA-AES256-GCM-SHA384
- ECDHE-RSA-AES256-GCM-SHA384
- ECDHE-ECDSA-CHACHA20-POLY1305
- ECDHE-RSA-CHACHA20-POLY1305
- ECDHE-ECDSA-AES128-GCM-SHA256
- ECDHE-RSA-AES128-GCM-SHA256
```

After editing restart kibana.service

#### Cerebro

Since 7.6.1 there is a default configuration for enabled algorithms on path `/opt/cerebro/conf/java.config`.

You can edit it and after restarting cerebro.service, changes will be applied.

##### 7.6.0 and before

1. To recreate current default behavior, create file `/opt/cerebro/conf/java.config` with content:

    ```conf
    security.useSystemPropertiesFile=false
    jdk.tls.ephemeralDHKeySize=2048
    jdk.certpath.disabledAlgorithms=MD2, SHA1, MD5, DSA, RSA keySize < 2048
    jdk.tls.disabledAlgorithms=DH keySize < 2048, TLSv1.1, TLSv1, SSLv3, SSLv2, TLS_RSA_WITH_AES_256_CBC_SHA256, TLS_RSA_WITH_AES_256_CBC_SHA, TLS_RSA_WITH_AES_128_CBC_SHA256, TLS_RSA_WITH_AES_128_CBC_SHA, TLS_RSA_WITH_AES_256_GCM_SHA384, TLS_RSA_WITH_AES_128_GCM_SHA256, DHE_DSS, RSA_EXPORT, DHE_DSS_EXPORT, DHE_RSA_EXPORT, DH_DSS_EXPORT, DH_RSA_EXPORT, DH_anon, ECDH_anon, DH_RSA, DH_DSS, ECDH, 3DES_EDE_CBC, DES_CBC, RC4_40, RC4_128, DES40_CBC, RC2, HmacMD5, TLS_DHE_RSA_WITH_AES_128_CBC_SHA, TLS_DHE_RSA_WITH_AES_256_CBC_SHA
    jdk.tls.legacyAlgorithms=
    ```

1. Edit `ExecStart` definition of `/usr/lib/systemd/system/cerebro.service` like so:

    ```conf
    ExecStart=/opt/cerebro/bin/cerebro "-Djava.security.properties=/opt/cerebro/conf/java.config" "-Dconfig.file=/opt/cerebro/conf/application.conf"
    ```

1. Reload systemd and restart cerebro.service

    ```bash
    systemctl daemon-reload
    systemctl reenable cerebro
    systemctl restart cerebro
    ```

#### E-doc

Since 7.6.1 there is a default configuration for enabled ciphers on path `/opt/e-doc/env.config`.

You can edit it and after restarting e-doc.service, changes will be applied.

##### 7.6.0 and before

1. To recreate current default behavior, create file `/opt/e-doc/env.config` with content:

    ```conf
    NODE_OPTIONS=--tls-cipher-list='TLS_AES_256_GCM_SHA384:TLS_CHACHA20_POLY1305_SHA256:TLS_AES_128_GCM_SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:DHE-RSA-AES256-SHA384:ECDHE-RSA-AES256-SHA256:DHE-RSA-AES256-SHA256:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!SRP:!CAMELLIA'
    ```

1. Edit `/usr/lib/systemd/system/e-doc.service`. Add following under `[Service]` section:

    ```conf
    EnvironmentFile=-/opt/e-doc/env.config
    ```

1. Reload systemd and restart e-doc.service

    ```bash
    systemctl daemon-reload
    systemctl reenable e-doc
    systemctl restart e-doc
    ```

## Network Probe (logstash)

Since 7.6.1 there is a default configuration for enabled algorithms on path `/etc/logstash/java.properties`.

Make sure there is a fallowing definition in `/etc/logstash/jvm.options`:

```conf
-Djava.security.properties=/etc/logstash/java.properties
```

You can edit it and after restarting logstash.service, changes will be applied.

##### 7.6.0 and before

1. To recreate current default behavior, create file `/etc/logstash/java.properties` with content:

    ```conf
    security.useSystemPropertiesFile=false
    jdk.tls.ephemeralDHKeySize=2048
    jdk.certpath.disabledAlgorithms=MD2, SHA1, MD5, DSA, RSA keySize < 2048
    jdk.tls.disabledAlgorithms=DH keySize < 2048, TLSv1.1, TLSv1, SSLv3, SSLv2, TLS_RSA_WITH_AES_256_CBC_SHA256, TLS_RSA_WITH_AES_256_CBC_SHA, TLS_RSA_WITH_AES_128_CBC_SHA256, TLS_RSA_WITH_AES_128_CBC_SHA, TLS_RSA_WITH_AES_256_GCM_SHA384, TLS_RSA_WITH_AES_128_GCM_SHA256, DHE_DSS, RSA_EXPORT, DHE_DSS_EXPORT, DHE_RSA_EXPORT, DH_DSS_EXPORT, DH_RSA_EXPORT, DH_anon, ECDH_anon, DH_RSA, DH_DSS, ECDH, 3DES_EDE_CBC, DES_CBC, RC4_40, RC4_128, DES40_CBC, RC2, HmacMD5, TLS_DHE_RSA_WITH_AES_128_CBC_SHA, TLS_DHE_RSA_WITH_AES_256_CBC_SHA
    jdk.tls.legacyAlgorithms=
    ```

1. And add to `/etc/logstash/jvm.options`:

    ```conf
    -Djava.security.properties=/etc/logstash/java.properties
    ```

1. After restarting logstash.service, changes will be applied.

#### Masteragent

Since 7.6.1 Masteragent has a predefined strong ciphers already set. Updating is recommended.

## Browser layer encryption

Secure Sockets Layer (SSL) and Transport Layer Security (TLS) provide encryption for data-in-transit. While these terms are often used interchangeably, ITRS Log Analytics GUI supports only TLS, which supersedes the old SSL protocols. Browsers send traffic to ITRS Log Analytics  GUI and ITRS Log Analytics GUI sends traffic to Elasticsearch database. These communication channels are configured separately to use TLS. TLS requires X.509 certificates to authenticate the communicating parties and perform encryption of data-in-transit. Each certificate contains a public key and has an associated — but separate — private key; these keys are used for cryptographic operations. ITRS Log Analytics  GUI supports certificates and private keys in PEM format and supports the TLS 1.3 version.

### Configuration steps

1. Obtain a server certificate and private key for ITRS Log Analytics GUI.

   Kibana will need to use this "server certificate" and the corresponding private key when receiving connections from web browsers.

   When you obtain a server certificate, you must set its subject alternative name (SAN) correctly to ensure that modern web browsers with hostname verification will trust it. You can set one or more SANs to the ITRS Log Analytics GUI server’s fully qualified domain name (FQDN), hostname, or IP address. When choosing the SAN, you should pick whichever attribute you will be using to connect to Kibana in your browser, which is likely the FQDN in a production environment.

2. Configure ITRS Log Analytics GUI to access the server certificate and private key.

   `vi /etc/kibana/kibana.yml`

   ```bash
   server.ssl.enabled: true
   server.ssl.supportedProtocols: ["TLSv1.3"]
   server.ssl.certificate: "/path/to/kibana-server.crt"
   server.ssl.key: "/path/to/kibana-server.key"
   ```

3. Set HTTPS in configuration file for the License server:

  ```bash
  vi /opt/license-service/license-service.conf
  ```

  ```bash
  elasticsearch_connection:
    hosts: ["els_host_IP:9200"]

    username: license
    password: "license_user_password"

    https: true
  ```

## Building a cluster

### Node roles

Every instance of the Elasticsearch server is called a *node*.
A collection of connected nodes is called a *cluster*.
All nodes know about all the other nodes in the cluster
and can forward client requests to the appropriate node.

Besides that, each node serves one or more purposes:

- Master-eligible node - A node that has a *node.master* set to true (default), which makes it eligible to be elected as the master node, which controls the cluster
- Data node - A node that has a *node.data* set to true (default). Data nodes hold data and perform data-related operations such as CRUD, search, and aggregations
- Client node - A client node has both *node.master* and *node.data* set to false. It can neither hold data nor become the master node. It behaves as a "*smart router*" and is used to forward cluster-level requests to the master node and data-related requests (such as search) to the appropriate data nodes
- Tribe node - A tribe node, configured via the *tribe.** settings, is a special type of client node that can connect to multiple clusters and perform search and other operations across all connected clusters.

### Naming convention

Elasticsearch requires little configuration before going to work.

The following settings must be considered before going to production:

- **path.data** and **path.logs** - default locations of these files are
`/var/lib/elasticsearch` and `/var/log/elasticsearch`.
- **cluster.name** - A node can only join a cluster when it shares its
`cluster.name` with all the other nodes in the cluster. The default name
is "elasticsearch", but you should change it to an appropriate name that describes the purpose of the cluster. You can do this in the `/etc/elasticsearch/elasticsearch.yml` file.
- **node.name** - By default, Elasticsearch will use the first seven characters of the randomly
generated UUID as the node ID. Node ID is persisted and does not change when a node restarts.
It is worth configuring a more human-readable name: `node.name: prod-data-2`
in file `/etc/elstaicsearch/elasticsearch.yml`
- **network.host** - parameter specifying network interfaces to which Elasticsearch can bind. The default is `network.host`: ["\_local\_", "\_site\_"].
- **discovery** - Elasticsearch uses a custom discovery implementation called "Zen Discovery".
There are two important settings:
  - `discovery.zen.ping.unicast.hosts` - specify a list of other nodes in the cluster that are likely to be live and contactable;
  - `discovery.zen.minimum_master_nodes` - to prevent data loss, you can configure this setting so that each master-eligible node knows the minimum number of master-eligible nodes that must be visible to form a cluster.
- **heap size** - By default, Elasticsearch tells the JVM to use a heap with a minimum (Xms) and maximum (Xmx)
size of 1 GB. When moving to production, it is important to configure heap size to ensure that
Elasticsearch has enough heap available

### Config files

To configure the Elasticsearch cluster you  must specify some parameters
in the following configuration files on every node that will be connected to the cluster:

- `/etc/elsticsearch/elasticserach.yml`:
  - `cluster.name:name_of_the_cluster` - same for every node;
  - `node.name:name_of_the_node` - uniq for every node;
  - `node.master:true_or_false`
  - `node.data:true_or_false`
  - `network.host:["_local_","_site_"]`
  - `discovery.zen.ping.multicast.enabled`
  - `discovery.zen.ping.unicast.hosts`
- `/etc/elsticsearch/log4j2.properties`:
  - `logger: action: DEBUG` - for easier debugging.

### TLS Certificates

To generate TLS certificates for each node of the cluster, you can check the `logserver-cluster.yml` config that is provided with the `tlstool.sh`.

```bash
cd /usr/share/elasticsearch/utils/tlstool
bash tlstool.sh -c config/logserver-cluster.yml -ca -crt
```

### Example setup

Example of the Elasticsearch cluster configuration:

- file `/etc/elasticsearch/elasticsearch.yml`:

  cluster.name: tm-lab
  node.name: "elk01"
  node.master: true
  node.data: true
  network.host: 127.0.0.1,10.0.0.4
  http.port: 9200
  discovery.zen.ping.multicast.enabled: false
  discovery.zen.ping.unicast.hosts: ["10.0.0.4:9300","10.0.0.5:9300","10.0.0.6:9300"]

- to start the Elasticsearch cluster execute the command:

    ```bash
    systemctl restart elasticsearch
    ```

- to check the status of the Elasticsearch cluster execute the command:
    - check the Elasticsearch cluster nodes status via TCP port:
  
        ```bash
         curl -XGET '127.0.0.1:9200/_cat/nodes?v'

           host            ip   heap.percent ram.percent load node.role master name
           10.0.0.4   10.0.0.4     18           91      0.00 -        -       elk01
           10.0.0.5   10.0.0.5     66           91      0.00 d        *       elk02
           10.0.0.6   10.0.0.6     43           86      0.65 d        m       elk03
           10.0.0.7   10.0.0.7     45           77      0.26 d        m       elk04
        ```

    - check the status of the Elasticsearch cluster via the log file:

        ```bash
        tail -f /var/log/elasticsearch/tm-lab.log (cluster.name)
        ```

### Adding a new node to the existing cluster

Install the new ITRS Log Analytics instance. The description of the installation can be found in the chapter "First Configuration Steps"

Change the following parameters in the configuration file:

- `cluster.name:`name_of_the_cluster same for every node;
- `node.name:`name_of_the_node uniq for every node;
- `node.master:`true_or_false
- `node.data:`true_or_false
- `discovery.zen.ping.unicast.hosts:` [ "10.0.0.4:9300", "10.0.0.5:9300", "10.0.0.6:9300" ] - IP addresses and instances of nodes in the cluster.

If you add a node with the role `data`, delete the contents of the `path.data` directory, by default in `/var/lib/elasticsearch`

Restart the Elasticsearch instance of the new node:

```bash
systemctl restart elasticsearch
```
## Disk-based shard allocation

Since version **7.4.3** of Logserver a feature was added to keep you informed about your disk usage. Disk-based shard allocation settings are used to determine the GUI behaviour.

![your cluster is running low on disk space low stage](/media/media/01_low_water.png)

![your cluster is running low on disk space high stage](/media/media/02_high_water.png)

![your cluster is running low on disk space flood stage](/media/media/03_flood_water.png)

These labels will appear when a certain watermark level is exceeded. Its function is to inform you to take action. Maybe tweak your retention settings or add disk space to your servers.

With the "FLOOD STAGE", non-administrative users will lose the ability to log into GUI, and those already logged in will be redirected to the status page. An administrator will still be able to browse and will have a chance to take action to fix the situation. 

This is because with "FLOOD STAGE", the system switches into a read-only mode. No new documents can be created or updated.

### What is a watermark

1. Low stage

    Controls the low watermark for disk usage. When exceeded Logserver will not allocate shards to that node. This setting does not affect the primary shards of newly-created indices but will prevent their replicas from being allocated.

2. High stage

    Controls the high watermark. When exceeded Logserver will attempt to relocate shards away from a node whose disk exceeds it. This setting affects the allocation of all shards, whether previously allocated or not.

3. Flood stage

    **This setting is a last resort to prevent nodes from running out of disk space - which should be at all costs avoided.**

    Controls the flood stage watermark. Logserver enforces a read-only index block (index.blocks.read_only_allow_delete) on every index that has one or more shards allocated on the node, and that has at least one disk exceeding the flood stage. The index block is automatically released when the disk utilization falls below the high watermark.

**Even if you are running Logserver in a single node environment, configuring the above is highly recommended.**

While the GUI will always inform you about your disk usage, to take advantage of the above benefits you will need to configure the thresholds yourself **especially if you are updating from an earlier Logserver version**.

### Configuring watermark stages

1. On fresh **7.4.3** or newer installations of Logserver these are the default watermark values:

    - low: 95%
    - high: 97%
    - flood: 99%

2. To change them, you can use Logserver API like in the following example:

    ```bash
    curl localhost:9200/_cluster/settings -XPUT -H 'content-type: application/json' -d '{
      "persistent": {
        "cluster.routing.allocation.disk.threshold_enabled": "true",
        "cluster.routing.allocation.disk.watermark.flood_stage": "10gb",
        "cluster.routing.allocation.disk.watermark.high": "25gb",
        "cluster.routing.allocation.disk.watermark.low": "50gb"
      }
    }'
    ```

    With that the "low stage" starts when the disk space for Logserver indices falls below the 50 GB mark; "high" below 25 GB and "flood" below 10 GB.

3. You can also use percentages for that **but not both - you cannot mix byte values and percentages**.

4. You can also modify Logserver configuration file `/etc/elasticsearch/elasticsearch.yml`:

    ```yaml
    cluster.routing.allocation.disk.threshold_enabled: true
    cluster.routing.allocation.disk.watermark.low: "50gb"
    cluster.routing.allocation.disk.watermark.high: "25gb"
    cluster.routing.allocation.disk.watermark.flood_stage: "10gb"
    ```

    Take in mind you will have to change those values on all of your cluster nodes this way. Restart is not required as API was used earlier.

    **Important!** Thanks to that, settings will be protected against a state failure.

### Flood stage and read-only mode

When the cluster reaches the "flood stage", it is automatically put into a read-only mode. It prevents a cluster failure - **reaching 100% disk usage on a Logserver cluster is a critical issue!** 

The best way to remove the read-only mode is to make more disk space available for the cluster - either by adding more space or removing data (indices) from it. When the cluster reaches the "low stage" or below, it will automatically switch from the read-only mode.

Adjusting the levels with the above API examples to suit your installation is another option.

Disabling the threshold checking is not recommended! Also, changing the "threshold_enabled" setting to "false" does not turn the read-only mode off automatically!

## Authentication with Active Directory

The AD configuration should be done in the `/etc/elasticsearch/properties.yml`
file.

Below is a list of settings to be made in the `properties.yml` file
(the commented section in the file for the AD settings to
start working, this fragment should be uncommented):

 ```yaml
ldaps:  
  - name: "example.com"  # domain that is configured 
    host: "127.0.0.1,127.0.0.2"  # list of server for this domain  
    #port: 389 # optional, default 389 for unencrypted session or 636 for encrypted sessions  
    ssl_enabled: false  # optional, default true 
    #ssl_trust_all_certs: true # optional, default false 
    #ssl.keystore.file: "path" # path to the truststore store 
    #ssl.keystore.password: "path" # password to the trusted certificate store 
    bind_dn: [admin@example.com] # account name administrator 
    bind_password: "password" # password for the administrator account 
    search_user_base_DN: "OU=lab,DC=example,DC=com" # search for the DN user tree database 
    #user_id_attribute: "uid # search for a user attribute optional, by default "uid" 
    #search_groups_base_DN: "OU=lab,DC=example,DC=com" # group database search. This is a catalog main, after which the groups will be sought. 
    #unique_member_attribute: "uniqueMember" # optional, default "uniqueMember" 
    connection_pool_size: 10 # optional, default 30 
    connection_timeout_in_sec: 10 # optional, default 1 
    request_timeout_in_sec: 10 # optional, default 1* 
    cache_ttl_in_sec: 60 # optional, default 0 - cache disabled 
    #authentication_only: true    # optional ignore role-mapping settings 
    #default_authentication_roles: [ "roleName1", "roleName2" ]      # roles asigned to new users authenticating using this LDAP server, used when authentication_only = true
 ```

If we want to configure multiple domains, then in this configuration
file we copy the \# LDAP section below and configure it for the next
domain.

Below is an example of how an entry for 2 domains should look
like. (It is important to take the interpreter to read these values
​​correctly).

```yaml
ldaps:
  - name: "example1.com" #DOMAIN 1
    host: "127.0.0.1,127.0.0.2"
    bind_dn: "esauth@example1.com"
    bind_password: "password"
    search_user_base_DN: "cn=Users,DC=example1,DC=com"
    ssl_enabled: false
  - name: "example2.com" #DOMAIN 2
    host: "127.0.0.1,127.0.0.2"
    bind_dn: "esauth@example2.com"
    bind_password: "password"
    search_user_base_DN: "cn=Users,DC=example2,DC=com"
    ssl_enabled: false
```

After completing the LDAP section entry in the `properties.yml` file,
save the changes and reload the module with the below command:

```bash
curl -sS -uUSER:PASSWORD localhost:9200/_logserver/auth/reload -XPOST
```

Example:

```bash
curl -sS -ulogserver:logserver localhost:9200/_logserver/auth/reload -XPOST
```

### Configure SSL support for AD authentication

Open the certificate manager on the AD server.

![](/media/media/image78_js.png)

Select the certificate and open it

![](/media/media/image79_js.png)

Select the option of copying to a file in the Details tab

![](/media/media/image80_js.png)

Click the Next button

![](/media/media/image81.png)

Keep the setting as shown below and click Next

![](/media/media/image83.png)

Keep the setting as shown below and click Next.

![](/media/media/image82.png)

Give the name a certificate

![](/media/media/image84.png)

After the certificate is exported, this certificate should be imported
into a trusted certificate file that will be used by the Elasticsearch
plugin.

To import a certificate into a trusted certificate file, a tool called
„keytool.exe" is located in the JDK installation directory.

Use the following command to import a certificate file:

```bash
 keytool -import -alias adding_certificate_keystore -file certificate.cer -keystore certificatestore
```

The values `certificat.cer` and `certificationstore` should be changed accordingly.

By doing this, he will ask you to set a password for the trusted
certificate store. Remember this password, because it must be set in
the configuration of the Elasticsearch plugin. The following settings
must be set in the `properties.yml` configuration for
SSL:

```yaml
 ssl.keystore.file: "<path to the trust certificate store>"
 ssl.keystore.password: "<password to the trust certificate store>"
```

### Role mapping

In the `/etc/elasticsearch/properties.yml` configuration file you can find
a section for configuring role mapping:

```bash
# LDAP ROLE MAPPING FILE
# rolemapping.file.path: /etc/elasticsearch/role-mappings.yml
```

This variable points to the file `/etc/elasticsearch/role-mappings.yml`
Below is the sample content for this file:

```yaml
# admin - superuser group
admin:
  - "CN=Admins,CN=Builtin,DC=example,DC=com"

gui-access:
  - "CN=Admins,CN=Builtin,DC=example,DC=com"
```

**Attention. The role you define in the `role-mapping.yml` file must be created in the ITRS Log Analytics.**

How to the mapping mechanism work? \
An AD user logs in to ITRS Log Analytics. In the application, there is a `gui-access` role, which through the file `role-mapping.yml` binds to the name of an AD group of which the user is a member. Additionally, this AD group binds to the ITRS Log Analytics admin role, which points to permission granted to the user in the application.

Similarly, the mechanism will work for any other role in the application. Important in this configuration is to add every AD group to `gui-access` which grants permission to log in and at least one more role which grants permission to some data.

The `gui-access` role is not visible in GUI, it's only used to grant permission to log in.

If field `authentication_only` is `true`, user roles will not be mapped and they will be taken from the `default_authentication_roles` field. When the `default_authentication_roles` field is not added in properties.yaml, a user without a role will be created.

Below is a screenshot of the console on which are marked accounts that were created by users logging in from AD

![](/media/media/image85_js.png)

If you map roles from several domains, for example, dev.example1.com, and dev.example2.com then in the User List we will see which user from which domain with which role logged in ITRS Log Analytics.

### Password encryption

For security reasons, you can provide the encrypted password for Active Directory integration.\
To do this use *pass-encrypter.sh* script that is located in the *Utils* directory in the installation folder.

1. Installation of *pass-encrypter*

    ```bash
    cp -pr /instalation_folder/elasticsearch/pass-encrypter /usr/share/elasticsearch/
    ```

1. Use *pass-encrypter*

    ```conf
    /usr/share/elasticsearch/utils/pass-encrypter/pass-encrypter.sh

    Enter the string for encryption :
    new_password
    Encrypted string : MTU1MTEwMDcxMzQzMg==1GEG8KUOgyJko0PuT2C4uw==
    ```

## Authentication with Radius

To use the Radius protocol, install the latest available version of ITRS Log Analytics.

### Configuration

The default configuration file is located at /etc/elasticsearch/properties.yml:

```yaml
# Radius opts
#radius.host: "10.4.3.184"
#radius.secret: "querty1q2ww2q1"
#radius.port: 1812
```

Use appropriate secret based on config file in Radius server. The secret is configured on `clients.conf` in the Radius server.

In this case, since the plugin will try to do Radius auth, the client IP address should be the IP address where the Elasticsearch is deployed.

Every user by default at present gets the admin role

## Authentication with LDAP

To use OpenLDAP authorization, install or update ITRS Log Analytics too at least 7.0.2.

### Configuration

The default configuration file is located at `/etc/elasticsearch/properties.yml`:

- ldap_groups_search  - Enable Open LDAP authorization. The `ldap_groups_search` switch with true/false values.

- search filter - you can define `search_filter` for each domain. When polling the LDAP / AD server, the placeholder is changed to the `userId` (everything before @domain) of the user who is trying to log in. Sample search_filter:

  ```bash
  search_filter: "(&(objectClass=inetOrgPerson)(cn=%s))"
  ```

  If no search_filter is given, the default will be used:

  ```bash
  (&(&(objectCategory=Person)(objectClass=User))(samaccountname=%s))
  ```

- max_connections - for each domain (must be> = 1), this is the maximum number of connections that will be created with the LDAP / AD server for a given domain. Initially, one connection is created, if necessary another, up to the maximum number of connections set. If max_connections is not given, the default value = 10 will be used.

- ldap_groups_search - filter will be used to search groups on the AD / LDAP server to which the user is trying to log in. An example of groups_search_filter that works quite universally is:

  ```bash
  groups_search_filter: "(|(uniqueMember=%s)(member=%s))"
  ```

  Sample configuration:

  ```bash
  licenseFilePath: /usr/share/elasticsearch/
  
  ldaps:
      
      - name: "dev.it.example.com"
        host: "192.168.0.1"
        port: 389                                                  # optional, default 389
        #ssl_enabled: false                                        # optional, default true
        #ssl_trust_all_certs: true                                 # optional, default false
        bind_dn: "Administrator@dev2.it.example.com"                     
        bind_password: "Buspa#mexaj1"                                 
        search_user_base_DN: "OU=lab,DC=dev,DC=it,DC=example,DC=pl"
        search_filter: "(&(objectClass=inetOrgperson)(cn=%s))"     # optional, default "(&(&(objectCategory=Person)(objectClass=User))(samaccountname=%s))"
        user_id_attribute: "uid"                                   # optional, default "uid"
        search_groups_base_DN: "OU=lab,DC=dev,DC=it,DC=example,DC=pl" # base DN, which will be used for searching user's groups in LDAP tree
        groups_search_filter: "(member=%s)"                        # optional, default (member=%s), if ldap_groups_search is set to true, this filter will be used for searching user's membership of LDAP groups
        ldap_groups_search: false                                  # optional, default false - user groups will be determined basing on user's memberOf attribute
        unique_member_attribute: "uniqueMember"                    # optional, default "uniqueMember"
        max_connections: 10                                        # optional, default 10
        connection_timeout_in_sec: 10                              # optional, default 1
        request_timeout_in_sec: 10                                 # optional, default 1
        cache_ttl_in_sec: 60                                       # optional, default 0 - cache disabled
  
  ```

    When the password is longer than 20 characters, we recommend using our pass-encrypter, otherwise, the backslash must be escaped with another backslash. Endpoint `role-mapping/_reload` has been changed to `_role-mapping/reload`. This is a unification of API conventions, following Elasticsearch conventions.

## Configuring Single Sign On (SSO)

To configure SSO, the system should be accessible by domain name URL, not IP address or localhost.

**Correct:** https://loggui.com:5601/login <br>
**Wrong:** https://localhost:5601/login, https://10.0.10.120:5601/login


The configuration description described below is based on:

- AD Domain / Realm: `example.com`

- AD IP Address: `192.168.3.111`

- GUI Url: `loggui.com`


To enable SSO on your system, follow the steps below.

### Configuration steps

1. Create a **User** Account for Elasticsearch auth plugin <br>
   In this step, a Kerberos Principal representing the Elasticsearch auth plugin is created on the Active Directory. The principal name would be `name@EXAMPLE.COM`, while the `EXAMPLE.COM` is the administrative name of the realm.<br><br>

   Create a User in AD. Set "Account never expires" and enable support for Kerberos encryption as shown below.

   ![](/media/media/image107_js.png)
   <br>

1. Define the Service Principal Name (SPN) and Create a keytab file for it

    Use the following command to create the keytab file identyfying the SPN:

    ```bash
      C:> ktpass -out c:\Users\Administrator\esauth.keytab -princ HTTP/loggui.com@EXAMPLE.COM -mapUser esauth -mapOp set -pass 'Sprint$123' -crypto ALL -pType KRB5_NT_PRINCIPAL
    ```

    Details of the used switches:


    - `-out` - path to the keytab file

    - `-mapUser` - name of the previously created AD user. It might need to be preceded with pre-Windows 2000 logon if user cannot be found (e.g. `EXAMPLE\esauth` on the screenshot).

    - `-princ` - service principal name. Must start with uppercase HTTP/ and must end with uppercase domain after the @ sign. Will be used later to configure principal.

    - `-pass` - password that secures the keytab file itself (not connected user's password!). Will be used later to configure principal's password.

    For more details about the `ktpass tool`, please refer to the official documentation: [ktpass details](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/ktpass).

    The `esauth.keytab` file should be placed on your elasticsearch node - preferably `/etc/elasticsearch/` with  read permissions for elasticsearch user:

    ```bash
    chmod 640 /etc/elasticsearch/esauth.keytab
    chown elasticsearch: /etc/elasticsearch/esauth.keytab
    ```

    <br>

1. Create a file named *krb5Login.conf*:

    ```bash
      com.sun.security.jgss.initiate {
          com.sun.security.auth.module.Krb5LoginModule required
          principal="HTTP/loggui.com@EXAMPLE.COM"
          useKeyTab=true
          keyTab=/etc/elasticsearch/esauth.keytab
          storeKey=true
          debug=true;
        };
      com.sun.security.jgss.krb5.accept {
        com.sun.security.auth.module.Krb5LoginModule required
        principal="HTTP/loggui.com@EXAMPLE.COM"
        useKeyTab=true
        keyTab=/etc/elasticsearch/esauth.keytab
        storeKey=true
        debug=true;
      };
    ```

      The principal user and keyTab location should be changed as per the values created in Step 2. Make sure the domain is in **UPPERCASE** as shown above. \
      The `krb5Login.conf` file should be placed on your elasticsearch node, for   instance, `/etc/elasticsearch/` with read permissions for the elasticsearch user:

      ```bash
      sudo chmod 640 /etc/elasticsearch/krb5Login.conf
      sudo chown elasticsearch: /etc/elasticsearch/krb5Login.conf
      ```
    
      <br>

1. Uncomment and edit JVM arguments, in `/etc/elasticsearch/jvm.options.d/single-sign-logon.options` as shown below:
    ```
    -Dsun.security.krb5.debug=false \
    -Djava.security.krb5.realm=**EXAMPLE.COM** \
    -Djava.security.krb5.kdc=**192.168.3.111** \
    -Djava.security.auth.login.config=/etc/elasticsearch/krb5Login.conf \
    -Djavax.security.auth.useSubjectCredsOnly=false
    ```
    Change the `.krb5.realm` and `.krb5.kdc` to the appropriate values. `Realm` is defined as used domain (must be in UPPERCASE) realm and `.kdc` is AD's IP address. Those JVM arguments have to be set for the Elasticsearch server.
  
    <br>

1. Authentication options if ```authentication_only: true``` is set

   If a user does not exist, Logserver will create the user without a role.
   Role in `role-mapping.yml` would be ignored and role `gui-access` from ```default_authentication_roles: ["gui-access"]``` will be assigned.
   <br>

1. Add the following additional (sso.domain, service_principal_name, service_principal_name_password) settings for LDAP in properties.yml file:

   ```yaml
   sso.domain: "example.com"
   ldaps:
    - name: "example.com"
        host: "IP_address"
        port: 389                                      # optional, default 389
        ssl_enabled: false                             # optional, default    true
        ssl_trust_all_certs: false                     # optional, default false
        bind_dn: "esauth@example.com"                  # optional, skip for anonymous bind
        bind_password: "password"                      # optional, skip for anonymous bind (AD admin's password)
        search_user_base_DN: "cn=Users,DC=example,DC=com"
        user_id_attribute: "uid"                       # optional, default "uid"
        unique_member_attribute: "uniqueMember"        # optional, default "uniqueMember"
        
        service_principal_name: "HTTP/loggui.com@EXAMPLE.COM" # principal name used while generating the keytab file
        service_principal_name_password: "Sprint$123" # -pass used during keytab creation

   ```

   Note: At this moment, SSO works for only a single domain. So you have to mention for what domain SSO should work in the above property `sso.domain` - in this example it should be "example.com".
   <br>

1. After completing the LDAP section entry in the properties.yml file, save the changes and send a request  for reload authentication  data with the command:

   ```bash
   curl -sS -u username:password localhost:9200/_logserver/auth/reload -XPOST
   ```

   <br>

1. Enable the SSO feature in the `kibana.yml` file:

   ```bash
   login.sso_enabled: true
   ```

   <br>

1. After that Kibana has to be restarted:

   ```bash
   sudo systemctl restart kibana.service
   ```

   <br>

### Client (Browser) Configuration

#### Internet Explorer configuration

1. Go to `Internet Options` from the `Tools` menu and click on `Security` Tab:

    ![](/media/media/image108.png)

1. Select `Local intranet`, click on `Site` -> `Advanced` -> Provide correct URL -> Click `Add`:

    ![](/media/media/image109_js.png)

    After adding the site click close.

1. Click on the custom level and select the option as shown below:

    ![](/media/media/image110_js.png)

#### Chrome configuration

For Chrome, the settings are taken from the IE browser.

#### Firefox Configuration

Update the following config:

![](/media/media/image111_js.png)

### KBC error codes

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-qahb{border-color:inherit;font-weight:bold;text-align:left;vertical-align:middle}
.tg .tg-0pky{border-color:inherit;text-align:left;vertical-align:top}
</style>
<table class="tg" style="undefined;table-layout: fixed; width: 666px">
<colgroup>
<col style="width: 160px">
<col style="width: 506px">
</colgroup>
<thead>
  <tr>
    <th class="tg-qahb">KDC error codes</th>
    <th class="tg-qahb">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">0</td>
    <td class="tg-0pky">No error<br></td>
  </tr>
  <tr>
    <td class="tg-0pky">1</td>
    <td class="tg-0pky">Client entry is expired</td>
  </tr>
  <tr>
    <td class="tg-0pky">2</td>
    <td class="tg-0pky">Server entry is expired</td>
  </tr>
  <tr>
    <td class="tg-0pky">3</td>
    <td class="tg-0pky">Protocol version is not supported</td>
  </tr>
  <tr>
    <td class="tg-0pky">4</td>
    <td class="tg-0pky">Client key is encrypted in an old master key</td>
  </tr>
  <tr>
    <td class="tg-0pky">5</td>
    <td class="tg-0pky">Server key is encrypted in an old master key</td>
  </tr>
  <tr>
    <td class="tg-0pky">6</td>
    <td class="tg-0pky">Client is not defined in the security registry</td>
  </tr>
  <tr>
    <td class="tg-0pky">7</td>
    <td class="tg-0pky">Server is not defined in the security registry</td>
  </tr>
  <tr>
    <td class="tg-0pky">8</td>
    <td class="tg-0pky">Principal is not unique in the security registry</td>
  </tr>
  <tr>
    <td class="tg-0pky">9</td>
    <td class="tg-0pky">No key is available for the principal</td>
  </tr>
  <tr>
    <td class="tg-0pky">10</td>
    <td class="tg-0pky">Ticket is not eligible for postdating</td>
  </tr>
  <tr>
    <td class="tg-0pky">11</td>
    <td class="tg-0pky">Ticket is never valid</td>
  </tr>
  <tr>
    <td class="tg-0pky">12</td>
    <td class="tg-0pky">Request rejected due to KDC policy</td>
  </tr>
  <tr>
    <td class="tg-0pky">13</td>
    <td class="tg-0pky">Request option is not supported</td>
  </tr>
  <tr>
    <td class="tg-0pky">14</td>
    <td class="tg-0pky">Encryption type is not supported</td>
  </tr>
  <tr>
    <td class="tg-0pky">15</td>
    <td class="tg-0pky">Checksum type is not supported</td>
  </tr>
  <tr>
    <td class="tg-0pky">16</td>
    <td class="tg-0pky">Preauthentication type is not supported</td>
  </tr>
  <tr>
    <td class="tg-0pky">17</td>
    <td class="tg-0pky">Transited data type is not supported</td>
  </tr>
  <tr>
    <td class="tg-0pky">18</td>
    <td class="tg-0pky">Client account is revoked</td>
  </tr>
  <tr>
    <td class="tg-0pky">19</td>
    <td class="tg-0pky">Server account is revoked</td>
  </tr>
  <tr>
    <td class="tg-0pky">20</td>
    <td class="tg-0pky">TGT is revoked</td>
  </tr>
  <tr>
    <td class="tg-0pky">21</td>
    <td class="tg-0pky">Client account is not valid yet</td>
  </tr>
  <tr>
    <td class="tg-0pky">22</td>
    <td class="tg-0pky">Server account is not valid yet</td>
  </tr>
  <tr>
    <td class="tg-0pky">23</td>
    <td class="tg-0pky">Password is expired</td>
  </tr>
  <tr>
    <td class="tg-0pky">24</td>
    <td class="tg-0pky">Preauthentication failed</td>
  </tr>
  <tr>
    <td class="tg-0pky">25</td>
    <td class="tg-0pky">Preauthentication required</td>
  </tr>
  <tr>
    <td class="tg-0pky">26</td>
    <td class="tg-0pky">Supplied authentication ticket is not for the requested server</td>
  </tr>
  <tr>
    <td class="tg-0pky">27</td>
    <td class="tg-0pky">Server requires user-to-user protocol</td>
  </tr>
  <tr>
    <td class="tg-0pky">31</td>
    <td class="tg-0pky">Decryption integrity check failed</td>
  </tr>
  <tr>
    <td class="tg-0pky">32</td>
    <td class="tg-0pky">Ticket is expired</td>
  </tr>
  <tr>
    <td class="tg-0pky">33</td>
    <td class="tg-0pky">Ticket is not valid yet</td>
  </tr>
  <tr>
    <td class="tg-0pky">34</td>
    <td class="tg-0pky">Request is a replay of a previous request</td>
  </tr>
  <tr>
    <td class="tg-0pky">35</td>
    <td class="tg-0pky">Supplied authentication ticket is not for the current realm</td>
  </tr>
  <tr>
    <td class="tg-0pky">36</td>
    <td class="tg-0pky">Ticket and authenticator do not match</td>
  </tr>
  <tr>
    <td class="tg-0pky">37</td>
    <td class="tg-0pky">Clock skew is too great</td>
  </tr>
  <tr>
    <td class="tg-0pky">38</td>
    <td class="tg-0pky">Incorrect network address</td>
  </tr>
  <tr>
    <td class="tg-0pky">39</td>
    <td class="tg-0pky">Protocol version mismatch</td>
  </tr>
  <tr>
    <td class="tg-0pky">40</td>
    <td class="tg-0pky">Invalid message type</td>
  </tr>
  <tr>
    <td class="tg-0pky">41</td>
    <td class="tg-0pky">Message stream has been modified</td>
  </tr>
  <tr>
    <td class="tg-0pky">42</td>
    <td class="tg-0pky">Message is out of order</td>
  </tr>
  <tr>
    <td class="tg-0pky">44</td>
    <td class="tg-0pky">Key version is not available</td>
  </tr>
  <tr>
    <td class="tg-0pky">45</td>
    <td class="tg-0pky">Service key is not available</td>
  </tr>
  <tr>
    <td class="tg-0pky">46</td>
    <td class="tg-0pky">Mutual authentication failed</td>
  </tr>
  <tr>
    <td class="tg-0pky">47</td>
    <td class="tg-0pky">Incorrect message direction</td>
  </tr>
  <tr>
    <td class="tg-0pky">48</td>
    <td class="tg-0pky">Alternative authentication method required</td>
  </tr>
  <tr>
    <td class="tg-0pky">49</td>
    <td class="tg-0pky">Incorrect message sequence number</td>
  </tr>
  <tr>
    <td class="tg-0pky">50</td>
    <td class="tg-0pky">Inappropriate checksum type</td>
  </tr>
  <tr>
    <td class="tg-0pky">60</td>
    <td class="tg-0pky">Generic error detected</td>
  </tr>
  <tr>
    <td class="tg-0pky">61</td>
    <td class="tg-0pky">Field is too long</td>
  </tr>
  <tr>
    <td class="tg-0pky">62</td>
    <td class="tg-0pky">Client certificate is not acceptable</td>
  </tr>
  <tr>
    <td class="tg-0pky">63</td>
    <td class="tg-0pky">KDC certificate is not trusted or does not meet requirements</td>
  </tr>
  <tr>
    <td class="tg-0pky">64</td>
    <td class="tg-0pky">Certificate signature not valid</td>
  </tr>
  <tr>
    <td class="tg-0pky">65</td>
    <td class="tg-0pky">Client Diffie-Hellman key parameters not accepted</td>
  </tr>
  <tr>
    <td class="tg-0pky">70</td>
    <td class="tg-0pky">Client certificate could not be verified</td>
  </tr>
  <tr>
    <td class="tg-0pky">71</td>
    <td class="tg-0pky">Client certificate chain validation error occurred</td>
  </tr>
  <tr>
    <td class="tg-0pky">72</td>
    <td class="tg-0pky">Client certificate chain contains a revoked certificate</td>
  </tr>
  <tr>
    <td class="tg-0pky">73</td>
    <td class="tg-0pky">Revocation status for the certificate chain could not be determined</td>
  </tr>
  <tr>
    <td class="tg-0pky">75</td>
    <td class="tg-0pky">Kerberos client name does not match name bound to the client certificate</td>
  </tr>
  <tr>
    <td class="tg-0pky">76</td>
    <td class="tg-0pky">Kerberos KDC name does not match name bound to the KDC certificate</td>
  </tr>
  <tr>
    <td class="tg-0pky">77</td>
    <td class="tg-0pky">Key purpose restricts certificate usage</td>
  </tr>
  <tr>
    <td class="tg-0pky">78</td>
    <td class="tg-0pky">Certificate signature digest algorithm is not supported</td>
  </tr>
  <tr>
    <td class="tg-0pky">79</td>
    <td class="tg-0pky">PKAuthenticator is missing the required paChecksum</td>
  </tr>
  <tr>
    <td class="tg-0pky">80</td>
    <td class="tg-0pky">The signedData digest algorithm is not supported</td>
  </tr>
  <tr>
    <td class="tg-0pky">81</td>
    <td class="tg-0pky">The Public Key encryption delivery method is not supported</td>
  </tr>
</tbody>
</table>

## Default home page

To set the default application for the GUI home page, please do the following:

- edit `/etc/kibana/kibana.yml` configuration file:

  ```bash
  vi /etc/kibana/kibana.yml
  ```

- change the following directives:

  ```yml
  # Home Page settings
  #kibana.defaultAppId: "home"
  ```

  example:

  ```yml
  # Home Page settings
  kibana.defaultAppId: "alerts"
  ```

## Configure email delivery

### Configure email delivery for sending PDF reports in Scheduler

The default e-mail client that installs with the Linux CentOS system,
which is used by ITRS Log Analytics to send reports (Section 5.3 of the
[Reports](/05-00-00-Reports/05-03-00-PDF_Report.md) chapter), is ***postfix***.

#### Configuration file for **postfix** mail client

The *postfix* configuration directory for CentOS is */etc/postfix*. It
contains files:

**main.cf** - the main configuration file for the program specifying the basic parameters

 Some of its directives:
 </br>
 </br>
<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-1wig{border-color:inherit;font-weight:bold;text-align:left;vertical-align:top}
.tg .tg-t3tv{text-align:left;vertical-align:middle}
</style>
<table class="tg" style="undefined;table-layout: fixed; width: 700px">
<colgroup>
<col style="width: 141px">
<col style="width: 559px">
</colgroup>
<thead>
  <tr>
    <th class="tg-1wig">Directive</th>
    <th class="tg-1wig">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-t3tv">queue_directory</td>
    <td class="tg-t3tv">The postfix queue location.</td>
  </tr>
  <tr>
    <td class="tg-t3tv">command_directory</td>
    <td class="tg-t3tv">The location of Postfix commands.</td>
  </tr>
  <tr>
    <td class="tg-t3tv">daemon_directory</td>
    <td class="tg-t3tv">Location of Postfix daemons.</td>
  </tr>
  <tr>
    <td class="tg-t3tv">mail_owner</td>
    <td class="tg-t3tv">The owner of Postfix domain name of the server</td>
  </tr>
  <tr>
    <td class="tg-t3tv">myhostname</td>
    <td class="tg-t3tv">The fully qualified domain name of the server.</td>
  </tr>
  <tr>
    <td class="tg-t3tv">mydomain</td>
    <td class="tg-t3tv">Server domain</td>
  </tr>
  <tr>
    <td class="tg-t3tv">myorigin</td>
    <td class="tg-t3tv">Host or domain to be displayed as origin on email leaving the server.</td>
  </tr>
  <tr>
    <td class="tg-t3tv">inet_interfaces</td>
    <td class="tg-t3tv">Network interface to be used for incoming email.</td>
  </tr>
  <tr>
    <td class="tg-t3tv">mydestination</td>
    <td class="tg-t3tv">Domains from which the server accepts mail.</td>
  </tr>
  <tr>
    <td class="tg-t3tv">mynetworks</td>
    <td class="tg-t3tv">The IP address of trusted networks.</td>
  </tr>
  <tr>
    <td class="tg-t3tv">relayhost</td>
    <td class="tg-t3tv">Host or other mail server through which mail will be sent. This server will act as an outbound gateway.</td>
  </tr>
  <tr>
    <td class="tg-t3tv">alias_maps</td>
    <td class="tg-t3tv">Database of aliases used by the local delivery agent.</td>
  </tr>
  <tr>
    <td class="tg-t3tv">alias_database</td>
    <td class="tg-t3tv">Alias database generated by the new aliases command.</td>
  </tr>
  <tr>
    <td class="tg-t3tv">mail_spool_directory</td>
    <td class="tg-t3tv">The location where user boxes will be stored.</td>
  </tr>
</tbody>
</table>

</br>
</br>

 **master.cf** - defines the configuration settings for the master
 daemon and the way it should work with other agents to deliver mail.
 For each service installed in the master.cf file seven columns define how the service should be used.

</br>
</br>

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-qahb{border-color:inherit;font-weight:bold;text-align:left;vertical-align:middle}
.tg .tg-ie02{border-color:inherit;text-align:left;vertical-align:middle}
</style>
<table class="tg" style="undefined;table-layout: fixed; width: 719px">
<colgroup>
<col style="width: 157px">
<col style="width: 562px">
</colgroup>
<thead>
  <tr>
    <th class="tg-qahb">Column</th>
    <th class="tg-qahb">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-ie02">service</td>
    <td class="tg-ie02">The name of the service</td>
  </tr>
  <tr>
    <td class="tg-ie02">type</td>
    <td class="tg-ie02">The transport mechanism to be used.</td>
  </tr>
  <tr>
    <td class="tg-ie02">private</td>
    <td class="tg-ie02">Is the service only for user by Postfix.</td>
  </tr>
  <tr>
    <td class="tg-ie02">unpriv</td>
    <td class="tg-ie02">Can the service be run by ordinary users</td>
  </tr>
  <tr>
    <td class="tg-ie02">chroot</td>
    <td class="tg-ie02">Whether the service is to change the main directory (chroot) for the mail. Queue.</td>
  </tr>
  <tr>
    <td class="tg-ie02">wakeup</td>
    <td class="tg-ie02">Wake up interval for the service.</td>
  </tr>
  <tr>
    <td class="tg-ie02">maxproc</td>
    <td class="tg-ie02">The maximum number of processes on which the service can be forked (to divide into branches)</td>
  </tr>
  <tr>
    <td class="tg-ie02">command + args</td>
    <td class="tg-ie02">A command associated with the service plus any argument</td>
  </tr>
</tbody>
</table>

</br>
</br>

**access** - can be used to control access based on an e-mail address,
 host address, domain, or network address.

*Examples of entries in the file*

</br>
</br>
<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-jn0s{border-color:inherit;font-weight:bold;text-align:left;vertical-align:middle}
.tg .tg-t3tv{border-color:inherit;text-align:left;vertical-align:middle}
</style>
<table class="tg" style="undefined;table-layout: fixed; width: 558px">
<colgroup>
<col style="width: 298px">
<col style="width: 260px">
</colgroup>
<thead>
  <tr>
    <th class="tg-jn0s">Description</th>
    <th class="tg-jn0s">Example</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-t3tv">To allow access for specific IP address:</td>
    <td class="tg-t3tv">192.168.122.20 OK</td>
  </tr>
  <tr>
    <td class="tg-t3tv">To allow access for a specific domain:</td>
    <td class="tg-t3tv">example.com OK</td>
  </tr>
  <tr>
    <td class="tg-t3tv">To deny access from the 192.168.3.0/24 network:</td>
    <td class="tg-t3tv">192.168.3 REJECT</td>
  </tr>
</tbody>
</table>

</br>
</br>

 After making changes to the access file, you must convert its contents
 to the access.db database with the postmap command:

```bash
  postmap /etc/postfix/access

  ll /etc/postfix/access*
  
   -rw-r--r--. 1 root root 20876 Jan 26 2014 /etc/postfix/access
   -rw-r--r--. 1 root root 12288 Feb 12 07:47 /etc/postfix/access.db
```

**canonical** - mapping incoming e-mails to local users.

 *Examples of entries in the file:*

 To forward emails to user1 to the
 [user1@yahoo.com] mailbox:

   ```bash
   user1 user1@yahoo.com
   ```

 To forward all emails for example.org to another example.com domain:

   ```bash
   @example.org @example.com
   ```

 After making changes to the canonical file, you must convert its
 contents to the canonical.db database with the postmap command:

```bash
  postmap /etc/postfix/canonical

  ll /etc/postfix/canonical*

  -rw-r--r--. 1 root root 11681 2014-06-10 /etc/postfix/canonical
  -rw-r--r--. 1 root root 12288 07-31 20:56 /etc/postfix/canonical.db
```

**generic** - mapping of outgoing e-mails to local users. The syntax
 is the same as a canonical file. After you make a change to this file,
 you must also run the postmap command.

```bash
  postmap /etc/postfix/generic

  ll /etc/postfix/generic*

  -rw-r--r--. 1 root root 9904 2014-06-10 /etc/postfix/generic
  -rw-r--r--. 1 root root 12288 07-31 21:15 /etc/postfix/generic.db
```

**relocated** -- information about users who have been transferred.
 The syntax of the file is the same as canonical and generic files.

 Assuming the user1 was moved from example.com to example.net, you can
 forward all emails received at the old address to the new address:

 Example of an entry in the file:

  ```bash
  <user1@example.com> <user1@example.net>
  ```

 After you make a change to this file, you must also run the postmap
 command.

```bash
postmap /etc/postfix/relocated
ll /etc/postfix/relocated*

  -rw-r--r--. 1 root root 6816 2014-06-10 /etc/postfix/relocated
  -rw-r--r--. 1 root root 12288 07-31 21:26 /etc/postfix/relocated.d
```

**transport** -- mapping between e-mail addresses and the server through which these e-mails are to be sent (next hops) in the transport
 format: nexthop.

 Example of an entry in the file:
  
  ```bash
  <user1@example.com> smtp:host1.example.com
  ```

 After you make changes to this file, you must also run the postmap
 command.

```bash
postmap /etc/postfix/transport
ll /etc/postfix/transport*

  -rw-r--r--. 1 root root 12549 2014-06-10 /etc/postfix/transport
  -rw-r--r--. 1 root root 12288 07-31 21:32 /etc/postfix/transport.db
```

**virtual** - user to redirect e-mails intended for a certain user to
 the account of another user or multiple users. It can also be used to
 implement the domain alias mechanism.

 *Examples of the entries in the file:*

 Redirecting email for user1, to root users and user3:

```conf
user1 root,user3
```

 Redirecting email for user 1 in the example.com domain to the root
 user:
  
  ```bash
  <user1@example.com> root
  ```

 After you make a change to this file, you must also run the postmap
 command:

   ```bash
   postmap /etc/postfix/virtual

   ll /etc/postfix/virtual

  -rw-r--r--. 1 root root 12494 2014-06-10 /etc/postfix/virtual
  -rw-r--r--. 1 root root 12288 07-31 21:58 /etc/postfix/virtual.db
  ```

#### Basic *postfix* configuration

Base configuration of *postfix* application you can make in
`/etc/postfix/main.cf` configuration file, which must be completed with the following entry:

- section *# RECEIVING MAIL*

  ```bash
  inet_interfaces = all
  inet_protocols = ipv4
  ```

- section *# INTERNET OR INTRANET*

  ```bash
  relayhost = [IP mail server]:25 (port number)
  ```

In the next step, you must complete the canonical file
of the *postfix*

At the end, you should restart the *postfix*:

```bash
 systemctl restart postfix
```

#### Example of postfix configuration with SSL encryption enabled

To configure email delivery with SSL encryption you need to make
the following changes in the *postfix* configuration files:

- **`/etc/postfix/main.cf`** - file should contain the following
entries in addition to standard (unchecked entries):
  
  ```bash
  mydestination = $myhostname, localhost.$mydomain, localhost
  myhostname = example.com
  relayhost = [smtp.example.com]:587
  smtp_sasl_auth_enable = yes
  smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
  smtp_sasl_security_options = noanonymous
  smtp_tls_CAfile = /root/certs/cacert.cer
  smtp_use_tls = yes
  smtp_sasl_mechanism_filter = plain, login
  smtp_sasl_tls_security_options = noanonymous
  canonical_maps = hash:/etc/postfix/canonical
  smtp_generic_maps = hash:/etc/postfix/generic
  smtpd_recipient_restrictions = permit_sasl_authenticated
  ```

- **`/etc/postfix/sasl_passwd`** - file should define the data for authorized

   ```bash
   [smtp.example.com]:587 [USER@example.com:PASS]
   [smtp.example.com]:587 username:password
   ```

You need to give appropriate permissions:

  ```bash
  chmod 400 /etc/postfix/sasl_passwd
  ```

and map configuration to the database:
  
  ```bash
  postmap /etc/postfix/sasl_passwd
  postmap /etc/postfix/canonical
  postmap /etc/postfix/generic
  ```

next, you need to generate a CA cert file:

  ```bash
  cat /etc/ssl/certs/Example_Server_CA.pem | tee -a etc/postfix/cacert.pem
  ```

Finally, you need to restart the postfix

  ```bash
  systemctl restart postfix
  ```

## Custom notification on the workstation

The mechanism of *personalization of notification at the workstation* will be implemented by combining alerting mechanisms, triggering integrated commands, and triggering interaction scripts allowing for the transfer of a personalized notification to the workstation.
The notifications will use a specific script, which can inform all logged-in users or the selected one about the detection of individual incidents.

Configuration steps

1. Create a new alert rule or edit an existing one according to the instruction: [Creating Alerts](https://itrs-log-analytics-7x.readthedocs.io/en/latest/06-SIEM_Plan/06-SIEM_Plan.html#creating-alerts),

1. In the `Alert`` Method` field select the `Command` method,

1. Add the following script name to `Path to script/command` field:

   ```notifyworkstation.py```

## Agents module

Before use ensure that you have all the required files

- Tool for generating the necessary certificates: `/usr/share/elasticsearch/utils/tlstool/tlstool.sh`;
- Logstash utilities:

    ```conf
      ./integrations/masteragent/conf.d/masteragent {01-input-agents.conf, 050-filter-agents.conf, 100-output-agents.conf}
      ./integrations/masteragent/masteragent.yml.off.
    ```

- Linux Agent files: `./agents/masteragent/agents/linux/masteragent`:

  - Executable: `MasterBeatAgent.jar`
  - Configuration File for MasterAgent (server): `MasterBeatAgent.conf`
  - Configuration File for Agent (client): `agent.conf`
  - Service file: `masteragent.service`

### Preparations

EVERY COMMAND HAS TO BE EXECUTED FROM /INSTALL DIRECTORY.

1. Generate the certificates using `tlstools.sh` script from `/usr/share/elasticsearch/utils/tlstool/`.

    - Update the IP of the node directive, by replacing `<logstash ip address`> with the logstash server ip in the provided masteragent.yml config (`/usr/share/elasticsearch/utils/tlstool/config/masteragent.yml`).
    - Generate certs using masteragent configuration (by default it will be saved to the `out/` dir):

        ```bash
        /usr/share/elasticsearch/utils/tlstool/tlstool.sh -c /usr/share/elasticsearch/utils/tlstool/config/masteragent.yml -ca -crt -t agents/masteragent/certificates
        ```

    - Create KeyStore and TrustStore. Set the KeyStore password of your choice that is utilized to securely store certificates:

        ```bash
        cd agents/masteragent/certificates
        keytool -import -file rootCA.crt -alias root -keystore root.jks -storetype jks
        openssl pkcs12 -export -in localhost.crt -inkey localhost.key -out node_name.p12 -name localhost -certfile rootCA.crt
        cd -
        ```

    - Set the KeyStore password of your choice that is utilized to securely store certificates.
    - Type 'yes' when "Trust this certificate?" monit will be shown.
    - Set the TrustStore password of your choice that is used to secure CAs. Remember entered passwords - they'll be used later!

1. Configure firewall to enable communication on used ports (defaults: TCP 8080 -> logstash, TCP 8081 -> agent's server).

    - These ports can be changed but must reflect "port" and "logstash" directives from an agent.conf file to ensure a connection with the agent.
    - Commands for default ports:

      ```bash
      firewall-cmd --permanent --zone public --add-port 8080/tcp
      firewall-cmd --permanent --zone public --add-port 8081/tcp
      ```

1. Configure Logstash:

    - Copy files:

      ```bash
      cp -rf ./integrations/masteragent/conf.d/* /etc/logstash/conf.d/
      ```

    - Copy pipeline configuration:

      ```bash
      cp -rf ./integrations/masteragent/*.yml.off /etc/logstash/pipelines.d/masteragent.yml
      cat ./integrations/masteragent/masteragent.yml.off >> /etc/logstash/pipelines.yml
      ```

    - Configure SSL connection, by copying previously generated certificates:

      ```bash
      mkdir -p /etc/logstash/conf.d/masteragent/ssl
      /bin/cp -rf ./agents/masteragent/certificates/localhost.* ./agents/masteragent/certificates/rootCA.crt /etc/logstash/conf.d/masteragent/ssl/
      ```

    - Set permissions:

      ```bash
      chown -R logstash:logstash /etc/logstash/conf.d/masteragent
      ```

    - Restart service:

      ```bash
      systemctl restart logstash
      ```

### Installation of MasterAgent - Server Side

- Copy executable and config:

    ```bash
    mkdir -p /opt/agents
    /bin/cp -rf ./agents/masteragent/agents/linux/masteragent/MasterBeatAgent.jar /opt/agents
    /bin/cp -rf ./agents/masteragent/agents/linux/masteragent/MasterBeatAgent.conf /opt/agents/agent.conf
    ```

- Copy certificates:

    ```bash
    /bin/cp -rf ./agents/masteragent/certificates/node_name.p12 ./agents/masteragent/certificates/root.jks /opt/agents/
    ```

- Set permissions:

    ```bash
    chown -R kibana:kibana /opt/agents
    ```

- Update the configuration file with KeyStore/TrustStore paths and passwords. Use your preferred editor eg. vim:

    ```bash
    vim /opt/agents/agent.conf
    ```

### Installation of Agent - Client Side

#### Linux

FOR WINDOWS AND LINUX: `Client requires at least Java 1.8+.

Linux Agent - software installed on clients running on Linux OS:

1. Install net-tools package to use Agent on Linux RH / Centos:

    ```bash
    yum install net-tools
    ```

1. Copy executable and config:

    ```bash
    mkdir -p /opt/masteragent
    /bin/cp -rf ./agents/masteragent/agents/linux/masteragent/agent.conf ./agents/masteragent/agents/linux/masteragent/MasterBeatAgent.jar /opt/masteragent
    /bin/cp -rf ./agents/masteragent/agents/linux/masteragent/masteragent.service /usr/lib/systemd/system/masteragent.service
    ```

1. Copy certificates:

    ```bash
    /bin/cp -rf ./certificates/node_name.p12 ./certificates/root.jks /opt/masteragent/
    ```

1. Update the configuration file with KeyStore/TrustStore paths and passwords. Also, update the IP and port (by default 8080 is used) of the logstash host that the agent will connect to with the 'logstash' directive. Use your preferred editor eg. vim:

    ```bash
    vim /opt/masteragent/agent.conf
    ```

1. Enable masteragent service:

    ```bash
    systemctl daemon-reload
    systemctl enable masteragent
    systemctl start masteragent
    ```

1. Finally, verify in the Kibana 'Agents' plugin if a newly added agent is present. Check masteragent logs executing:

    ```bash
    journalctl -fu masteragent
    ```

#### Windows

FOR WINDOWS AND LINUX: `Client requires at least Java 1.8+.

1. Ensure that you have all required files (`./install/agents/masteragent/agents/windows/masteragent`):

    - Installer and manifest: `agents.exe`, `agents.xml`
    - Client: `Agents.jar`
    - Configuration File: `agent.conf`

1. Configure firewall:

    Add an exception to the firewall to listen on TCP port 8081. \
    Add an exception to the firewall to allow outgoing connection to TCP port masteragent:8080 (reasonable only with configured "`http_enabled = true`")

1. Create `C:\Program Files\MasterAgent` directory.

1. Copy the contents of the `./install/agents/masteragent/agents/windows/masteragent` directory to the `C:\Program Files\MasterAgent`.

1. Copy node_name.p12 and root.jks files from the `./install/agents/masteragent/certificates` to desired directory.

1. Update the `C:\Program Files\MasterAgent\agent.conf` file with KeyStore/TrustStore paths from the previous step and passwords. Also, update the IP and port (by default 8080 is used) of the logstash host that the agent will connect to with the 'logstash' directive.

1. Start PowerShell as an administrator:

    To install an agent you can use interchangeably the following methods:

    - Method 1 - use installer:

      ```ps
      cd "C:\Program Files\MasterAgent"
      .\agents.exe install
      .\agents.exe start
      ```

    - Method 2 - manually creating service:

      ```ps
      New-Service -name masteragent -displayName masteragent -binaryPathName "C:\Program Files\MasterAgent\agents.exe"
      ```

1. Finally, verify in the Kibana '`Agents`' plugin if a newly added agent is present. To check out logs and errors, look for '`agents.out`.log' and '`agents.err.log`' files in the `C:\Program Files\MasterAgent` directory after the service starts. Also, check the service status:

      `.\agents.exe status`

### Beats - configuration templates

1. Go to the `Agents` which is located in the main menu. Then go to `Templates` and click the `Add template` button.

    ![](/media/media/image242.png)

1. Click the `Create new` file button at the bottom.

    ![](/media/media/image243.png)

1. you will see the form to create a file that will be on a client system. \
    There are inputs such as:
    - Destination Path,
    - File name,
    - Description,
    - Upload file,
    - Content.
    ![](/media/media/image244.png)

1. Remember that you must provide the exact path to your directory in the Destination Path field

    ![](/media/media/image245.png)

1. After that add your file to the template by checking it from the `Available files` list and clicking `Add` and then `Create new file`.

    ![](/media/media/image246.png)

1. You can now see your template in the `Template` tab

    ![](/media/media/image247.png)

1. The next step will be to add the template to the agent by checking the agent's form list and clicking `Apply Template`.

    ![](/media/media/image248.png)

1. The last step is to apply the template by checking it from the list and clicking the `Apply` button.

    ![](/media/media/image249.png)

    You can also select multiple agents. Remember, if your file path is Windows type You can only select Windows agents.
    You can check the Logs by clicking the icon in the `logs` column.

    ![](/media/media/image250.png)

### Agent module compatibility

The Agents module works with Beats agents in the following versions:

<table border="1" class="docutils" id="id1">
<colgroup>
<col width="3%" />
<col width="12%" />
<col width="13%" />
<col width="71%" />
</colgroup>
<thead valign="bottom">
<tr class="row-odd"><th class="head">No</th>
<th class="head">Agent Name</th>
<th class="head">Beats Version</th>
<th class="head">Link to download</th>
</tr>
</thead>
<tbody valign="top">
<tr class="row-even"><td><p class="first last">1</p>
</td>
<td><p class="first last">Filebeat</p>
</td>
<td><p class="first last">OSS 7.17.8</p>
</td>
<td><p class="first last">https://www.elastic.co/downloads/past-releases/filebeat-oss-7-17-8</p>
</td>
</tr>
<tr class="row-odd"><td><p class="first last">2</p>
</td>
<td><p class="first last">Packetbeat</p>
</td>
<td><p class="first last">OSS 7.17.8</p>
</td>
<td><p class="first last">https://www.elastic.co/downloads/past-releases/packetbeat-oss-7-17-8</p>
</td>
</tr>
<tr class="row-even"><td><p class="first last">3</p>
</td>
<td><p class="first last">Winlogbeat</p>
</td>
<td><p class="first last">OSS 7.17.8</p>
</td>
<td><p class="first last">https://www.elastic.co/downloads/past-releases/winlogbeat-oss-7-17-8</p>
</td>
</tr>
<tr class="row-odd"><td><p class="first last">4</p>
</td>
<td><p class="first last">Metricbeat</p>
</td>
<td><p class="first last">OSS 7.17.8</p>
</td>
<td><p class="first last">https://www.elastic.co/downloads/past-releases/metricbeat-oss-7-17-8</p>
</td>
</tr>
<tr class="row-even"><td><p class="first last">5</p>
</td>
<td><p class="first last">Heartbeat</p>
</td>
<td><p class="first last">OSS 7.17.8</p>
</td>
<td><p class="first last">https://www.elastic.co/downloads/past-releases/heartbeat-oss-7-17-8</p>
</td>
</tr>
<tr class="row-odd"><td><p class="first last">6</p>
</td>
<td><p class="first last">Auditbeat</p>
</td>
<td><p class="first last">OSS 7.17.8</p>
</td>
<td><p class="first last">https://www.elastic.co/downloads/past-releases/auditbeat-oss-7-17-8</p>
</td>
</tr>
<tr class="row-even"><td><p class="first last">7</p>
</td>
<td><p class="first last">Logstash</p>
</td>
<td><p class="first last">OSS 7.17.8</p>
</td>
<td><p class="first last">https://www.elastic.co/downloads/past-releases/logstash-oss-7-17-8</p>
</td>
</tr>
</table>

### Windows - Beats agents installation

#### Winlogbeat

##### Installation

1. Copy the Winlogbeat installer from the installation directory `install/Agents/beats/windows/winlogbeat-oss-7.17.8-windows-x86_64.zip` and unpack

1. Copy the installation files to the `C:\Program Files\Winlogbeat` directory

##### Configuration

Editing the file: `C:\Program Files\Winlogbeat\winlogbeat.yml`:

1. In section:

   ```yml
   winlogbeat.event_logs:
     - name: Application
       ignore_older: 72h
     - name: Security
     - name: System
   ```

   change to:

   ```yml
   winlogbeat.event_logs:
     - name: Application
       ignore_older: 72h
     - name: Security
       ignore_older: 72h
     - name: System
       ignore_older: 72h
   ```

1. In section:

   ```yml
   setup.template.settings:
     index.number_of_shards: 1
   ```

   change to:

   ```yml
   #setup.template.settings:
     #index.number_of_shards: 1
   ```

1. In section:

   ```yml
   setup.kibana:
   ```

   change to:

   ```yml
   #setup.kibana:
   ```

1. In section:

   ```yml
   output.elasticsearch:
     # Array of hosts to connect to.
     hosts: ["localhost:9200"]
   ```

   change to:

   ```yml
   #output.elasticsearch:
     # Array of hosts to connect to.
     #hosts: ["localhost:9200"]
   ```

1. In section:

   ```yml
   #output.logstash:
     # The Logstash hosts
     #hosts: ["localhost:5044"]
   ```

   change to:

   ```yml
   output.logstash:
     # The Logstash hosts
     hosts: ["LOGSTASH_IP:5044"]
   ```

1. In section:

   ```yml
   #tags: ["service-X", "web-tier"]
   ```

   change to:

   ```yml
   tags: ["winlogbeat"]
   ```

1. Run the `PowerShell` console as Administrator and execute the following commands:

    ```powershell
    cd 'C:\Program Files\Winlogbeat'
    .\install-service-winlogbeat.ps1

    Security warning
    Run only scripts that you trust. While scripts from the internet can be useful,
    this script can potentially harm your computer. If you trust this script, use
    the Unblock-File cmdlet to allow the script to run without this warning message.
    Do you want to run C:\Program Files\Winlogbeat\install-service-winlogbeat.ps1?
    [D] Do not run  [R] Run once  [S] Suspend  [?] Help (default is "D"): R

    ```

    Output:

    ```powershell
    Status   Name               DisplayName
    ------   ----               -----------
    Stopped    Winlogbeat      Winlogbeat
    ```

1. Start Winlogbeat service:

    ```powershell
    sc start Winlogbeat
    ```

Test configuration:

```ps
cd 'C:\Program Files\Winlogbeat'
winlogbeat.exe test config
winlogbeat.exe test output
```

##### Drop event

We can also drop events on the agent side. To do this we need to use the ```drop_event``` processor

```yml
processors:
  - drop_event:
      when:
        condition
```

Each condition receives a field to compare. You can specify multiple fields under the same condition by using ```AND``` between the fields (for example, ```field1 AND field2```).

For each field, you can specify a simple field name or a nested map, for example, ```dns.question.name```.

See Exported Fields for a list of all the fields that are exported by Winlogbeat.

The supported conditions are:

- equals
- contains
- regexp
- range
- network
- has_fields
- or
- and
- not

###### equals

With the ```equals``` condition, you can compare if a field has a certain value. The condition accepts only an integer or a string value.

For example, the following condition checks if the response code of the HTTP transaction is 200:

```yml
equals:
  http.response.code: 200
```

###### contains

The ```contains``` condition checks if a value is part of a field. The field can be a string or an array of strings. The condition accepts only a string value.

For example, the following condition checks if an error is part of the transaction status:

```yml
contains:
  status: "Specific error"
```

###### regexp

The ```regexp``` condition checks the field against a regular expression. The condition accepts only strings.

For example, the following condition checks if the process name starts with ```foo```:

```yml
regexp:
  system.process.name: "^foo.*"
```

###### range

The range condition checks if the field is in a certain ```range``` of values. The condition supports ```lt, lte, gt, and gte```. The condition accepts only integer or float values.

For example, the following condition checks for failed HTTP transactions by comparing the ```http.response.code``` field with 400.

```yml
range:
  http.response.code:
    gte: 400
```

This can also be written as:

```yml
range:
  http.response.code.gte: 400
```

The following condition checks if the CPU usage in percentage has a value between 0.5 and 0.8.

```yml
range:
  system.cpu.user.pct.gte: 0.5
  system.cpu.user.pct.lt: 0.8
```

###### network

The ```network``` condition checks if the field is in a certain IP network range. Both IPv4 and IPv6 addresses are supported. The network range may be specified using CIDR notation, like "192.0.2.0/24" or "2001:db8::/32", or by using one of these named ranges:

- ```loopback``` - Matches loopback addresses in the range of 127.0.0.0/8 or ::1/128.
- ```unicast``` - Matches global unicast addresses defined in RFC 1122, RFC 4632, and RFC 4291 with the exception of the IPv4 broadcast address (```255.255.255.255```). This includes private address ranges.
- ```multicast``` - Matches multicast addresses.
- ```interface_local_multicast``` - Matches IPv6 interface-local multicast addresses.
- ```link_local_unicast``` - Matches link-local unicast addresses.
- ```link_local_multicast``` - Matches link-local multicast addresses.
- ```private``` - Matches private address ranges defined in RFC 1918 (IPv4) and RFC 4193 (IPv6).
- ```public``` - Matches addresses that are not loopback, unspecified, IPv4 broadcast, link-local unicast, link-local multicast, interface local multicast, or private.
- ```unspecified``` - Matches unspecified addresses (either the IPv4 address "0.0.0.0" or the IPv6 address "::").

The following condition returns true if the source.ip value is within the private address space.

```yml
network:
  source.ip: private
```

This condition returns true if the ```destination.ip``` value is within the IPv4 range of ```192.168.1.0``` - ```192.168.1.255```.

```yml
network:
  destination.ip: '192.168.1.0/24'
```

This condition returns true when ```destination.ip``` is within any of the given subnets.

```yml
network:
  destination.ip: ['192.168.1.0/24', '10.0.0.0/8', loopback]
```

###### has_fields

The ```has_fields``` condition checks if all the given fields exist in the event. The condition accepts a list of string values denoting the field names.

For example, the following condition checks if the ```http.response.code``` field is present in the event.

```yml
has_fields: ['http.response.code']
```

###### or

The `or` operator receives a list of conditions.

```yml
or:
  - <condition1>
  - <condition2>
  - <condition3>
  ...
```

For example, to configure the condition ```http.response.code = 304 OR http.response.code = 404```:

```yml
or:
  - equals:
      http.response.code: 304
  - equals:
      http.response.code: 404
```

###### and

The ```and``` operator receives a list of conditions.

```yml
and:
  - <condition1>
  - <condition2>
  - <condition3>
  ...
```

For example, to configure the condition ```http.response.code = 200 AND status = OK```:

```yml
or:
  - <condition1>
  - and:
    - <condition2>
    - <condition3>
```

###### not

The ```not``` operator receives the condition to negate.

```yml
not:
  <condition>
```

For example, to configure the condition ```NOT status = OK```:

```yml
not:
  equals:
    status: OK
```

##### Internal queue

Winlogbeat uses an internal queue to store events before publishing them. The queue is responsible for buffering and combining events into batches that can be consumed by the outputs. The outputs will use bulk operations to send a batch of events in one transaction.

You can configure the type and behavior of the internal queue by setting options in the ```queue``` section of the ```winlogbeat.yml``` config file. Only one queue type can be configured.

This sample configuration sets the memory queue to buffer up to 4096 events:

```yml
queue.mem:
  events: 4096
```

Configure the memory queue
The memory queue keeps all events in memory.

If no flush interval and no number of events to flush is configured, all events published to this queue will be directly consumed by the outputs. To enforce spooling in the queue, set the ```flush.min_events``` and ```flush.timeout options```.

By default ```flush.min_events``` is set to 2048 and ```flush.timeout``` is set to 1s.

The output’s ```bulk_max_size``` setting limits the number of events being processed at once.

The memory queue waits for the output to acknowledge or drop events. If the queue is full, no new events can be inserted into the memory queue. Only after the signal from the output will the queue free up space for more events to be accepted.

This sample configuration forwards events to the output if 512 events are available or the oldest available event has been waiting for 5s in the queue:

```yml
queue.mem:
  events: 4096
  flush.min_events: 512
  flush.timeout: 5s
```

Configuration options

You can specify the following options in the ```queue.mem``` section of the ```winlogbeat.yml``` config file:
```events```
Number of events the queue can store.
The default value is ```4096``` events.

```flush.min_events```
Minimum number of events required for publishing. If this value is set to 0, the output can start publishing events without additional waiting times. Otherwise, the output has to wait for more events to become available.

The default value is ```2048```.

```flush.timeout```
Maximum wait time for flush.min_events to be fulfilled. If set to 0s, events will be immediately available for consumption.
The default value is 1s.

Configure disk queue
The disk queue stores pending events on the disk rather than the main memory. This allows Beats to queue a larger number of events than is possible with the memory queue, and to save events when a Beat or device is restarted. This increased reliability comes with a performance tradeoff, as every incoming event must be written and read from the device’s disk. However, for setups where the disk is not the main bottleneck, the disk queue gives a simple and relatively low-overhead way to add a layer of robustness to incoming event data.

The disk queue is expected to replace the file spool in a future release.

To enable the disk queue with default settings, specify a maximum size:

```yml
queue.disk:
  max_size: 10GB
```

The queue will be used up to the specified maximum size on the disk. It will only use as much space as required. For example, if the queue is only storing 1GB of events, then it will only occupy 1GB on disk no matter how high the maximum is. Queue data is deleted from the disk after it has been successfully sent to the output.

Configuration options

You can specify the following options in the ```queue.disk``` section of the ```winlogbeat.yml``` config file:

```path```
The path to the directory where the disk queue should store its data files. The directory is created on startup if it doesn’t exist.

The default value is ```"${path.data}/diskqueue"```.

```max_size (required)```
The maximum size the queue should use on disk. Events that exceed this maximum will either pause their input or be discarded, depending on the input’s configuration.

A value of 0 means that no maximum size is enforced, and the queue can grow up to the amount of free space on the disk. This value should be used with caution, as filling a system’s main disk can make it inoperable. It is best to use this setting only with a dedicated data or backup partition that will not interfere with Winlogbeat or the rest of the host system.

The default value is ```10GB```.

```segment_size```
Data added to the queue is stored in segment files. Each segment contains some number of events waiting to be sent to the outputs and is deleted when all its events are sent. By default, segment size is limited to 1/10 of the maximum queue size. Using a smaller size means that the queue will use more data files, but they will be deleted more quickly after use. Using a larger size means some data will take longer to delete, but the queue will use fewer auxiliary files. It is usually fine to leave this value unchanged.

The default value is ```max_size / 10```.

```read_ahead```
The number of events that should be read from disk into memory while waiting for an output to request them. If you find outputs are slowing down because they can’t read as many events at a time, adjusting this setting upward may help, at the cost of higher memory usage.

The default value is ```512```.

```write_ahead```
The number of events the queue should accept and store in memory while waiting for them to be written to disk. If you find the queue’s memory use is too high because events are waiting too long to be written to disk, adjusting this setting downward may help, at the cost of reduced event throughput. On the other hand, if inputs are waiting or discarding events because they are being produced faster than the disk can handle, adjusting this setting upward may help, at the cost of higher memory usage.

The default value is ```2048```.

```retry_interval```
Some disk errors may block the operation of the queue, for example, a permission error writing to the data directory, or a disk full error while writing an event. In this case, the queue reports the error and retries after pausing for the time specified in retry_interval.

The default value is ```1s``` (one second).

```max_retry_interval``` When multiple consecutive errors are written to the disk, the queue increases the retry interval by factors of 2 up to a maximum of max_retry_interval. Increase this value if you are concerned about logging too many errors or overloading the host system if the target disk becomes unavailable for an extended time.

The default value is ```30s``` (thirty seconds).

#### Filebeat

##### Installation

1. Copy the Filebeat installer from the installation directory `install/Agents/beats/windows/filebeat-oss-7.17.8-windows-x86_64.zip` and unpack

1. Copy the installation files to the `C:\Program Files\Filebeat` directory

##### Configuration

Editing the file: `C:\Program Files\Filebeat\filebeat.yml`:

1. In section:

   ```yml
   - type: log
   
     # Change to true to enable this input configuration.
     enabled: false
   ```

   change to:

   ```yml
   - type: log
   
     # Change to true to enable this input configuration.
     enabled: true
   ```

1. In section:

   ```yml
       paths:
       - /var/log/*.log
       #- c:\programdata\elasticsearch\logs\*
   ```

   change to:

   ```yml
   paths:
       #- /var/log/*.log
       #- c:\programdata\elasticsearch\logs\*
       - "C:\Program Files\Microsoft SQL Server\*\MSSQL\Log\*"
       - "C:\inetpub\logs\*""
   ```

1. In section:

   ```yml
   setup.template.settings:
     index.number_of_shards: 1
   ```

   change to:

   ```yml
   #setup.template.settings:
     #index.number_of_shards: 1
   ```

1. In section:

   ```yml
   setup.kibana:
   ```

   change to:

   ```yml
   #setup.kibana:
   ```

1. In section:

   ```yml
   output.elasticsearch:
     # Array of hosts to connect to.
     hosts: ["localhost:9200"]
   ```

   change to:

   ```yml
   #output.elasticsearch:
     # Array of hosts to connect to.
     #hosts: ["localhost:9200"]
   ```

1. In section:

   ```yml
   #output.logstash:
     # The Logstash hosts
     #hosts: ["localhost:5044"]
   ```

   change to:

   ```yml
   output.logstash:
     # The Logstash hosts
     hosts: ["LOGSTASH_IP:5044"]
   ```

1. In section:

   ```yml
   #tags: ["service-X", "web-tier"]
   ```

   change to:

   ```yml
   tags: ["filebeat"]
   ```

1. Run the `PowerShell` console as Administrator and execute the following commands:

    ```powershell
    cd 'C:\Program Files\Filebeat'
    .\install-service-filebeat.ps1

    Security warning
    Run only scripts that you trust. While scripts from the internet can be useful,
    this script can potentially harm your computer. If you trust this script, use
    the Unblock-File cmdlet to allow the script to run without this warning message.
    Do you want to run C:\Program Files\Filebeat\install-service-filebeat.ps1?
    [D] Do not run  [R] Run once  [S] Suspend  [?] Help (default is "D"): R

    ```

    Output:

    ```powershell
    Status   Name               DisplayName
    ------   ----               -----------
    Stopped  Filebeat        Filebeat
    ```

1. Start Filebeat service:

    ```powershell
    sc start filebeat
    ```

You can enable, disable, and list Filebeat modules using the following command:

```cmd
cd 'C:\Program Files\Filebeat'
filebeat.exe modules list
filebeat.exe modules apache enable
filebeat.exe modules apache disable
```

Test configuration:

```cmd
cd 'C:\Program Files\Filebeat'
filebeat.exe test config
filebeat.exe test output
```

#### Metricbeat

##### Installation

1. Copy the Metricbeat installer from the installation directory `install/Agents/beats/windows/merticbeat-oss-7.17.8-windows-x86_64.zip` and unpack

1. Copy the installation files to the `C:\Program Files\Merticbeat` directory

##### Configuration

Editing the file: `C:\Program Files\Merticbeat\metricbeat.yml`:

1. In section:

   ```yml
   setup.template.settings:
     index.number_of_shards: 1
     index.codec: best_compression
   ```

   change to:

   ```yml
   #setup.template.settings:
     #index.number_of_shards: 1
     #index.codec: best_compression
   ```

1. In section:

   ```yml
   setup.kibana:
   ```

   change to:

   ```yml
   #setup.kibana:
   ```

1. In section:

   ```yml
   output.elasticsearch:
     # Array of hosts to connect to.
     hosts: ["localhost:9200"]
   ```

   change to:

   ```yml
   #output.elasticsearch:
     # Array of hosts to connect to.
     #hosts: ["localhost:9200"]
   ```

1. In section:

   ```yml
   #output.logstash:
     # The Logstash hosts
     #hosts: ["localhost:5044"]
   ```

   change to:

   ```yml
   output.logstash:
     # The Logstash hosts
     hosts: ["LOGSTASH_IP:5044"]
   ```

1. In section:

   ```yml
   #tags: ["service-X", "web-tier"]
   ```

   change to:

   ```yml
   tags: ["metricbeat"]
   ```

1. Run the `PowerShell` console as Administrator and execute the following commands:

    ```powershell
    cd 'C:\Program Files\Metricbeat'
    .\install-service-metricbeat.ps1

    Security warning
    Run only scripts that you trust. While scripts from the internet can be useful,
    this script can potentially harm your computer. If you trust this script, use
    the Unblock-File cmdlet to allow the script to run without this warning message.
    Do you want to run C:\Program Files\Metricbeat\install-service-metricbeat.ps1?
    [D] Do not run  [R] Run once  [S] Suspend  [?] Help (default is "D"): R

    ```

    Output:

    ```powershell
    Status   Name               DisplayName
    ------   ----               -----------
    Stopped  Metricbeat        Metricbeat
    ```

1. Start Filebeat service:

    ```powershell
    sc start metricbeat
    ```

You can enable, disable, and list Metricbeat modules using the following command:

```cmd
cd 'C:\Program Files\Metricbeat'
metricbeat.exe modules list
metricbeat.exe modules apache enable
metricbeat.exe modules apache disable
```

Test configuration:

```cmd
cd 'C:\Program Files\Metricbeat'
metricbeat.exe test config
metricbeat.exe test output
```

#### Packetbeat

##### Installation

1. Copy the Packetbeat installer from the installation directory `install/Agents/beats/windows/packetbeat-oss-7.17.8-windows-x86_64.zip` and unpack

1. Copy the installation files to the `C:\Program Files\Packetbeat` directory

##### Configuration

Editing the file: `C:\Program Files\Packetbeat\packetbeat.yml`:

1. In section:

   ```yml
   setup.template.settings:
     index.number_of_shards: 3
   ```

   change to:

   ```yml
   #setup.template.settings:
     #index.number_of_shards: 3
   ```

1. In section:

   ```yml
   setup.kibana:
   ```

   change to:

   ```yml
   #setup.kibana:
   ```

1. In section:

   ```yml
   output.elasticsearch:
     # Array of hosts to connect to.
     hosts: ["localhost:9200"]
   ```

   change to:

   ```yml
   #output.elasticsearch:
     # Array of hosts to connect to.
     #hosts: ["localhost:9200"]
   ```

1. In section:

   ```yml
   #output.logstash:
     # The Logstash hosts
     #hosts: ["localhost:5044"]
   ```

   change to:

   ```yml
   output.logstash:
     # The Logstash hosts
     hosts: ["LOGSTASH_IP:5044"]
   ```

1. In section:

   ```yml
   #tags: ["service-X", "web-tier"]
   ```

   change to:

   ```yml
   tags: ["packetbeat"]
   ```

1. Run the `PowerShell` console as Administrator and execute the following commands:

    ```powershell
    cd 'C:\Program Files\Packetbeat'
    .\install-service-packetbeat.ps1
    
    Security warning
    Run only scripts that you trust. While scripts from the internet can be useful,
    this script can potentially harm your computer. If you trust this script, use
    the Unblock-File cmdlet to allow the script to run without this warning message.
    Do you want to run C:\Program Files\Packetbeat\install-service-packetbeat.ps1?
    [D] Do not run  [R] Run once  [S] Suspend  [?] Help (default is "D"): R
    
    ```

    Output:

    ```powershell
    Status   Name               DisplayName
    ------   ----               -----------
    Stopped  Packetbeat        Packetbeat
    ```

1. Start Packetbeat service:

    ```powershell
    sc start packetbeat
    ```

Test configuration:

```cmd
cd 'C:\Program Files\Packetbeat'
packetbeat.exe test config
packetbeat.exe test output
```

### Linux - Beats agents installation

#### Filebeat

##### Installation

1. Copy the Filebeat installer from the installation directory `install/Agents/beats/linux/filebeat-oss-7.17.8-x86_64.rpm`

1. Install filebeat with the following command:

   ```bash
   yum install -y filebeat-oss-7.17.8-x86_64.rpm
   ```

##### Configuration

Editing the file: `/etc/filebeat/filebeat.yml`:

1. In section:

   ```yml
   - type: log
   
     # Change to true to enable this input configuration.
     enabled: false
   ```

   change to:

   ```yml
   - type: log
   
     # Change to true to enable this input configuration.
     enabled: true
   ```

1. In section:

   ```yml
   setup.template.settings:
     index.number_of_shards: 1
   ```

   change to:

   ```yml
   #setup.template.settings:
     #index.number_of_shards: 1
   ```

1. In section:

   ```yml
   setup.kibana:
   ```

   change to:

   ```yml
   #setup.kibana:
   ```

1. In section:

   ```yml
   output.elasticsearch:
     # Array of hosts to connect to.
     hosts: ["localhost:9200"]
   ```

   change to:

   ```yml
   #output.elasticsearch:
     # Array of hosts to connect to.
     #hosts: ["localhost:9200"]
   ```

1. In section:

   ```yml
   #output.logstash:
     # The Logstash hosts
     #hosts: ["localhost:5044"]
   ```

   change to:

   ```yml
   output.logstash:
     # The Logstash hosts
     hosts: ["LOGSTASH_IP:5044"]
   ```

1. In section:

   ```yml
   #tags: ["service-X", "web-tier"]
   ```

   change to:

   ```yml
   tags: ["filebeat"]
   ```

1. Start Filebeat service:

    ```bash
    systemctl start filebeat
    ```

You can enable, disable, and list Filebeat modules using the following command:

```bash
filebeat modules list
filebeat modules apache enable
filebeat modules apache disable
```

Test configuration:

```bash
filebeat test config
filebeat test output
```

#### Metricbeat

##### Installation

1. Copy the Metricbeat installer from the installation directory `install/Agents/beats/linux/metricbeat-oss-7.17.8-x86_64.rpm`

2. Install Metricbeat with the following command:

   ```bash
   yum install -y metricbeat-oss-7.17.8-x86_64.rpm
   ```

##### Configuration

Editing the file: `/etc/metricbeat/metricbeat.yml`:

1. In section:

   ```yml
   setup.template.settings:
     index.number_of_shards: 1
     index.codec: best_compression
   ```

   change to:

   ```yml
   #setup.template.settings:
     #index.number_of_shards: 1
     #index.codec: best_compression
   ```

2. In section:

   ```yml
   setup.kibana:
   ```

   change to:

   ```yml
   #setup.kibana:
   ```

3. In section:

   ```yml
   output.elasticsearch:
     # Array of hosts to connect to.
     hosts: ["localhost:9200"]
   ```

   change to:

   ```yml
   #output.elasticsearch:
     # Array of hosts to connect to.
     #hosts: ["localhost:9200"]
   ```

4. In section:

   ```yml
   #output.logstash:
     # The Logstash hosts
     #hosts: ["localhost:5044"]
   ```

   change to:

   ```yml
   output.logstash:
     # The Logstash hosts
     hosts: ["LOGSTASH_IP:5044"]
   ```

5. In section:

   ```yml
   #tags: ["service-X", "web-tier"]
   ```

   change to:

   ```yml
   tags: ["metricbeat"]
   ```

Start Filebeat service:

```powershell
systemctl start metricbeat
```

You can enable, disable, and list Metricbeat modules using the following command:

```cmd
metricbeat modules list
metricbeat modules apache enable
metricbeat modules apache disable
```

Test configuration:

```cmd
metricbeat test config
metricbeat test output
```

#### Packetbeat

##### Installation

1. Copy the Packetbeat installer from the installation directory `install/Agents/beats/linux/packetbeat-oss-7.17.8-x86_64.rpm`

2. Install Packetbeat with the following command:

   ```bash
   yum install -y packetbeat-oss-7.17.8-x86_64.rpm
   ```

##### Configuration

Editing the file: `/etc/packetbeat/packetbeat.yml`:

1. In section:

   ```yml
   setup.template.settings:
     index.number_of_shards: 3
   ```

   change to:

   ```yml
   #setup.template.settings:
     #index.number_of_shards: 3
   ```

2. In section:

   ```yml
   setup.kibana:
   ```

   change to:

   ```yml
   #setup.kibana:
   ```

3. In section:

   ```yml
   output.elasticsearch:
     # Array of hosts to connect to.
     hosts: ["localhost:9200"]
   ```

   change to:

   ```yml
   #output.elasticsearch:
     # Array of hosts to connect to.
     #hosts: ["localhost:9200"]
   ```

4. In section:

   ```yml
   #output.logstash:
     # The Logstash hosts
     #hosts: ["localhost:5044"]
   ```

   change to:

   ```yml
   output.logstash:
     # The Logstash hosts
     hosts: ["LOGSTASH_IP:5044"]
   ```

5. In section:

   ```yml
   #tags: ["service-X", "web-tier"]
   ```

   change to:

   ```yml
   tags: ["packetbeat"]
   ```

Start Packetbeat service:

```powershell
servicectl start packetbeat
```

Test configuration:

```cmd
packetbeat test config
packetbeat test output
```

## Kafka

Kafka allows you to distribute the load between nodes receiving data and encrypts communication.

Architecture example:

![](/media/media/image124.PNG)

### The Kafka installation

To install the Kafka, follow the steps below:

1. Java installation

   ```bash
   yum install java-11-openjdk-headless.x86_64
   ```

2. Create users for Kafka

   ```bash
   useradd kafka -m -d /opt/kafka -s /sbin/nologin
   ```

3. Download  the installation package::

   ```bash
   https://www.apache.org/dyn/closer.cgi?path=/kafka/3.2.0/kafka_2.13-3.2.0.tgz
   ```

4. Unpack installation files to the `/opt/kafka` directory:

   ```bash
   tar -xzvf kafka_2.13-3.2.0.tgz -C /opt/
   mv /opt/kafka_2.13-3.2.0 /opt/kafka
   ```

5. Set the necessary permissions

   ```bash
   chown -R kafka:kafka /opt/kafka
   ```

6. Edit configs and set the data and log directory:

   ```bash
   vim  /opt/kafka/config/server.properties
   ```

   ```bash
   log.dirs=/tmp/kafka-logs
   ```

7. Set the necessary firewall rules:

   ```bash
   firewall-cmd --permanent --add-port=2181/tcp
   firewall-cmd --permanent --add-port=2888/tcp
   firewall-cmd --permanent --add-port=3888/tcp
   firewall-cmd --permanent --add-port=9092/tcp
   firewall-cmd --reload
   ```

8. Create service files:

   `vim /usr/lib/systemd/system/zookeeper.service`

   ```bash
   [Unit]
   Requires=network.target remote-fs.target
   After=network.target remote-fs.target
   
   [Service]
   Type=simple
   User=kafka
   ExecStart=/opt/kafka/bin/zookeeper-server-start.sh /opt/kafka/config/zookeeper.properties
   ExecStop=/opt/kafka/bin/zookeeper-server-stop.sh
   Restart=on-abnormal
   
   [Install]
   WantedBy=multi-user.target
   ```

   `vim create /usr/lib/systemd/system/kafka.service`

   ```bash
   [Unit]
   Requires=zookeeper.service
   After=zookeeper.service
   
   [Service]
   Type=simple
   User=kafka
   ExecStart=/bin/sh -c '/opt/kafka/bin/kafka-server-start.sh /opt/kafka/config/server.properties > /opt/kafka/kafka.log 2>&1'
   ExecStop=/opt/kafka/bin/kafka-server-stop.sh
   Restart=on-abnormal
   
   [Install]
   WantedBy=multi-user.target
   ```

9. Reload `systemctl` daemon and the Kafka services:

   ```bash
   systemctl daemon-reload
   systemctl enable zookeeper kafka
   systemctl start zookeeper kafka
   ```

10. To test add the Kafka topic:

      ```bash
      /opt/kafka/bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --partitions 1 --replication-factor 1 --topic test
      ```

11. List existing topics:

      ```bash
      /opt/kafka/bin/kafka-topics.sh --bootstrap-server localhost:9092 --list
      ```

12. Generate test messages

      ```bash
      /opt/kafka/bin/kafka-console-producer.sh --topic test --bootstrap-server localhost:9092
         message 1
         message 2
         ...
      ```

13. Read test messages

      ```bash
      /opt/kafka/bin/kafka-console-consumer.sh --topic test --from-beginning --bootstrap-server localhost:9092
      ```

## Kafka encryption

1. Generate server keystore with certificate pair.

   Complete:
    - Certificate validity period;
    - The name of the alias;
    - The FQDN of the server;
    - Server IP;

   ```bash
   keytool -keystore server.keystore.jks -alias {alias_name} -validity {validity} -genkey -keyalg RSA -ext SAN=DNS:{FQDN},IP:{server_IP}
   ```

2. Creating your own CA

   ```bash
   openssl req -new -x509 -keyout rootCA.key -out rootCA.crt -days 365
   ```

3. Import CA to server keystore and client keystore:

   ```bash
   keytool -keystore server.truststore.jks -alias CARoot -import -file rootCA.crt
   keytool -keystore client.truststore.jks -alias CARoot -import -file rootCA.crt
   ```

4. Create a certificate signing request:

   Complete:
    - The name of the alias;
    - The FQDN of the server;
    - Server IP;

   ```bash
   keytool -keystore server.keystore.jks -alias {alias_name} -certreq -file cert-file -ext SAN=DNS:{FQDN},IP:{server_IP}
   ```

5. Sign in certificate

   Complete:
    - The name of the alias;
    - The FQDN of the server;
    - Server IP;
    - Password

   ```bash
   openssl x509 -req -extfile <(printf"subjectAltName = DNS:{FQDN},IP:{server_IP}") -CA rootCA.crt -CAkey rootCA.key -in cert-file -out cert-signed -days 3650 -CAcreateserial -passin pass:{password}
   ```

6. Import rootCA and cert-signed to server keystore

   ```bash
   keytool -keystore server.keystore.jks -alias CARoot -import -file rootCA.crt
   keytool -keystore server.keystore.jks -alias els710 -import -file cert-signed
   ```

7. If you have trusted certificates, you must import them into the JKS keystore as follows:

   Create a keystore:

   Complete:
    - Certificate validity period;
    - The name of the alias;
    - The FQDN of the server;
    - Server IP;

   ```bash
   keytool -keystore client.keystore.jks -alias {alias_name} -validity {validity} -keyalg RSA -genkey
   ```

8. Combine the certificate and key file into a certificate in p12 format:

   Complete:
    - your cert name;
    - your key name;
    - friendly name;
    - CA cert file;

   ```bash
   openssl pkcs12 -export -in {your_cert_name} -inkey {your_key_name} -out {your_pair_name}.p12 -name {friendly_name} -CAfile ca.crt -caname root
   ```

9. Import the CA certificate into a truststore:

   Complete:
    - CA cert file;

   ```bash
   keytool -keystore client.truststore.jks -alias CARoot -import -file {CAfile}
   ```

10. Import the CA certificate into a keystore:

    Complete:

    - CA cert file.

    ```bash
    keytool -keystore client.keystore.jks -alias CARoot -import -file {CAfile}
    ```

11. Import the p12 certificate into a keystore:

    Complete:

    - Your p12 pair;
    - Keystore password;

    ```bash
    keytool -importkeystore -deststorepass {keystore_password} -destkeystore client.keystore.jks -srckeystore {your_pair_name}.p12 -srcstoretype PKCS12
    ```

### Configuring Kafka Brokers

1. In `/opt/kafka/server.properties` file set the following options:

   Complete:
    - Path to server keystore;
    - Keystore password;
    - Password for certificate key;
    - Path to server truststore;
    - Truststore password.

   ```yaml
   listeners=PLAINTEXT://localhost:9092,SSL://{FQDN}:9093
   ssl.keystore.location={path_to_server_keystore}/server.keystore.jks
   ssl.keystore.password={keysotre_passowrd}
   ssl.key.password={key_password}
   ssl.truststore.location={path_to_server_truststore}/server.truststore.jks
   ssl.truststore.password={truststore_passowrd}
   ssl.enabled.protocols=TLSv1.2
   ssl.client.auth=required
   security.inter.broker.protocol=SSL
   ```

2. Restart the Kafka service

   ```bash
   systemctl restart kafka
   ```

### Configuring Kafka Clients

1. Configure the output section in Logstash based on the following example:

   Complete:
    - Server FQDN;
    - Path to client truststore;
    - Truststore password.

   ```yaml
   output {
     kafka {
       bootstrap_servers => "{FQDN}:9093"
       security_protocol => "SSL"
       ssl_truststore_type => "JKS"
       ssl_truststore_location => "{path_to_client_truststore}/client.truststore.jks"
       ssl_truststore_password => "{password_to_client_truststore}"
       client_id => "host.name"
       topic_id => "Topic-1"
       codec => json
     }
   }
   ```

2. Configure the input section in Logstash based on the following example:

   Complete:
    - Server FQDN;
    - Path to client truststore;
    - Truststore password.

   ```yaml
   input {
     kafka {
       bootstrap_servers => "{}:port"
       security_protocol => "SSL"
       ssl_truststore_type => "JKS"
       ssl_truststore_location => "{path_to_client_truststore}/client.truststore.jks"
       ssl_truststore_password => "{password_to_client_truststore}"
       consumer_threads => 4
       topics => [ "Topic-1" ]
       codec => json
       tags => ["kafka"]
      }
   }
   ```

### Log retention for Kafka topic

The Kafka durably persists all published records—whether or not they have been consumed—using a configurable retention period. For example, if the retention policy is set to two days, then for the two days after a record is published, it is available for consumption, after which it will be discarded to free up space. Kafka's performance is effectively constant concerning data size so storing data for a long time is not a problem.

## Event Collector

The Event Collector allows you to get events from remote Windows computers and store them in the ITRS Log Analytics indexes. The destination log path for the events is a property of the subscription. The ITRS Log Analytics Event Collector allows to definition of an event subscription on an ITRS Log Analytics collector without defining the event source computers. Multiple remote event source computers can then be set up (using for example a group policy setting) to forward events to the ITRS Log Analytics. The Event Collector doesn't require installation of any additional applications/agents on Windows source hosts.

### Configuration steps

#### Installation of Event Collector

```bash
tar zxf wec_7x-master.tar.gz -C /opt/
mkdir /opt/wec
mv /opt/wec_7x-master/ /opt/wec/
mkdir /etc/wec
cp /opt/wec/sub_manager/config.yaml /etc/wec/config.yaml
```

#### Generate certificate

```bash
mkdir /opt/wec/certgen
cd /opt/wec/certgen
vim server-certopts.cnf
```

- Set `DNS.1` and `IP.1` for the WEC server:

  ```bash
  [req]
  default_bits = 4096
  default_md = sha256
  req_extensions = req_ext
  keyUsage = keyEncipherment,dataEncipherment
  basicConstraints = CA:FALSE
  distinguished_name = dn
  
  [ req_ext ]
  subjectAltName = @alt_names
  extendedKeyUsage = serverAuth,clientAuth
  
  [ alt_names ]
  DNS.1 = wec.local.domain
  IP.1 = 192.168.13.163
  
  [dn]
  ```

- Set `DNS.1` and `IP.1` for client certificate:

  ```bash
  vim client-certopts.cnf
  ```

  ```bash
  [req]
  default_bits = 4096
  default_md = sha256
  req_extensions = req_ext
  keyUsage = keyEncipherment,dataEncipherment
  basicConstraints = CA:FALSE
  distinguished_name = dn
  
  [ req_ext ]
  subjectAltName = @alt_names
  extendedKeyUsage = serverAuth,clientAuth
  
  [ alt_names ]
  DNS.1 = *local.domain
  
  [dn]
  ```

- Generate the CA certificate and private key, next check fingerprint:

  ```bash
  openssl genrsa -out ca.key 4096
  openssl req -x509 -new -nodes -key ca.key -days 3650 -out ca.crt -subj '/CN=wec.local.domain/O=example.com/C=CA/ST=QC/L=Montreal'
  openssl x509 -in ca.crt -fingerprint -sha1 -noout | sed -e 's/\://g' > ca.fingerprint
  ```

- Generate the client certificate and export it together with the CA in PFX format to be imported into the Windows certificate store:

  ```bash
  openssl req -new -newkey rsa:4096 -nodes -out server.csr -keyout server.key -subj '/CN=wec.local.domain/O=example.com/C=CA/ST=QC/L=Montreal'
  openssl x509 -req -in server.csr -out server.crt -CA ca.crt -CAkey ca.key -CAcreateserial -extfile server-certopts.cnf -extensions req_ext -days 365
  ```

- Generate the server certificate to be used by the WEC:

  ```bash
  openssl req -new -newkey rsa:4096 -nodes -out client.csr -keyout client.key -subj '/CN=wec.local.domain/O=example.com/C=CA/ST=QC/L=Montreal'
  openssl x509 -req -in client.csr -out client.crt -CA ca.crt -CAkey ca.key -CAcreateserial -extfile client-certopts.cnf -extensions req_ext -days 365
  openssl pkcs12 -export  -inkey client.key -in client.crt -certfile ca.crt -out client.p12
  ```

#### Event Collector Configuration

- Copy the server certificate and server key to the Event Collector installation directory:

  ```bash
  cp server.crt server.key /opt/wec/sub_manager/certificates/
  ```

- Edit configuration file `config.yaml`

  ```bash
  vim /etc/wec/config.yaml
  ```

  - set the following options:

  ```bash
  external_host: wec.local.domain
  #check ca.fingerprint file
  ca_fingerprint: 97DDCD6F3AFA511EED5D3312BC50D194A9C9FA9A
  certificate: /opt/wec/sub_manager/certificates/server.crt
  key: /opt/wec/sub_manager/certificates/server.key
  
  ```

  - set the output for Event Collector to Logstash forwarding:

  ```bash
  remote_syslog:
      # forward events to remote syslog server
      address: 192.168.13.170
      port: 5614
  ```

  - set the output to saving events to a local file:

  ```bash
  outputfile: /var/log/wec/events-{:%Y-%d-%m}.log
  ```

  - disable local syslog output:

  ```bash
  local_syslog: false
  ```

  - set the filter section:

  ```bash
  filters:
            # source list
    
    - source: 'Security'
            filter: '*[System[(Level=1 or Level=2 or Level=3 or Level=4 or Level=0 or Level=5) and (EventID=4672 or EventID=4624 or EventID=4634)]]'
       
       - source: 'Application'
            filter: '*[System[(Level=1 or Level=2 or Level=3 or Level=4 or Level=0 or Level=5)]]'
          
          - source: 'System'
            filter: '*[System[(Level=1 or Level=2 or Level=3 or Level=4 or Level=0 or Level=5)]]'
  ```

#### Install dependencies

1. Python 3.8 installation:

   ```bash
   sudo yum -y update
   sudo yum -y groupinstall "Development Tools"
   sudo yum -y install openssl-devel bzip2-devel libffi-devel
   sudo yum -y install wget
   wget https://www.python.org/ftp/python/3.8.3/Python-3.8.3.tgz
   tar xvf Python-3.8.3.tgz
   cd Python-3.8*/
   ./configure --enable-optimizations
   sudo make altinstall
   python3.8 --version
   ```

2. Python requirements installation:

   ```bash
   pip3.8 install PyYAML
   pip3.8 install sslkeylog
   ```

#### Running Event Collector service

   ```bash
   vim /etc/systemd/system/wec.service
   ```

   ```bash
   
   [Unit]
   Description=WEC Service
   After=network.target
   
   [Service]
   Type=simple
   ExecStart=/usr/local/bin/python3.8 /opt/wec/sub_manager/run.py -c /etc/wec/config.yaml
   Restart=on-failure
   RestartSec=42s
   StandardOutput=syslog
   StandardError=syslog
   SyslogIdentifier=wecservice
   
   [Install]
   WantedBy=multi-user.target
   
   ```

   ```bash
   systemctl daemon-reload
   systemctl start wc
   ```

#### Windows host configuration

1. Open the `Microsoft Management Console (mmc.exe)`, select `File -> Add/Remove Snap-ins`, and add the `Certificates` snap-in.

2. Select `Computer Account`.

3. Right-click the `Personal` node, and select `All Tasks > Import`.

4. Find and select the client certificate (client.p12) and import this file.

5. The `PKCS #12` archive contains the CA certificate as well.

6. Move the CA certificate to the `Trusted Root Certification Authorities` node after the import.

7. Give `NetworkService` access to the private key  file of the client authentication certificate:

8. To forward security logs:
   - In `CompMgmt.msc`, under `Local Users and Groups`, click `Groups > Event Log Readers` to open `Event Log Readers Properties`.
   - Add the "NETWORK SERVICE" account to the `Event Log Readers group`.

   8.1. For domain controller use "Group Policy Manager Editor" and edit: "Default Domain Controller Policy":

    - From `Computer Configuration` > `Policy`, expand `Windows Settings` > `Security Settings` > `Restricted Groups`;
    - From the contest menu add: `Add Group`
    - Add the following configuration:
       - Group = `BUILTIN\Event Log Readers`
          - Members = `NT Authority\NETWORK SERVICE`

9. Make sure the collector server is reachable from the Windows machine

10. Run `winrm qc` and accept changes on the Windows machine

11. Run `winrm set winrm/config/client/auth @{Certificate="true"}` on windows machine to enable certificate authentication

12. Open `gpedit.msc`

13. Under the `Computer Configuration node`, expand the `Administrative Templates` node, then expand the `Windows Components` node, and then select the `Event Forwarding` node.

14. Select the **SubscriptionManagers** setting and enable it. Click the **Show** button to add a subscription (use the CA thumbprint you saved earlier):

    ```cmd
    Server=https://<FQDN of the collector>:5986/wsman/SubscriptionManager/WEC,Refresh=<Refresh interval in seconds>,IssuerCA=<Thumbprint of the root CA>
    ```

    For example:

    ```cmd
    Server=HTTPS://logserver.diplux.com:5986/wsman/SubscriptionManager/WEC,Refresh=60,IssuerCA=549A72B56560A5CAA392078D9C38B52458616D2
    5
    ```

    NOTE: If you wish to set up multiple subscriptions because you want to forward Windows events to multiple event collectors (such as WEC), then you can do that here.

15. Run the `cmd` console with administrative privileges and make the following command

    ```cmd
    gpupdate /force
    ```

#### Logstash pipeline configuration

Create a directory for Event Collector pipeline configuration files:

```bash
mkdir /etc/logstash/conf.d/syslog_wec
```

Copy the following Logstash configuration files to the pipeline directory:

```bash
cp 001-input-wec.conf /etc/logstash/conf.d/syslog_wec/
cp 050-filter-wec.conf /etc/logstash/conf.d/syslog_wec/
cp 060-filter-wec-siem.conf /etc/logstash/conf.d/syslog_wec/
cp 100-output-wec.conf /etc/logstash/conf.d/syslog_wec/
```

#### Enabling Logstash pipeline

To enable the `syslog_wec` Logstash pipeline edit the `pipelie.yml` file:

```bash
vim /etc/logstash/pipeline.yml
```

Add the following section:

```bash
- pipeline.id: syslog_wec
  path.config: "/etc/logstash/conf.d/syslog_wec/*.conf"
```

And restart Logstash:

```bash
systemctl restart logstash
```

#### Elasticsearch template

Install the Elasticsearch template for the Event Collector data index:

```bash
curl -ulogserver:logserver -X PUT "http://localhost:9200/_template/syslog_wec?pretty" -H 'Content-Type: application/json' -d@template_wec.json
```

#### Building the subscription filter

1. Browse to Event Viewer

1. Right-click **Subscriptions** and **create subscription**

1. Click on Select Events and choose the type of logs that you want, for example, Event Level, Event Logs, Include Exclude Event ID, Keyword, etc.

1. Switch to XML view tab;

1. Copy the value of the `Select Path` key, for example:

   ```xml
   <QueryList>
     <Query Id="0" Path="Security">
       <Select Path="Security">*[System[(Level=1  or Level=2 or Level=3) and (EventID=4672 or EventID=4624 or EventID=4634)]]</Select>
     </Query>
   </QueryList>
   ```

   string to copy:

   ```xml
   *[System[(Level=1  or Level=2 or Level=3) and (EventID=4672 or EventID=4624 or EventID=4634)]]
   ```

1. Paste the above definition into the Event Collector configuration file in the `filters` section:

   ```bash
   vim /etc/wec/config.yaml
   ```

   ```yaml
         filters:
           - source: 'Security'
             filter: '*[System[(Level=1  or Level=2 or Level=3) and (EventID=4672 or EventID=4624 or EventID=4634)]]'
   
   ```

   Restart the Event Collector service

   ```bash
   systemctl restart wec
   ```

## Cerebro Configuration

Configuration file: `/opt/cerebro/conf/application.conf`

- Authentication

   ```bash

   auth = {
     type: basic
       settings: {
         username = "logserver"
         password = "logserver"
       }
   }
   ```

- A list of known Elasticsearch hosts

   ```bash
   hosts = [
     {
       host = "https://localhost:9200"
       name = "itrs-log-analytics"
       auth = {
         username = "logserver"
         password = "logserver"
       }
     }
   ]

   play.ws.ssl {
     trustManager = {
       stores = [
         { type = "PEM", path = "/etc/elasticsearch/ssl/rootCA.crt" }
       ]
     }
   } 
   play.ws.ssl.loose.acceptAnyCertificate=true
   ```

- SSL access to Cerebro

   ```bash
      http = {
        port = "disabled"
      }
      https = {
        port = "5602"
      }
      
      # SSL access to cerebro - no self signed certificates
      #play.server.https {
      #  keyStore = {
      #    path = "keystore.jks",
      #    password = "SuperSecretKeystorePassword"
      #  }
      #}
      
      #play.ws.ssl {
      #  trustManager = {
      #    stores = [
      #      { type = "JKS", path = "truststore.jks", password =       SuperSecretTruststorePassword"  }
      #    ]
      #  }
      #}
   ```

- service restart

   ```bash
    systemctl start cerebro
   ```

- register backup/snapshot repository for Elasticsearch

   ```bash
      curl -k -XPUT "https://127.0.0.1:9200/_snapshot/backup?pretty" -H 'Content-Type: plication/      json' -d'
      {
        "type": "fs",
        "settings": {
          "location": "/var/lib/elasticsearch/backup/"
        }
      }' -u logserver:logserver
   ```

- login using curl/kibana

   ```bash
      curl -k -XPOST 'https://192.168.3.11:5602/auth/login' -H 'mimeType: application/      -www-form-urlencoded' -d 'user=logserver&password=logserver' -c cookie.txt
      curl -k -XGET 'https://192.168.3.11:5602' -b cookie.txt
   ```

## Field level security

You can restrict access to specific fields in documents for a user role. For example: the user can only view specific fields in the Discovery module, other fields will be inaccessible to the user. You can do this by:

1. You can do this by adding the index to the `field includes` or `field excludes` in the `Create Role` tab.

    - Includes are only fields that will be visible to the user.
    - Excludes are fields that the user cannot see.

    ![](/media/media/image251.png)

1. After that, you will see the new role in the `Role list` tab.

    ![](/media/media/image252.png)

1. Add your user to the new `Role`

    ![](/media/media/image253.png)

You can now log in as a user with a new role, the user in the Discovery module should only see selected fields.

![](/media/media/image254.png)

## Default Language

### Changing default language for GUI

The GUI language can be changed as follows:

1. Add `.i18nrc.json` to `/usr/share/kibana/` directory:

   ```json
   {
       "translations": ["translations/ja-JP.json"]
   }
   ```

2. Upload a translation to /usr/share/kibana/translations/ directory

3. Set the permission:

   `# chown -R kibana:kibana /usr/share/kibana/translations/`

4. Set in `kibana.yml` file:

   `i18n.locale: "ja-JP"`

5. Restart:

   `# systemctl restart kibana`

6. Finally, the result should be as shown in the picture:

   ![](/media/media/image255.png)

### Preparing translation for GUI

Source file to use as a base for translations: `/usr/share/kibana/translations/en-EN.example.json`

#### Bullet points for translations

For the translation to work you have to follow these steps. \
Omitting some may result in missing translation in some parts of an application or an empty screen when entering a broken portion of an app.

The file with translation is JSON.

Translated values have the following structure:

```json
{
    "message": {
      "key.for.the.value": "Translated value for the key"
    }
}

```

Every key is meant to be unique. There can be only one value for each key. In the `messages` object, each key has a "text" value, not a number and not an object.

But there are some structures in a source file that you will use as a base of your translation that have to be addressed during the process to achieve that.

1. Objects

    ```json
    {
      "messages": {
        "common.ui.aggTypes.buckets.filtersTitle": {
          "text": "Filters",
          "comment": "The name of an aggregation, that allows to specify multiple individual filters to group data by."
        }
      }
    }
    ```

    This has to be transformed as described above - a key `common.ui.aggTypes.buckets.filtersTitle` has to have a text assigned to it. The value that needs to be translated is in the fields "text" and "comment" described to you how the value needs to be translated. The result of such will be:

    ```json
    {
      "messages":{
        "common.ui.aggTypes.buckets.filtersTitle": "Filtry"
      }
    }
    ```

1. Template variables

    ```json
    {
      "messages": {
        "common.ui.aggTypes.buckets.dateHistogramLabel": "{filedName} per {intervalDescription}"
      }
    }
    ```

    Any text that is encapsulated in `{}` has to be left as is. Those values are substituted by the application.

1. How to treat complicated structures, eg.: plurals, etc.

   ```json
   {
    "messages": {
      "kbn.discover.hitsPluralTitle": "{hits, plural, one {hit} other {hits}}"
    }
   }
   ```

   As of now, there is a single example of the above. Contrary to the last point the value in `{}` has to be translated for that key. So `{hit}` and `{hits}`.

1. React compliant filenames

    In the application codebase, some methods will take translated keys and substitute them. But many of those will work only if the name of the translation file is one of:
      - `en`
      - `en-US`
      - `en-xa`
      - `es`
      - `es-LA`
      - `fr`
      - `fr-FR`
      - `de`
      - `de-DE`
      - `ja`
      - `ja-JP`
      - `ko`
      - `ko-KR`
      - `zh`
      - `zh-CN`
      - `pl`
      - `ru`
      - `ru-BY`
      - `ru-KG`
      - `ru-KZ`
      - `ru-MD`
      - `ru-UA`

#### FAQ

1. Can I just paste everything into a basic(or advanced) translation software? \
     ~No. There are some points to follow for the translation file to work at all.

1. I have the following error - is the application broken:
    - **Error formatting message: A message must be provided as a String or AST** \
     ~It is possible you have not followed point 1 - you have left some object structures in your file.
    - **Blank  page in GUI** \
     ~It is usually caused by not following point 2 -some variable names were changed.

1. I have set "i18n.locale" in the configuration file but the app is not translated. \
     ~You may have forgotten to put a reference for your file in `.i18nrc.json` file.

#### Known issues

1. Some text may not be translated in **Management -> Advanced settings** even though keys for them are present in translation files.

1. The same thing may happen in **Discover -> View surrounding documents**.

1. Not an issue but plugin names (links on the left menu) do not translate.
