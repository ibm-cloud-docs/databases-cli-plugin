---

copyright:
  years:  2023
lastupdated: "2023-12-06"

keywords: change log for Cloud Databases CLI, updates to Cloud Databases CLI

subcollection: cloud-databases

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.databases-for}} CLI change log
{: #cli-change-log}

In this change log, you can learn about the latest changes, improvements, and updates for the {{site.data.keyword.databases-for}} CLI plug-in.

## Version 0.17.1
{: #cli-0171}

- Adds `deployment-user-set` command to update Redis roles.
- Removes default role from `deployment-user-create`.
- Updates description of `deployment-user-create` since Redis is also using this command.

## Version 0.16.9
{: #cli-0169}

## Version 0.16.8
{: #cli-0168}

## Version 0.16.7
{: #cli-0167}

## Version 0.16.6
{: #cli-0166}

## Version 0.16.5
{: #cli-0165}

## Version 0.16.4
{: #cli-0164}

## Version 0.16.3
{: #cli-0163}

## Version 0.16.2
{: #cli-0162}

## Version 0.16.1
{: #cli-0161}

- The [`capability` commands](/docs/databases-cli-plugin?topic=databases-cli-plugin-cdb-reference#capability) help you to identify which features are available and supported for your databases and backups.
   - The [`capability-show` command](/docs/databases-cli-plugin?topic=databases-cli-plugin-cdb-reference#capability-show) discovers if a capability is supported for a particular database type.
   - The [`backup-capability-show`](/docs/databases-cli-plugin?topic=databases-cli-plugin-cdb-reference#capability-backup-show) command discovers if a database type can be restored from a particular instance.
   - The [`deployment-capability-show`](/docs/databases-cli-plugin?topic=databases-cli-plugin-cdb-reference#deployment-capability-show) command discovers if a particular deployment or formation supports a particular capability.
- The [`ibmcloud cdb elasticsearch user-list` command](/docs/databases-cli-plugin?topic=databases-cli-plugin-cdb-reference#elasticsearch-user-list) lists all users from the database internal credential store. For more information, see [Retrieve and update user passwords](/docs/databases-for-elasticsearch?topic=databases-for-elasticsearch-upgrading&interface=cli#esupgrade-retrieve-update-user-passwords).
- The [`regions` command](/docs/databases-cli-plugin?topic=databases-cli-plugin-cdb-reference#regions) lists all of the regions that deployments can be provisioned into from the current region.
- The [`mongodbee earliest-pitr-timestamp` command](/docs/databases-cli-plugin?topic=databases-cli-plugin-cdb-reference#mongodbee-earliest-pitr-timestamp) returns the earliest available time for point-in-time-recovery in ISO8601 UTC format. For more information, see [Point in Time Recovery](/docs/databases-for-mongodb?topic=databases-for-mongodb-pitr&interface=ui).
