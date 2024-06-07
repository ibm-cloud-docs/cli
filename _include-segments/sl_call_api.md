


## ibmcloud sl call-api
{: #sl__call_api}

Call arbitrary API endpoints

ibmcloud sl call-api SERVICE METHOD [OPTIONS]

**Examples**:
 
	ibmcloud sl call-api SoftLayer_Network_Storage editObject --init 57328245 --parameters '[{"notes":"Testing."}]'
	This command edit a volume notes.

	ibmcloud sl call-api SoftLayer_User_Customer getObject --init 7051629 --mask "id,firstName,lastName"
	This command show a user detail.

	ibmcloud sl call-api SoftLayer_Account getVirtualGuests --filter '{"virtualGuests":{"hostname":{"operation":"cli-test"}}}'
	This command list virtual guests.

```bash
ibmcloud sl call-api [flags]
```
{: codeblock}


**Command options**:

--filter
:    Object filters

--init
:    Init parameter

--limit
:    Result limit

--mask
:    Object mask: use to limit fields returned

--offset
:    Result offset

--parameters
:    Append parameters to web call
