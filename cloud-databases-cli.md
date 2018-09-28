---
 
copyright:
  years: 2018
lastupdated: "2018-08-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# {{site.data.keyword.databases-for}} CLI Plug-in
{: #cloud-databases}

The {{site.data.keyword.databases-for}} CLI Plug-in offers extra methods of accessing the capabilities of the {{site.data.keyword.databases-for}} services. You can use {{site.data.keyword.databases-for}} CLI to manage and connect to {{site.data.keyword.databases-for-postgresql_full}} and {{site.data.keyword.databases-for-redis_full}}. Both services use the {{site.data.keyword.databases-for}} API.
{:shortdesc} 

**Note**: {{site.data.keyword.databases-for}} CLI Plug-in requires IBM Cloud CLI to be installed.

## How to install the {{site.data.keyword.databases-for}} CLI Plug-in
{: #how_to_install_cli}

The {{site.data.keyword.databases-for}} CLI plugin requires that the {{site.data.keyword.cloud_notm}} CLI is installed.

## The {{site.data.keyword.cloud_notm}} CLI
{: #install_cli}
The {{site.data.keyword.cloud_notm}} CLI is a general-purpose developer tool that provides access to your {{site.data.keyword.cloud_notm}} account and services through a command line interface.

An introduction and installation instructions are available on the [{{site.data.keyword.cloud_notm}} CLI Overview](https://console.{DomainName}/docs/cli/index.html#overview) page. If you install the CLI from the cURL command that is provided, you get a selection of extra plug-ins and extensions for multiple IDEs.
 
You can install just the stand-alone package from the [Installing the stand-alone IBM Cloud CLI](https://console.{DomainName}/docs/cli/reference/ibmcloud/download_cli.html#install_use) page. 

 ## The {{site.data.keyword.databases-for}} CLI plug-in
 {: installing_cli_plugin}

 Once you have the {{site.data.keyword.cloud_notm}} CLI, [login](https://console.{DomianName}/docs/cli/reference/ibmcloud/bx_cli.html#ibmcloud_login) and ask it to install the cloud databases plug-in. 
 
 `ibmcloud plugin install cloud-databases`
 
Use `ibmcloud cdb help` for a list of commands and usage, or see the [documentation](https://console.{DomainName}/docs/databases-cli-plugin/cloud-databases-cli.html#cloud-databases-cli-plug-in) for a command reference. 

## {{site.data.keyword.databases-for}} CLI Plug-in commands index
{: #commands_index}

You can specify one of the following commands:

<table summary="Alphabetically ordered  {{site.data.keyword.Bluemix_notm}} infrastructure Block Storage commands that have links that bring you to more info for the command">
<caption>Table 1. Deployment commands</caption>  
 <thead>
 <th colspan="5">Deployment commands</th>
 </thead>
 <tbody> 
 <tr> 
 <td>[`deployments`](#deployments)</td> 
 <td>[`deployment-about`](#deployment-about)</td> 
 <td>[`deployment-backups-list`](#deployment-backups-list)<td>

 </tr> 
 <tr> 
  <td>[`deployment-backup-now`](#deployment-backup-now)</td>
  <td>[`deployment-cacert`](#deployment-cacert)</td>
  <td>[`deployment-connections`](#deployment-connections)</td>
 </tr>
 <tr> 
  <td>[`deployment-groups`](#deployment-groups)</td>
  <td>[`deployment-groups-set`](#deployment-groups-set)</td>
  <td>[`deployment-tasks-list`](#deployment-tasks-list)</td>
</tr>
<tr>
 <td>[`deployment-user-create`](#deployment-user-create)</td>
 <td>[`deployment-user-delete`](#deployment-user-delete)</td>
 <td>[`deployment-user-password`](#deployment-user-password)</td>
 </tr>
 <tr>
 <td>[`deployment-whitelist-list`](#deployment-whitelist-list)</td>
 <td>[`deployment-whitelist-add`](#deployment-whitelist-add)</td>
 <td>[`deployment-whitelist-delete`](#deployment-whitelist-delete)</td>
 </tr>
 <tr> 
 </tr>
</tbody> 
</table> 


<table summary="Alphabetically ordered  {{site.data.keyword.Bluemix_notm}} infrastructure Block Storage commands that have links that bring you to more info for the command">
<caption>Table 1. Other commands</caption>  
 <thead>
 <th colspan="5">Other commands</th>
 </thead>
 <tbody> 
 <tr> 
 <td>[`backup-show`](#backup-show)</td> 
 <td>[`deployables-group-show`](#deployables-group-show)</td> 
 <td>[`deployables-show`](#deployables-show)</td>
 </tr> 
 <tr> 
 <td>[`task-show`](...)</td>
 <td>[`help`](...)</td>
 </tr>
  </tbody> 
 </table> 


## `ibmcloud cdb deployments`
{: #deployments}

Short version - `ls`

Use this command to list the deployments associated with the account.

```
ibmcloud cdb deployments [--all]
```

**Command options**
<dl>
   <dt>`--all` or `-a`</dt>
   <dd>Display instance name and CRN.</dd>
</dl>
 
**Examples**
List all current deployments with an account.
```
ibmcloud cdb ls
```

## `ibmcloud cdb deployment-about`
{: #deployment-about}

Short version - `about`

Use this command to get details of which database is deployed within the instance, which version and any options applied. Also displayed are the ID and GUID for the resource controller, resource plans, current state, type, and last known operation.

```
ibmcloud cdb deployment-about <deployment name or CRN> [--all]
```

**Command options**  
<dl>
   <dt>`--all` or `-a`</dt>
   <dd>Display all the available data from the resource controller's records.</dd>
</dl>
 
**Examples**
List details of a deployment named "RedisDBOne".
```
ibmcloud cdb about RedisDBOne
```

## `ibmcloud cdb deployment-backups-list`
{: #deployment-backups-list}

Short version - `backups`

Displays a list of backups that are associated with a deployment. The result is a table that is composed of the backups ID, type, status, and date of creation. The results are sorted with most recent backups first.

```
ibmcloud cdb deployment-backups-list <deployment name or CRN>
```

**Command options**  
<dl>
   <dt>`--scheduled` or `-s`</dt>
   <dd>Output only scheduled backups.</dd>
   <dt>`--first` or `-f`</dt>
   <dd>Output only the first (or most recent) backup found.</dd>
</dl>

**Examples**
Display the backups available on a deployment named "Postgres2000"
```
ibmcloud cdb backups Postgres2000
```



## `ibmcloud cdb deployment-backup-now`
{: #deployment-backups-now}

Short version - `backup-now`

Initiated an on-demand backup on the deployment. The command will poll the running backup and exit when it has completed.

```
ibmcloud cdb deployment-backup-now <deployment name or CRN> [--nowait]
```

**Command options**
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the backup task to complete. Display the backup task details and exit.</dd>
</dl>

 
**Examples**
Create a backup of a deployment called "PgTips"
```
ibmcloud cdb deployment-backup-now PgTips
```


## `ibmcloud cdb deployment-cacert`
{: #deployment-cacert}

Short version - `cacert`

Display the self-signed certificate that is used for verifying TLS/SSL connections to the deployment. The result is, by default, output to the console but can be saved to a file too.

```
ibmcloud cdb deployment-cacert <deployment name or CRN> [--user <userid>] [--save] [--certroot <path>]
```

**Command options**
<dl>
   <dt>`--user <userid>` or `-u`</dt>
   <dd>By default, the admin user is used to obtain the certificate. This flag optionally allows a user to be specified where the deployment supports per user certificates.</dd>
   <dt>`--save` or `-s`</dt>
   <dd>Save the decoded certificate into the certificate root directory. The default is $HOME/.bluemix/plugins/cdb/cdbcerts/.</dd>
   <dt>`--certroot <path>` or `-c`</dt>
   <dd>Use the path as the certificate root directory. If the path doesn't exist, it is created automatically. Works with the `--save` flag. The certificate root value can also be set in the `$CERTROOT` environment variable.</dd>
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



## `ibmcloud cdb deployment-connections`
{: #deployment-connections}

Short version - `cxn`

Displays connection strings and other connection details for a deployment with or without user credentials inserted. The `--start` flag tells the command to attempt to connect to the deployment. The plug-in uses the default commands for command-line interaction and managing the CA certificate for the deployment. This ensures a secure TLS session.

```
ibmcloud cdb deployment-connections [--user <userid>] [--password <password>] [--all] [--start] [--certroot <path>]
```

**Command options**  
<dl>
   <dt>`--start` or `-s`</dt>
   <dd>Start a connection by running the CLI command generated. If a password isn't specified in the flags, the command prompts for a password interactively. Defaults to connecting as the deployment's admin user.</dt>
   <dt>`--user <userid>` or `-u`</dt>
   <dd>Sets the userid that is used when retrieving connection settings. It is substituted into connection strings. Defaults to the deployment's admin user.</dd>
   <dt>`--password <password>` or `-p`</dt>
   <dd>Sets the password that is used when retrieving connection settings. It is substituted into connection strings where $PASSWORD appears as default.</dt>
   <dt>`--all` or `-a`</dt>
   <dd>Lists all connection settings available including component parts of connection strings.</dt>
   <dt>`--certroot <path>` or `-c`</dt>
   <dd>Use the path as the certificate root. If the path doesn't exist, it is created automatically. Works with the `--save` flag. The certificate root value can also be set in the `$CERTROOT` environment variable.</dd>
   <dt>`--only [app or cli]` or `-o`</dt>
   <dd>Show only the settings that are relevant to `app` connections or `cli` connections.</dd>
</dl>
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



## `ibmcloud cdb deployment-groups`
{: #deployment-groups}

Short version - `groups`

Displays the scaling group values for a deployment's members. The scaling groups relate to Memory, CPU, and Disk. The default group is named "member". For each group, the number of nodes in the group are shown followed by
* **Memory** The total memory allocation, the allocation per member, the minimum allocation and the increments the total memory can be varied by.
* **CPU** The number of CPUs dedicated to the group. The CPU section shows 0 values in all the fields when there are no dedicated CPUs configures. The CPU group is  only displayed when it is adjustable.
* **Disk** The total disk allocation, the allocation per member, the minimum allocation and the increments the total disk can be varied by.

```
ibmcloud cdb deployment-groups <deployment name or CRN>
```

**Command options**  
No command-specific options.

**Examples**
Display the scaling group settings for a database deployment named "MyRedis"
```
ibmcloud cdb deployment-groups MyRedis
```



## `ibmcloud cdb deployment-groups-set`
{: #deployment-groups-set}

Short version - `groups-set`

Sets the values for scaling groups (see deployment-groups). The user is able to set the total memory size in MB or total disk storage in MB, both of which are which is evenly divided between the members. Where available, the number of allocated CPUs can also be set.

```
ibmcloud cdb deployment-groups-set <deployment name or CRN> <memberid> [--memory <memory size>] [--cpu <cpu count>] [--nowait]
```

The `memberid` is the name of the group for which these values are to be set. The name can be found through the deployment-groups command. Typically, it is "member".

**Command options**  
<dl>
   <dt>`--memory <memory size>` or `-m`</dt>
   <dd>Set the specified deployment group's total memory use to be "memsize", a value in MB.</dd>
   <dt>`--cpu <cpu count>` or `-c`</dt>
   <dd>Set the number of dedicated CPUs for the specified deployment group to use.</dd>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the group setting task to complete. Display the scaling task's details and exit.</dd>
</dl>

 
**Examples**
Set a PostgreSQL deployment named "MyPGSQL" with a "member" group to have a total memory to 4096 MB.
```
ibmcloud cdb deployment-groups-set MyPGSQL member --memory 4096
```


## `ibmcloud cdb deployment-tasks-list`
{: #deployment-tasks-list}

Short version - `tasks`

Displays a list of all tasks that have been run on a specified deployment since it was created. The list includes backup tasks, group scaling tasks, and password tasks. Each task is displayed with its CRN, readable description, percentage completeness, status, and date of creation.

```
ibmcloud cdb deployment-tasks-list <deployment name or CRN>
```

**Command options**  
No command-specific options.

**Examples**
Display a list of the tasks that have been run against a deployment named "NewRedis"
```
ibmcloud cdb deployment-tasks-list NewRedis
```



## `ibmcloud cdb deployment-user-create`
{: #deployment-user-create}

Short version - `user-create`

Create a user on the deployment database.

```
ibmcloud cdb deployment-user-create <deployment name or CRN> <newusername> <newpassword>
```

The `newusername` needs to be a correctly formatted user name for use on the deployment's database. The `newpassword` needs to comply with the database's password rules and must be at least 10 characters long.

**Command options**  
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the user creation task to complete. Display the user creation task details and exit.</dd>
</dl>

 
**Examples**
Create a database user called "fred" with a password of "X1234Y5678" on the "MyPSQL" deployment.

```
ibmcloud cdb deployment-user-create MyPSQL fred X1234Y5678
```



## `ibmcloud cdb deployment-user-delete`
{: #deployment-user-delete}

Short version - `user-delete`

Removes an existing user from the specified database deployment.

```
ibmcloud cdb deployment-user-delete <deployment name or CRN> <username>
```

**Command options**  
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the user deletion task to complete. Display the user deletion task details and exit.</dd>
</dl>

 
**Examples**
Remove the database user called "fred" from the "MyPSQL" deployment
```
ibmcloud cdb deployment-user-delete MyPSQL fred
```


## `ibmcloud cdb deployment-user-password`
{: #deployment-user-password}

Short version - `user-password`

Changes the password for a named user on a specified database deployment.

```
ibmcloud cdb deployment-user-password <deployment name or CRN> <username> <newpassword>
```

**Command options**  
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the user password change task to complete. Display the user password change task details and exit.</dd>
</dl>

**Examples**
Change the password of user "fred" on the database deployment "MyPSQL" to "A9876B5432"
```
ibmcloud cdb deployment-password MyPSQL fred A9876B5432
```



## `ibmcloud cdb deployment-whitelist-list`
{: #deployment-whitelist-list}

Short version - `wl-ls`

Displays the current whitelist for a deployment.

```
ibmcloud cdb deployment-whitelist-list <deployment name or CRN>
```

**Command options**  
No command-specific options.
 
**Examples**
List the current whitelist for the "MyPSQL" deployment
```
ibmcloud cdb deployment-whitelist-list MyPSQL
```


## `ibmcloud cdb deployment-whitelist-add`
{: #deployment-whitelist-add}

Short version - `wl-add`

Add an IP address or range to the current whitelist for a deployment. An IP address is an IPv4 or IPv6 address while a range is a masked IPv4 address, for example, 1.2.3.0/24. The description is required to be a human readable string that describes the whitelisted address or range.

```
ibmcloud cdb deployment-whitelist-add <deployment name or CRN> <whitelist address or range> <description>
```

**Command options**  
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the whitelist add task to complete. Display the whitelist add task details and exit.</dd>
</dl>

 
**Examples**
Add the IP address 198.51.100.1 to the current whitelist for the "MyPSQL" deployment
```
ibmcloud cdb deployment-whitelist-add MyPSQL 198.51.100.1 "Whitelisted for testing"
```

Add the IP range 198.51.100.0 to 198.51.100.255 to the current whitelist for the "MyPSQL" deployment
```
ibmcloud cdb deployment-whitelist-add MyPSQL 198.51.100.0/24 "Testing range is now open"
```



## `ibmcloud cdb deployment-whitelist-delete`
{: #deployment-whitelist-delete}

Short version - `wl-del`

Removes an IP address or range from the current whitelist for a deployment. An IP address is an IPv4 or IPv6 address while a range is a masked IPv4 address, for example, 1.2.3.0/24. 
```
ibmcloud cdb deployment-whitelist-delete <deployment name or CRN> <whitelist address or range>
```

**Command options**  
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the whitelist delete task to complete. Display the whitelist delete task details and exit.</dd>
</dl>

 
**Examples**
Remove the IP address 198.51.100.1 from the current whitelist for the "MyPSQL" deployment
```
ibmcloud cdb deployment-whitelist-delete MyPSQL 198.51.100.1 "Whitelisted for testing"
```

Remove the IP range 198.51.100.0 to 198.51.100.255 from the current whitelist for the "MyPSQL" deployment
```
ibmcloud cdb deployment-whitelist-delete MyPSQL 198.51.100.0/24 "Testing range is now open"
```



## `ibmcloud cdb backup-show`
{: #backup-show}

Show details about a backup. The backup is identified by its CRN ID as shown with the `deployment-backups-list` command.

```
ibmcloud cdb backup-show <CRN>
```

**Command options**
No command-specific options.
 
**Examples**
Show details of a particular backup.
```
ibmcloud cdb backup-show crn:v1:bluemix:public:databases-for-postgresql:us-south:a/54e8ffe85dcedf470db5b5ee6ac4a8d8:1b8f53db-fc2d-4e24-8470-f82b15c71717:backup:ebcea542-8d8c-4b6e-a7d4-922ffd08eb50
```




## `ibmcloud cdb deployables-groups-show`
{: #deployables-groups-show}

Each deployment is created from a deployable template. The `deployables-groups-show` command shows the initial or default scaling group for a particular type of database. The type names can be discovers through the `deployables-show` command.

```
ibmcloud cdb deployables-groups-show <deployabletype>
```

**Command options**  
No command-specific options.

**Examples**
Show the default group settings for a PostgreSQL database deployment
```
ibmcloud cdb deployables-groups-show postgresql
```


## `ibmcloud cdb deployables-show`
{: #deployables-show}

The `deployables` are the templates available for new database deployments. This command shows deployable database types, specifically the available versions of databases, and their preferred or stable status.

```
ibmcloud cdb deployables-show [--stable] [--preferred]
```

**Command options**  
<dl>
   <dt>`--stable` or `-s`</dt>
   <dd>Only list stable versions of databases.</dd>
   <dt>`--preferred` or `-p`</dt>
   <dd>Only list preferred versions of databases.</dd>
</dl>

 
**Examples**
Show all the stable versions of databases available.
```
ibmcloud cdb deployables-show --stable
```


## `ibmcloud cdb task-show`
{: #task-show}

Short version - `task`

Show the current status of a particular task. The task is identified by its CRN ID as shown with the `deployment-tasks-list` command. If the task is running, the command waits for the task to complete, reporting status changes as it regularly polls.

```
ibmcloud cdb task-show <CRN>
```

**Command options**
<dl>
   <dt>`--nowait` or `-n`</dt>
   <dd>Do not wait for the task to complete. Display the user password change task details and exit.</dd>
</dl>

**Examples**
Show details of a particular backup task.
```
ibmcloud cdb task-show crn:v1:bluemix:public:databases-for-postgresql:us-south:a/54e8ffe85dcedf470db5b5ee6ac4a8d8:1b8f53db-fc2d-4e24-8470-f82b15c71717:task:0faea465-de5a-4f14-a5ff-b402fefbd652
```


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


## Common options

All commands take the `--json`(or `-j`) and `--raw`(or `-r`) command-line flags. 

* `--json` outputs the results of the underlying API request that are processed by the plug-in as formatted JSON. The output can include more data than is output by the command normally.
* `--raw` outputs the results of the underlying API request, unprocessed by the plug-in as unformatted JSON. The flag is reserved for use in debugging.
