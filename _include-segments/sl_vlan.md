


## ibmcloud sl vlan cancel
{: #sl_vlan_cancel}

Cancel a VLAN

ibmcloud sl vlan cancel IDENTIFIER [OPTIONS]

**Examples**:

   ibmcloud sl vlan cancel 12345678 -f
   This command cancels vlan with ID 12345678 without asking for confirmation.

```bash
ibmcloud sl vlan cancel IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

## ibmcloud sl vlan create
{: #sl_vlan_create}

Create a new VLAN

ibmcloud sl vlan create [OPTIONS]

**Examples**:

   ibmcloud sl vlan create -t public -d dal09 -n myvlan
   This command creates a public vlan located in datacenter dal09 named "myvlan".
   ibmcloud sl vlan create -r bcr01a.dal09 -n myvlan
   This command creates a vlan on router bcr01a.dal09 named "myvlan".

```bash
ibmcloud sl vlan create [flags]
```
{: codeblock}


**Command options**:

--d, datacenter
:    The short name of the datacenter

--f, force
:    Force operation without confirmation

--n, name
:    The name of the VLAN

--r, router
:    The hostname of the router

--t, vlan-type
:    The type of the VLAN, either public or private

## ibmcloud sl vlan detail
{: #sl_vlan_detail}

Get details about a VLAN

**Examples**:

   ibmcloud sl vlan detail 12345678	--no-vs --no-hardware
   This command shows details of vlan with ID 12345678, and not list virtual server or hardware server.

```bash
ibmcloud sl vlan detail IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--no-hardware
:    Hide hardware listing

--no-vs
:    Hide virtual server listing

## ibmcloud sl vlan edit
{: #sl_vlan_edit}

Edit the details about a VLAN

ibmcloud sl vlan edit IDENTIFIER [OPTIONS]

**Examples**:

   ibmcloud sl vlan edit 12345678 -n myvlan-rename
   This command updates vlan with ID 12345678 and gives it a new name "myvlan-rename".

```bash
ibmcloud sl vlan edit IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--n, name
:    The name of the VLAN

## ibmcloud sl vlan list
{: #sl_vlan_list}

List all the VLANs on your account

**Examples**:

   ibmcloud sl vlan list -d dal09 --sortby number
   This commands lists all vlans on current account filtering by datacenter equals to dal09, and sort them by vlan number.
 
Note: In field Pod, if add (*) indicated that closed soon

```bash
ibmcloud sl vlan list [flags]
```
{: codeblock}


**Command options**:

--d, datacenter
:    Filter by datacenter shortname

--name
:    Filter by VLAN name

--n, number
:    Filter by VLAN number

--order
:    Filter by ID of the order that purchased the VLAN

--sortby
:    Column to sort by. Options are: id,number,name,firewall,datacenter,hardware,virtual_servers,public_ips

## ibmcloud sl vlan options
{: #sl_vlan_options}

List all the options for creating VLAN



```bash
ibmcloud sl vlan options
```
{: codeblock}
