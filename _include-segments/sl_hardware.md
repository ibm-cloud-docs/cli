


## ibmcloud sl hardware authorize-storage
{: #sl_hardware_authorize_storage}

Authorize File and Block Storage to a Hardware Server



```bash
ibmcloud sl hardware authorize-storage IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--u, username-storage
:    The storage username to be added to the hardware server.

## ibmcloud sl hardware bandwidth
{: #sl_hardware_bandwidth}

Bandwidth data over date range.

ibmcloud sl hardware bandwidth IDENTIFIER [OPTIONS]
Time formats that are either '2006-01-02', '2006-01-02T15:04' or '2006-01-02T15:04-07:00'

Due to some rounding and date alignment details, results here might be slightly different than results in the control portal.
Bandwidth is listed in GB, if no time zone is specified, GMT+0 is assumed.

**Examples**:


   ibmcloud sl hardware bandwidth 1234 -s 2006-01-02T15:04 -e 2006-01-02T15:04-07:00

```bash
ibmcloud sl hardware bandwidth IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--e, end
:    End date for bandwidth reporting

--q, quite
:    Only show the summary table.

--r, rollup
:    Number of seconds to report as one data point. 300, 600, 1800, 3600 (default), 43200 or 86400 seconds

--s, start
:    Start date for bandwdith reporting

## ibmcloud sl hardware billing
{: #sl_hardware_billing}

Get billing for a hardware device.



```bash
ibmcloud sl hardware billing IDENTIFIER
```
{: codeblock}


## ibmcloud sl hardware cancel
{: #sl_hardware_cancel}

Cancel a hardware server



```bash
ibmcloud sl hardware cancel IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--c, comment
:    An optional comment to add to the cancellation ticket

--f, force
:    Force operation without confirmation

--i, immediate
:    Cancels the server immediately (instead of on the billing anniversary)

--r, reason
:    An optional cancellation reason. See '${COMMAND_NAME} sl hardware cancel-reasons' for a list of available options

## ibmcloud sl hardware cancel-reasons
{: #sl_hardware_cancel_reasons}

Display a list of cancellation reasons



```bash
ibmcloud sl hardware cancel-reasons
```
{: codeblock}


## ibmcloud sl hardware create
{: #sl_hardware_create}

Order/create a hardware server



```bash
ibmcloud sl hardware create [flags]
```
{: codeblock}


**Command options**:

--b, billing
:    Billing rate, either hourly or monthly, default is hourly if not specified

--d, datacenter
:    Datacenter shortname[required]

--D, domain
:    Domain portion of the FQDN[required]

--x, export
:    Exports options to a template file

--e, extra
:    Extra options, multiple occurrence allowed

--f, force
:    Force operation without confirmation

--H, hostname
:    Host portion of the FQDN[required]

--k, key
:    SSH keys to add to the root user, multiple occurrence allowed

--n, no-public
:    Private network only

--o, os
:    OS install code[required]

--p, port-speed
:    Port speed[required]

--i, post-install
:    Post-install script to download

--s, size
:    Hardware size[required]

--m, template
:    A template file that defaults the command-line options

--t, test
:    Do not actually create the virtual server

## ibmcloud sl hardware create-credential
{: #sl_hardware_create_credential}

Create a password for a software component.



```bash
ibmcloud sl hardware create-credential IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--n, notes
:    A note string stored for this username/password pair.

--P, password
:    The password part of the username/password pair.

--software
:    The name of this specific piece of software.

--U, username
:    The username part of the username/password pair.

## ibmcloud sl hardware create-options
{: #sl_hardware_create_options}

Server order options for a given chassis



```bash
ibmcloud sl hardware create-options
```
{: codeblock}


## ibmcloud sl hardware credentials
{: #sl_hardware_credentials}

List hardware server credentials



```bash
ibmcloud sl hardware credentials IDENTIFIER
```
{: codeblock}


## ibmcloud sl hardware detail
{: #sl_hardware_detail}

Get details for a hardware server



```bash
ibmcloud sl hardware detail IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--components
:    Show associated hardware components

--p, passwords
:    Show passwords (check over your shoulder!)

--c, price
:    Show associated prices

## ibmcloud sl hardware edit
{: #sl_hardware_edit}

Edit hardware server details



```bash
ibmcloud sl hardware edit IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--D, domain
:    Domain portion of the FQDN

--H, hostname
:    Host portion of the FQDN

--v, private-speed
:    Private port speed, options are: 0,10,100,1000,10000

--p, public-speed
:    Public port speed, options are: 0,10,100,1000,10000

--g, tag
:    Tags to set or empty string to remove all (multiple occurrence permitted).

--u, userdata
:    User defined metadata string

--F, userfile
:    Read userdata from file

## ibmcloud sl hardware list
{: #sl_hardware_list}

List hardware servers



```bash
ibmcloud sl hardware list [flags]
```
{: codeblock}


**Command options**:

--column
:    Column to display,  options are: id,hostname,domain,public_ip,private_ip,datacenter,status,guid,cpu,memory,os,ipmi_ip,created,created_by,tags. This option can be specified multiple times

--c, cpu
:    Filter by number of CPU cores

--d, datacenter
:    Filter by datacenter

--D, domain
:    Filter by domain

--H, hostname
:    Filter by hostname

--m, memory
:    Filter by memory in gigabytes

--n, network
:    Filter by network port speed in Mbps

--o, order
:    Filter by ID of the order which purchased hardware server

--owner
:    Filter by ID of the owner

--v, private-ip
:    Filter by private IP address

--p, public-ip
:    Filter by public IP address

--sortby
:    Column to sort by, default:hostname, option:id,guid,hostname,domain,public_ip,private_ip,cpu,memory,os,datacenter,status,ipmi_ip,created,created_by

--g, tag
:    Filter by tags, multiple occurrence allowed

## ibmcloud sl hardware monitoring-list
{: #sl_hardware_monitoring_list}

Get details for a hardware monitors device.



```bash
ibmcloud sl hardware monitoring-list IDENTIFIER
```
{: codeblock}


## ibmcloud sl hardware notifications
{: #sl_hardware_notifications}

Shows who gets notified when the server has a monitoring issues.



```bash
ibmcloud sl hardware notifications IDENTIFIER
```
{: codeblock}


## ibmcloud sl hardware notifications-add
{: #sl_hardware_notifications_add}

Create a user hardware notification entry.



```bash
ibmcloud sl hardware notifications-add IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--users
:    User ID to be notified on monitoring failure, multiple occurrence allowed

## ibmcloud sl hardware notifications-delete
{: #sl_hardware_notifications_delete}

Remove a user hardware notification entry.



```bash
ibmcloud sl hardware notifications-delete IDENTIFIER
```
{: codeblock}


## ibmcloud sl hardware power-cycle
{: #sl_hardware_power_cycle}

Power cycle a server



```bash
ibmcloud sl hardware power-cycle IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

## ibmcloud sl hardware power-off
{: #sl_hardware_power_off}

Power off an active server



```bash
ibmcloud sl hardware power-off IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

## ibmcloud sl hardware power-on
{: #sl_hardware_power_on}

Power on a server



```bash
ibmcloud sl hardware power-on IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

## ibmcloud sl hardware reboot
{: #sl_hardware_reboot}

Reboot an active server



```bash
ibmcloud sl hardware reboot IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--hard
:    Perform a hard reboot

--soft
:    Perform a soft reboot

## ibmcloud sl hardware reflash-firmware
{: #sl_hardware_reflash_firmware}

Reflash server firmware.



```bash
ibmcloud sl hardware reflash-firmware IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

## ibmcloud sl hardware reload
{: #sl_hardware_reload}

Reload operating system on a server



```bash
ibmcloud sl hardware reload IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--k, key
:    IDs of SSH key to add to the root user, multiple occurrence allowed

--i, postinstall
:    Post-install script to download, only HTTPS executes, HTTP leaves file in /root

--b, upgrade-bios
:    Upgrade BIOS

--w, upgrade-firmware
:    Upgrade all hard drives' firmware

## ibmcloud sl hardware rescue
{: #sl_hardware_rescue}

Reboot server into a rescue image



```bash
ibmcloud sl hardware rescue IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

## ibmcloud sl hardware sensor
{: #sl_hardware_sensor}

Retrieve a server’s hardware state via its internal sensors.



```bash
ibmcloud sl hardware sensor IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--discrete
:    Show discrete units associated hardware sensor

## ibmcloud sl hardware storage
{: #sl_hardware_storage}

Get storage details for a hardware server.



```bash
ibmcloud sl hardware storage IDENTIFIER
```
{: codeblock}


## ibmcloud sl hardware toggle-ipmi
{: #sl_hardware_toggle_ipmi}

Toggle the IPMI interface on and off. This command is asynchronous.



```bash
ibmcloud sl hardware toggle-ipmi IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--disable
:    Disable the IPMI interface.

--enable
:    Enable the IPMI interface.

--q, quiet
:    Suppress verbose output

## ibmcloud sl hardware update-firmware
{: #sl_hardware_update_firmware}

Update server firmware



```bash
ibmcloud sl hardware update-firmware IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

## ibmcloud sl hardware vlan-add
{: #sl_hardware_vlan_add}

Trunks a VLAN to the this server.

IDENTIFIER is the id of the server
VLANS is the ID of the VLANs. Multiple vlans can be added at the same time.

```bash
ibmcloud sl hardware vlan-add IDENTIFIER VLAN...
```
{: codeblock}


## ibmcloud sl hardware vlan-remove
{: #sl_hardware_vlan_remove}

Remove VLANs trunked to this server.

IDENTIFIER is the id of the server
VLANS is the ID of the VLANs. Multiple vlans can be added at the same time.

```bash
ibmcloud sl hardware vlan-remove IDENTIFIER VLAN...
```
{: codeblock}


## ibmcloud sl hardware vlan-trunkable
{: #sl_hardware_vlan_trunkable}

Lists VLANs this server can be given access to.

This command will only show VLANs not yet trunked to this server.

```bash
ibmcloud sl hardware vlan-trunkable IDENTIFIER
```
{: codeblock}

