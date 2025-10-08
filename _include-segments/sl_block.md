


## ibmcloud sl block access-authorize
{: #sl_block_access_authorize}

Authorize hosts to access a given volume.

**Examples**:

   ibmcloud sl block access-authorize 12345678 --virtual-id 87654321
   This command authorizes virtual server with ID 87654321 to access volume with ID 12345678.

   ibmcloud sl block access-authorize 5555 --subnet-id 1111
   This command adds subnet with id 1111 to the Allowed Host with id 5555. Use 'access-list' to find this id.
   SoftLayer_Account::iscsiIsolationDisabled must be False for this command to do anything.

```bash
ibmcloud sl block access-authorize IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--d, hardware-id
:    The ID of one hardware server to authorize.

--p, ip-address
:    An IP address to authorize.

--i, ip-address-id
:    The ID of one IP address to authorize.

--s, subnet-id
:    A Subnet Id. With this option IDENTIFIER should be an 'allowed_host_id' from the access-list command.

--v, virtual-id
:    The ID of one virtual server to authorize.

## ibmcloud sl block access-list
{: #sl_block_access_list}

List hosts that are authorized to access the volume.

Access Hosts marked 'IN ACL' belong to a parent Access Host with the same allowed_host_id.
**Examples**:

   ibmcloud sl block access-list 12345678 --sortby id 
   This command lists all hosts that are authorized to access volume with ID 12345678 and sorts them by ID.

```bash
ibmcloud sl block access-list IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--column
:    Column to display. Options are: id, name, type, private_ip_address, source_subnet, host_iqn, username, password, allowed_host_id.

--sortby
:    Column to sort by. Options are: id, name, type, private_ip_address, source_subnet, host_iqn, username, password, allowed_host_id.

## ibmcloud sl block access-password
{: #sl_block_access_password}

Changes a password for a volume's access.

ibmcloud sl block access-password ACCESS_ID --password PASSWORD

	ACCESS_ID is the allowed_host_id from 'ibmcloud sl block access-list'

```bash
ibmcloud sl block access-password IDENTIFIER
```
{: codeblock}


**Command options**:

--p, password
:    Password you want to set, this command will fail if the password is not strong. [required]

## ibmcloud sl block access-revoke
{: #sl_block_access_revoke}

Revoke authorization for hosts that are accessing a specific volume.

**Examples**:

   ibmcloud sl block access-revoke 12345678 --virtual-id 87654321
   This command revokes access of virtual server with ID 87654321 to volume with ID 12345678.

   ibmcloud sl block access-revoke 5555 --subnet-id 1111
   This command removes subnet with id 1111 from the Allowed Host with id 5555. Use 'access-list' to find this id.

```bash
ibmcloud sl block access-revoke IDENTIFIER [flags]
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
:    A Subnet Id. With this option IDENTIFIER should be an 'allowed_host_id' from the access-list command.

--v, virtual-id
:    The ID of one virtual server to revoke

## ibmcloud sl block disaster-recovery-failover
{: #sl_block_disaster_recovery_failover}

Failover an inaccessible volume to its available replicant volume.

If a volume (with replication) becomes inaccessible due to a disaster event, this method can be used to immediately
failover to an available replica in another location. This method does not allow for fail back via the API.
To fail back to the original volume after using this method, open a support ticket.
To test failover, use 'ibmcloud sl block replica-failover' instead.

**Examples**:

	ibmcloud sl block disaster-recovery-failover 12345678 87654321
	This command performs failover operation for volume with ID 12345678 to replica volume with ID 87654321.

```bash
ibmcloud sl block disaster-recovery-failover IDENTIFIER REPLICA_ID
```
{: codeblock}


## ibmcloud sl block duplicate-convert-status
{: #sl_block_duplicate_convert_status}

Get status for split or move completed percentage of a given block storage duplicate volume.



```bash
ibmcloud sl block duplicate-convert-status IDENTIFIER
```
{: codeblock}


## ibmcloud sl block object-list
{: #sl_block_object_list}

List cloud block storage.



```bash
ibmcloud sl block object-list
```
{: codeblock}


## ibmcloud sl block object-storage-detail
{: #sl_block_object_storage_detail}

Display details for a cloud object storage.



```bash
ibmcloud sl block object-storage-detail IDENTIFIER
```
{: codeblock}


## ibmcloud sl block object-storage-permission
{: #sl_block_object_storage_permission}

Display permission details for a cloud object storage.



```bash
ibmcloud sl block object-storage-permission IDENTIFIER
```
{: codeblock}


## ibmcloud sl block replica-failback
{: #sl_block_replica_failback}

Failback a block volume from replica

ibmcloud sl block replica-failback VOLUME_ID

**Examples**:

   ibmcloud sl block replica-failback 12345678
   This command performs failback operation for volume with ID 12345678.

```bash
ibmcloud sl block replica-failback IDENTIFIER
```
{: codeblock}


## ibmcloud sl block replica-failover
{: #sl_block_replica_failover}

Failover a block volume to the given replica volume

**Examples**:

   ibmcloud sl block replica-failover 12345678 87654321
   This command performs failover operation for volume with ID 12345678 to replica volume with ID 87654321.

```bash
ibmcloud sl block replica-failover IDENTIFIER REPLICA_ID
```
{: codeblock}


## ibmcloud sl block replica-locations
{: #sl_block_replica_locations}

List suitable replication datacenters for the given volume


**Examples**:

   ibmcloud sl block replica-locations 12345678
   This command lists suitable replication data centers for block volume with ID 12345678.

```bash
ibmcloud sl block replica-locations IDENTIFIER
```
{: codeblock}


## ibmcloud sl block replica-order
{: #sl_block_replica_order}

Order a block storage replica volume

**Examples**:

   ibmcloud sl block replica-order 12345678 -s DAILY -d dal09 --tier 4 --os-type LINUX
   This command orders a replica for volume with ID 12345678, which performs DAILY replication, is located at dal09, tier level is 4, OS type is Linux.

```bash
ibmcloud sl block replica-order IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--d, datacenter
:    Short name of the datacenter for the replica. For example, dal09 [required]

--f, force
:    Force operation without confirmation

--i, iops
:    Performance Storage IOPs, between 100 and 6000 in multiples of 100,if no IOPS value is specified, the IOPS value of the original volume will be used

--o, os-type
:    Operating System Type (eg. LINUX) of the primary volume for which a replica is ordered [optional], options are: HYPER_V,LINUX,VMWARE,WINDOWS_2008,WINDOWS_GPT,WINDOWS,XEN

--s, snapshot-schedule
:    Snapshot schedule to use for replication. Options are: HOURLY,DAILY,WEEKLY [required]

--t, tier
:    Endurance Storage Tier (IOPS per GB) of the primary volume for which a replica is ordered [optional], options are: 0.25,2,4,10,if no tier is specified, the tier of the original volume will be used

## ibmcloud sl block replica-partners
{: #sl_block_replica_partners}

List existing replicant volumes for a block volume

**Examples**:

   ibmcloud sl block replica-partners 12345678
   This command lists existing replicant volumes for block volume with ID 12345678.

```bash
ibmcloud sl block replica-partners IDENTIFIER
```
{: codeblock}


## ibmcloud sl block snapshot-cancel
{: #sl_block_snapshot_cancel}

Cancel existing snapshot space for a given volume

**Examples**:

   ibmcloud sl block snapshot-cancel 12345678 --immediate -f 
   This command cancels snapshot with ID 12345678 immediately without asking for confirmation.

```bash
ibmcloud sl block snapshot-cancel IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--immediate
:    Cancel the snapshot space immediately instead of on the billing anniversary

--reason
:    An optional reason for cancellation

## ibmcloud sl block snapshot-create
{: #sl_block_snapshot_create}

Create a snapshot on a given volume

ibmcloud sl block snapshot-create VOLUME_ID [OPTIONS]

**Examples**:

   ibmcloud sl block snapshot-create 12345678 --note snapshotforibmcloud
   This command creates a snapshot for volume with ID 12345678 and with addition note as snapshotforibmcloud.

```bash
ibmcloud sl block snapshot-create IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--n, note
:    Notes to set on the new snapshot

## ibmcloud sl block snapshot-delete
{: #sl_block_snapshot_delete}

Delete a snapshot on a given volume



```bash
ibmcloud sl block snapshot-delete IDENTIFIER
```
{: codeblock}


## ibmcloud sl block snapshot-disable
{: #sl_block_snapshot_disable}

Disable snapshots on the specified schedule for a given volume

ibmcloud sl block snapshot-disable VOLUME_ID [OPTIONS]

**Examples**:

   ibmcloud sl block snapshot-disable 12345678 -s DAILY
   This command disables daily snapshot for volume with ID 12345678.

```bash
ibmcloud sl block snapshot-disable IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--s, schedule-type
:    Snapshot schedule [required], options are: HOURLY,DAILY,WEEKLY

## ibmcloud sl block snapshot-enable
{: #sl_block_snapshot_enable}

Enable snapshots for a given volume on the specified schedule

See https://sldn.softlayer.com/reference/services/SoftLayer_Network_Storage/enableSnapshots/ for more details about these options.
**Examples**:

   ibmcloud sl block snapshot-enable 12345678 -s WEEKLY -c 5 -m 0 --hour 2 -d 0
   This command enables snapshot for volume with ID 12345678, snapshot is taken weekly on every Sunday at 2:00, and up to 5 snapshots are retained.

```bash
ibmcloud sl block snapshot-enable IDENTIFIER [flags]
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

## ibmcloud sl block snapshot-get-notification-status
{: #sl_block_snapshot_get_notification_status}

Get snapshots space usage threshold warning flag setting for a given volume.



```bash
ibmcloud sl block snapshot-get-notification-status IDENTIFIER
```
{: codeblock}


## ibmcloud sl block snapshot-list
{: #sl_block_snapshot_list}

List block storage snapshots


**Examples**:

   ibmcloud sl block snapshot-list 12345678 --sortby id 
   This command lists all snapshots of volume with ID 12345678 and sorts them by ID.

```bash
ibmcloud sl block snapshot-list IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--sortby
:    Column to sort by. Options are: id,name,created,size_bytes

## ibmcloud sl block snapshot-order
{: #sl_block_snapshot_order}

Order snapshot space for a block storage volume

See https://cloud.ibm.com/docs/BlockStorage?topic=BlockStorage-getting-started for sizing options.
ibmcloud sl block volume-options' to get available options.

**Examples**:

   ibmcloud sl block snapshot-order 12345678 -s 1000 -t 4 
   This command orders snapshot space for volume with ID 12345678, the size is 1000GB, the tier level is 4 IOPS per GB.

```bash
ibmcloud sl block snapshot-order IDENTIFIER [flags]
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

## ibmcloud sl block snapshot-restore
{: #sl_block_snapshot_restore}

Restore block volume using a given snapshot


**Examples**:

   ibmcloud sl block snapshot-restore 12345678 87654321
   This command restores volume with ID 12345678 from snapshot with ID 87654321.

```bash
ibmcloud sl block snapshot-restore IDENTIFIER SNAPSHOT_ID
```
{: codeblock}


## ibmcloud sl block snapshot-schedule-list
{: #sl_block_snapshot_schedule_list}

List snapshot schedules for a given volume



```bash
ibmcloud sl block snapshot-schedule-list IDENTIFIER
```
{: codeblock}


## ibmcloud sl block snapshot-set-notification
{: #sl_block_snapshot_set_notification}

Enables/Disables snapshot space usage threshold warning for a given volume.



```bash
ibmcloud sl block snapshot-set-notification IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--disable
:    Disable snapshot notification.

--enable
:    Enable snapshot notification.

## ibmcloud sl block subnets-assign
{: #sl_block_subnets_assign}

Assign block storage subnets to the given host id.

access_id is the host_id obtained by: sl block access-list volume_id SoftLayer_Account::iscsiisolationdisabled must be False to use this command ibmcloud sl block subnets-assign ACCESS_ID [OPTIONS]

**Examples**:

   ibmcloud sl block subnets-assign 111111 --subnet-id 222222
   ibmcloud sl block subnets-assign 111111 --subnet-id 222222 --subnet-id 333333
   ACCESS_ID is the host_id obtained by: ibmcloud sl block access-list volume_id

```bash
ibmcloud sl block subnets-assign IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--subnet-id
:    IDs of the subnets to assign; e.g.: --subnet-id 1234

## ibmcloud sl block subnets-list
{: #sl_block_subnets_list}

List block storage assigned subnets for the given host id.

access_id is the host_id obtained by: sl block access-list volume_id ibmcloud sl block subnets-list ACCESS_ID [OPTIONS]

**Examples**:

   ibmcloud sl block subnets-list 12345678 
   ACCESS_ID is the host_id obtained by: ibmcloud sl block access-list volume_id

```bash
ibmcloud sl block subnets-list IDENTIFIER
```
{: codeblock}


## ibmcloud sl block subnets-remove
{: #sl_block_subnets_remove}

Remove block storage subnets to the given host id.

access_id is the host_id obtained by: sl block access-list volume_id SoftLayer_Account::iscsiisolationdisabled must be False to use this command ibmcloud sl block subnets-remove ACCESS_ID [OPTIONS]

**Examples**:

   ibmcloud sl block subnets-remove 111111 --subnet-id 222222
   ibmcloud sl block subnets-remove 111111 --subnet-id 222222 --subnet-id 333333
   ACCESS_ID is the host_id obtained by: ibmcloud sl block access-list volume_id

```bash
ibmcloud sl block subnets-remove IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--subnet-id
:    IDs of the subnets to remove

## ibmcloud sl block volume-cancel
{: #sl_block_volume_cancel}

Cancel an existing block storage volume

ibmcloud sl block volume-cancel VOLUME_ID [OPTIONS]

**Examples**:

   ibmcloud sl block volume-cancel 12345678 --immediate -f 
   This command cancels volume with ID 12345678 immediately and without asking for confirmation.

```bash
ibmcloud sl block volume-cancel IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--immediate
:    Cancel the block storage volume immediately instead of on the billing anniversary

--reason
:    An optional reason for cancellation

## ibmcloud sl block volume-convert
{: #sl_block_volume_convert}

Convert a dependent duplicate volume to an independent volume.



```bash
ibmcloud sl block volume-convert IDENTIFIER
```
{: codeblock}


## ibmcloud sl block volume-count
{: #sl_block_volume_count}

List number of block storage volumes per datacenter



```bash
ibmcloud sl block volume-count [flags]
```
{: codeblock}


**Command options**:

--d, datacenter
:    Filter by datacenter shortname

--s, sortby
:    Column to sort by

## ibmcloud sl block volume-detail
{: #sl_block_volume_detail}

Display details for a specified volume



```bash
ibmcloud sl block volume-detail IDENTIFIER
```
{: codeblock}


## ibmcloud sl block volume-duplicate
{: #sl_block_volume_duplicate}

Order a block volume by duplicating an existing volume

ibmcloud sl block volume-duplicate VOLUME_ID [OPTIONS]

**Examples**:

   ibmcloud sl block volume-duplicate 12345678 
   This command shows order a new volume by duplicating the volume with ID 12345678.

```bash
ibmcloud sl block volume-duplicate IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--billing
:    Optional parameter for Billing rate (default to monthly) Choices: hourly or monthly

--d, dependent-duplicate
:    Whether or not this duplicate will be a dependent duplicate of the origin volume.    [default: False]

--i, duplicate-iops
:    Performance Storage IOPS, between 100 and 6000 in multiples of 100, if no IOPS value is specified, the IOPS value of the original volume will be used Requirements: [If IOPS/GB for the origin volume is less than 0.3, IOPS/GB for the duplicate must also be less than 0.3. If IOPS/GB for the origin volume is greater than or equal to 0.3, IOPS/GB for the duplicate must also be greater than or equal to 0.3.]

--s, duplicate-size
:    Size of duplicate block volume in GB, if no size is specified, the size of the original volume will be used Potential Sizes: [20, 40, 80, 100, 250, 500, 1000, 2000, 4000, 8000, 12000] Minimum: [the size of the origin volume]

--n, duplicate-snapshot-size
:    The size of snapshot space to order for the duplicate, if no snapshot space size is specified, the snapshot space size of the origin volume will be used Input `0` for this parameter to order a duplicate volume with no snapshot space.

--t, duplicate-tier
:    Endurance Storage Tier, if no tier is specified, the tier of the original volume will be used Requirements: [If IOPS/GB for the origin volume is 0.25, IOPS/GB for the duplicate must also be 0.25. If IOPS/GB for the origin volume is greater than 0.25, IOPS/GB for the duplicate must also be greater than 0.25.] Choices: 0.25, 2, 4, 10

--f, force
:    Force operation without confirmation

--o, origin-snapshot-id
:    ID of an origin volume snapshot to use for duplication

## ibmcloud sl block volume-limits
{: #sl_block_volume_limits}

Lists the storage limits per datacenter for this account.

ibmcloud sl block volume-limits [OPTIONS]

**Examples**:

	ibmcloud sl block volume-limits
	This command lists the storage limits per datacenter for this account.

```bash
ibmcloud sl block volume-limits
```
{: codeblock}


## ibmcloud sl block volume-list
{: #sl_block_volume_list}

List block storage

ibmcloud sl block volume-list [OPTIONS]

**Examples**:

   ibmcloud sl block volume-list -d dal09 -t endurance --sortby capacity_gb
   This command lists all endurance volumes on current account that are located at dal09, and sorts them by capacity.

```bash
ibmcloud sl block volume-list [flags]
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
:    Filter by ID of the order that purchased the block storage

--sortby
:    Column to sort by, default:id, options are: id,username,datacenter,storage_type,capacity_gb,bytes_used,ip_addr,lunId,active_transactions,created_by

--t, storage-type
:    Filter by type of storage volume, options are: performance,endurance

--u, username
:    Filter by volume username

## ibmcloud sl block volume-modify
{: #sl_block_volume_modify}

Modify an existing block storage volume

Valid size and iops options can be found here:
https://cloud.ibm.com/docs/BlockStorage/index.html#provisioning-considerations
https://cloud.ibm.com/docs/BlockStorage?topic=BlockStorage-orderingBlockStorage&interface=cli

   **Examples**:

	  ibmcloud sl block volume-modify 12345678 --new-size 1000 --new-iops 4000 
	  This command modify a volume 12345678 with size is 1000GB, IOPS is 4000.
	  ibmcloud sl block volume-modify 12345678 --new-size 500 --new-tier 4
	  This command modify a volume 12345678 with size is 500GB, tier level is 4 IOPS per GB.

```bash
ibmcloud sl block volume-modify IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--i, new-iops
:    Performance Storage IOPS, between 100 and 6000 in multiples of 100 [only for performance volumes] ***If no IOPS value is specified, the original IOPS value of the volume will be used.***

--c, new-size
:    New Size of block volume in GB. ***If no size is given, the original size of volume is used.***
      Potential Sizes: [20, 40, 80, 100, 250, 500, 1000, 2000, 4000, 8000, 12000]
      Minimum: [the original size of the volume]

--t, new-tier
:    Endurance Storage Tier (IOPS per GB) [only for endurance volumes] ***If no tier is specified, the original tier of the volume will be used.***
Tiers: [0.25, 2, 4, 10]

## ibmcloud sl block volume-options
{: #sl_block_volume_options}

List all options for ordering a block or file storage volume

List all options for ordering a block or file storage volume

See Also:
	https://cloud.ibm.com/docs/BlockStorage/index.html#provisioning-considerations
	https://cloud.ibm.com/docs/BlockStorage?topic=BlockStorage-orderingBlockStorage&interface=cli


```bash
ibmcloud sl block volume-options [flags]
```
{: codeblock}


**Command options**:

--prices
:    Show prices in the storage, snapshot and iops range tables.

## ibmcloud sl block volume-order
{: #sl_block_volume_order}

Order a block storage volume

**Examples**:

   ibmcloud sl block volume-order --storage-type performance --size 1000 --iops 4000 --os-type LINUX -d dal09
   This command orders a performance volume with size is 1000GB, IOPS is 4000, OS type is LINUX, located at dal09.
   ibmcloud sl block volume-order --storage-type endurance --size 500 --tier 4 --os-type XEN -d dal09 --snapshot-size 500
   This command orders a endurance volume with size is 500GB, tier level is 4 IOPS per GB, OS type is XEN, located at dal09, and additional snapshot space size is 500GB.

```bash
ibmcloud sl block volume-order [flags]
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

--o, os-type
:    Operating System [required], options are: HYPER_V,LINUX,VMWARE,WINDOWS_2008,WINDOWS_GPT,WINDOWS,XEN

--s, size
:    Size of storage volume in GB [required]

--n, snapshot-size
:    Optional parameter for ordering snapshot space along with endurance block storage; specifies the size (in GB) of snapshot space to order

--t, storage-type
:    Type of storage volume [required], options are: performance,endurance

--e, tier
:    Endurance Storage Tier (IOP per GB) [required for storage-type endurance], options are: 0.25,2,4,10

## ibmcloud sl block volume-refresh
{: #sl_block_volume_refresh}

Refresh a duplicate volume with a snapshot from its parent.

Refresh a duplicate volume with a snapshot from its parent. ibmcloud sl block volume-refresh VOLUME_ID SNAPSHOT_ID

**Examples**:

	ibmcloud sl block volume-refresh VOLUME_ID SNAPSHOT_ID
	Refresh a duplicate VOLUME_ID with a snapshot from its parent SNAPSHOT_ID.

```bash
ibmcloud sl block volume-refresh IDENTIFIER SNAPSHOT_ID [flags]
```
{: codeblock}


**Command options**:

--f, force-refresh
:    Force the volume refresh, will cancel any ongoing transactions.

## ibmcloud sl block volume-set-lun-id
{: #sl_block_volume_set_lun_id}

Set the LUN ID on an existing block storage volume

Set the LUN ID on an existing block storage volume ibmcloud sl block volume-set-lun-id VOLUME_ID LUN_ID

	The LUN ID only takes effect during the Host Authorization process. It is
	recommended (but not necessary) to de-authorize all hosts before using
	this method. See "block access-revoke".
	VOLUME_ID - the volume ID on which to set the LUN ID
	LUN_ID - recommended range is an integer between 0 and 255. Advanced users
	can use an integer between 0 and 4095

```bash
ibmcloud sl block volume-set-lun-id IDENTIFIER LUN_ID
```
{: codeblock}


## ibmcloud sl block volume-set-note
{: #sl_block_volume_set_note}

Set note for an existing block storage volume.

Set note for an existing block storage volume. ibmcloud sl block volume-set-note [OPTIONS] VOLUME_ID

**Examples**:

   ibmcloud sl block volume-set-note 12345678 --note 'this is my note'

```bash
ibmcloud sl block volume-set-note IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--n, note
:    Public notes related to a Storage volume  [required]
