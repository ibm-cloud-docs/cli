


## ibmcloud sl ticket attach
{: #sl_ticket_attach}

Attach devices to ticket

ibmcloud sl ticket attach TICKETID [OPTIONS]
  
**Examples**:

    ibmcloud sl ticket attach 7676767 --hardware 8675654 
    ibmcloud sl ticket attach 7676767 --virtual 1234567 

```bash
ibmcloud sl ticket attach [flags]
```
{: codeblock}


**Command options**:

--hardware
:    The identifier for hardware to attach

--virtual
:    The identifier for a virtual server to attach

## ibmcloud sl ticket create
{: #sl_ticket_create}

Create a support ticket

ibmcloud sl ticket create [OPTIONS]

**Examples**:
 	
    ibmcloud sl ticket create --title "Example title" --subject-id 1522 --body "This is an example ticket. Please disregard."
    ibmcloud sl ticket create --title "Example title" --subject-id 1522 --body "This is an example ticket. Please disregard." --attachment 8675654 --attachment-type hardware --rootpwd passw0rd
    ibmcloud sl ticket create --title "Example title" --subject-id 1522 --body "This is an example ticket. Please disregard." --attachment 1234567 --attachment-type virtual --rootpwd passw0rd
    ibmcloud sl ticket create --title "Example title" --subject-id 1522 --attachment 8675654 --rootpwd passw0rd
    ibmcloud sl ticket create --title "Example title" --subject-id 1522

```bash
ibmcloud sl ticket create [flags]
```
{: codeblock}


**Command options**:

--attachment
:    Initial object ID number to attach to ticket

--attachment-type
:    Specify the type of attachment, hardware or virtual. default is hardware

--body
:    The ticket body

--priority
:    Ticket priority [1|2|3|4], from 1 (Critical) to 4 (Minimal Impact). Only settable with Advanced and Premium support. See https://www.ibm.com/cloud/support

--rootpwd
:    Root password associated with attached device id

--subject-id
:    The subject id to use for the ticket, issue '${COMMAND_NAME} sl ticket subjects' to get the list. [required]

--title
:    The title of the ticket. [required]

## ibmcloud sl ticket detach
{: #sl_ticket_detach}

Detach devices from a ticket

ibmcloud sl ticket detach TICKETID [OPTIONS]
  
**Examples**:

    ibmcloud sl ticket detach 767676 --hardware 8675654
    ibmcloud sl ticket detach 767676 --virtual 1234567

```bash
ibmcloud sl ticket detach [flags]
```
{: codeblock}


**Command options**:

--hardware
:    The identifier for hardware to detach

--virtual
:    The identifier for a virtual server to detach

## ibmcloud sl ticket detail
{: #sl_ticket_detail}

Get details for a ticket

ibmcloud sl ticket detail TICKETID [OPTIONS]
  
**Examples**:

    ibmcloud sl ticket detail 767676
    ibmcloud sl ticket detail 767676 --count 10

```bash
ibmcloud sl ticket detail [flags]
```
{: codeblock}


**Command options**:

--count
:    Number of updates

## ibmcloud sl ticket list
{: #sl_ticket_list}

List tickets



```bash
ibmcloud sl ticket list [flags]
```
{: codeblock}


**Command options**:

--closed
:    Display only closed tickets

--open
:    Display only open tickets

## ibmcloud sl ticket subjects
{: #sl_ticket_subjects}

List Subject IDs for ticket creation



```bash
ibmcloud sl ticket subjects
```
{: codeblock}


## ibmcloud sl ticket summary
{: #sl_ticket_summary}

Summary info about tickets



```bash
ibmcloud sl ticket summary
```
{: codeblock}


## ibmcloud sl ticket update
{: #sl_ticket_update}

Adds an update to an existing ticket

ibmcloud sl ticket update TICKETID ["CONTENTS"] 
  
    If the second argument is not specified on a non-Windows machine, it will attempt to use either the value stored in the EDITOR environmental variable, or find either nano, vim, or emacs in that order.
  
**Examples**:

    ibmcloud sl ticket update 767676 "A problem has been detected."
    ibmcloud sl ticket update 767667

```bash
ibmcloud sl ticket update TICKETID
```
{: codeblock}


## ibmcloud sl ticket upload
{: #sl_ticket_upload}

Adds an attachment to an existing ticket

ibmcloud sl ticket upload TICKETID FILEPATH
  
**Examples**:

	ibmcloud sl ticket upload 767676 "/home/user/screenshot.png"

```bash
ibmcloud sl ticket upload TICKETID FILEPATH [flags]
```
{: codeblock}


**Command options**:

--name
:    The name of the attachment shown in the ticket
