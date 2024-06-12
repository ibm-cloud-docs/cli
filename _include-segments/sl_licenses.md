


## ibmcloud sl licenses cancel
{: #sl_licenses_cancel}

Cancel a license.



```bash
ibmcloud sl licenses cancel IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--immediate
:    Immediate cancellation.

## ibmcloud sl licenses create
{: #sl_licenses_create}

Order/Create License.



```bash
ibmcloud sl licenses create [flags]
```
{: codeblock}


**Command options**:

--datacenter
:    Datacenter shortname  [required]

--key
:    The VMware License Key. To get the required package you can use the command sl licenses create-options Package. E.g VMWARE_VSAN_ENTERPRISE_TIER_III_65_124_TB_6_X_2  [required]

## ibmcloud sl licenses create-options
{: #sl_licenses_create_options}

Server order options for a given chassis.



```bash
ibmcloud sl licenses create-options
```
{: codeblock}

