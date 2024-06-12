


## ibmcloud sl tags cleanup
{: #sl_tags_cleanup}

Removes all empty tags.



```bash
ibmcloud sl tags cleanup [flags]
```
{: codeblock}


**Command options**:

--dry-run
:    Don't delete, just show what will be deleted.

## ibmcloud sl tags delete
{: #sl_tags_delete}

Removes an empty tag from your account.



```bash
ibmcloud sl tags delete [TAG NAME]
```
{: codeblock}


## ibmcloud sl tags detail
{: #sl_tags_detail}

Get information about the resources using the selected tag.



```bash
ibmcloud sl tags detail [TAG NAME]
```
{: codeblock}


## ibmcloud sl tags list
{: #sl_tags_list}

List all tags currently on your account



```bash
ibmcloud sl tags list [flags]
```
{: codeblock}


**Command options**:

--d, detail
:    List information about devices using the tag.

## ibmcloud sl tags set
{: #sl_tags_set}

Set Tags.

ibmcloud sl tags set [OPTIONS]

**Examples**:

	ibmcloud sl tags set --tags 'tag1,tag2' --key-name HARDWARE --resource-id 123456


```bash
ibmcloud sl tags set [flags]
```
{: codeblock}


**Command options**:

--key-name
:    Key name of a tag type e.g. GUEST, HARDWARE. See slcli tags taggable output.  [required]

--resource-id
:    ID of the object being tagged  [required]

--tags
:    Comma seperated list of tags, enclosed in quotes. 'tag1,tag2'  [required]
