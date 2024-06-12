


## ibmcloud sl globalip assign
{: #sl_globalip_assign}

Assign a global IP to a target router or device

ibmcloud sl globalip assign IDENTIFIER TARGET [OPTIONS]

**Examples**:

    ibmcloud sl globalip assign 12345678 9.111.123.456
	This command assigns IP address with ID 12345678 to a target device whose IP address is 9.111.123.456.

```bash
ibmcloud sl globalip assign IDENTIFIER TARGET
```
{: codeblock}


## ibmcloud sl globalip cancel
{: #sl_globalip_cancel}

Cancel a global IP



```bash
ibmcloud sl globalip cancel IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

## ibmcloud sl globalip create
{: #sl_globalip_create}

Create a global IP

ibmcloud sl globalip create [OPTIONS]

**Examples**:

    ibmcloud sl globalip create --v6 
	This command creates an IPv6 address.

```bash
ibmcloud sl globalip create [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--test
:    Test order

--v6
:    Order an IPv6 IP address

## ibmcloud sl globalip list
{: #sl_globalip_list}

List all global IPs on your account



```bash
ibmcloud sl globalip list [flags]
```
{: codeblock}


**Command options**:

--order
:    Filter by the ID of order that purchased this IP address

--v4
:    Display IPv4 IPs only

--v6
:    Display IPv6 IPs only

## ibmcloud sl globalip unassign
{: #sl_globalip_unassign}

Unassign a global IP from a target router or device



```bash
ibmcloud sl globalip unassign IDENTIFIER
```
{: codeblock}

