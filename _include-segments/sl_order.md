


## ibmcloud sl order cancelation
{: #sl_order_cancelation}

List cancelations.



```bash
ibmcloud sl order cancelation
```
{: codeblock}


## ibmcloud sl order category-list
{: #sl_order_category_list}

List the categories of a package

ibmcloud sl order category-list [OPTIONS] PACKAGE_KEYNAME

**Examples**:
 
   ibmcloud sl order category-list BARE_METAL_SERVER
   This command lists the categories of Bare Metal servers.

```bash
ibmcloud sl order category-list PACKAGE_KEYNAME [flags]
```
{: codeblock}


**Command options**:

--required
:    List only the required categories for the package

## ibmcloud sl order item-list
{: #sl_order_item_list}

List package items that are used for ordering



```bash
ibmcloud sl order item-list PACKAGE_KEYNAME [flags]
```
{: codeblock}


**Command options**:

--category
:    Category code that is used to filter items

--keyword
:    A word (or string) that is used to filter item names

## ibmcloud sl order lookup
{: #sl_order_lookup}

Provides some details related to order owner, date order, cost information, initial invoice.



```bash
ibmcloud sl order lookup IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--details
:    Shows a very detailed list of charges

## ibmcloud sl order package-list
{: #sl_order_package_list}

List packages that can be ordered with the placeOrder API



```bash
ibmcloud sl order package-list [flags]
```
{: codeblock}


**Command options**:

--keyword
:    A word (or string) that is used to filter package names

--package-type
:    The keyname for the type of package. For example, BARE_METAL_CPU

## ibmcloud sl order package-locations
{: #sl_order_package_locations}

List datacenters a package can be ordered in



```bash
ibmcloud sl order package-locations PACKAGE_KEYNAME
```
{: codeblock}


## ibmcloud sl order place
{: #sl_order_place}

Place or verify an order

**Examples**:
 
	ibmcloud sl order place CLOUD_SERVER DALLAS13 GUEST_CORES_4 RAM_16_GB REBOOT_REMOTE_CONSOLE 1_GBPS_PUBLIC_PRIVATE_NETWORK_UPLINKS BANDWIDTH_0_GB_2 1_IP_ADDRESS GUEST_DISK_100_GB_SAN OS_UBUNTU_16_04_LTS_XENIAL_XERUS_MINIMAL_64_BIT_FOR_VSI MONITORING_HOST_PING NOTIFICATION_EMAIL_AND_TICKET AUTOMATED_NOTIFICATION UNLIMITED_SSL_VPN_USERS_1_PPTP_VPN_USER_PER_ACCOUNT NESSUS_VULNERABILITY_ASSESSMENT_REPORTING --billing hourly --extras '{"virtualGuests": [{"hostname": "test", "domain": "softlayer.com"}]}' --complex-type SoftLayer_Container_Product_Order_Virtual_Guest
	This command orders an hourly VSI with 4 CPU, 16 GB RAM, 100 GB SAN disk, Ubuntu 16.04, and 1 Gbps public & private uplink in dal13

```bash
ibmcloud sl order place PACKAGE_KEYNAME LOCATION ORDER_ITEM1 ORDER_ITEM2 ORDER_ITEM3 ORDER_ITEM4... [flags]
```
{: codeblock}


**Command options**:

--billing
:    Billing rate [hourly|monthly], [default: hourly]

--complex-type
:    The complex type of the order. The type begins with 'SoftLayer_Container_Product_Order_'

--extras
:    JSON string that denotes extra data needs to be sent with the order

--f, force
:    Force operation without confirmation

--preset
:    The order preset (if required by the package)

--quantity
:    The quantity of the item being ordered. This value defaults to 1

--verify
:    Flag denoting whether to verify the order, or not place it

## ibmcloud sl order place-quote
{: #sl_order_place_quote}

Place a quote

**Examples**:
 
    ibmcloud sl order place-quote CLOUD_SERVER DALLAS13 GUEST_CORES_4 RAM_16_GB REBOOT_REMOTE_CONSOLE 1_GBPS_PUBLIC_PRIVATE_NETWORK_UPLINKS BANDWIDTH_0_GB_2 1_IP_ADDRESS GUEST_DISK_100_GB_SAN OS_UBUNTU_16_04_LTS_XENIAL_XERUS_MINIMAL_64_BIT_FOR_VSI MONITORING_HOST_PING NOTIFICATION_EMAIL_AND_TICKET AUTOMATED_NOTIFICATION UNLIMITED_SSL_VPN_USERS_1_PPTP_VPN_USER_PER_ACCOUNT NESSUS_VULNERABILITY_ASSESSMENT_REPORTING --extras '{"virtualGuests": [{"hostname": "test", "domain": "softlayer.com"}]}' --complex-type SoftLayer_Container_Product_Order_Virtual_Guest --name "foobar" --send-email
    This command places a quote for a VSI with 4 CPU, 16 GB RAM, 100 GB SAN disk, Ubuntu 16.04, and 1 Gbps public & private uplink in datacenter dal13

```bash
ibmcloud sl order place-quote PACKAGE_KEYNAME LOCATION ORDER_ITEM1 ORDER_ITEM2 ORDER_ITEM3 ORDER_ITEM4... [flags]
```
{: codeblock}


**Command options**:

--complex-type
:    The complex type of the order. The type begins with 'SoftLayer_Container_Product_Order_'

--extras
:    JSON string that denotes extra data needs to be sent with the order

--name
:    A custom name to be assigned to the quote (optional)

--preset
:    The order preset (if required by the package)

--send-email
:    The quote will be sent to the associated email address

## ibmcloud sl order preset-list
{: #sl_order_preset_list}

List package presets



```bash
ibmcloud sl order preset-list [flags]
```
{: codeblock}


**Command options**:

--keyword
:    A word (or string) used to filter presets

--prices
:    Lists the prices for each item in this preset

## ibmcloud sl order quote
{: #sl_order_quote}

View and Order a quote

ibmcloud sl order quote IDENTIFIER [OPTIONS]

**Examples**:
 
	ibmcloud sl order quote 123456 --fqdn testquote.test.com --verify --quantity 1 --postinstall https://mypostinstallscript.com --userdata Myuserdata
	ibmcloud sl order quote 123456 --fqdn testquote.test.com --key 111111 --image 222222 --complex-type SoftLayer_Container_Product_Order_Hardware_Server

```bash
ibmcloud sl order quote IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--complex-type
:    The complex type of the order. Starts with 'SoftLayer_Container_Product_Order'.  [default: SoftLayer_Container_Product_Order_Hardware_Server]

--fqdn
:    hostname.domain.name.tld formatted name to use. Specify one fqdn per server (multiple occurrence permitted)  [required]

--image
:    Image ID. See: 'ibmcloud sl image list' for reference

--key
:    SSH key Id's to add to the root user. See: 'ibmcloud sl security sshkey-list' for reference (multiple occurrence permitted)

--postinstall
:    Post-install script to download

--quantity
:    The quantity of the item being ordered if different from quoted value

--userdata
:    User defined metadata string

--userfile
:    Read userdata from file

--verify
:    If specified, will only show what the quote will order, will NOT place an order [default: False]

## ibmcloud sl order quote-delete
{: #sl_order_quote_delete}

Delete the quote of an order.



```bash
ibmcloud sl order quote-delete IDENTIFIER
```
{: codeblock}


## ibmcloud sl order quote-detail
{: #sl_order_quote_detail}

View a quote



```bash
ibmcloud sl order quote-detail IDENTIFIER
```
{: codeblock}


## ibmcloud sl order quote-list
{: #sl_order_quote_list}

List all active quotes on an account



```bash
ibmcloud sl order quote-list
```
{: codeblock}


## ibmcloud sl order quote-save
{: #sl_order_quote_save}

Save a quote



```bash
ibmcloud sl order quote-save IDENTIFIER
```
{: codeblock}
