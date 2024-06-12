


## ibmcloud sl account billing-items
{: #sl_account_billing_items}

Lists billing items with some other useful information.



```bash
ibmcloud sl account billing-items [flags]
```
{: codeblock}


**Command options**:

--category
:    Category name.

--create
:    The date the billing item was created (YYYY-MM-DD).

--ordered
:    Name that ordered the item.

## ibmcloud sl account cancel-item
{: #sl_account_cancel_item}

Cancels a billing item.

Cancel the resource or service for a billing Item. By default the billing item will be canceled
on the next bill date and reclaim of the resource will begin shortly after the cancellation

```bash
ibmcloud sl account cancel-item IDENTIFIER
```
{: codeblock}


## ibmcloud sl account event-detail
{: #sl_account_event_detail}

Details of a specific event, and ability to acknowledge event.



```bash
ibmcloud sl account event-detail IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--ack
:    Acknowledge Event. Doing so will turn off the popup in the control portal.

## ibmcloud sl account events
{: #sl_account_events}

Summary and acknowledgement of upcoming and ongoing maintenance events.



```bash
ibmcloud sl account events [flags]
```
{: codeblock}


**Command options**:

--ack-all
:    Acknowledge every upcoming event. Doing so will turn off the popup in the control portal.

--announcement
:    Show only announcement events.

--d, date-min
:    Earliest date to retrieve events for [YYYY-MM-DD]. Default: 2 days ago.

--planned
:    Show only planned events.

--unplanned
:    Show only unplanned events.

## ibmcloud sl account hook-create
{: #sl_account_hook_create}

Order/create a provisioning script.



```bash
ibmcloud sl account hook-create [flags]
```
{: codeblock}


**Command options**:

--N, name
:    The name of the hook. [required]

--U, uri
:    The endpoint that the script will be downloaded. [required]

## ibmcloud sl account hook-delete
{: #sl_account_hook_delete}

Delete a provisioning scriptt.



```bash
ibmcloud sl account hook-delete IDENTIFIER
```
{: codeblock}


## ibmcloud sl account hooks
{: #sl_account_hooks}

Show all Provisioning Scripts.



```bash
ibmcloud sl account hooks
```
{: codeblock}


## ibmcloud sl account invoice-detail
{: #sl_account_invoice_detail}

Invoice details.



```bash
ibmcloud sl account invoice-detail IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--details
:    Shows a very detailed list of charges.

## ibmcloud sl account invoices
{: #sl_account_invoices}

List invoices.



```bash
ibmcloud sl account invoices [flags]
```
{: codeblock}


**Command options**:

--all
:    Return ALL invoices. There may be a lot of these.

--closed
:    Include invoices with a CLOSED status.

--limit
:    How many invoices to get back.

## ibmcloud sl account item-detail
{: #sl_account_item_detail}

Gets detailed information about a billing item.



```bash
ibmcloud sl account item-detail IDENTIFIER
```
{: codeblock}


## ibmcloud sl account licenses
{: #sl_account_licenses}

Show all licenses.



```bash
ibmcloud sl account licenses
```
{: codeblock}


## ibmcloud sl account orders
{: #sl_account_orders}

Lists account orders.

Lists account orders. Use `ibmcloud sl order lookup ID` to find more details about a specific order.

```bash
ibmcloud sl account orders [flags]
```
{: codeblock}


**Command options**:

--limit
:    How many results to get in one api call.

--upgrades
:    Show upgrades orders.

## ibmcloud sl account summary
{: #sl_account_summary}

Prints some various bits of information about an account.



```bash
ibmcloud sl account summary
```
{: codeblock}

