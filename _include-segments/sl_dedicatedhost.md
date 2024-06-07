


## ibmcloud sl dedicatedhost cancel-guests
{: #sl_dedicatedhost_cancel_guests}

Cancel all virtual guests of the dedicated host immediately.



```bash
ibmcloud sl dedicatedhost cancel-guests [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

## ibmcloud sl dedicatedhost create
{: #sl_dedicatedhost_create}

Create a dedicatedhost



```bash
ibmcloud sl dedicatedhost create [flags]
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

--test
:    Do not actually create the dedicatedhost

--v, vlan-private
:    The ID of the private VLAN on which you want the dedicated host placed. See: '${COMMAND_NAME} sl vlan list' for reference

## ibmcloud sl dedicatedhost create-options
{: #sl_dedicatedhost_create_options}

Host order options for a given dedicated host.

ibmcloud sl dedicatedhost create-options [OPTIONS]

**Examples**:

   ibmcloud sl dedicatedhost create-options

   To get the list of available private vlans use this command: ibmcloud sl dedicatedhost create-options --datacenter dal05 --flavor 56_CORES_X_242_RAM_X_1_4_TB"

```bash
ibmcloud sl dedicatedhost create-options [flags]
```
{: codeblock}


**Command options**:

--d, datacenter
:    Filter private vlans by Datacenter shortname e.g. ams01, (requires --flavor)

--f, flavor
:    Dedicated Virtual Host flavor (requires --datacenter) e.g. 56_CORES_X_242_RAM_X_1_4_TB

## ibmcloud sl dedicatedhost detail
{: #sl_dedicatedhost_detail}

Get details for a dedicated host.



```bash
ibmcloud sl dedicatedhost detail IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--guests
:    Show guests on dedicated host

--price
:    Show associated prices

## ibmcloud sl dedicatedhost list
{: #sl_dedicatedhost_list}

List dedicated hosts on your account



```bash
ibmcloud sl dedicatedhost list [flags]
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

## ibmcloud sl dedicatedhost list-guests
{: #sl_dedicatedhost_list_guests}

List Dedicated Host Guests.

ibmcloud sl dedicatedhost list-guests IDENTIFIER[OPTIONS]

**Examples**:

   ibmcloud sl dedicatedhost list-guests -d dal09 --sortby hostname 1234567
   This command list all Dedicated Host guests in the Account.

```bash
ibmcloud sl dedicatedhost list-guests IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--column
:    Column to display. [Options are: guid, cpu, memory, datacenter, primary_ip, backend_ip, created_by, power_state, tags] [default: id,hostname,domain,primary_ip,backend_ip,power_state].

--c, cpu
:    Filter by the number of CPU cores

--d, domain
:    Filter by domain portion of the FQDN.

--H, hostname
:    Filter by host portion of the FQDN.

--m, memory
:    Filter by Memory capacity in megabytes.

--sortby
:    Column to sort by

--t, tag
:    Filter by tags.
