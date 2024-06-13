---
 
copyright:
  years: 2018, 2024
lastupdated: "2024-05-20"

keywords: cloud databases, migrating, disk size, memory size, CPU size, resources, cli, postgresql administrator, cloud database cli

subcollection: cloud-databases

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.databases-for}} CLI
{: #cdb-reference}

The {{site.data.keyword.databases-for}} CLI plug-in offers extra methods of accessing the capabilities of the {{site.data.keyword.databases-for}} services. You can use the {{site.data.keyword.databases-for}} CLI to manage and connect to the following services:
- [{{site.data.keyword.databases-for-postgresql_full}}](/docs/databases-for-postgresql)
- [{{site.data.keyword.databases-for-mysql_full}}](/docs/databases-for-mysql)
- [{{site.data.keyword.databases-for-enterprisedb_full}}](/docs/databases-for-enterprisedb)
- [{{site.data.keyword.databases-for-redis_full}}](/docs/databases-for-redis) 
- [{{site.data.keyword.databases-for-elasticsearch_full}}](/docs/databases-for-elasticsearch)
- [{{site.data.keyword.databases-for-etcd_full}}](/docs/databases-for-etcd)
- [{{site.data.keyword.messages-for-rabbitmq_full}}](/docs/messages-for-rabbitmq)
- [{{site.data.keyword.databases-for-mongodb_full}}](/docs/databases-for-mongodb)
- [{{site.data.keyword.databases-for-cassandra_full}}](/docs/databases-for-cassandra)

The {{site.data.keyword.databases-for}} CLI plug-in requires [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started) to be installed.
{: .note}

## The {{site.data.keyword.cloud_notm}} CLI
{: #install_cli}

The {{site.data.keyword.cloud_notm}} CLI is a general-purpose developer tool that provides access to your {{site.data.keyword.cloud_notm}} account and services through a command-line interface.

An introduction and installation instructions are available on the [{{site.data.keyword.cloud_notm}} CLI Getting Started page](/docs/cli?topic=cli-getting-started){: .external}. If you install the CLI from the cURL command that is provided, you get a selection of extra plug-ins and extensions for multiple IDEs.
 
Install the stand-alone package from the [Installing the stand-alone IBM Cloud CLI](/docs/cli?topic=cli-install-ibmcloud-cli) page. 

Access to services via {{site.data.keyword.cloud_notm}} CLI is governed through Identity and Access Management. In order to use the CLI to view or manage a service (or to grant privileges to another user on your account), you must set the correct permissions. For more information about IAM management, see the [IAM Getting Started tutorial](/docs/account?topic=account-access-getstarted)

## Installing the {{site.data.keyword.databases-for}} CLI plug-in
{: #installing-cli-plugin}

Once you have the {{site.data.keyword.cloud_notm}} CLI, [log in](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login) and install the {{site.data.keyword.databases-for}} plug-in, using a command like:
```sh
ibmcloud plugin install cloud-databases
```
{: .pre}
 
For a list of commands and usage information, use a command like: 
```sh
ibmcloud cdb help
```
{: .pre}

## `ibmcloud cdb help`
{: #help}

On its own, the `ibmcloud cdb help` command displays the available top-level commands. When followed by another command, it displays specific help for that command.

```sh
ibmcloud cdb help [<command>]
```
{: .pre}

### Command options
{: #ibmcloud-cdb-help-cmd-options}

No command-specific options.
 
### Examples 
{: #ibmcloud-cdb-help-examples}

Get help on the task-show command.
```sh
ibmcloud cdb help task-show
```
{: .pre}

## Deployments and Deployables
{: #deployments-and-deployables}

Get information about the deployable databases and database versions on the {{site.data.keyword.databases-for}} platform. Also, get a list of all of the {{site.data.keyword.databases-for}} on your {{site.data.keyword.cloud_notm}} account.

### `ibmcloud cdb deployables-show`
{: #deployables-show}

The `deployables` are the templates available for new database deployments. This command shows deployable database types, specifically the available versions of databases, and their preferred or stable status.

```sh
ibmcloud cdb deployables-show [--stable] [--preferred] [--json]
```
{: .pre}

Short version - `deployables`

#### Command options  
{: #deployments-and-deployables-cmd-options}

- `--stable` or `-s`
   Only list stable versions of databases.
- `--preferred` or `-p`
   Only list preferred versions of databases.
- `--json` or `-j`
   Display results as JSON.

 
#### Examples
{: #deployments-and-deployables-examples}

Show all the stable versions of databases available.
```sh
ibmcloud cdb deployables-show --stable
```
{: .pre}

### `ibmcloud cdb deployments`
{: #deployments}

Short version - `ls`

Use this command to list the deployments associated with the account.

```sh
ibmcloud cdb deployments [--all] [--json]
```
{: .pre}

#### Command options
{: #deployments-cmd-options}

- `--all` or `-a`
   Display instance name and CRN.
- `--json` or `-j`
   Display results as JSON.
 
#### Examples
{: #deployments-examples}

List all current deployments with an account.
```sh
ibmcloud cdb ls
```
{: .pre}

### `ibmcloud cdb deployment-about`
{: #deployment-about}

Short version - `about`

Use this command to get details of which database is deployed within the instance, which version, and any options applied. Also displayed are the ID and GUID for the resource controller, resource plans, current state, type, and last known operation.

```sh
ibmcloud cdb deployment-about <deployment name or CRN> [--all] [--json]
```
{: .pre}

#### Command options
{: #deployment-about-cmd-options}

- `--all` or `-a`
   Display all the available data from the resource controller's records.
- `--json` or `-j`
   Display results as JSON.
 
#### Examples
{: #deployment-about-examples}

List details of a deployment named "RedisDBOne".
```sh
ibmcloud cdb about RedisDBOne
```
{: .pre}

## Connections
{: #connections}

Get connection strings and certificate information to use when you connect to your deployment. Manage connections for those databases that have the option.

### `ibmcloud cdb deployment-connections`
{: #deployment-connections}

Short version - `cxn`

Displays connection strings and other connection details for a deployment with or without user credentials inserted. 

```sh
ibmcloud cdb deployment-connections [--user <userid>] [--password <password>] [--endpoint-type <endpoint type>] [--all] [--only] [--start] [--certroot <path>] [--json]
```
{: .pre}

#### Command options
{: #connections-command-options}

- `--start` or `-s`
   Start a connection by running the CLI command generated. If a password isn't specified in the flags, the command prompts for a password interactively. The plug-in uses the default commands for command-line interaction and managing the CA certificate to ensure a secure TLS session. Defaults to connecting as the deployment's admin user.
- `--user <userid>` or `-u`
   Sets the user ID that is used when retrieving connection settings. It is substituted into connection strings. Defaults to the deployment's admin user.
- `--password <password>` or `-p`
   Sets the password that is used when retrieving connection settings. It is substituted into connection strings where $PASSWORD appears as default.
- `--endpoint-type [public or private]` or `-e [public or private]`
   Endpoint type for returned connection strings. Either 'public' or 'private'. (default: "public"). Endpoint type is not enforced and is only for display purposes.
- `--all` or `-a`
   Lists all connection settings available including component parts of connection strings.
- `--certroot <path>` or `-c`
   Use the path as the certificate root. If the path doesn't exist, it is created automatically. Works with the `--save` flag. The certificate root value can also be set in the `$CERTROOT` environment variable.
- `--only [app or cli]` or `-o`
   Show only the settings that are relevant to `app` connections or `cli` connections.
- `--json` or `-j`
   Display results as JSON.
- `--endpoint-type` or `-e`
   Endpoint type for returned connection strings, either `public` or `private`. Default is `public`.
   As the default is `public`, if there are no `public` endpoints then none will be found and you will receive an error: `{"errors":"not_found"}`. Use the `-e private` flag to use `private` endpoints. 

#### Examples
{: #connections-examples}

Display how to connect to a deployment.
```sh
ibmcloud cdb deployment-connections MyPSQL
```
{: .pre}

(Shows a connection string and a CLI command string)

Connect to a deployment as admin.
```sh
ibmcloud cdb deployment-connections MyPSQL --start
```
{: .pre}

When run, the plug-in prompts for the admin password, then runs the CLI command string. The command that is used in the CLI command string must be installed.

Show all details of how to make a connection to a deployment for a particular user and password combination.
```sh
ibmcloud cdb cxn MyPSQL -a -u auser -p auserpassword
```
{: .pre}

### `ibmcloud cdb deployment-cacert`
{: #deployment-cacert}

Short version - `cacert`

Display the self-signed certificate that is used for verifying TLS/SSL connections to the deployment. The result is, by default, output to the console but can be saved to a file too.

```sh
ibmcloud cdb deployment-cacert <deployment name or CRN> [--user <userid>] [--save] [--certroot <path>] [--json]
```
{: .pre}

#### Command options
{: #deployment-cacert-command-options}

- `--user <userid>` or `-u`
   By default, the admin user is used to obtain the certificate. This flag optionally allows a user to be specified where the deployment supports per user certificates.
- `--save` or `-s`
   Save the decoded certificate into the certificate root directory. The default is $HOME/.cloud/plugins/cdb/cdbcerts/.
- `--certroot <path>` or `-c`
   Use the path as the certificate root directory. If the path doesn't exist, it is created automatically. Works with the `--save` flag. The certificate root value can also be set in the `$CERTROOT` environment variable.
- `--json` or `-j`
   Display results as JSON.

#### Examples
{: #deployment-cacert-examples}

Display the certificate for a deployment named MyPostgreSQL.
```sh
ibmcloud cdb deployment-cacert MyPostgreSQL
```

Save a certificate for the same deployment in the current directory. 
```sh
ibmcloud cdb deployment-cacert MyPostgreSQL --save --certroot .
```
{: .pre}

Note: The file name is based on the certificate name.


### `ibmcloud cdb deployment-kill-connections`
{: #deployment-kill-connections}

Short version - `kill-connections`

Closes all the connections on a deployment. Available for PostgreSQL ONLY.
```sh
ibmcloud cdb deployment-kill-connections <deployment name or CRN> [--nowait] [--json]
```
{: .pre}

#### Command options  
{: #deployment-kill-connections-command-options}

- `--nowait` or `-n`
   Do not wait for the user creation task to complete. Display the user creation task details and exit.
- `--json` or `-j`
   Display results as JSON.


#### Examples
{: #deployment-kill-connections-examples}

This command kills all of the external connections to a deployment named `postgresq-preproduction`.
```sh
ibmcloud cdb deployment-kill-connections postgresq-preproduction
```
{: .pre}

## Capability
{: #capability}

The capability commands help you to identify which features are available and supported for your databases and backups.
```sh
ibmcloud cdb capability
```
{: pre}

### `capability-show`
{: #capability-show}

This command discovers if a capability is supported for a particular database type.

Short version - `cs`

```sh
ibmcloud cdb capability-show CAPABILITY_ID TYPE VERSION PLATFORM LOCATION TARGET_PLATFORM TARGET_LOCATION [--json] [--api-version]
```
{: pre}

#### Command options  
{: #capability-show-command-options}

- `--json` or `-j`
   Display results as JSON.
- `--api-version` or `-v`
   API Version used for request.
- `--hostflavor`
   Host flavor for groups capability.

#### Capability ID options
{: #capability-show-id-options}

- `autoscaling`
- `encryption`
- `endpoints`
- `groups`
- `locations`
- `point_in_time_recovery`
- `remotes`
- `restores`
- `versions`

#### Examples
{: #capability-show-examples}

```sh
ibmcloud cdb capability-show 5f2d37a0-40a5-4a39-bf6a-0dbb1249ac5e database 3.2.1 IBMCloud us-south
```
{: pre}

```sh
ibmcloud cdb capability-show groups postgresql 15 classic eu-gb classic us-south --hostflavor multitenant
```
{: pre}

```sh
ibmcloud cdb capability-show groups postgresql 15 classic eu-gb classic us-south --hostflavor b3c.4x16.encrypted
```
{: pre}

### `backup-capability-show`
{: #capability-backup-show}

This command discovers if a database type can be restored from a particular instance.

Short version - `bcs`

```sh
ibmcloud cdb discover-capability-information-from-backup (BACKUP_ID) (CAPABILITY_ID) (TARGET_PLATFORM) (TARGET_LOCATION) [--json] [--api-version] [--nowait]
```
{: pre}

#### Command options  
{: #capability-backup-show-command-options}

- `--json` or `-j`
   Display results as JSON.
- `--api-version` or `-v`   
   API Version used for request.

#### Capability ID options
{: #capability-backup-show-id-options}

- `restores`

#### Examples
{: #capability-backup-show-examples}

```sh
  ibmcloud cdb discover-capability-information-from-backup f7d318b6-6d4e-4d2a-9be4-7c1efbc94a52 5f2d37a0-40a5-4a39-bf6a-0dbb1249ac5e IBMCloud us-south --json --api-version 2021-09-30 --nowait
```
{: pre}

### `deployment-capability-show`
{: #deployment-capability-show}

This command discovers if a particular deployment or formation supports a particular capability.

Short version - `dcs`

```sh
ibmcloud cdb deployment-capability-show (NAME|ID) (CAPABILITY_ID) [--target-platform] [--target-location] [--json] [--api-version] [--nowait]
```
{: pre}

#### Command options  
{: #deployment-capability-show-command-options}

- `--json` or `-j`
   Display results as JSON.
- `--api-version` or `-v`   
   API Version used for request.
- `--target-platform` or `-p`
   Target platform for request
- `--target-location` or `-l`
   Target location for request

#### Capability ID options
{: #deployment-capability-show-id-options}

- `autoscaling`
- `encryption`
- `endpoints`
- `groups`
- `locations`
- `point_in_time_recovery`
- `remotes`
- `versions`

#### Examples
{: #deployment-capability-show-examples}

```sh
ibmcloud cdb deployment-capability-show my-deployment 5f2d37a0-40a5-4a39-bf6a-0dbb1249ac5e --target-location us-south --json --api-version 2021-09-30 --nowait
```
{: pre}

## Users
{: #users}

Create, delete, or change the password for users on your deployment.

### `ibmcloud cdb deployment-user-create`
{: #deployment-user-create}

Short version - `user-create`

Create a user on the deployment database.

```sh
ibmcloud cdb deployment-user-create <deployment name or CRN> <newusername> <newpassword> [--nowait] [--json] 
```
{: .pre}

The `newusername` needs to be a correctly formatted username for use on the deployment's database. The `newpassword` needs to comply with the database's password rules and must be at least 10 characters long.

#### Command options  
{: #deployment-user-create-command-options}

- `--nowait` or `-n`
   Do not wait for the user creation task to complete. Display the user creation task details and exit.
- `--json` or `-j`
   Display results as JSON.


 
#### Examples
{: #deployment-user-create-examples}

Create a database user called "fred" with a password of "X1234Y5678" on the "MyPSQL" deployment.

```sh
ibmcloud cdb deployment-user-create MyPSQL fred X1234Y5678
```
{: .pre}

### `ibmcloud cdb deployment-user-delete`
{: #deployment-user-delete}

Short version - `user-delete`

Removes an existing user from the specified database deployment.

```sh
ibmcloud cdb deployment-user-delete <deployment name or CRN> <username> [--nowait] [--json]
```
{: .pre}

#### Command options  
{: #deployment-user-delete-command-options}

- `--nowait` or `-n`
   Do not wait for the user deletion task to complete. Display the user deletion task details and exit.
- `--json` or `-j`
   Display results as JSON.
 
#### Examples
{: #deployment-user-delete-examples}

Remove the database user called "fred" from the "MyPSQL" deployment
```sh
ibmcloud cdb deployment-user-delete MyPSQL fred
```
{: .pre}

### `ibmcloud cdb deployment-user-password`
{: #deployment-user-password}

Short version - `user-password`

Changes the password for a named user on a specified database deployment.

```sh
ibmcloud cdb deployment-user-password <deployment name or CRN> <username> <newpassword> [--nowait] [--json]
```
{: .pre}

#### Command options  
{: #deployment-user-password-command-options}

- `--nowait` or `-n`
   Do not wait for the user password change task to complete. Display the user password change task details and exit.
- `--json` or `-j`
   Display results as JSON.


#### Examples
{: #deployment-user-password-examples}

Change the password of user "fred" on the database deployment "MyPSQL" to "A9876B5432"
```sh
ibmcloud cdb deployment-password MyPSQL fred A9876B5432
```
{: .pre}

## Database Configuration
{: #database-configuration}

List or change configurable settings on a deployment. The new configuration is specified in a JSON file or JSON string of settings. Settings vary by database type, see _Changing the Database Configuration_ for [PostgreSQL](/docs/services/databases-for-postgresql?topic=databases-for-postgresql-changing-configuration) or for [Redis](/docs/services/databases-for-redis?topic=databases-for-redis-changing-configuration).

### `ibmcloud cdb deployment-configuration-schema`
{: #deployment-configuration-schema}

Short version - `config-schema`

Gets the default configuration of the specified deployment.
```sh
ibmcloud cdb deployment-configuration-schema <deployment name or CRN> [--description] [--json]
```
{: .pre}

The `ibmcloud cdb deployment-configuration-schema` shows the default configuration. To verify a current configuration value, query the configuration directly from your database.{: .note}

#### Command options
{: #deployment-configuration-schema-command-options}

- `--json` or `-j`
   Display results as JSON.
- `--description` or `-d`
   Show settings description.


#### Examples
{: #deployment-configuration-schema-examples}

```sh
ibmcloud cdb deployment-configuration-schema my-redis-cache
```
{: .pre}

### `ibmcloud cdb deployment-configuration`
{: #deployment-configuration}

Short version - `configuration`

Changes the configuration of the specified deployment.

```sh
ibmcloud cdb deployment-configuration <deployment name or CRN> [@JSON_FILE | JSON_STRING] [--json] [--nowait]
```
{: .pre}

#### Command options
{: #deployment-configuration-command-options}

- `--json` or `-j`
   Display results as JSON.
- `--nowait` or `-n`
   Do not wait for the group setting task to complete. Display the scaling task's details and exit.


#### Examples
{: #deployment-configuration-examples}

Change the max_connections for a PostgreSQL deployment named "PGSettings4" to 150.
```sh
ibmcloud cdb deployment-configuration PGSettings4 '{"configuration":{"max_connections":150}}'
```
{: .pre}

## Scaling
{: #scaling}

Retrieve and configure the resources that are allocated to your deployment. 

### `ibmcloud cdb deployables-groups-show`
{: #deployables-groups-show}

Each deployment is created from a deployable template. The `deployables-groups-show` command shows the initial or default scaling group for a particular type of database. The type names can be discovered through the `deployables-show` command.

```sh
ibmcloud cdb deployables-groups-show <deployable type> [--json]
```
{: .pre}

#### Command options  
{: #deployables-groups-show-command-options}

- `--json` or `-j`
   Display results as JSON.
   

#### Examples
{: #deployables-groups-show-examples}

Show the default group settings for a PostgreSQL database deployment
```sh
ibmcloud cdb deployables-groups-show postgresql
```
{: .pre}

### `ibmcloud cdb deployment-groups`
{: #deployment-groups}

Short version - `groups`

Displays the scaling group values for a deployment's members. The scaling groups relate to Memory, CPU, and Disk. The default group is named "member". For each group, the number of nodes in the group are shown followed by
* **Memory** The total memory allocation, the allocation per member, the minimum allocation and the increments the total memory can be varied by.
* **CPU** The number of CPUs dedicated to the group. The CPU section shows 0 values in all the fields when no dedicated CPUs are configured. The CPU group is only displayed when it is adjustable.
* **Disk** The total disk allocation, the allocation per member, the minimum allocation and the increments the total disk can be varied by.

```sh
ibmcloud cdb deployment-groups <deployment name or CRN> [--json]
```
{: .pre}

#### Command options  
{: #deployment-groups-command-options}

- `--json` or `-j`
   Display results as JSON.


#### Examples
{: #deployment-groups-examples}

Display the scaling group settings for a database deployment named "MyRedis"
```sh
ibmcloud cdb deployment-groups MyRedis
```
{: .pre}

### `ibmcloud cdb deployment-groups-set`
{: #deployment-groups-set}

Short version - `groups-set`

Sets the values for scaling groups (see deployment-groups). The user is able to set the total memory size in MB or total disk storage in MB, both of which are which is evenly divided between the members. Where available, the number of allocated CPUs can also be set.

```sh
ibmcloud cdb deployment-groups-set <deployment name or CRN> <memberid> [--memory <memory size>] [--disk <disk size>] [--cpu <value>] [--hostflavor <val>] [--nowait] [--json]
```
{: .pre}

The `memberid` is the name of the group for which these values are to be set. The name can be found through the `deployment-groups` command. Typically, it is "member".

#### Command options  
{: #deployment-groups-set-command-options}

- `--memory <memory size>` or `-m`
   Set the specified deployment group's total memory, a value in MB.
- `--disk <disk size>` or `-d`
   Set the specified deployment group's total disk size, a value in MB.
- `--cpu <value>` or `-c`
   Set number of dedicated CPU cores.
- `--hostflavor <val>` 
   Set the hosting flavor of the database: select from `multitenant` for Shared Compute or the individual size selections for Isolated Compute. 
- `--nowait` or `-n`
   Do not wait for the group setting task to complete. Display the scaling task's details and exit.
- `--json` or `-j`
   Results as JSON.


#### Examples
{: #deployment-groups-set-examples}

Set a PostgreSQL deployment named "MyPGSQL" with a "member" group to have a total memory to 4096 MB.
```sh
ibmcloud cdb deployment-groups-set MyPGSQL member --memory 4096
```
{: .pre}

## Regions
{: #regions}

Lists all of the regions that deployments can be provisioned into from the current region.

```sh
ibmcloud cdb regions [--json] [--api-version]
```
{: .pre}

### Command options
{: #regions-command-options}

- `--json` or `-j`
   Return the results as JSON.
- `api-version value`
   API Version used for request.

### Examples
{: #regions-examples}

Return a JSON of all the regions that deployments can be provisioned into from the current region.
```sh
ibmcloud cdb regions --json
```
{: .pre}

## Autoscaling
{: #autoscaling-config}

The Autoscaling configuration represents the various conditions that control autoscaling for a deployment. 

### `ibmcloud cdb deployment-autoscaling`
{: #deployment-autoscaling}

Short version - `autoscaling`

Retrieve of all autoscaling conditions for a particular deployment. 
```sh
ibmcloud cdb deployment-autoscaling <deployment name or CRN> GROUP_ID [--json]
```
{: .pre}

Autoscaling currently only applies to the data members on your deployment, so the `GROUP_ID` is `member`.

#### Command options  
{: #deployment-autoscaling-command-options}

- `--json` or `-j`
   Return the results as JSON.


#### Examples
{: #deployment-autoscaling-examples}

```sh
ibmcloud cdb deployment-autoscaling elasticsearch-preproduction member
```
{: .pre}

### `ibmcloud cdb deployment-autoscaling-set`
{: #deployment-autoscaling-set}

Short version - `autoscaling-set`

Enable, disable, or set the conditions for autoscaling on your deployment.
```sh
ibmcloud cdb deployment-autoscaling-set (NAME|ID) GROUP_ID (@JSON_FILE|JSON_STRING) [--json] [--nowait]
```
{: .pre}

Autoscaling currently only applies to the data members on your deployment, so the `GROUP_ID` is `member`. The autoscaling parameters that you would like to be set or unset are defined in a JSON object.

#### Command options  
{: #deployment-autoscaling-set-command-options}

- `--json` or `-j`
   Return the results as JSON.
- `--nowait` or `-n`
   Do not wait for command completion.


#### Examples
{: #deployment-autoscaling-set-examples}

This command sets memory to autoscale when I/O utilization hits a certain threshold for a deployment named `elasticsearch-preproduction`.
```sh
ibmcloud cdb deployment-autoscaling-set elasticsearch-preproduction member '{"autoscaling": { "memory": {"scalers": {"io_utilization": {"enabled": true, "over_period": "5m","above_percent": 90}},"rate": {"increase_percent": 10.0, "period_seconds": 300,"limit_mb_per_member": 125952,"units": "mb"}}}}'
```
{: .pre}

## Read-only Replicas
{: #config-retrieve-read-only-replicas}

Retrieve and configure read-only replicas. Currently, only PostgreSQL deployments support read-only replicas.

### `ibmcloud cdb deployment-read-replicas`
{: #deployment-read-replicas}

Short version - `read-replicas`

Lists all the read-only replicas for the specified deployment. 

```sh
ibmcloud cdb deployment-read-replicas <deployment name or CRN> [--long] [--json]
```
{: .pre}

#### Command options  
{: #deployment-read-replicas-command-options}

- `--json` or `-j`
   Return the results as JSON.
- `--long` or `-l`
   Shows additional fields in the output.


#### Examples
{: #deployment-read-replicas-examples}

List the read-only replicas for a PostgreSQL deployment named "MyPGSQL".
```sh
ibmcloud cdb deployment-read-replicas MyPGSQL
```
{: .pre}

### `ibmcloud cdb read-replica-leader`
{: #read-replica-leader}

Short version - `rr-leader`

Returns the leader for the specified read-only replica deployment.

```sh
ibmcloud cdb read-replica-leader <deployment name or CRN> [--long] [--json]
```
{: .pre}

#### Command options  
{: #read-replica-leader-command-options}

- `--json` or `-j`
   Return the results as JSON.
- `--long` or `-l`
   Shows additional fields in the output.


#### Examples
{: #read-replica-leader-examples}

List the leader for a PostgreSQL read-only replica deployment named "MyPGSQL-replica".
```sh
ibmcloud cdb read-replica-leader MyPGSQL-replica
```
{: .pre}

### `ibmcloud cdb read-replica-promote`
{: #read-replica-promote}

Short version - `rr-promote`

Promotes the read-only replica to a stand-alone instance.

```sh
ibmcloud cdb read-replica-promote <deployment name or CRN> [--json] [--nowait] [--skip-initial-backup]
```
{: .pre}

#### Command options  
{: #read-replica-promote-command-options}

- `--json` or `-j`
   Return the results as JSON.
- `--nowait` or `-n`
   Do not wait for command completion.
- `--skip-initial-backup` or `s`
   Option to restore instance without taking a backup once data is restored. Allows restored deployment to be available sooner.


#### Examples
{: #read-replica-promote-examples}

Promotes a PostgreSQL read-only replica deployment named "MyPGSQL-replica" to a stand-alone deployment.
```sh
ibmcloud cdb read-replica-promote MyPGSQL-replica
```
{: .pre}

### `ibmcloud cdb read-replica-resync`
{: #read-replica-resync}

Short version - `rr-resync`

Resyncs the read-only replica.

```sh
ibmcloud cdb read-replica-resync <deployment name or CRN> [--json] [--nowait]
```
{: .pre}

#### Command options  
{: #read-replica-resync-command-options}

- `--json` or `-j`
   Return the results as JSON.
- `--nowait` or `-n`
   Do not wait for command completion.


#### Examples
{: #read-replica-resync-examples}

Resyncs a PostgreSQL read-only replica deployment named "MyPGSQL-replica".
```sh
ibmcloud cdb read-replica-resync MyPGSQL-replica
```

## Backups
{: #backups}

Manage the backups on your deployment or take an on-demand backup.

### `ibmcloud cdb deployment-backups-list`
{: #deployment-backups-list}

Short version - `backups`

Displays a list of backups that are associated with a deployment. The result is a table that is composed of the backups ID, type, status, and date of creation. The results are sorted with most recent backups first.

```sh
ibmcloud cdb deployment-backups-list <deployment name or CRN> [--scheduled] [--first] [--json]
```
{: .pre}

#### Command options  
{: #deployment-backups-list-command-options}

- `--scheduled` or `-s`
   Output only scheduled backups.
- `--first` or `-f`
   Output only the first (or most recent) backup found.
- `--json` or `-j`
   Display results as JSON.


#### Examples
{: #deployment-backups-list-examples}

Display the backups available on a deployment named "Postgres2000"
```sh
ibmcloud cdb backups Postgres2000
```
{: .pre}

### `ibmcloud cdb backup-show`
{: #backup-show}

Show details about a backup. The backup is identified by its CRN ID as shown with the `deployment-backups-list` command.

```sh
ibmcloud cdb backup-show <CRN> [--json]
```
{: .pre}

#### Command options
{: #backup-show-command-options}

- `--json` or `-j`
   Display results as JSON.

 
#### Examples
{: #backup-show-examples}

Show details of a particular backup.
```sh
ibmcloud cdb backup-show crn:v1:bluemix:public:databases-for-postgresql:us-south:a/54e8ffe85dcedf470db5b5ee6ac4a8d8:1b8f53db-fc2d-4e24-8470-f82b15c71717:backup:ebcea542-8d8c-4b6e-a7d4-922ffd08eb50
```
{: .pre}

### `ibmcloud cdb deployment-backup-now`
{: #deployment-backup-now}

Short version - `backup-now`

Initiates an on-demand backup on the deployment. The command polls the running backup and exits when it is completed.

```sh
ibmcloud cdb deployment-backup-now <deployment name or CRN> [--nowait] [--json]
```
{: .pre}

#### Command options
{: #deployment-backup-now-command-options}

- `--nowait` or `-n`
   Do not wait for the backup task to complete. Display the backup task details and exit.
- `--json` or `-j`
   Display results as JSON.

#### Examples
{: #deployment-backup-now-examples}

Create a backup of a deployment called "PgTips"
```sh
ibmcloud cdb deployment-backup-now PgTips
```
{: .pre}

## Security
{: #security}

Manage the IP allowlist for your deployment.

### `ibmcloud cdb deployment-allowlist-list`
{: #deployment-allowlist-list}

Short version - `wl-ls`

Displays the current allowlist for a deployment.

```sh
ibmcloud cdb deployment-allowlist-list <deployment name or CRN> [--json]
```
{: .pre}

#### Command options  
{: #deployment-allowlist-list-command-options}

- `--json` or `-j`
   Display results as JSON.

 
#### Examples
{: #deployment-allowlist-list-examples}

List the current allowlist for the "MyPSQL" deployment
```sh
ibmcloud cdb deployment-whitelist-list MyPSQL
```
{: .pre}

### `ibmcloud cdb deployment-allowlist-add`
{: #deployment-allowlist-add}

Short version - `wl-add`

Add an IP address or range to the current allowlist for a deployment. An IP address is an IPv4 or IPv6 address while a range is a masked IPv4 address, for example, 1.2.3.0/24. The description is required to be a human readable string that describes the allowlisted address or range.

```sh
ibmcloud cdb deployment-allowlist-add <deployment name or CRN> <allowlist address or range> <description> [--nowait] [--json]
```
{: .pre}

#### Command options  
{: #deployment-allowlist-add-command-options}

- `--nowait` or `-n`
   Do not wait for the allowlist add task to complete. Display the allowlist add task details and exit.
- `--json` or `-j`
   Display results as JSON.

#### Examples
{: #deployment-allowlist-add-examples}

Add the IP address 198.51.100.1 to the current allowlist for the "MyPSQL" deployment
```sh
ibmcloud cdb deployment-whitelist-add MyPSQL 198.51.100.1 "allowlisted for testing"
```
{: .pre}

Add the IP range 198.51.100.0 to 198.51.100.255 to the current allowlist for the "MyPSQL" deployment
```sh
ibmcloud cdb deployment-whitelist-add MyPSQL 198.51.100.0/24 "Testing range is now open"
```
{: .pre}

### `ibmcloud cdb deployment-allowlist-delete`
{: #deployment-allowlist-delete}

Short version - `wl-del`

Removes an IP address or range from the current allowlist for a deployment. An IP address is an IPv4 or IPv6 address while a range is a masked IPv4 address, for example, 1.2.3.0/24. 
```sh
ibmcloud cdb deployment-allowlist-delete <deployment name or CRN> <allowlist address or range> [--nowait] [--json]
```
{: .pre}

#### Command options  
{: #deployment-allowlist-delete-command-options}

- `--nowait` or `-n`
   Do not wait for the allowlist delete task to complete. Display the allowlist delete task details and exit.
- `--json` or `-j`
   Display results as JSON.

#### Examples
{: #deployment-allowlist-delete-examples}

Remove the IP address 198.51.100.1 from the current allowlist for the "MyPSQL" deployment
```sh
ibmcloud cdb deployment-whitelist-delete MyPSQL 198.51.100.1 "allowlisted for testing"
```
{: .pre}

Remove the IP range 198.51.100.0 to 198.51.100.255 from the current allowlist for the "MyPSQL" deployment
```sh
ibmcloud cdb deployment-whitelist-delete MyPSQL 198.51.100.0/24 "Testing range is now open"
```
{: .pre}

## Tasks
{: #tasks}

Tasks are created whenever you perform an action on your deployment. Tasks include things like taking a backup, group scaling, and changing a user password. Most `cdb` commands poll the running task and exit when it completes. You can change this behavior with the `--nowait` flag, which returns task information and exits. Records of successful tasks are shown for 24 - 48 hours, and unsuccessful tasks are shown for 7 - 8 days. A historical record of tasks from any time period is available through the [Activity Tracker integration](/docs/cloud-databases?topic=cloud-databases-activity-tracker).

### `ibmcloud cdb deployment-tasks-list`
{: #deployment-tasks-list}

Short version - `tasks`

Displays a list of all tasks that have been run on a specified deployment since it was created. Each task is displayed with its CRN, readable description, percentage completeness, status, and date of creation.

```sh
ibmcloud cdb deployment-tasks-list <deployment name or CRN> [--json]
```
{: .pre}

#### Command options  
{: #deployment-tasks-list-command-options}

- `--json` or `-j`
   Display results as JSON.

#### Examples
{: #deployment-tasks-list-examples}

Display a list of the tasks that have been run against a deployment named "NewRedis"
```sh
ibmcloud cdb deployment-tasks-list NewRedis
```
{: .pre}

### `ibmcloud cdb task-show`
{: #task-show}

Short version - `task`

Show the status of a particular task. The task is identified by its CRN ID as shown with the `deployment-tasks-list` command. If the task is running, the command waits for the task to complete, reporting status changes as it regularly polls.

```sh
ibmcloud cdb task-show <CRN> [--nowait] [--json]
```
{: .pre}

#### Command options
{: #task-show-command-options}

- `--nowait` or `-n`
   Do not wait for the task to complete. Display the user password change task details and exit.
- `--json` or `-j`
   Display results as JSON.

#### Examples
{: #task-show-examples}

Show details of a particular backup task.
```sh
ibmcloud cdb task-show crn:v1:bluemix:public:databases-for-postgresql:us-south:a/54e8ffe85dcedf470db5b5ee6ac4a8d8:1b8f53db-fc2d-4e24-8470-f82b15c71717:task:0faea465-de5a-4f14-a5ff-b402fefbd652
```
{: .pre}

## Elasticsearch
{: #elasticsearch}

Perform tasks specific to Elasticsearch deployments.

### `ibmcloud cdb elasticsearch file-sync`
{: #elasticsearch-file-sync}

Short version - `fs`

Synchronizes files from the `ibm_file_sync` index to disk. For more information, see the [Uploading Files to Elasticsearch](/docs/services/databases-for-elasticsearch?topic=databases-for-elasticsearch-uploading-files) documentation for more information.

```sh
ibmcloud cdb elasticsearch file-sync <deployment name or CRN> [--json] [--nowait]
```
{: .pre}

#### Command options  
{: #elasticsearch-file-sync-command-options}

- `--nowait` or `-n`
   Do not wait for the group setting task to complete. Display the scaling task's details and exit.
- `--json` or `-j`
   Return the results as JSON.

#### Examples
{: #elasticsearch-file-sync-examples}

Sync a file to disk on a deployment named "MyElasticsearch".
```sh
ibmcloud cdb elasticsearch file-sync MyElasticsearch
```
{: .pre}

### `ibmcloud cdb elasticsearch user-list`
{: #elasticsearch-user-list}

Short version - `ul`

Lists all users from the database internal credential store. For more information, see [Retrieve and update user passwords](/docs/databases-for-elasticsearch?topic=databases-for-elasticsearch-upgrading&interface=cli#esupgrade-retrieve-update-user-passwords).

```sh
ibmcloud cdb elasticsearch user-list (NAME|ID) (ADMIN_PASSWORD) [--json] [-c DIRECTORY] [--api-version]
```
{: .pre}

#### Command options  
{: #elasticsearch-file-sync-command-options}

- `--json` or `-j`
   Return the results as JSON.
- `-c DIRECTORY`
   Certificate Root
- `--api-version`
   API Version used for request.

#### Examples
{: #elasticsearch-file-sync-examples}

The `user-list` command outputs various options for your account's user list.
```sh
ibmcloud cdb elasticsearch user-list
```
{: .pre}

## PostgreSQL
{: #postgresql}

Perform tasks specific to PostgreSQL deployments.

### `ibmcloud cdb postgresql earliest-pitr-timestamp`
{: #postgresql-earliest-pitr-timestamp}

Short version - `ept`

Returns the earliest available time for point-in-time-recovery in ISO8601 UTC format. For more information, see the [Point in Time Recovery](/docs/databases-for-postgresql?topic=databases-for-postgresql-pitr) documentation for more information.

```sh
ibmcloud cdb postgresql earliest-pitr-timestamp <deployment name or CRN> [--json] [--nowait]
```
{: .pre}

#### Command options
{: #postgresql-earliest-pitr-timestamp-command-options}

- `--nowait` or `-n`
   Do not wait for the group setting task to complete. Display the scaling task's details and exit.
- `--json` or `-j`
   Return the results as JSON.

#### Examples
{: #postgresql-earliest-pitr-timestamp-examples}

```sh
ibmcloud cdb postgresql earliest-pitr-timestamp postgresql-preproduction
```
{: .pre}

### `ibmcloud cdb postgresql replication-slot-create`
{: #postgresql-replication-slot-create}

Short version - `rsc`

Creates a new PostgreSQL replication slot. For more information, see the [Wal2json](/docs/services/databases-for-postgresql?topic=databases-for-postgresql-wal2json) documentation for more information.

```sh
ibmcloud cdb postgresql replication-slot-create <deployment name or CRN> <databasename> <slotname> <plugintype> [--json] [--nowait]
```
{: .pre}

The plug-in type is required to be "wal2json".

#### Command options  
{: #postgresql-replication-slot-create-command-options}

- `--nowait` or `-n`
   Do not wait for the group setting task to complete. Display the scaling task's details and exit.
- `--json` or `-j`
   Return the results as JSON.

#### Examples
{: #postgresql-replication-slot-create-examples}

Create a replication slot on a deployment named "MyPostgres", database named "testdb", and slot named "slot1".
```sh
ibmcloud cdb postgresql replication-slot-create MyPostgres testdb slot1 wal2json
```
{: .pre}

### `ibmcloud cdb postgresql replication-slot-delete`
{: #postgresql-replication-slot-delete}

Short version - `rsd`

Deletes the specified PostgreSQL replication slot. See the [Wal2json](/docs/services/databases-for-postgresql?topic=databases-for-postgresql-wal2json) documentation for more information.

```sh
ibmcloud cdb postgresql replication-slot-delete <deployment name or CRN> <slotname> [--json] [--nowait]
```
{: .pre}

#### Command options  
{: #postgresql-replication-slot-delete-command-options}

- `--nowait` or `-n`
   Do not wait for the group setting task to complete. Display the scaling task's details and exit.
- `--json` or `-j`
   Return the results as JSON.

#### Examples
{: #postgresql-replication-slot-delete-examples}

Deletes a replication slot on a deployment named "MyPostgres"  and slot named "slot1".
```sh
ibmcloud cdb postgresql replication-slot-delete MyPostgres slot1
```
{: .pre}

## EnterpriseDB
{: #enterprisedb}

Perform tasks specific to EnterpriseDB deployments.

### `ibmcloud cdb enterprisedb earliest-pitr-timestamp`
{: #enterprisedb-earliest-pitr-timestamp}

Short version - `ept`

Returns the earliest available time for point-in-time-recovery in ISO8601 UTC format. For more information, see [Point in Time Recovery](/docs/databases-for-postgresql?topic=databases-for-postgresql-pitr).

```sh
ibmcloud cdb enterprisedb earliest-pitr-timestamp <deployment name or CRN> [--json] [--nowait]
```
{: .pre}

#### Command options
{: #enterprisedb-earliest-pitr-timestamp-command-options}

- `--nowait` or `-n`
   Do not wait for the group setting task to complete. Display the scaling task's details and exit.
- `--json` or `-j`
   Return the results as JSON.
- `api-version value`
   API Version used for request.

#### Examples
{: #enterprisedb-earliest-pitr-timestamp-examples}

```sh
ibmcloud cdb enterprisedb earliest-pitr-timestamp enterprisedb-preproduction
```
{: .pre}

## MongoDB Enterprise
{: #mongodb}

Perform tasks specific to MongoDB Enterprise deployments.

### `ibmcloud cdb mongodbee earliest-pitr-timestamp`
{: #mongodbee-earliest-pitr-timestamp}

Short version - `ept`

Returns the earliest available time for point-in-time-recovery in ISO8601 UTC format. For more information, [Point in Time Recovery](https://cloud.ibm.com/docs/databases-for-mongodb?topic=databases-for-mongodb-pitr&interface=ui).

```sh
ibmcloud cdb mongodb-enterprise earliest-pitr-timestamp <deployment name or CRN> [--json] [--nowait]
```
{: .pre}

#### Command options
{: #mongodbee-earliest-pitr-timestamp-command-options}

- `--nowait` or `-n`
   Do not wait for the group setting task to complete. Display the scaling task's details and exit.
- `--json` or `-j`
   Return the results as JSON.
- `api-version value`
   API Version used for request.

#### Examples
{: #mongodbee-earliest-pitr-timestamp-examples}

```sh
ibmcloud cdb mongodb earliest-pitr-timestamp (NAME|ID)
```
{: .pre}
