


## ibmcloud sl firewall add
{: #sl_firewall_add}

Create a new firewall



```bash
ibmcloud sl firewall add IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--force
:    Force operation without confirmation

--high-availability
:    High available firewall option

--type
:    Firewall type  [required]. Options are: vlan,vs,hardware

## ibmcloud sl firewall cancel
{: #sl_firewall_cancel}

Cancels a firewall



```bash
ibmcloud sl firewall cancel IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--force
:    Force operation without confirmation

## ibmcloud sl firewall detail
{: #sl_firewall_detail}

Detail information about a firewall

**Examples**:
 
ibmcloud sl firewall detail vs:12345
ibmcloud sl firewall detail server:234567
ibmcloud sl firewall detail vlan:345678
ibmcloud sl firewall detail multiVlan:456789

```bash
ibmcloud sl firewall detail IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--credentials
:    Display FortiGate username and FortiGate password to multi vlans

## ibmcloud sl firewall edit
{: #sl_firewall_edit}

Edit firewall rules



```bash
ibmcloud sl firewall edit IDENTIFIER
```
{: codeblock}


## ibmcloud sl firewall list
{: #sl_firewall_list}

List all firewalls on your account



```bash
ibmcloud sl firewall list
```
{: codeblock}
