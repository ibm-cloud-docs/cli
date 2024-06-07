


## ibmcloud sl event-log get
{: #sl_event_log_get}

Get Event Logs

ibmcloud sl event-log get [OPTIONS]

**Examples**:
 
   ibmcloud sl event-log get 
   ibmcloud sl event-log get --limit 5 --obj-id 123456 --obj-event Create --metadata
   ibmcloud sl event-log get --date-min 2021-03-31 --date-max 2021-04-31

```bash
ibmcloud sl event-log get [flags]
```
{: codeblock}


**Command options**:

--D, date-max
:    The latest date we want to search for event logs [YYYY-MM-DD].

--d, date-min
:    The earliest date we want to search for event logs [YYYY-MM-DD].

--l, limit
:    Total number of result to return. -1 to return ALL, there may be a LOT of these.  [default: 50]

--metadata
:    Display metadata if present  [default: no-metadata]

--e, obj-event
:    The event we want to get event logs for

--i, obj-id
:    The id of the object we want to get event logs for

--t, obj-type
:    The type of the object we want to get event logs for

--z, utc-offset
:    UTC Offset for searching with dates. +/-HHMM format  [default: -0000]

## ibmcloud sl event-log types
{: #sl_event_log_types}

Get Event Log types



```bash
ibmcloud sl event-log types
```
{: codeblock}

