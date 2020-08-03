---
 
copyright:
  years: 2018, 2020
lastupdated: "2020-03-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# {{site.data.keyword.databases-for}} CLI
{: #cdb-reference}

The {{site.data.keyword.databases-for}} CLI plug-in offers extra methods of accessing the capabilities of the {{site.data.keyword.databases-for}} services. You can use {{site.data.keyword.databases-for}} CLI to manage and connect to 
- {{site.data.keyword.databases-for-postgresql_full}} 
- {{site.data.keyword.databases-for-enterprisedb_full}}
- {{site.data.keyword.databases-for-redis_full}} 
- {{site.data.keyword.databases-for-elasticsearch_full}}
- {{site.data.keyword.databases-for-etcd_full}}
- {{site.data.keyword.messages-for-rabbitmq_full}}
- {{site.data.keyword.databases-for-mongodb_full}}

**Note**: The {{site.data.keyword.databases-for}} CLI plug-in requires IBM Cloud CLI to be installed.

## The {{site.data.keyword.cloud_notm}} CLI
{: #install_cli}

The {{site.data.keyword.cloud_notm}} CLI is a general-purpose developer tool that provides access to your {{site.data.keyword.cloud_notm}} account and services through a command-line interface.

An introduction and installation instructions are available on the [{{site.data.keyword.cloud_notm}} CLI Overview](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud-cli) page. If you install the CLI from the cURL command that is provided, you get a selection of extra plug-ins and extensions for multiple IDEs.
 
You can install just the stand-alone package from the [Installing the stand-alone IBM Cloud CLI](/docs/cli/reference/ibmcloud?topic=cloud-cli-install-ibmcloud-cli) page. 

Access to services via {{site.data.keyword.cloud_notm}} CLI is governed through Identity and Access Management. In order to use the CLI to view or manage a service (or to grant privileges to another user on your account), you must set the correct permissions. For more information about IAM management, see the [IAM Getting Started tutorial](/docs/iam?topic=iam-getstarted)

## Installing the {{site.data.keyword.databases-for}} CLI plug-in
{: installing_cli_plugin}

Once you have the {{site.data.keyword.cloud_notm}} CLI, [login](/docs/cli/reference/ibmcloud?topic=cloud-cli-ibmcloud_cli#ibmcloud_login) and ask it to install the cloud databases plug-in. 
 
`ibmcloud plugin install cloud-databases`
 
Use `ibmcloud cdb help` for a list of commands and usage information.

## `ibmcloud cdb help`
{: #help}

Display help for the plug-in. Alone, this command displays the available top-level commands. Followed by another command, it displays specific help for that command.

```
ibmcloud cdb help [<command>]
```

**Command options**  
No command-specific options.
 
**Examples**
Get help on the task-show command.
```
ibmcloud cdb help task-show
```



## Deployments and Deployables
{: #deployments-and-deployables}

Get information about the deployable databases and database versions on the {{site.data.keyword.databases-for}} platform. Also, get a list of all of the {{site.data.keyword.databases-for}} on your {{site.data.keyword.cloud_notm}} account.

### `ibmcloud cdb deployables-show`
{: #deployables-show}

The `deployables` are the templates available for new database deployments. This command shows deployable database types, specifically the available versions of databases, and their preferred or stable status.

```
ibmcloud cdb deployables-show [--stable] [--preferred] [--json]
```

Short version - `deployables`

**Command options**  
<dl>
   <dt>`--stable` or `-s`</dt>
   <dd>Only list stable versions of databases.</dd>
   <dt>`--preferred` or `-p`</dt>
   <dd>Only list preferred versions of databases.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
</dl>

 
**Examples**
Show all the stable versions of databases available.
```
ibmcloud cdb deployables-show --stable
```

### `ibmcloud cdb deployments`
{: #deployments}

Short version - `ls`

Use this command to list the deployments associated with the account.

```
ibmcloud cdb deployments [--all] [--json]
```

**Command options**
<dl>
   <dt>`--all` or `-a`</dt>
   <dd>Display instance name and CRN.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
</dl>
 
**Examples**
List all current deployments with an account.
```
ibmcloud cdb ls
```

### `ibmcloud cdb deployment-about`
{: #deployment-about}

Short version - `about`

Use this command to get details of which database is deployed within the instance, which version and any options applied. Also displayed are the ID and GUID for the resource controller, resource plans, current state, type, and last known operation.

```
ibmcloud cdb deployment-about <deployment name or CRN> [--all] [--json]
```

**Command options**  
<dl>
   <dt>`--all` or `-a`</dt>
   <dd>Display all the available data from the resource controller's records.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
</dl>
 
**Examples**
List details of a deployment named "RedisDBOne".
```
ibmcloud cdb about RedisDBOne
```


## Connections
{: #connections}

Get connection strings and certificate information to use when you connect to your deployment. Manage connections for those databases that have the option.

### `ibmcloud cdb deployment-connections`
{: #deployment-connections}

Short version - `cxn`

Displays connection strings and other connection details for a deployment with or without user credentials inserted. 

```
ibmcloud cdb deployment-connections [--user <userid>] [--password <password>] [--endpoint-type <endpoint type>] [--all] [--only] [--start] [--certroot <path>] [--json]
```

**Command options**  
<dl>
   <dt>`--start` or `-s`</dt>
   <dd>Start a connection by running the CLI command generated. If a password isn't specified in the flags, the command prompts for a password interactively. The plug-in uses the default commands for command-line interaction and managing the CA certificate to ensure a secure TLS session. Defaults to connecting as the deployment's admin user.</dt>
   <dt>`--user <userid>` or `-u`</dt>
   <dd>Sets the user ID that is used when retrieving connection settings. It is substituted into connection strings. Defaults to the deployment's admin user.</dd>
   <dt>`--password <password>` or `-p`</dt>
   <dd>Sets the password that is used when retrieving connection settings. It is substituted into connection strings where $PASSWORD appears as default.</dt>
   <dt>`--endpoint-type [public or private]` or `-e [public or private]`</dt>
   <dd>Endpoint type for returned connection strings. Either 'public' or 'private'. (default: "public"). Endpoint type is not enforced and is only for display purposes.</dd>
   <dt>`--all` or `-a`</dt>
   <dd>Lists all connection settings available including component parts of connection strings.</dt>
   <dt>`--certroot <path>` or `-c`</dt>
   <dd>Use the path as the certificate root. If the path doesn't exist, it is created automatically. Works with the `--save` flag. The certificate root value can also be set in the `$CERTROOT` environment variable.</dd>
   <dt>`--only [app or cli]` or `-o`</dt>
   <dd>Show only the settings that are relevant to `app` connections or `cli` connections.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
</dl>

 
**Examples**
Display how to connect to a deployment.
```
ibmcloud cdb deployment-connections MyPSQL
```
(Shows a connection string and a CLI command string)

Connect to a deployment as admin.
```
ibmcloud cdb deployment-connections MyPSQL --start
```
When run, the plug-in prompts for the admin password, then runs the CLI command string. The command that is used in the CLI command string must be installed.

Show all details of how to make a connection to a deployment for a particular user and password combination.
```
ibmcloud cdb cxn MyPSQL -a -u auser -p auserpassword
```

### `ibmcloud cdb deployment-cacert`
{: #deployment-cacert}

Short version - `cacert`

Display the self-signed certificate that is used for verifying TLS/SSL connections to the deployment. The result is, by default, output to the console but can be saved to a file too.

```
ibmcloud cdb deployment-cacert <deployment name or CRN> [--user <userid>] [--save] [--certroot <path>] [--json]
```

**Command options**
<dl>
   <dt>`--user <userid>` or `-u`</dt>
   <dd>By default, the admin user is used to obtain the certificate. This flag optionally allows a user to be specified where the deployment supports per user certificates.</dd>
   <dt>`--save` or `-s`</dt>
   <dd>Save the decoded certificate into the certificate root directory. The default is $HOME/.cloud/plugins/cdb/cdbcerts/.</dd>
   <dt>`--certroot <path>` or `-c`</dt>
   <dd>Use the path as the certificate root directory. If the path doesn't exist, it is created automatically. Works with the `--save` flag. The certificate root value can also be set in the `$CERTROOT` environment variable.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
</dl>

 
**Examples**
Display the certificate for a deployment named MyPostgreSQL.
```
ibmcloud cdb deployment-cacert MyPostgreSQL
```

Save a certificate for the same deployment in the current directory. 
```
ibmcloud cdb deployment-cacert MyPostgreSQL --save --certroot .
```
Note: The file name is based on the certificate name.


### `ibmcloud cdb deployment-kill-connections`
{: deployment-kill-connections}

Short version - `kill-connections`

Closes all the connections on a deployment. Available for PostgreSQL ONLY.
```
ibmcloud cdb deployment-kill-connections <deployment name or CRN> [--nowait] [--json]
```

**Command options**  
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the user creation task to complete. Display the user creation task details and exit.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
</dl>

**Examples**
This command kills all of the external connections to a deployment named `postgresq-preproduction`.
```
ibmcloud cdb deployment-kill-connections postgresq-preproduction
```

## Users
{: #users}

Create, delete, or change the password for users on your deployment.

### `ibmcloud cdb deployment-user-create`
{: #deployment-user-create}

Short version - `user-create`

Create a user on the deployment database.

```
ibmcloud cdb deployment-user-create <deployment name or CRN> <newusername> <newpassword> [--nowait] [--json] 
```

The `newusername` needs to be a correctly formatted username for use on the deployment's database. The `newpassword` needs to comply with the database's password rules and must be at least 10 characters long.

**Command options**  
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the user creation task to complete. Display the user creation task details and exit.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
</dl>

 
**Examples**
Create a database user called "fred" with a password of "X1234Y5678" on the "MyPSQL" deployment.

```
ibmcloud cdb deployment-user-create MyPSQL fred X1234Y5678
```


### `ibmcloud cdb deployment-user-delete`
{: #deployment-user-delete}

Short version - `user-delete`

Removes an existing user from the specified database deployment.

```
ibmcloud cdb deployment-user-delete <deployment name or CRN> <username> [--nowait] [--json]
```

**Command options**  
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the user deletion task to complete. Display the user deletion task details and exit.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
</dl>

 
**Examples**
Remove the database user called "fred" from the "MyPSQL" deployment
```
ibmcloud cdb deployment-user-delete MyPSQL fred
```


### `ibmcloud cdb deployment-user-password`
{: #deployment-user-password}

Short version - `user-password`

Changes the password for a named user on a specified database deployment.

```
ibmcloud cdb deployment-user-password <deployment name or CRN> <username> <newpassword> [--nowait] [--json]
```

**Command options**  
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the user password change task to complete. Display the user password change task details and exit.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
</dl>

**Examples**
Change the password of user "fred" on the database deployment "MyPSQL" to "A9876B5432"
```
ibmcloud cdb deployment-password MyPSQL fred A9876B5432
```



## Database Configuration
{: #database-configuration}

Lists or Changes configurable settings on a deployment. The new configuration is specified in a JSON file or JSON string of settings. Settings vary by database type, see _Changing the Database Configuration_ for [PostgreSQL](/docs/services/databases-for-postgresql?topic=databases-for-postgresql-changing-configuration) or for [Redis](/docs/services/databases-for-redis?topic=databases-for-redis-changing-configuration).

### `ibmcloud cdb deployment-configuration-schema`
{: #deployment-configuration-schema}

Short version - `config-schema`

Gets the current configuration of the specified deployment.
```
ibmcloud cdb deployment-configuration-schema <deployment name or CRN> [--description] [--json]
```

**Command options**
<dl>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
   <dt>`--description` or `-d`</dt>
   <dd>Show settings description.</dd>
</dl>

**Examples**
```
ibmcloud cdb deployment-configuration-schema my-redis-cache
```


### `ibmcloud cdb deployment-configuration`
{: #deployment-configuration}

Short version - `configuration`

Changes the configuration of the specified deployment.

```
ibmcloud cdb deployment-configuration <deployment name or CRN> [@JSON_FILE | JSON_STRING] [--json] [--nowait]
```

**Command options**
<dl>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the group setting task to complete. Display the scaling task's details and exit.</dd>
</dl>

**Examples**
Change the max_connections for a PostgreSQL deployment named "PGSettings4" to 150.
```
ibmcloud cdb deployment-configuration PGSettings4 '{"configuration":{"max_connections":150}}'
```


## Scaling
{: #scaling}

Retrieve and configure the resources that are allocated to your deployment. 

### `ibmcloud cdb deployables-groups-show`
{: #deployables-groups-show}

Each deployment is created from a deployable template. The `deployables-groups-show` command shows the initial or default scaling group for a particular type of database. The type names can be discovered through the `deployables-show` command.

```
ibmcloud cdb deployables-groups-show <deployable type> [--json]
```

**Command options**  
<dl>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
</dl>   

**Examples**
Show the default group settings for a PostgreSQL database deployment
```
ibmcloud cdb deployables-groups-show postgresql
```


### `ibmcloud cdb deployment-groups`
{: #deployment-groups}

Short version - `groups`

Displays the scaling group values for a deployment's members. The scaling groups relate to Memory, CPU, and Disk. The default group is named "member". For each group, the number of nodes in the group are shown followed by
* **Memory** The total memory allocation, the allocation per member, the minimum allocation and the increments the total memory can be varied by.
* **CPU** The number of CPUs dedicated to the group. The CPU section shows 0 values in all the fields when no dedicated CPUs are configured. The CPU group is only displayed when it is adjustable.
* **Disk** The total disk allocation, the allocation per member, the minimum allocation and the increments the total disk can be varied by.

```
ibmcloud cdb deployment-groups <deployment name or CRN> [--json]
```

**Command options**  
<dl>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
</dl>

**Examples**
Display the scaling group settings for a database deployment named "MyRedis"
```
ibmcloud cdb deployment-groups MyRedis
```


### `ibmcloud cdb deployment-groups-set`
{: #deployment-groups-set}

Short version - `groups-set`

Sets the values for scaling groups (see deployment-groups). The user is able to set the total memory size in MB or total disk storage in MB, both of which are which is evenly divided between the members. Where available, the number of allocated CPUs can also be set.

```
ibmcloud cdb deployment-groups-set <deployment name or CRN> <memberid> [--memory <memory size>] [--disk <disk size>] [--cpu <value>] [--nowait] [--json]
```

The `memberid` is the name of the group for which these values are to be set. The name can be found through the `deployment-groups` command. Typically, it is "member".

**Command options**  
<dl>
   <dt>`--memory <memory size>` or `-m`</dt>
   <dd>Set the specified deployment group's total memory, a value in MB.</dd>
   <dt>`--disk <disk size>` or `-d`</dt>
   <dd>Set the specified deployment group's total disk size, a value in MB.</dd>
   <dt>`--cpu <value>` or `-c`</dt>
   <dd>Set number of dedicated CPU cores.</dd>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the group setting task to complete. Display the scaling task's details and exit.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Results as JSON.</dd>
</dl>

**Examples**
Set a PostgreSQL deployment named "MyPGSQL" with a "member" group to have a total memory to 4096 MB.
```
ibmcloud cdb deployment-groups-set MyPGSQL member --memory 4096
```

## Autoscaling
{: #autoscaling}

The Autoscaling configuration represents the various conditions that control autoscaling for a deployment. 

### `ibmcloud cdb deployment-autoscaling`

Short version - `autoscaling`

Retrieve of all autoscaling conditions for a particular deployment. 
```
ibmcloud cdb deployment-autoscaling <deployment name or CRN> GROUP_ID [--json]
```
Autoscaling currently only applies to the data members on your deployment, so the `GROUP_ID` is `member`.

**Command options**  
<dl>
   <dt>`--json` or `-j`</dt>
   <dd>Return the results as JSON.</dd>
</dl>

**Examples**
```
ibmcloud cdb deployment-autoscaling elasticsearch-preproduction member
```

### `ibmcloud cdb deployment-autoscaling-set`

Short version - `autoscaling-set`

Enable, disable, or set the conditions for autoscaling on your deployment.
```
ibmcloud cdb deployment-autoscaling-set (NAME|ID) GROUP_ID (@JSON_FILE|JSON_STRING) [--json] [--nowait]
```
Autoscaling currently only applies to the data members on your deployment, so the `GROUP_ID` is `member`. The autoscaling parameters that you would like to be set or unset are defined in a JSON object.

**Command options**  
<dl>
   <dt>`--json` or `-j`</dt>
   <dd>Return the results as JSON.</dd>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for command completion.</dd>
</dl>

**Examples**
This command sets memory to autoscale when I/O utilization hits a certain threshold for a deployment named `elasticsearch-preproduction`.
```
ibmcloud cdb deployment-autoscaling-set elasticsearch-preproduction member '{"autoscaling": { "memory": {"scalers": {"io_utilization": {"enabled": true, "over_period": "5m","above_percent": 90}},"rate": {"increase_percent": 10.0, "period_seconds": 300,"limit_mb_per_member": 125952,"units": "mb"}}}}'
```

## Read-only Replicas
{: #read-only-replicas}

Retrieve and configure read-only replicas. Currently, only PostgreSQL deployments support read-only replicas.

### `ibmcloud cdb deployment-read-replicas`
{: #deployment-read-replicas}

Short version - `read-replicas`

Lists all the read-only replicas for the specified deployment. 

```
ibmcloud cdb deployment-read-replicas <deployment name or CRN> [--long] [--json]
```

**Command options**  
<dl>
   <dt>`--json` or `-j`</dt>
   <dd>Return the results as JSON.</dd>
   <dt>`--long` or `-l`</dt>
   <dd>Shows additional fields in the output.</dd>
</dl>

**Examples**
List the read-only replicas for a PostgreSQL deployment named "MyPGSQL".
```
ibmcloud cdb deployment-read-replicas MyPGSQL
```

### `ibmcloud cdb read-replica-leader`
{: #read-replica-leader}

Short version - `rr-leader`

Returns the leader for the specified read-only replica deployment.

```
ibmcloud cdb read-replica-leader <deployment name or CRN> [--long] [--json]
```

**Command options**  
<dl>
   <dt>`--json` or `-j`</dt>
   <dd>Return the results as JSON.</dd>
   <dt>`--long` or `-l`</dt>
   <dd>Shows additional fields in the output.</dd>
</dl>

**Examples**
List the leader for a PostgreSQL read-only replica deployment named "MyPGSQL-replica".
```
ibmcloud cdb read-replica-leader MyPGSQL-replica
```


### `ibmcloud cdb read-replica-promote`
{: #read-replica-promote}

Short version - `rr-promote`

Promotes the read-only replica to a stand-alone instance.

```
ibmcloud cdb read-replica-promote <deployment name or CRN> [--json] [--nowait] [--skip-initial-backup]
```

**Command options**  
<dl>
   <dt>`--json` or `-j`</dt>
   <dd>Return the results as JSON.</dd>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for command completion.</dd>
   <dt>`--skip-initial-backup` or `s`</dt>
   <dd>Option to restore instance without taking a backup once data is restored. Allows restored deployment to be available sooner.</dd>
</dl>

**Examples**
Promotes a PostgreSQL read-only replica deployment named "MyPGSQL-replica" to a stand-alone deployment.
```
ibmcloud cdb read-replica-promote MyPGSQL-replica
```

### `ibmcloud cdb read-replica-resync`
{: #read-replica-resync}

Short version - `rr-resync`

Resyncs the read-only replica.

```
ibmcloud cdb read-replica-resync <deployment name or CRN> [--json] [--nowait]
```

**Command options**  
<dl>
   <dt>`--json` or `-j`</dt>
   <dd>Return the results as JSON.</dd>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for command completion.</dd>
</dl>

**Examples**
Resyncs a PostgreSQL read-only replica deployment named "MyPGSQL-replica".
```
ibmcloud cdb read-replica-resync MyPGSQL-replica
```



## Backups
{: #backups}

Manage the backups on your deployment or take an on-demand backup.

### `ibmcloud cdb deployment-backups-list`
{: #deployment-backups-list}

Short version - `backups`

Displays a list of backups that are associated with a deployment. The result is a table that is composed of the backups ID, type, status, and date of creation. The results are sorted with most recent backups first.

```
ibmcloud cdb deployment-backups-list <deployment name or CRN> [--scheduled] [--first] [--json]
```

**Command options**  
<dl>
   <dt>`--scheduled` or `-s`</dt>
   <dd>Output only scheduled backups.</dd>
   <dt>`--first` or `-f`</dt>
   <dd>Output only the first (or most recent) backup found.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
</dl>

**Examples**
Display the backups available on a deployment named "Postgres2000"
```
ibmcloud cdb backups Postgres2000
```


### `ibmcloud cdb backup-show`
{: #backup-show}

Show details about a backup. The backup is identified by its CRN ID as shown with the `deployment-backups-list` command.

```
ibmcloud cdb backup-show <CRN> [--json]
```

**Command options**
<dl>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
</dl>
 
**Examples**
Show details of a particular backup.
```
ibmcloud cdb backup-show crn:v1:bluemix:public:databases-for-postgresql:us-south:a/54e8ffe85dcedf470db5b5ee6ac4a8d8:1b8f53db-fc2d-4e24-8470-f82b15c71717:backup:ebcea542-8d8c-4b6e-a7d4-922ffd08eb50
```


### `ibmcloud cdb deployment-backup-now`
{: #deployment-backup-now}

Short version - `backup-now`

Initiated an on-demand backup on the deployment. The command polls the running backup and exits when it is completed.

```
ibmcloud cdb deployment-backup-now <deployment name or CRN> [--nowait] [--json]
```

**Command options**
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the backup task to complete. Display the backup task details and exit.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
</dl>

 
**Examples**
Create a backup of a deployment called "PgTips"
```
ibmcloud cdb deployment-backup-now PgTips
```



## Security
{: #security}

Manage the IP allowlist for your deployment.

### `ibmcloud cdb deployment-allowlist-list`
{: #deployment-allowlist-list}

Short version - `wl-ls`

Displays the current allowlist for a deployment.

```
ibmcloud cdb deployment-whitelist-list <deployment name or CRN> [--json]
```

**Command options**  
<dl>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
</dl>
 
**Examples**
List the current allowlist for the "MyPSQL" deployment
```
ibmcloud cdb deployment-whitelist-list MyPSQL
```


### `ibmcloud cdb deployment-whitelist-add`
{: #deployment-allowlist-add}

Short version - `wl-add`

Add an IP address or range to the current allowlist for a deployment. An IP address is an IPv4 or IPv6 address while a range is a masked IPv4 address, for example, 1.2.3.0/24. The description is required to be a human readable string that describes the allowlisted address or range.

```
ibmcloud cdb deployment-whitelist-add <deployment name or CRN> <allowlist address or range> <description> [--nowait] [--json]
```

**Command options**  
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the allowlist add task to complete. Display the allowlist add task details and exit.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
</dl>

 
**Examples**
Add the IP address 198.51.100.1 to the current allowlist for the "MyPSQL" deployment
```
ibmcloud cdb deployment-whitelist-add MyPSQL 198.51.100.1 "allowlisted for testing"
```

Add the IP range 198.51.100.0 to 198.51.100.255 to the current allowlist for the "MyPSQL" deployment
```
ibmcloud cdb deployment-whitelist-add MyPSQL 198.51.100.0/24 "Testing range is now open"
```


### `ibmcloud cdb deployment-whitelist-delete`
{: #deployment-allowlist-delete}

Short version - `wl-del`

Removes an IP address or range from the current allowlist for a deployment. An IP address is an IPv4 or IPv6 address while a range is a masked IPv4 address, for example, 1.2.3.0/24. 
```
ibmcloud cdb deployment-whitelist-delete <deployment name or CRN> <allowlist address or range> [--nowait] [--json]
```

**Command options**  
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the allowlist delete task to complete. Display the allowlist delete task details and exit.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
</dl>

 
**Examples**
Remove the IP address 198.51.100.1 from the current allowlist for the "MyPSQL" deployment
```
ibmcloud cdb deployment-whitelist-delete MyPSQL 198.51.100.1 "allowlisted for testing"
```

Remove the IP range 198.51.100.0 to 198.51.100.255 from the current allowlist for the "MyPSQL" deployment
```
ibmcloud cdb deployment-whitelist-delete MyPSQL 198.51.100.0/24 "Testing range is now open"
```


## Tasks
{: #tasks}

Tasks are created whenever you perform an action on your deployment. Tasks include things like taking a backup, group scaling, and changing a user password. Most `cdb` commands poll the running task and exit when it completes. You can change this behavior with the `--nowait` flag, which returns task information and exits. Records of successful tasks are shown for 24 - 48 hours, and unsuccessful tasks are shown for 7 - 8 days. A historical record of tasks from any time period is available through the [Activity Tracker integration](/docs/cloud-databases?topic=cloud-databases-activity-tracker).

### `ibmcloud cdb deployment-tasks-list`
{: #deployment-tasks-list}

Short version - `tasks`

Displays a list of all tasks that have been run on a specified deployment since it was created. Each task is displayed with its CRN, readable description, percentage completeness, status, and date of creation.

```
ibmcloud cdb deployment-tasks-list <deployment name or CRN> [--json]
```

**Command options**  
<dl>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
</dl>   

**Examples**
Display a list of the tasks that have been run against a deployment named "NewRedis"
```
ibmcloud cdb deployment-tasks-list NewRedis
```

### `ibmcloud cdb task-show`
{: #task-show}

Short version - `task`

Show the status of a particular task. The task is identified by its CRN ID as shown with the `deployment-tasks-list` command. If the task is running, the command waits for the task to complete, reporting status changes as it regularly polls.

```
ibmcloud cdb task-show <CRN> [--nowait] [--json]
```

**Command options**
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the task to complete. Display the user password change task details and exit.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Display results as JSON.</dd>
</dl>

**Examples**
Show details of a particular backup task.
```
ibmcloud cdb task-show crn:v1:bluemix:public:databases-for-postgresql:us-south:a/54e8ffe85dcedf470db5b5ee6ac4a8d8:1b8f53db-fc2d-4e24-8470-f82b15c71717:task:0faea465-de5a-4f14-a5ff-b402fefbd652
```


## Elasticsearch
{: #elasticsearch}

Perform tasks specific to Elasticsearch deployments.

### `ibmcloud cdb elasticsearch file-sync`
{: #elasticsearch-file-sync}

Short version - `fs`

Synchronizes files from the `ibm_file_sync` index to disk. For more information, see the [Uploading Files to Elasticsearch](/docs/services/databases-for-elasticsearch?topic=databases-for-elasticsearch-uploading-files) documentation for more information.

```
ibmcloud cdb elasticsearch file-sync <deployment name or CRN> [--json] [--nowait]
```

**Command options**  
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the group setting task to complete. Display the scaling task's details and exit.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Return the results as JSON.</dd>
</dl>

**Examples**
Sync a file to disk on a deployment named "MyElasticsearch".
```
ibmcloud cdb elasticsearch file-sync MyElasticsearch
```


## PostgreSQL
{: #postgresql}

Perform tasks specific to PostgreSQL deployments.

### `ibmcloud cdb postgresql earliest-pitr-timestamp`
{: #postgresql-earliest-pitr-timestamp}

Short version - `ept`

Returns the earliest available time for point-in-time-recovery in ISO8601 UTC format. For more information, see the [Point in Time Recovery](/docs/databases-for-postgresql?topic=databases-for-postgresql-pitr) documentation for more information.

```
ibmcloud cdb postgresql earliest-pitr-timestamp <deployment name or CRN> [--json] [--nowait]
```

**Command options**
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the group setting task to complete. Display the scaling task's details and exit.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Return the results as JSON.</dd>
</dl>

**Examples**
```
ibmcloud cdb postgresql earliest-pitr-timestamp postgresql-preproduction
```


### `ibmcloud cdb postgresql replication-slot-create`
{: #postgresql-replication-slot-create}

Short version - `rsc`

Creates a new PostgreSQL replication slot. For more information, see the [Wal2json](/docs/services/databases-for-postgresql?topic=databases-for-postgresql-wal2json) documentation for more information.

```
ibmcloud cdb postgresql replication-slot-create <deployment name or CRN> <databasename> <slotname> <plugintype> [--json] [--nowait]
```
The plug-in type is required to be "wal2json".

**Command options**  
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the group setting task to complete. Display the scaling task's details and exit.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Return the results as JSON.</dd>
</dl>

**Examples**
Create a replication slot on a deployment named "MyPostgres", database named "testdb", and slot named "slot1".
```
ibmcloud cdb postgresql replication-slot-create MyPostgres testdb slot1 wal2json
```

### `ibmcloud cdb postgresql replication-slot-delete`
{: #postgresql-replication-slot-delete}

Short version - `rsd`

Deletes the specified PostgreSQL replication slot. See the [Wal2json](/docs/services/databases-for-postgresql?topic=databases-for-postgresql-wal2json) documentation for more information.

```
ibmcloud cdb postgresql replication-slot-delete <deployment name or CRN> <slotname> [--json] [--nowait]
```

**Command options**  
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the group setting task to complete. Display the scaling task's details and exit.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Return the results as JSON.</dd>
</dl>

**Examples**
Deletes a replication slot on a deployment named "MyPostgres"  and slot named "slot1".
```
ibmcloud cdb postgresql replication-slot-delete MyPostgres slot1
```

## EnterpriseDB
{: #enterprisedb}

Perform tasks specific to EnterpriseDB deployments.

### `ibmcloud cdb enterprisedb earliest-pitr-timestamp`
{: #enterprisedb-earliest-pitr-timestamp}

Short version - `ept`

Returns the earliest available time for point-in-time-recovery in ISO8601 UTC format. For more informaiton, see the [Point in Time Recovery](/docs/databases-for-postgresql?topic=databases-for-postgresql-pitr) documentation for more information.

```
ibmcloud cdb enterprisedb earliest-pitr-timestamp <deployment name or CRN> [--json] [--nowait]
```

**Command options**
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the group setting task to complete. Display the scaling task's details and exit.</dd>
   <dt>`--json` or `-j`</dt>
   <dd>Return the results as JSON.</dd>
</dl>

**Examples**
```
ibmcloud cdb enterprisedb earliest-pitr-timestamp enterprisedb-preproduction
```
