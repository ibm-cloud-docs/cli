


## ibmcloud sl subnet cancel
{: #sl_subnet_cancel}

Cancel a subnet

ibmcloud sl subnet cancel IDENTIFIER [OPTIONS]

**Examples**:

   ibmcloud sl subnet cancel 12345678 -f
   This command cancels subnet with ID 12345678 without asking for confirmation.

```bash
ibmcloud sl subnet cancel IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

## ibmcloud sl subnet clear-route
{: #sl_subnet_clear_route}

Removes the routing for a specified subnet, turning it into an unrouted portable subnet.



```bash
ibmcloud sl subnet clear-route IDENTIFIER
```
{: codeblock}


## ibmcloud sl subnet create
{: #sl_subnet_create}

Add a new subnet to your account

Valid quantities vary by type.
	- public IPv4: 4, 8, 16, 32
	- private IPv4: 4, 8, 16, 32, 64
	- public IPv6: 64

**Examples**:

	ibmcloud sl subnet create public 16 567
	This command creates a public subnet with 16 IPv4 addresses and places it on vlan with ID 567.

```bash
ibmcloud sl subnet create NETWORK QUANTITY VLAN [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--6, ipv6
:    Order IPv6 Addresses

--test
:    Do not order the subnet; just get a quote

## ibmcloud sl subnet detail
{: #sl_subnet_detail}

Get details of a subnet

ibmcloud sl subnet detail IDENTIFIER [OPTIONS]

**Examples**:

   ibmcloud sl subnet detail 12345678 
   This command shows detailed information about subnet with ID 12345678, including virtual servers and hardware servers information.

```bash
ibmcloud sl subnet detail IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--no-Tag
:    Hide Tag listing

--no-hardware
:    Hide hardware listing

--no-ip
:    Hide IP address listing

--no-vs
:    Hide virtual server listing

## ibmcloud sl subnet edit
{: #sl_subnet_edit}

Edit note and tags of a subnet.

ibmcloud sl subnet edit IDENTIFIER [OPTIONS]

**Examples**:

   ibmcloud sl subnet edit 12345678 --note myNote
   ibmcloud sl subnet edit 12345678 --tags tag1

```bash
ibmcloud sl subnet edit IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--note
:    The note

--tags
:    Comma separated list of tags, enclosed in quotes. 'tag1, tag2'

## ibmcloud sl subnet edit-ip
{: #sl_subnet_edit_ip}

Set the note of the ipAddress.

ibmcloud sl subnet edit-ip IDENTIFIER [OPTIONS]

**Examples**:

   ibmcloud sl subnet edit-ip 11.22.33.44 --note myNote
   ibmcloud sl subnet edit-ip 12345678 --note myNote

```bash
ibmcloud sl subnet edit-ip IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--note
:    The note

## ibmcloud sl subnet list
{: #sl_subnet_list}

List all subnets on your account

ibmcloud sl subnet list [OPTIONS]

**Examples**:

   ibmcloud sl subnet list -d dal09 -t PRIMARY --network-space PUBLIC --v4
   This command lists IPv4 subnets on the current account, and filters by datacenter is dal09, subnet type is PRIMARY, and network space is PUBLIC.

```bash
ibmcloud sl subnet list [flags]
```
{: codeblock}


**Command options**:

--d, datacenter
:    Filter by datacenter shortname

--identifier
:    Filter by network identifier

--4, ipv4
:    Display IPv4 subnets only

--6, ipv6
:    Display IPv6 subnets only

--network-space
:    Filter by network space

--order
:    Filter by the ID of order that purchased the subnets

--sortby
:    Column to sort by. Options are: id,identifier,type,network_space,datacenter,vlan_id,IPs,hardware,vs

--t, subnet-type
:    Filter by subnet type

## ibmcloud sl subnet lookup
{: #sl_subnet_lookup}

Find an IP address and display its subnet and device information

ibmcloud sl subnet lookup IP_ADDRESS [OPTIONS]

**Examples**:

   ibmcloud sl subnet lookup 9.125.235.255
   This command finds the IP address record with IP address 9.125.235.255 and displays its subnet and device information.

```bash
ibmcloud sl subnet lookup IDENTIFIER
```
{: codeblock}


## ibmcloud sl subnet route
{: #sl_subnet_route}

Change how a secondary subnet is routed.

Allows you to change the route of your secondary subnets.
Subnets may be routed as either Static or Portable, and that designation is dictated by the routing destination specified.
Static subnets have an ultimate routing destination of a single IP address but may not be routed to an existing subnet’s IP address whose subnet is routed as a Static.
Portable subnets have an ultimate routing destination of a VLAN.
A subnet can be routed to any resource within the same 'routing region' as the subnet itself, usually limited to a single data center.

See Also: https://sldn.softlayer.com/reference/services/SoftLayer_Network_Subnet/route/

**Examples**:

	ibmcloud sl subnet route 1234567 --ip 11.22.33.44
	ibmcloud sl subnet route 1234567 --server myUniqueHostnamedomain.com
	ibmcloud sl subnet route 1234567 --vsi vsiId
	ibmcloud sl subnet route 1234567 --vlan vlanId



```bash
ibmcloud sl subnet route IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--i, ip
:    A Network_Subnet_IpAddress.id, A dotted-quad IPv4 address, or A full or compressed IPv6 address.

--s, server
:    A Hardware_Server.id or UUID value of the desired server. A value corresponding to a unique
fully-qualified domain name in the format 'hostnamedomain' where  and  are literal, e.g. myhostmydomain.com

--l, vlan
:    A Network_Vlan.id value of the desired VLAN or A semantic VLAN identifier of the form data center short name.router.vlan number,
eg. dal13.fcr01.1234 - the router name may optionally contain the 'a' or 'b' redundancy qualifier 

--v, vsi
:    A Virtual_Guest.id or UUID value of the desired server. A value corresponding to a unique
fully-qualified domain name in the format 'hostnamedomain' where  and  are literal, e.g. myhostmydomain.com
