> Apache Ranger manages access through a UI that ensures consistent policies across all resources.

* **Security Zones**, **Tag-based** (Ranger TagSync)

## I. Ranger Auditing
* Centralized framework for collecting **access audit history** from Hadoop components.

* Filter on various parameters.

* Support multiple audit destinations.
    - **Solr**: short term, displayed in Ranger Admin Web UI.
    - **HDFS**: long term for archival purposes.

### 1.1 Config Solr Ranger audit properties
Change default time settings that control how long Ranger keep audit data collected by Solr

### 1.2 Config HDFS Ranger audit properties
Change how audit data is written to hdfs.

### 1.3 Ranger Audit Filters
Control the amount of audit data collected and stored on cluster.

* Ranger allows user to config the audit policy for each service (attach a JSON string to each service config)

* properties in a filter policy:
    - `Is Audited`: Yes - No, include or not a filter in the audit logs for a service.
    - `Access Result`: include that access result in the audit log filter
    - `Resources`: include or remove the resource from the audit log filter
    - `Operations`: include or remove action/operationname in the audit log filter
    - `Permissions`: add or remove permissions (read, write, execute)
    - `Users`:
    - `Groups`:
    - `Roles`:

### 1.4 Excluding audits for specific users, groups and roles
Exclude audits from each service from appearing in Ranger UI.

* In default, Ranger creates audit log records for access and authorization requests.
-> Too much write operations to Solr can limit the availability of it.

* Add in service properties:
    - `ranger.plugin.audit.exclude.users`:
    - `ranger.plugin.audit.exclude.groups`:
    - `ranger.plugin.audit.exclude.roles`:

## II. Ranger Authorization
* Policy can have various level: db, table, column, file levels ...

* LDAP-based groups or indv users.

* Pluggable -> can be extend to any data source.

* After being authenticated, user's access right must be determined.

* Ranger enables creating services for each datasources, and add specific policies to those services.

### 2.1 Plugin Overview
* Ranger use **Plugin Model**.
    - Plugins run as part of the same process as the namenode (HDFS), HiveMetaStore (Hbase)...

```shell
User ---(request)--> [Ranger plugin] --> Resource
```

* Plugin stay between user and resource
    - Allow or deny accessing user requests 
    - Collect and store access request (as _audit log records_)

* Plugins pull the policies defined in Admin Policy DB, cache locally.

* Ranger policies are independent from native permissions (os).
    - Ranger uses native permissions to authorize when there is no policies defined in the db.

### 2.2 Policy Overview
* Ranger has two types of policy: **resource-based** and **tag-based**

#### Resource-based services and policies
* consist of two major components:
    - Resources that policy applied to
    - Access condition of specific users and groups (Allow, Deny, Exclude from A/D) 

* **Policy Label**: to group a set of policy
* **Policy Condition**: ip address
* **Importing/Exporting**: from test cluster to prod cluster, or for backups

#### Tag-based services and policies
* Seperate resource-classification from access-authorization
Ex: HDFS file/direct, Five db/table/col contains sensitive data (credit card num, health data ...) can be tagged.
After that, the authorization for the tag is automatically enforced.

=> No need to create dedicated policies for each component.

* **Tag Store**: tag-resource associations are stored.
    - In the evaluation process, tag is pulled by plugin, saved on cache (same as policies).
    - Update cache when there is any change.
    - Ranger Admin presists the tag details in its policy store and provides a REST interface

* **TagSync**: Ranger TagSync is used to synchronize tag store with external metadata (Apache Atlas)

![Evaluation process](https://docs.cloudera.com/runtime/7.2.18/security-ranger-authorization/images/security-ranger-policy-evaluation-flow-with-tags.png)
_Evaluation Flow with Tags_

* Once policies on requested resource are found, they will be evaluate:
    - if one policy results in deny --> deny access
    - if none policy deny, and one policy results in allow --> allow access.

### 2.3 Ranger Security Zones
Enable to organize


## III. Ranger User Management

## IV. Ranger Config Authentication
### 4.1 UNIX

### 4.2 LDAP

### 4.3 AD


## V. Manage Log Rotation
