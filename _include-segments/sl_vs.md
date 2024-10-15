


## ibmcloud sl vs authorize-storage
{: #sl_vs_authorize_storage}

Authorize File, Block and Portable Storage to a Virtual Server

ibmcloud sl vs authorize-storage [OPTIONS] IDENTIFIER

**Examples**:

   ibmcloud sl vs authorize-storage --username-storage SL01SL30-37 1234567
   Authorize File, Block and Portable Storage to a Virtual Server.

```bash
ibmcloud sl vs authorize-storage IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--p, portable-id
:    The portable storage id to be added to the virtual server

--u, username-storage
:    The storage username to be added to the virtual server.

## ibmcloud sl vs bandwidth
{: #sl_vs_bandwidth}

Bandwidth data over date range.

ibmcloud sl vs bandwidth IDENTIFIER [OPTIONS]
Time formats that are either '2006-01-02', '2006-01-02T15:04' or '2006-01-02T15:04-07:00'

Due to some rounding and date alignment details, results here might be slightly different than results in the control portal.
Bandwidth is listed in GB, if no time zone is specified, GMT+0 is assumed.

**Examples**:


   ibmcloud sl vs bandwidth 1234 -s 2006-01-02T15:04 -e 2006-01-02T15:04-07:00

```bash
ibmcloud sl vs bandwidth IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--e, end
:    End date for bandwidth reporting

--q, quiet
:    Only show the summary table.

--r, rollup
:    Number of seconds to report as one data point. 300, 600, 1800, 3600 (default), 43200 or 86400 seconds

--s, start
:    Start date for bandwdith reporting

## ibmcloud sl vs billing
{: #sl_vs_billing}

Get billing details for a virtual server instance



```bash
ibmcloud sl vs billing IDENTIFIER
```
{: codeblock}


## ibmcloud sl vs cancel
{: #sl_vs_cancel}

Cancel virtual server instance



```bash
ibmcloud sl vs cancel IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

## ibmcloud sl vs capacity-create
{: #sl_vs_capacity_create}

Create a Reserved Capacity instance.

ibmcloud sl vs capacity-create [OPTIONS]
**Examples**:

ibmcloud sl vs capacity-create -n myvsi -b 1234567 -fl C1_2X2_1_YEAR_TERM -i 2
This command orders a Reserved Capacity instance with name is myvsi, backendRouterId 1234567, flavor C1_2X2_1_YEAR_TERM and 2 instances,
ibmcloud sl vs capacity-create --name myvsi --backendRouterId 1234567 --flavor C1_2X2_1_YEAR_TERM --instances 2 --test
This command tests whether the order is valid with above options before the order is actually placed.

WARNING: Reserved Capacity is on a yearly contract and not cancelable until the contract is expired.

```bash
ibmcloud sl vs capacity-create [flags]
```
{: codeblock}


**Command options**:

--b, backendRouterId
:    BackendRouterId, create-options has a list of valid ids to use. [required]

--l, flavor
:     Capacity keyname (C1_2X2_1_YEAR_TERM for example). [required]

--f, force
:    Force operation without confirmation

--i, instances
:    Number of VSI instances this capacity reservation can support. [required]

--n, name
:    Name for your new reserved capacity  [required]

--test
:     Do not actually create the reserved capacity

## ibmcloud sl vs capacity-create-options
{: #sl_vs_capacity_create_options}

List options for creating Reserved Capacity Group instance



```bash
ibmcloud sl vs capacity-create-options
```
{: codeblock}


## ibmcloud sl vs capacity-detail
{: #sl_vs_capacity_detail}

Get Reserved Capacity Group details.



```bash
ibmcloud sl vs capacity-detail IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--column
:    Column to display. Options are: id, hostname, domain, primary_ip, backend_ip. This option can be specified multiple times

--sortby
:    Column to sort by. Options are: id, hostname, domain, primary_ip, backend_ip

## ibmcloud sl vs capacity-list
{: #sl_vs_capacity_list}

List Reserved Capacity groups.



```bash
ibmcloud sl vs capacity-list
```
{: codeblock}


## ibmcloud sl vs capture
{: #sl_vs_capture}

Capture virtual server instance into an image

ibmcloud sl vs capture IDENTIFIER [OPTIONS]

**Examples**:

   ibmcloud sl vs capture 12345678 -n mycloud --all --note testing
   This command captures virtual server instance with ID of 12345678 with all disks into an image named "mycloud" with note "testing".

```bash
ibmcloud sl vs capture IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--all
:    Capture all block devices that belong to the virtual server

--device
:    The block device ID´s to archive, multiple occurrence allowed

--n, name
:    Name of the image [required]

--note
:    Add a note to be associated with the image

## ibmcloud sl vs create
{: #sl_vs_create}

Create virtual server instance

ibmcloud sl vs create [OPTIONS]

**Examples**:

   ibmcloud sl vs create -H myvsi -D ibm.com -c 4 -m 4096 -d dal10 -o UBUNTU_16_64 --disk 100 --disk 1000 --vlan-public 413
	This command orders a virtual server instance with hostname is myvsi, domain is ibm.com, 4 cpu cores, 4096M memory, located at datacenter: dal10,
	operation system is UBUNTU 16 64 bits, 2 disks, one is 100G, the other is 1000G, and placed at public vlan with ID 413.
	ibmcloud sl vs create -H myvsi -D ibm.com -c 4 -m 4096 -d dal10 -o UBUNTU_16_64 --disk 100 --disk 1000 --vlan-public 413 --test
	This command tests whether the order is valid with above options before the order is actually placed.
	ibmcloud sl vs create -H myvsi -D ibm.com -c 4 -m 4096 -d dal10 -o UBUNTU_16_64 --disk 100 --disk 1000 --vlan-public 413 --export ~/myvsi.txt
	This command exports above options to a file: myvsi.txt under user home directory for later use.

```bash
ibmcloud sl vs create [flags]
```
{: codeblock}


**Command options**:

--billing
:    Billing rate. Default is: hourly. Options are: hourly, monthly

--boot-mode
:    Specify the mode to boot the OS in. Supported modes are HVM and PV.

--c, cpu
:    Number of CPU cores [required]

--d, datacenter
:    Datacenter shortname [required]

--dedicated
:    Create a dedicated Virtual Server (Private Node)

--disk
:    Disk sizes (multiple occurrence permitted)

--D, domain
:    Domain portion of the FQDN [required]

--export
:    Exports options to a template file

--flavor
:    Public Virtual Server flavor key name

--f, force
:    Force operation without confirmation

--host-id
:    Host Id to provision a Dedicated Virtual Server onto

--H, hostname
:    Host portion of the FQDN [required]

--image
:    Image ID. See: '${COMMAND_NAME} sl image list' for reference

--k, key
:    The IDs of the SSH keys to add to the root user (multiple occurrence permitted)

--like
:    Use the configuration from an existing virtual server

--m, memory
:    Memory in megabytes [required]

--n, network
:    Network port speed in Mbps

--o, os
:    OS install code. Tip: you can specify OS_LATEST

--placement-group-id
:    Placement Group Id to order this guest on.

--i, postinstall
:    Post-install script to download

--private
:    Forces the virtual server to only have access the private network

--s, private-security-group
:    Security group ID to associate with the private interface (multiple occurrence permitted)

--S, public-security-group
:    Security group ID to associate with the public interface (multiple occurrence permitted)

--quantity
:    The quantity of virtual server be created. It should be greater or equal to 1. This value defaults to 1.

--san
:    Use SAN storage instead of local disk

--subnet-private
:    The ID of the private SUBNET on which you want the virtual server placed

--subnet-public
:    The ID of the public SUBNET on which you want the virtual server placed

--g, tag
:    Tags to add to the instance (multiple occurrence permitted)

--t, template
:    A template file that defaults the command-line options

--test
:    Do not actually create the virtual server

--transient
:    Create a transient virtual server

--u, userdata
:    User defined metadata string

--F, userfile
:    Read userdata from file

--vlan-private
:    The ID of the private VLAN on which you want the virtual server placed

--vlan-public
:    The ID of the public VLAN on which you want the virtual server placed

--wait
:    Wait until the virtual server is finished provisioning for up to X seconds before returning. It's not compatible with option --quantity

## ibmcloud sl vs credentials
{: #sl_vs_credentials}

List virtual server instance credentials

ibmcloud sl vs authorize-storage [OPTIONS] IDENTIFIER

**Examples**:

   ibmcloud sl vs authorize-storage --username-storage SL01SL30-37 1234567
   Authorize File, Block and Portable Storage to a Virtual Server.

```bash
ibmcloud sl vs credentials IDENTIFIER
```
{: codeblock}


## ibmcloud sl vs detail
{: #sl_vs_detail}

Get details for a virtual server instance



```bash
ibmcloud sl vs detail IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--passwords
:    Show passwords (check over your shoulder!)

--price
:    Show associated prices

## ibmcloud sl vs dns-sync
{: #sl_vs_dns_sync}

Synchronize DNS records for a virtual server instance

ibmcloud sl vs dns-sync IDENTIFIER [OPTIONS]
   Note: If you don't specify any arguments, it will attempt to update both the A
   and PTR records. If you don't want to update both records, you may use the
   -a or --ptr arguments to limit the records updated.
 
**Examples**:

   ibmcloud sl vs dns-sync 12345678 --a-record --ttl 3600
   This command synchronizes A record(IP V4 address) of virtual server instance with ID 12345678 to DNS server and sets ttl of this A record to 3600.
   ibmcloud sl vs dns-sync 12345678 --aaaa-record --ptr
   This command synchronizes both AAAA record(IP V6 address) and PTR record of virtual server instance with ID 12345678 to DNS server.

```bash
ibmcloud sl vs dns-sync IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--a, a-record
:    Sync the A record for the host

--aaaa-record
:    Sync the AAAA record for the host

--f, force
:    Force operation without confirmation

--ptr
:    Sync the PTR record for the host

--ttl
:    Sets the TTL for the A and/or PTR records, default is: 7200

## ibmcloud sl vs edit
{: #sl_vs_edit}

Edit a virtual server instance's details

ibmcloud sl vs edit IDENTIFIER [OPTIONS]

**Examples**:

   ibmcloud sl vs edit 12345678 -D ibm.com -H myapp --tag testcli --public-speed 1000
   This command updates virtual server instance with ID 12345678 and set its domain to be "ibm.com", hostname to "myapp", tag to "testcli", 
   and public network port speed to 1000 Mbps.

```bash
ibmcloud sl vs edit IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--D, domain
:    Domain portion of the FQDN

--H, hostname
:    Host portion of the FQDN. example: server

--private-speed
:    Private port speed, options are: 0,10,100,1000,10000

--public-speed
:    Public port speed, options are: 0,10,100,1000,10000

--g, tag
:    Tags to set or empty string to remove all

--u, userdata
:    User defined metadata string

--F, userfile
:    Read userdata from file

## ibmcloud sl vs host-create
{: #sl_vs_host_create}

Create a host for dedicated virtual servers



```bash
ibmcloud sl vs host-create [flags]
```
{: codeblock}


**Command options**:

--b, billing
:    Billing rate. Default is: hourly. Options are: hourly, monthly

--d, datacenter
:    Datacenter shortname [required]

--D, domain
:    Domain portion of the FQDN [required]

--f, force
:    Force operation without confirmation

--H, hostname
:    Host portion of the FQDN [required]

--s, size
:    Size of the dedicated host, currently only one size is available: 56_CORES_X_242_RAM_X_1_4_TB

--v, vlan-private
:    The ID of the private VLAN on which you want the dedicated host placed. See: '${COMMAND_NAME} sl vlan list' for reference

## ibmcloud sl vs host-list
{: #sl_vs_host_list}

List dedicated hosts on your account



```bash
ibmcloud sl vs host-list [flags]
```
{: codeblock}


**Command options**:

--d, datacenter
:    Filter by datacenter of the dedicated host

--n, name
:    Filter by name of the dedicated host

--order
:    Filter by ID of the order which purchased this dedicated host

--owner
:    Filter by owner of the dedicated host

--sortby
:    Column to sort by (Id, Name, Datacenter, Router, Cpu, Memory, Disk, Guests) [default: Id]

## ibmcloud sl vs list
{: #sl_vs_list}

List virtual server instances on your account

ibmcloud sl vs list [OPTIONS]

**Examples**:

   ibmcloud sl vs list --domain ibm.com --hourly --sortby memory
   This command lists all hourly-billing virtual server instances on current account filtering domain equals to "ibm.com" and sort them by memory.

```bash
ibmcloud sl vs list [flags]
```
{: codeblock}


**Command options**:

--column
:    Column to display. Options are: id,hostname,domain,cpu,memory,public_ip,private_ip,datacenter,action,guid,power_state,created_by,tags. This option can be specified multiple times

--c, cpu
:    Filter by number of CPU cores

--d, datacenter
:    Filter by datacenter shortname

--D, domain
:    Filter by domain portion of the FQDN

--H, hostname
:    Filter by host portion of the FQDN

--hourly
:    Show only hourly instances

--m, memory
:    Filter by memory in megabytes

--monthly
:    Show only monthly instances

--n, network
:    Filter by network port speed in Mbps

--o, order
:    Filter by ID of the order which purchased this instance

--owner
:    Filtered by Id of user who owns the instances

--p, private-ip
:    Filter by private IP address

--P, public-ip
:    Filter by public IP address

--sortby
:    Column to sort by, default is:hostname, options are:id,hostname,domain,datacenter,cpu,memory,public_ip,private_ip

--g, tag
:    Filter by tags (multiple occurrence permitted)

## ibmcloud sl vs migrate
{: #sl_vs_migrate}

Manage VSIs that require migration

ibmcloud sl vs migrate [OPTIONS]

**Examples**:

   ibmcloud sl vs migrate --guest 1234567
   Manage VSIs that require migration. Can migrate Dedicated Instance from one dedicated host to another dedicated host as well.

```bash
ibmcloud sl vs migrate [flags]
```
{: codeblock}


**Command options**:

--a, all
:    Migrate ALL guests that require migration immediately.

--g, guest
:    Guest ID to immediately migrate.

--H, host
:    Dedicated Host ID to migrate to. Only works on guests that are already on a dedicated host.

## ibmcloud sl vs monitoring-list
{: #sl_vs_monitoring_list}

Get details for a vsi monitors device.



```bash
ibmcloud sl vs monitoring-list IDENTIFIER
```
{: codeblock}


## ibmcloud sl vs notifications
{: #sl_vs_notifications}

Shows who gets notified when the server virtual instance has a monitoring issues



```bash
ibmcloud sl vs notifications IDENTIFIER
```
{: codeblock}


## ibmcloud sl vs notifications-add
{: #sl_vs_notifications_add}

Create a user virtual notification entry.



```bash
ibmcloud sl vs notifications-add IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--users
:    User ID to be notified on monitoring failure, multiple occurrence allowed

## ibmcloud sl vs notifications-delete
{: #sl_vs_notifications_delete}

Remove a user VS notification entry.



```bash
ibmcloud sl vs notifications-delete IDENTIFIER
```
{: codeblock}


## ibmcloud sl vs options
{: #sl_vs_options}

List options for creating virtual server instance



```bash
ibmcloud sl vs options
```
{: codeblock}


## ibmcloud sl vs os-available
{: #sl_vs_os_available}

Get all available Operating Systems.



```bash
ibmcloud sl vs os-available
```
{: codeblock}


## ibmcloud sl vs pause
{: #sl_vs_pause}

Pause an active virtual server instance



```bash
ibmcloud sl vs pause IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

## ibmcloud sl vs power-off
{: #sl_vs_power_off}

Power off an active virtual server instance



```bash
ibmcloud sl vs power-off IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--hard
:    Perform a hard shutdown

--soft
:    Perform a soft shutdown

## ibmcloud sl vs power-on
{: #sl_vs_power_on}

Power on a virtual server instance



```bash
ibmcloud sl vs power-on IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

## ibmcloud sl vs ready
{: #sl_vs_ready}

Check if a virtual server instance is ready for use

Will periodically check the status of a virtual server's active transaction.
When the transcation is finished the virtual server should be ready for use.

```bash
ibmcloud sl vs ready IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--wait
:    Wait until the virtual server is finished provisioning for up to X seconds before returning

## ibmcloud sl vs reboot
{: #sl_vs_reboot}

Reboot an active virtual server instance



```bash
ibmcloud sl vs reboot IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--hard
:    Perform a hard reboot

--soft
:    Perform a soft reboot

## ibmcloud sl vs reload
{: #sl_vs_reload}

Reload operating system on a virtual server instance

ibmcloud sl vs reload IDENTIFIER [OPTIONS]

**Examples**:

   ibmcloud sl vs reload 12345678
   This command reloads current operating system for virtual server instance with ID 12345678.
   ibmcloud sl vs reload 12345678 --image 1234
   This command reloads operating system from image with ID 1234 for virtual server instance with ID 12345678.

```bash
ibmcloud sl vs reload IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--image
:    Image ID. The default is to use the current operating system.
See: '${COMMAND_NAME} sl image list' for reference

--k, key
:    The IDs of the SSH keys to add to the root user (multiple occurrence permitted)

--i, postinstall
:    Post-install script to download

## ibmcloud sl vs rescue
{: #sl_vs_rescue}

Reboot a virtual server instance into a rescue image



```bash
ibmcloud sl vs rescue IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

## ibmcloud sl vs resume
{: #sl_vs_resume}

Resume a paused virtual server instance



```bash
ibmcloud sl vs resume IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

## ibmcloud sl vs storage
{: #sl_vs_storage}

Get storage details for a virtual server.



```bash
ibmcloud sl vs storage IDENTIFIER
```
{: codeblock}


## ibmcloud sl vs upgrade
{: #sl_vs_upgrade}

Upgrade a virtual server instance

Note: This virtual server will be rebooted once the upgrade order is placed.
The instance is halted until the upgrade transaction is completed. However for Network, no reboot is required.

**Examples**:

	ibmcloud sl vs upgrade 12345678 -c 8 -m 8192 --network 1000
	This commands upgrades virtual server instance with ID 12345678 and set number of CPU cores to 8, memory to 8192M, network port speed to 1000 Mbps.

```bash
ibmcloud sl vs upgrade IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--add-disk
:    Add Hard disk in GB

--c, cpu
:    Number of CPU cores

--flavor
:    Flavor key name

--f, force
:    Force operation without confirmation

--m, memory
:    Memory in megabytes

--network
:    Network port speed in Mbps

--private
:    CPU core will be on a dedicated host server

--resize-disk
:    Update disk number to size in GB [capacity,diskNumber]. --resize-disk 250,2

## ibmcloud sl vs usage
{: #sl_vs_usage}

usage data over date range.

ibmcloud sl vs usage IDENTIFIER [OPTIONS]
Usage information of a virtual server.
**Examples**:

   ibmcloud sl vs usage 1234 --start 2006-01-02 --end 2006-01-02 --valid-data cpu0

```bash
ibmcloud sl vs usage IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--e, end
:    End Date e.g. 2019-4-2 (yyyy-MM-dd)  [required]

--s, start
:    Start Date e.g. 2019-3-4 (yyyy-MM-dd)  [required]

--p, summary-period
:    300, 600, 1800, 3600, 43200 or 86400 seconds.

--t, valid-data
:    Metric_Data_Type keyName e.g. CPU0, CPU1, MEMORY_USAGE, etc.  [required]
