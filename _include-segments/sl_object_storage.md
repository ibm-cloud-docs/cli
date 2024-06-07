


## ibmcloud sl object-storage accounts
{: #sl_object_storage_accounts}

List Object Storage accounts.

ibmcloud sl object-storage accounts

```bash
ibmcloud sl object-storage accounts
```
{: codeblock}


## ibmcloud sl object-storage credential-create
{: #sl_object_storage_credential_create}

Create credentials for an IBM Cloud Object Storage Account.

ibmcloud sl object-storage credential-create IDENTIFIER [OPTIONS]

Examples:
	ibmcloud sl object-storage credential-create 123456

```bash
ibmcloud sl object-storage credential-create
```
{: codeblock}


## ibmcloud sl object-storage credential-delete
{: #sl_object_storage_credential_delete}

Delete the credential of an Object Storage Account.

ibmcloud sl object-storage credential-delete IDENTIFIER [OPTIONS]

Examples:
	ibmcloud sl object-storage credential-delete 123456 --credential-id 654321

```bash
ibmcloud sl object-storage credential-delete [flags]
```
{: codeblock}


**Command options**:

--credential-id
:    This is the credential id associated with the volume. [Required]

## ibmcloud sl object-storage credential-limit
{: #sl_object_storage_credential_limit}

Credential limits for this IBM Cloud Object Storage account.

ibmcloud sl object-storage credential-limit IDENTIFIER [OPTIONS]

Examples:
	ibmcloud sl object-storage credential-limit 123456

```bash
ibmcloud sl object-storage credential-limit
```
{: codeblock}


## ibmcloud sl object-storage credential-list
{: #sl_object_storage_credential_list}

Retrieve credentials used for generating an AWS signature. Max of 2.

ibmcloud sl object-storage credential-list IDENTIFIER [OPTIONS]

```bash
ibmcloud sl object-storage credential-list
```
{: codeblock}


## ibmcloud sl object-storage delete
{: #sl_object_storage_delete}

Cancel an existing object storage instance.

ibmcloud sl object-storage delete VOLUME_ID [OPTIONS]

**Examples**:

   ibmcloud sl object-storage delete 12345678 --immediate -f 
   This command cancels volume with ID 12345678 immediately and without asking for confirmation.

```bash
ibmcloud sl object-storage delete IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--immediate
:    Cancel immediately instead of on the billing anniversary

--reason
:    An optional reason for cancellation

## ibmcloud sl object-storage endpoints
{: #sl_object_storage_endpoints}

List object storage endpoints.

ibmcloud sl object-storage endpoints IDENTIFIER

```bash
ibmcloud sl object-storage endpoints
```
{: codeblock}

