


## ibmcloud sl file access-authorize
{: #sl_file_access_authorize}

Authorize hosts  to access a given volume

ibmcloud sl file access-authorize VOLUME_ID [OPTIONS]

**Examples**:

   ibmcloud sl file access-authorize 12345678 --virtual-id 87654321
   This command authorizes virtual server with ID 87654321 to access volume with ID 12345678.

```bash
ibmcloud sl file access-authorize IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--d, hardware-id
:    The ID of one hardware server to authorize

--p, ip-address
:    An IP address to authorize

--i, ip-address-id
:    The ID of one IP address to authorize

--s, subnet-id
:    An ID of one subnet to authorize

--v, virtual-id
:    The ID of one virtual server to authorize

## ibmcloud sl file access-list
{: #sl_file_access_list}

List hosts that are authorized to access the volume.

Access Hosts marked 'IN ACL' belong to a parent Access Host with the same allowed_host_id.
**Examples**:

   ibmcloud sl file access-list 12345678 --sortby id 
   This command lists all hosts that are authorized to access volume with ID 12345678 and sorts them by ID.

```bash
ibmcloud sl file access-list IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--column
:    Column to display. Options are: id, name, type, private_ip_address, source_subnet, host_iqn, username, password, allowed_host_id.

--sortby
:    Column to sort by. Options are: id, name, type, private_ip_address, source_subnet, host_iqn, username, password, allowed_host_id.

## ibmcloud sl file access-revoke
{: #sl_file_access_revoke}

Revoke authorization for hosts that are accessing a specific volume

ibmcloud sl file access-revoke VOLUME_ID [OPTIONS]

**Examples**:

   ibmcloud sl file access-revoke 12345678 --virtual-id 87654321
   This command revokes access of virtual server with ID 87654321 to volume with ID 12345678.

```bash
ibmcloud sl file access-revoke IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--d, hardware-id
:    The ID of one hardware server to revoke

--p, ip-address
:    An IP address to revoke

--i, ip-address-id
:    The ID of one IP address to revoke

--s, subnet-id
:    An ID of one subnet to revoke

--v, virtual-id
:    The ID of one virtual server to revoke

## ibmcloud sl file disaster-recovery-failover
{: #sl_file_disaster_recovery_failover}

Failover an inaccessible volume to its available replicant volume.

If a volume (with replication) becomes inaccessible due to a disaster event, this method can be used to immediately
failover to an available replica in another location. This method does not allow for fail back via the API.
To fail back to the original volume after using this method, open a support ticket.
To test failover, use 'ibmcloud sl file replica-failover' instead.

**Examples**:

	ibmcloud sl file disaster-recovery-failover 12345678 87654321
	This command performs failover operation for volume with ID 12345678 to replica volume with ID 87654321.

```bash
ibmcloud sl file disaster-recovery-failover IDENTIFIER REPLICA_ID
```
{: codeblock}


## ibmcloud sl file duplicate-convert-status
{: #sl_file_duplicate_convert_status}

Get status for split or move completed percentage of a given block storage duplicate volume.



```bash
ibmcloud sl file duplicate-convert-status IDENTIFIER
```
{: codeblock}


## ibmcloud sl file replica-failback
{: #sl_file_replica_failback}

Failback a file volume from replica

ibmcloud sl file replica-failback VOLUME_ID

**Examples**:

   ibmcloud sl file replica-failback 12345678
   This command performs failback operation for volume with ID 12345678.

```bash
ibmcloud sl file replica-failback IDENTIFIER
```
{: codeblock}


## ibmcloud sl file replica-failover
{: #sl_file_replica_failover}

Failover a file volume to the given replica volume

**Examples**:

   ibmcloud sl file replica-failover 12345678 87654321
   This command performs failover operation for volume with ID 12345678 to replica volume with ID 87654321.

```bash
ibmcloud sl file replica-failover IDENTIFIER REPLICA_ID
```
{: codeblock}


## ibmcloud sl file replica-locations
{: #sl_file_replica_locations}

List suitable replication datacenters for the given volume


**Examples**:

   ibmcloud sl file replica-locations 12345678
   This command lists suitable replication data centers for block volume with ID 12345678.

```bash
ibmcloud sl file replica-locations IDENTIFIER
```
{: codeblock}


## ibmcloud sl file replica-order
{: #sl_file_replica_order}

Order a file storage replica volume

ibmcloud sl file replica-order VOLUME_ID [OPTIONS]

**Examples**:

   ibmcloud sl file replica-order 12345678 -s DAILY -d dal09 --tier 4 --os-type LINUX
   This command orders a replica for volume with ID 12345678, which performs DAILY replication, is located at dal09, tier level is 4, OS type is Linux.

```bash
ibmcloud sl file replica-order IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--d, datacenter
:    Short name of the datacenter for the replica. For example, dal09 [required]

--f, force
:    Force operation without confirmation

--i, iops
:    Performance Storage IOPs, between 100 and 6000 in multiples of 100,if no IOPS value is specified, the IOPS value of the original volume will be used

--s, snapshot-schedule
:    Snapshot schedule to use for replication. Options are: HOURLY,DAILY,WEEKLY [required]

--t, tier
:    Endurance Storage Tier (IOPS per GB) of the primary volume for which a replica is ordered [optional], options are: 0.25,2,4,10,if no tier is specified, the tier of the original volume will be used

## ibmcloud sl file replica-partners
{: #sl_file_replica_partners}

List existing replicant volumes for a block volume

**Examples**:

   ibmcloud sl file replica-partners 12345678
   This command lists existing replicant volumes for block volume with ID 12345678.

```bash
ibmcloud sl file replica-partners IDENTIFIER
```
{: codeblock}


## ibmcloud sl file snapshot-cancel
{: #sl_file_snapshot_cancel}

Cancel existing snapshot space for a given volume

ibmcloud sl file snapshot-cancel SNAPSHOT_ID [OPTIONS]

**Examples**:

   ibmcloud sl file snapshot-cancel 12345678 --immediate -f 
   This command cancels snapshot with ID 12345678 immediately without asking for confirmation.

```bash
ibmcloud sl file snapshot-cancel IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--immediate
:    Cancel the snapshot space immediately instead of on the billing anniversary

--reason
:    An optional reason for cancellation

## ibmcloud sl file snapshot-create
{: #sl_file_snapshot_create}

Create a snapshot on a given volume

ibmcloud sl file snapshot-create VOLUME_ID [OPTIONS]

**Examples**:

   ibmcloud sl file snapshot-create 12345678 --note snapshotforibmcloud
   This command creates a snapshot for volume with ID 12345678 and with addition note as snapshotforibmcloud.

```bash
ibmcloud sl file snapshot-create IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--n, note
:    Notes to set on the new snapshot

## ibmcloud sl file snapshot-delete
{: #sl_file_snapshot_delete}

Delete a snapshot on a given volume



```bash
ibmcloud sl file snapshot-delete IDENTIFIER
```
{: codeblock}


## ibmcloud sl file snapshot-disable
{: #sl_file_snapshot_disable}

Disable snapshots on the specified schedule for a given volume

ibmcloud sl file snapshot-disable VOLUME_ID [OPTIONS]

**Examples**:

   ibmcloud sl file snapshot-disable 12345678 -s DAILY
   This command disables daily snapshot for volume with ID 12345678.

```bash
ibmcloud sl file snapshot-disable IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--s, schedule-type
:    Snapshot schedule [required], options are: HOURLY,DAILY,WEEKLY

## ibmcloud sl file snapshot-enable
{: #sl_file_snapshot_enable}

Enable snapshots for a given volume on the specified schedule

See https://sldn.softlayer.com/reference/services/SoftLayer_Network_Storage/enableSnapshots/ for more details about these options.
**Examples**:

   ibmcloud sl file snapshot-enable 12345678 -s WEEKLY -c 5 -m 0 --hour 2 -d 0
   This command enables snapshot for volume with ID 12345678, snapshot is taken weekly on every Sunday at 2:00, and up to 5 snapshots are retained.

```bash
ibmcloud sl file snapshot-enable IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--d, day-of-week
:    Day of the week when snapshots should be taken, integer between 0 to 6. 
	      0 means Sunday,1 means Monday,2 means Tuesday,3 means Wendesday,4 means Thursday,5 means Friday,6 means Saturday

--r, hour
:    Hour of the day when snapshots should be taken, integer between 0 to 23

--m, minute
:    Minute of the hour when snapshots should be taken, integer between 0 to 59

--c, retention-count
:    Number of snapshots to retain

--s, schedule-type
:    Snapshot schedule, options are: INTERVAL, HOURLY, DAILY, WEEKLY

## ibmcloud sl file snapshot-get-notification-status
{: #sl_file_snapshot_get_notification_status}

Get snapshots space usage threshold warning flag setting for a given volume.



```bash
ibmcloud sl file snapshot-get-notification-status IDENTIFIER
```
{: codeblock}


## ibmcloud sl file snapshot-list
{: #sl_file_snapshot_list}

List file storage snapshots


**Examples**:

   ibmcloud sl file snapshot-list 12345678 --sortby id 
   This command lists all snapshots of volume with ID 12345678 and sorts them by ID.

```bash
ibmcloud sl file snapshot-list IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--sortby
:    Column to sort by. Options are: id,name,created,size_bytes

## ibmcloud sl file snapshot-order
{: #sl_file_snapshot_order}

Order snapshot space for a block storage volume

See https://cloud.ibm.com/docs/BlockStorage?topic=BlockStorage-getting-started for sizing options.
ibmcloud sl block volume-options' to get available options.

**Examples**:

   ibmcloud sl file snapshot-order 12345678 -s 1000 -t 4 
   This command orders snapshot space for volume with ID 12345678, the size is 1000GB, the tier level is 4 IOPS per GB.

```bash
ibmcloud sl file snapshot-order IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--i, iops
:    Performance Storage IOPs, between 100 and 6000 in multiples of 100

--s, size
:    Size of snapshot space to create in GB

--t, tier
:    Endurance Storage Tier (IOPS per GB) of the block volume for which space is ordered [optional], options are: 0.25,2,4,10

--u, upgrade
:    Flag to indicate that the order is an upgrade

## ibmcloud sl file snapshot-restore
{: #sl_file_snapshot_restore}

Restore file volume using a given snapshot


**Examples**:

   ibmcloud sl file snapshot-restore 12345678 87654321
   This command restores volume with ID 12345678 from snapshot with ID 87654321.

```bash
ibmcloud sl file snapshot-restore IDENTIFIER SNAPSHOT_ID
```
{: codeblock}


## ibmcloud sl file snapshot-schedule-list
{: #sl_file_snapshot_schedule_list}

List snapshot schedules for a given volume



```bash
ibmcloud sl file snapshot-schedule-list IDENTIFIER
```
{: codeblock}


## ibmcloud sl file snapshot-set-notification
{: #sl_file_snapshot_set_notification}

Enables/Disables snapshot space usage threshold warning for a given volume.



```bash
ibmcloud sl file snapshot-set-notification IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--disable
:    Disable snapshot notification.

--enable
:    Enable snapshot notification.

## ibmcloud sl file volume-cancel
{: #sl_file_volume_cancel}

Cancel an existing file storage volume

ibmcloud sl file volume-cancel VOLUME_ID [OPTIONS]

**Examples**:

   ibmcloud sl file volume-cancel 12345678 --immediate -f 
   This command cancels volume with ID 12345678 immediately and without asking for confirmation.

```bash
ibmcloud sl file volume-cancel IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--immediate
:    Cancel the file storage volume immediately instead of on the billing anniversary

--reason
:    An optional reason for cancellation

## ibmcloud sl file volume-convert
{: #sl_file_volume_convert}

Convert a dependent duplicate volume to an independent volume.



```bash
ibmcloud sl file volume-convert IDENTIFIER
```
{: codeblock}


## ibmcloud sl file volume-count
{: #sl_file_volume_count}

List number of file storage volumes per datacenter



```bash
ibmcloud sl file volume-count [flags]
```
{: codeblock}


**Command options**:

--d, datacenter
:    Filter by datacenter shortname

--s, sortby
:    Column to sort by

## ibmcloud sl file volume-detail
{: #sl_file_volume_detail}

Display details for a specified volume



```bash
ibmcloud sl file volume-detail IDENTIFIER
```
{: codeblock}


## ibmcloud sl file volume-duplicate
{: #sl_file_volume_duplicate}

Order a file volume by duplicating an existing volume

ibmcloud sl file volume-duplicate VOLUME_ID [OPTIONS]

**Examples**:

   ibmcloud sl file volume-duplicate 12345678 
   This command shows order a new volume by duplicating the volume with ID 12345678.

```bash
ibmcloud sl file volume-duplicate IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--d, dependent-duplicate
:    Whether or not this duplicate will be a dependent duplicate of the origin volume.

--i, duplicate-iops
:    Performance Storage IOPS, between 100 and 6000 in multiples of 100, if no IOPS value is specified, the IOPS value of the original volume will be used

--s, duplicate-size
:    Size of duplicate file volume in GB, if no size is specified, the size of the original volume will be used

--n, duplicate-snapshot-size
:    The size of snapshot space to order for the duplicate, if no snapshot space size is specified, the snapshot space size of the origin volume will be used

--t, duplicate-tier
:    Endurance Storage Tier, if no tier is specified, the tier of the original volume will be used

--f, force
:    Force operation without confirmation

--o, origin-snapshot-id
:    ID of an origin volume snapshot to use for duplication

## ibmcloud sl file volume-limits
{: #sl_file_volume_limits}

Lists the storage limits per datacenter for this account.

ibmcloud sl file volume-limits [OPTIONS]

**Examples**:

	ibmcloud sl file volume-limits
	This command lists the storage limits per datacenter for this account.

```bash
ibmcloud sl file volume-limits
```
{: codeblock}


## ibmcloud sl file volume-list
{: #sl_file_volume_list}

List file storage

ibmcloud sl file volume-list [OPTIONS]

**Examples**:

   ibmcloud sl file volume-list -d dal09 -t endurance --sortby capacity_gb
   This command lists all endurance volumes on current account that are located at dal09, and sorts them by capacity.

```bash
ibmcloud sl file volume-list [flags]
```
{: codeblock}


**Command options**:

--column
:    Column to display. Options are: id,username,datacenter,storage_type,capacity_gb,bytes_used,IOPs,ip_addr,lunId,created_by,active_transactions,rep_partner_count,notes. This option can be specified multiple times

--d, datacenter
:    Filter by datacenter shortname

--n, notes
:    Filter by notes

--o, order
:    Filter by ID of the order that purchased the file storage

--sortby
:    Column to sort by, default:id, options are: id,username,datacenter,storage_type,capacity_gb,bytes_used,ip_addr,lunId,active_transactions,created_by

--t, storage-type
:    Filter by type of storage volume, options are: performance,endurance

--u, username
:    Filter by volume username

## ibmcloud sl file volume-modify
{: #sl_file_volume_modify}

Modify an existing file storage volume

ibmcloud sl file volume-modify VOLUME_ID [OPTIONS]

   **Examples**:

	  ibmcloud sl file volume-modify 12345678 --new-size 1000 --new-iops 4000 
	  This command modify a volume 12345678 with size is 1000GB, IOPS is 4000.
	  ibmcloud sl file volume-modify 12345678 --new-size 500 --new-tier 4
	  This command modify a volume 12345678 with size is 500GB, tier level is 4 IOPS per GB.

```bash
ibmcloud sl file volume-modify IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--i, new-iops
:    Performance Storage IOPS, between 100 and 6000 in multiples of 100 [only for performance volumes] ***If no IOPS value is specified, the original IOPS value of the volume will be used.***

--c, new-size
:    New Size of file volume in GB. ***If no size is given, the original size of volume is used.***
      Potential Sizes: [20, 40, 80, 100, 250, 500, 1000, 2000, 4000, 8000, 12000]
      Minimum: [the original size of the volume]

--t, new-tier
:    Endurance Storage Tier (IOPS per GB) [only for endurance volumes] ***If no tier is specified, the original tier of the volume will be used.***

## ibmcloud sl file volume-options
{: #sl_file_volume_options}

List all options for ordering a block or file storage volume

List all options for ordering a block or file storage volume

See Also:
	https://cloud.ibm.com/docs/BlockStorage/index.html#provisioning-considerations
	https://cloud.ibm.com/docs/BlockStorage?topic=BlockStorage-orderingBlockStorage&interface=cli


```bash
ibmcloud sl file volume-options [flags]
```
{: codeblock}


**Command options**:

--prices
:    Show prices in the storage, snapshot and iops range tables.

## ibmcloud sl file volume-order
{: #sl_file_volume_order}

Order a file storage volume

**Examples**:

   ibmcloud sl file volume-order --storage-type performance --size 1000 --iops 4000 --os-type LINUX -d dal09
   This command orders a performance volume with size is 1000GB, IOPS is 4000, OS type is LINUX, located at dal09.
   ibmcloud sl file volume-order --storage-type endurance --size 500 --tier 4 --os-type XEN -d dal09 --snapshot-size 500
   This command orders a endurance volume with size is 500GB, tier level is 4 IOPS per GB, OS type is XEN, located at dal09, and additional snapshot space size is 500GB.

```bash
ibmcloud sl file volume-order [flags]
```
{: codeblock}


**Command options**:

--b, billing
:    Optional parameter for Billing rate (default to monthly), options are: hourly, monthly

--d, datacenter
:    Datacenter short name [required]

--f, force
:    Force operation without confirmation

--i, iops
:    Performance Storage IOPs, between 100 and 6000 in multiples of 100 [required for storage-type performance]

--s, size
:    Size of storage volume in GB [required]

--n, snapshot-size
:    Optional parameter for ordering snapshot space along with endurance file storage; specifies the size (in GB) of snapshot space to order

--t, storage-type
:    Type of storage volume [required], options are: performance,endurance

--e, tier
:    Endurance Storage Tier (IOP per GB) [required for storage-type endurance], options are: 0.25,2,4,10

## ibmcloud sl file volume-refresh
{: #sl_file_volume_refresh}

Refresh a duplicate volume with a snapshot from its parent.

Refresh a duplicate volume with a snapshot from its parent. ibmcloud sl file volume-refresh VOLUME_ID SNAPSHOT_ID

**Examples**:

	ibmcloud sl file volume-refresh VOLUME_ID SNAPSHOT_ID
	Refresh a duplicate VOLUME_ID with a snapshot from its parent SNAPSHOT_ID.

```bash
ibmcloud sl file volume-refresh IDENTIFIER SNAPSHOT_ID [flags]
```
{: codeblock}


**Command options**:

--f, force-refresh
:    Force the volume refresh, will cancel any ongoing transactions.

## ibmcloud sl file volume-set-note
{: #sl_file_volume_set_note}

Set note for an existing file storage volume.

Set note for an existing file storage volume. ibmcloud sl file volume-set-note [OPTIONS] VOLUME_ID

**Examples**:

   ibmcloud sl file volume-set-note 12345678 --note 'this is my note'

```bash
ibmcloud sl file volume-set-note IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--n, note
:    Public notes related to a Storage volume  [required]
