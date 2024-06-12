


## ibmcloud sl dns import
{: #sl_dns_import}

Import a zone based off a BIND zone file

ibmcloud sl dns import ZONEFILE [OPTIONS]

**Examples**:

   ibmcloud sl dns import ~/ibm.com.txt
   This command imports zone and its resource records from file: ~/ibm.com.txt.

```bash
ibmcloud sl dns import ZONEFILE [flags]
```
{: codeblock}


**Command options**:

--dry-run
:    Don't actually create records

## ibmcloud sl dns record-add
{: #sl_dns_record_add}

Add resource record in a zone

ibmcloud sl dns record-add ZONE RECORD TYPE DATA [OPTIONS]

**Examples**:

   ibmcloud sl dns record-add ibm.com ftp A 127.0.0.1 --ttl 86400
   This command adds an A record to zone: ibm.com, its host is "ftp", data is "127.0.0.1" and ttl is 86400 seconds.

```bash
ibmcloud sl dns record-add ZONE RECORD TYPE DATA [flags]
```
{: codeblock}


**Command options**:

--ttl
:    TTL(Time-To-Live) in seconds, such as: 86400. The default is: 7200

## ibmcloud sl dns record-edit
{: #sl_dns_record_edit}

Update resource records in a zone

ibmcloud sl dns record-edit ZONE [OPTIONS]

**Examples**:

   ibmcloud sl dns record-edit ibm.com --by-id 12345678 --data 127.0.0.2 --ttl 3600
   This command edits records under the zone: ibm.com, whose ID is 12345678, and sets its data to "127.0.0.2" and ttl to 3600.
   ibmcloud sl dns record-edit ibm.com --by-record kibana --ttl 3600
   This command edits records under the zone: ibm.com, whose host is "kibana", and sets their ttl all to 3600.

```bash
ibmcloud sl dns record-edit ZONE [flags]
```
{: codeblock}


**Command options**:

--by-id
:    Edit a single record by its ID

--by-record
:    Edit by host record, such as www

--data
:    Record data, such as an IP address

--ttl
:    TTL(Time-To-Live) in seconds, such as: 86400. The default is: 7200

## ibmcloud sl dns record-list
{: #sl_dns_record_list}

List all the resource records in a zone

ibmcloud sl dns record-list ZONE [OPTIONS]

**Examples**:

   ibmcloud sl dns record-list ibm.com --record elasticsearch --type A --ttl 900
   This command lists all A records under the zone: ibm.com, and filters by host is elasticsearch and ttl is 900 seconds.

```bash
ibmcloud sl dns record-list ZONE [flags]
```
{: codeblock}


**Command options**:

--data
:    Filter by record data, such as an IP address

--record
:    Filter by host record, such as www

--ttl
:    Filter by TTL(Time-To-Live) in seconds, such as 86400

--type
:    Filter by record type, such as A or CNAME

## ibmcloud sl dns record-remove
{: #sl_dns_record_remove}

Remove resource record from a zone

ibmcloud sl dns record-remove RECORD_ID


**Examples**:

   ibmcloud sl dns record-remove 12345678
   This command removes resource record with ID 12345678.

```bash
ibmcloud sl dns record-remove RECORD_ID
```
{: codeblock}


## ibmcloud sl dns zone-create
{: #sl_dns_zone_create}

Create a zone

ibmcloud sl dns zone-create ZONE [OPTIONS]

**Examples**:

   ibmcloud sl dns zone-create ibm.com 
   This command creates a zone that is named ibm.com.

```bash
ibmcloud sl dns zone-create ZONE
```
{: codeblock}


## ibmcloud sl dns zone-delete
{: #sl_dns_zone_delete}

Delete a zone

ibmcloud sl dns zone-delete ZONE

**Examples**:

   ibmcloud sl dns zone-delete ibm.com 
   This command deletes a zone that is named ibm.com.

```bash
ibmcloud sl dns zone-delete ZONE
```
{: codeblock}


## ibmcloud sl dns zone-list
{: #sl_dns_zone_list}

List all zones on your account

ibmcloud sl dns zone-list [OPTIONS]

**Examples**:

   ibmcloud sl dns zone-list
   This command lists all zones under current account.

```bash
ibmcloud sl dns zone-list
```
{: codeblock}


## ibmcloud sl dns zone-print
{: #sl_dns_zone_print}

Print zone and resource records in BIND format

ibmcloud sl dns zone-print ZONE

**Examples**:

   ibmcloud sl dns zone-print ibm.com
   This command prints zone that is named ibm.com, and in BIND format.

```bash
ibmcloud sl dns zone-print ZONE
```
{: codeblock}

