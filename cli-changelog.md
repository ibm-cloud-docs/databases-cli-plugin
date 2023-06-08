---

copyright:
  years:  2023
lastupdated: "2023-06-07"

keywords: change log for Cloud Databases CLI, updates to Cloud Databases CLI

subcollection: cloud-databases

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.databases-for}} CLI change log
{: #cli-change-log}

In this change log, you can learn about the latest changes, improvements, and updates for the {{site.data.keyword.databases-for}} CLI. 

## Version 0.16.1 - 17 May 2023
{: #cli-0161}

- The `capability` commands help you to identify which features are available and supported for your databases and backups.
   - The `capability-show` command discovers if a capability is supported for a particular database type.
   - The `backup-capability-show` command discovers if a database type can be restored from a particular instance.
   - The `deployment-capability-show` command discovers if a particular deployment or formation supports a particular capability.
- The `ibmcloud cdb elasticsearch user-list` command lists all users from the database internal credential store.
- The `regions` command lists all of the regions that deployments can be provisioned into from the current region.
- The `mongodbee earliest-pitr-timestamp` command returns the earliest available time for point-in-time-recovery in ISO8601 UTC format.
