


## ibmcloud sl ipsec cancel
{: #sl_ipsec_cancel}

Cancel a IPSec VPN tunnel context



```bash
ibmcloud sl ipsec cancel CONTEXT_ID [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--immediate
:    Cancel the IPSec immediately instead of on the billing anniversary

--reason
:    An optional reason for cancellation

## ibmcloud sl ipsec config
{: #sl_ipsec_config}

Request configuration of a tunnel context

ibmcloud sl ipsec config CONTEXT_ID [OPTIONS]

    Request configuration of a tunnel context.

    This action will update the advancedConfigurationFlag on the context
    instance and further modifications against the context will be prevented
    until all changes can be propagated to network devices.

```bash
ibmcloud sl ipsec config CONTEXT_ID
```
{: codeblock}


## ibmcloud sl ipsec detail
{: #sl_ipsec_detail}

List IPSec VPN tunnel context details

ibmcloud sl ipsec detail CONTEXT_ID [OPTIONS]

    List IPSEC VPN tunnel context details.

    Additional resources can be joined using multiple instances of the include
    option, for which the following choices are available.

    at: address translations
    is: internal subnets
    rs: remote subnets
    sr: statically routed subnets
    ss: service subnets

```bash
ibmcloud sl ipsec detail CONTEXT_ID [flags]
```
{: codeblock}


**Command options**:

--i, include
:    Include extra resources. Options are: at,is,rs,sr,ss

## ibmcloud sl ipsec list
{: #sl_ipsec_list}

List IPSec VPN tunnel contexts



```bash
ibmcloud sl ipsec list [flags]
```
{: codeblock}


**Command options**:

--order
:    Filter by ID of the order that purchased the IPSec

## ibmcloud sl ipsec order
{: #sl_ipsec_order}

Order a IPSec VPN tunnel



```bash
ibmcloud sl ipsec order [flags]
```
{: codeblock}


**Command options**:

--d, datacenter
:    Short name of the datacenter for the IPSec. For example, dal09[required]

## ibmcloud sl ipsec subnet-add
{: #sl_ipsec_subnet_add}

Add a subnet to an IPSec tunnel context

ibmcloud sl ipsec subnet-add CONTEXT_ID [OPTIONS] 

    Add a subnet to an IPSEC tunnel context.

    A subnet id may be specified to link to the existing tunnel context.

    Otherwise, a network identifier in CIDR notation should be specified,
    indicating that a subnet resource should first be created before
    associating it with the tunnel context. Note that this is only supported
    for remote subnets, which are also deleted upon failure to attach to a
    context.

    A separate configuration request should be made to realize changes on
    network devices.

```bash
ibmcloud sl ipsec subnet-add CONTEXT_ID [flags]
```
{: codeblock}


**Command options**:

--n, network
:    Subnet network identifier to create

--s, subnet-id
:    Subnet identifier to add, required

--t, subnet-type
:    Subnet type to add. Options are: internal,remote,service[required]

## ibmcloud sl ipsec subnet-remove
{: #sl_ipsec_subnet_remove}

Remove a subnet from an IPSEC tunnel context

ibmcloud sl ipsec subnet-remove CONTEXT_ID SUBNET_ID SUBNET_TYPE 

    Remove a subnet from an IPSEC tunnel context.

    The subnet id to remove must be specified.

    Remote subnets are deleted upon removal from a tunnel context.

    A separate configuration request should be made to realize changes on
    network devices.

```bash
ibmcloud sl ipsec subnet-remove CONTEXT_ID SUBNET_ID SUBNET_TYPE
```
{: codeblock}


## ibmcloud sl ipsec translation-add
{: #sl_ipsec_translation_add}

Add an address translation to an IPSec tunnel

ibmcloud sl ipsec translation-add CONTEXT_ID [OPTIONS]

    Add an address translation to an IPSEC tunnel context.

    A separate configuration request should be made to realize changes on
    network devices.

```bash
ibmcloud sl ipsec translation-add CONTEXT_ID [flags]
```
{: codeblock}


**Command options**:

--n, note
:    Note value

--r, remote-ip
:    Remote IP address[required]

--s, static-ip
:    Static IP address[required]

## ibmcloud sl ipsec translation-remove
{: #sl_ipsec_translation_remove}

Remove a translation entry from an IPSec

ibmcloud sl ipsec translation-remove CONTEXT_ID TRANSLATION_ID 

    Remove a translation entry from an IPSEC tunnel context.

    A separate configuration request should be made to realize changes on
    network devices.

```bash
ibmcloud sl ipsec translation-remove CONTEXT_ID TRANSLATION_ID
```
{: codeblock}


## ibmcloud sl ipsec translation-update
{: #sl_ipsec_translation_update}

Update an address translation for an IPSec

ibmcloud sl ipsec translation-update CONTEXT_ID TRANSLATION_ID [OPTIONS]

    Update an address translation for an IPSEC tunnel context.

    A separate configuration request should be made to realize changes on
    network devices.

```bash
ibmcloud sl ipsec translation-update CONTEXT_ID TRANSLATION_ID [flags]
```
{: codeblock}


**Command options**:

--n, note
:    Note

--r, remote-ip
:    Remote IP address[required]

--s, static-ip
:    Static IP address[required]

## ibmcloud sl ipsec update
{: #sl_ipsec_update}

Update tunnel context properties

ibmcloud sl ipsec update CONTEXT_ID [OPTIONS]

    Update tunnel context properties.

    Updates are made atomically, so either all are accepted or none are.

    Key life values must be in the range 120-172800.

    Phase 2 perfect forward secrecy must be in the range 0-1.

    A separate configuration request should be made to realize changes on
    network devices.

```bash
ibmcloud sl ipsec update CONTEXT_ID [flags]
```
{: codeblock}


**Command options**:

--n, name
:    Friendly name

--a, phase1-auth
:    Phase 1 authentication. Options are: MD5,SHA1,SHA256

--c, phase1-crypto
:    Phase 1 encryption. Options are: DES,3DES,AES128,AES192,AES256

--d, phase1-dh
:    Phase 1 Diffie-Hellman group. Options are: 0,1,2,5

--t, phase1-key-ttl
:    Phase 1 key life. Range is 120-172800

--u, phase2-auth
:    Phase 2 authentication. Options are: MD5,SHA1,SHA256

--y, phase2-crypto
:    Phase 2 encryption. Options are: DES,3DES,AES128,AES192,AES256

--e, phase2-dh
:    Phase 2 Diffie-Hellman group. Options are: 0,1,2,5

--f, phase2-forward-secrecy
:    Phase 2 perfect forward secrecy. Range is 0-1

--l, phase2-key-ttl
:    Phase 2 key life. Range is 120-172800

--k, preshared-key
:    Preshared key

--r, remote-peer
:    Remote peer IP address
