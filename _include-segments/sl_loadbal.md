


## ibmcloud sl loadbal cancel
{: #sl_loadbal_cancel}

Cancel an existing load balancer



```bash
ibmcloud sl loadbal cancel IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

## ibmcloud sl loadbal detail
{: #sl_loadbal_detail}

Get load balancer details



```bash
ibmcloud sl loadbal detail IDENTIFIER
```
{: codeblock}


## ibmcloud sl loadbal health-edit
{: #sl_loadbal_health_edit}

Manage LBaaS health checks.



```bash
ibmcloud sl loadbal health-edit IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--health-uuid
:    Health check UUID to modify [required]

--i, interval
:    Seconds between checks. [2-60]

--r, retry
:    Number of times before marking as DOWN. [1-10]

--t, timeout
:    Seconds to wait for a connection. [1-59]

--u, url
:    Url path for HTTP/HTTPS checks

## ibmcloud sl loadbal l7member-add
{: #sl_loadbal_l7member_add}

Add a new L7 pool member

ibmcloud sl loadbal member-add (--pool-uuid L7POOL_UUID) (--address IP_ADDRESS) (--port PORT)

```bash
ibmcloud sl loadbal l7member-add [flags]
```
{: codeblock}


**Command options**:

--address
:    Backend servers IP address. [required]

--pool-uuid
:    UUID for the load balancer pool [required]

--t, port
:    Backend servers port. [required]

## ibmcloud sl loadbal l7member-delete
{: #sl_loadbal_l7member_delete}

Remove a load balancer member

ibmcloud sl loadbal l7member-del (--pool-uuid L7POOL_UUID) (--member-uuid L7MEMBER_UUID)

```bash
ibmcloud sl loadbal l7member-delete [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--member-uuid
:    UUID for the load balancer member [required]

--pool-uuid
:    UUID for the load balancer pool [required]

## ibmcloud sl loadbal l7policies
{: #sl_loadbal_l7policies}

List L7 policies

ibmcloud sl loadbal l7policies (--protocol-id PROTOCOL_ID)

```bash
ibmcloud sl loadbal l7policies [flags]
```
{: codeblock}


**Command options**:

--protocol-id
:    ID for the load balancer protocol [required]

## ibmcloud sl loadbal l7policy-add
{: #sl_loadbal_l7policy_add}

Add a new L7 policy

ibmcloud sl loadbal l7policy-add (--protocol-uuid PROTOCOL_UUID) (-n, --name NAME) (-a,--action REJECT | REDIRECT_POOL | REDIRECT_URL | REDIRECT_HTTPS) [-r,--redirect REDIRECT] [-p,--priority PRIORITY]

```bash
ibmcloud sl loadbal l7policy-add [flags]
```
{: codeblock}


**Command options**:

--a, action
:    Policy action: REJECT | REDIRECT_POOL | REDIRECT_URL | REDIRECT_HTTPS

--n, name
:    Policy name

--p, priority
:    Policy priority

--protocol-uuid
:    UUID for the load balancer protocol [required]

--r, redirect
:    POOL_UUID, URL or HTTPS_PROTOCOL_UUID . It's only available in REDIRECT_POOL | REDIRECT_URL | REDIRECT_HTTPS action

## ibmcloud sl loadbal l7policy-delete
{: #sl_loadbal_l7policy_delete}

Delete a L7 policy

ibmcloud sl loadbal l7policy-delete (--policy-id POLICY_ID) [-f, --force]

```bash
ibmcloud sl loadbal l7policy-delete [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--policy-id
:    ID for the load balancer policy [required]

## ibmcloud sl loadbal l7policy-edit
{: #sl_loadbal_l7policy_edit}

Edit a L7 policy

ibmcloud sl loadbal l7policy-edit (--policy-d POLICY_ID) (-n, --name NAME) (-a,--action REJECT | REDIRECT_POOL | REDIRECT_URL | REDIRECT_HTTPS) [-r,--redirect REDIRECT] [-p,--priority PRIORITY]

```bash
ibmcloud sl loadbal l7policy-edit [flags]
```
{: codeblock}


**Command options**:

--a, action
:    Policy action: REJECT | REDIRECT_POOL | REDIRECT_URL | REDIRECT_HTTPS

--n, name
:    Policy name

--policy-id
:    ID for the load balancer policy [required]

--p, priority
:    Policy priority

--r, redirect
:    POOL_UUID, URL or HTTPS_PROTOCOL_UUID . It's only available in REDIRECT_POOL | REDIRECT_URL | REDIRECT_HTTPS action

## ibmcloud sl loadbal l7pool-add
{: #sl_loadbal_l7pool_add}

Add a new L7 pool

-s is in colon deliminated format to make grouping IP:port:weight a bit easier.

```bash
ibmcloud sl loadbal l7pool-add [flags]
```
{: codeblock}


**Command options**:

--health-interval
:    Health check interval between checks

--health-path
:    Health check path

--health-retry
:    Health check number of times before marking as DOWN

--health-timeout
:    Health check timeout

--id
:    ID for the load balancer [required]

--m, method
:    Balancing Method: [ROUNDROBIN|LEASTCONNECTION|WEIGHTED_RR]

--n, name
:    Name for this L7 pool. [required]

--p, protocol
:    Protocol type to use for incoming connections

--s, server
:    Backend servers that are part of this pool. Format: BACKEND_IP:PORT. eg. 10.0.0.1:80 (multiple occurrence permitted)

--sticky
:    Use 'cookie' or 'source-ip' to stick

## ibmcloud sl loadbal l7pool-delete
{: #sl_loadbal_l7pool_delete}

Delete a L7 pool

ibmcloud sl loadbal l7pool-delete (--pool-id L7POOL_ID)

```bash
ibmcloud sl loadbal l7pool-delete [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--pool-id
:    ID for the load balancer pool [required]

## ibmcloud sl loadbal l7pool-detail
{: #sl_loadbal_l7pool_detail}

Show L7 pool details

ibmcloud sl loadbal l7pool-detail (--pool-id L7POOL_ID)

```bash
ibmcloud sl loadbal l7pool-detail [flags]
```
{: codeblock}


**Command options**:

--pool-id
:    ID for the load balancer pool [required]

## ibmcloud sl loadbal l7pool-edit
{: #sl_loadbal_l7pool_edit}

Edit a L7 pool

ibmcloud sl loadbal l7pool-edit (--pool-uuid L7POOL_UUID) [-m, --method METHOD] [-s, --server BACKEND_IP:PORT] [-p, --protocol PROTOCOL] [--health-path PATH] [--health-interval INTERVAL] [--health-retry RETRY] [--health-timeout TIMEOUT] [--sticky cookie | source-ip]

```bash
ibmcloud sl loadbal l7pool-edit [flags]
```
{: codeblock}


**Command options**:

--health-interval
:    Health check interval between checks

--health-path
:    Health check path

--health-retry
:    Health check number of times before marking as DOWN

--health-timeout
:    Health check timeout

--m, method
:    Balancing Method: [ROUNDROBIN|LEASTCONNECTION|WEIGHTED_RR]

--n, name
:    Name of the load balancer L7 pool

--pool-uuid
:    UUID for the load balancer pool [required]

--p, protocol
:    Protocol type to use for incoming connections

--s, server
:    Backend servers that are part of this pool. Format: BACKEND_IP:PORT. eg. 10.0.0.1:80 (multiple occurrence permitted)

--sticky
:    Use 'cookie' or 'source-ip' to stick

## ibmcloud sl loadbal l7rule-add
{: #sl_loadbal_l7rule_add}

Add a new L7 rule

ibmcloud sl loadbal l7rule-add (--policy-uuid L7POLICY_UUID) (-t, --type HOST_NAME | FILE_TYPE | HEADER | COOKIE | PATH ) (-c, --compare-type EQUAL_TO | ENDS_WITH | STARTS_WITH | REGEX | CONTAINS) (-v,--value VALUE) [-k,--key KEY] [--invert 0 | 1]

```bash
ibmcloud sl loadbal l7rule-add [flags]
```
{: codeblock}


**Command options**:

--c, compare-type
:    Compare type: EQUAL_TO | ENDS_WITH | STARTS_WITH | REGEX | CONTAINS. [required]

--invert
:    Invert rule: 0 | 1.

--k, key
:    Key name. It's only available in HEADER or COOKIE type

--policy-uuid
:    UUID for the load balancer policy [required]

--t, type
:    Rule type: HOST_NAME | FILE_TYPE | HEADER | COOKIE | PATH. [required]

--v, value
:    Compared Value [required]

## ibmcloud sl loadbal l7rule-delete
{: #sl_loadbal_l7rule_delete}

Delete a L7 rule

ibmcloud sl loadbal l7rule-delete (--policy-uuid L7POLICY_UUID) (--rule-uuid L7RULE_UUID) [-f, --force]

```bash
ibmcloud sl loadbal l7rule-delete [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--policy-uuid
:    UUID for the load balancer policy [required]

--rule-uuid
:    UUID for the load balancer rule [required]

## ibmcloud sl loadbal l7rules
{: #sl_loadbal_l7rules}

List l7 rules

ibmcloud sl loadbal l7rules (--policy-id Policy_ID)

```bash
ibmcloud sl loadbal l7rules [flags]
```
{: codeblock}


**Command options**:

--policy-id
:    ID for the load balancer policy [required]

## ibmcloud sl loadbal list
{: #sl_loadbal_list}

List active load balancers

ibmcloud sl loadbal list

```bash
ibmcloud sl loadbal list
```
{: codeblock}


## ibmcloud sl loadbal member-add
{: #sl_loadbal_member_add}

Add a new load balancer member

ibmcloud sl loadbal member-add (--id LOADBAL_ID) (--ip PRIVATE_IP)

```bash
ibmcloud sl loadbal member-add [flags]
```
{: codeblock}


**Command options**:

--id
:    ID for the load balancer [required]

--ip
:    Private IP of the new member [required]

## ibmcloud sl loadbal member-delete
{: #sl_loadbal_member_delete}

Remove a load balancer member

ibmcloud sl loadbal member-del (--lb-id LOADBAL_ID) (-m, --member-uuid MEMBER_UUID)

```bash
ibmcloud sl loadbal member-delete [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--lb-id
:    ID for the load balancer [required]

--m, member-uuid
:    Member UUID [required]

## ibmcloud sl loadbal ns-detail
{: #sl_loadbal_ns_detail}

Get Netscaler details.

ibmcloud sl  loadbal ns-detail [OPTIONS] IDENTIFIER

```bash
ibmcloud sl loadbal ns-detail IDENTIFIER
```
{: codeblock}


## ibmcloud sl loadbal ns-list
{: #sl_loadbal_ns_list}

List netscalers

ibmcloud sl loadbal netscalers

```bash
ibmcloud sl loadbal ns-list
```
{: codeblock}


## ibmcloud sl loadbal order
{: #sl_loadbal_order}

Order a load balancer

ibmcloud sl loadbal order (-n, --name NAME) (-d, --datacenter DATACENTER) (-t, --type PublicToPrivate | PrivateToPrivate | PublicToPublic ) [-l, --label LABEL] [ -s, --subnet SUBNET_ID] [--frontend-protocol PROTOCOL] [--frontend-port PORT] [--backend-protocol PROTOCOL] [--backend-port PORT] [-m, --method METHOD] [-c, --connections CONNECTIONS] [--sticky cookie | source-ip] [--use-public-subnet] [--verify]

```bash
ibmcloud sl loadbal order [flags]
```
{: codeblock}


**Command options**:

--backend-port
:    Backend port [default: 80]

--backend-protocol
:    Backend protocol [default: HTTP]

--c, connections
:    Maximum number of connections to allow

--d, datacenter
:    Datacenter name. It can be found from the keyName in the command '${COMMAND_NAME} sl order package-locations LBAAS' output. [required]

--f, force
:    Force operation without confirmation

--frontend-port
:    Frontend port

--frontend-protocol
:    Frontend protocol

--l, label
:    A descriptive label for this load balancer

--m, method
:    Balancing Method: [ROUNDROBIN|LEASTCONNECTION|WEIGHTED_RR]

--n, name
:    Name for this load balancer [required]

--sticky
:    Use 'cookie' or 'source-ip' to stick

--s, subnet
:    Private subnet Id to order the load balancer. See '${COMMAND_NAME} sl loadbal order-options'. Only available in PublicToPrivate and PrivateToPrivate load balancer type

--t, type
:    Load balancer type: PublicToPrivate | PrivateToPrivate | PublicToPublic [required]

--use-public-subnet
:    If this option is specified, the public ip will be allocated from a public subnet in this account. Otherwise, it will be allocated form IBM system pool. Only available in PublicToPrivate load balancer type.

--verify
:    Only verify an order, dont actually create one

## ibmcloud sl loadbal order-options
{: #sl_loadbal_order_options}

List options for order a load balancer

ibmcloud sl loadbal order-options [-d, --datacenter DATACENTER]

```bash
ibmcloud sl loadbal order-options [flags]
```
{: codeblock}


**Command options**:

--d, datacenter
:    Show only selected datacenter, use shortname (dal13) format

## ibmcloud sl loadbal protocol-add
{: #sl_loadbal_protocol_add}

Add a new load balancer protocol

Creates a new mapping between incoming traffic to the loadbalancer and the backend servers.
Use '{COMMAND_NAME}  sl security cert-list' to get IDs for the --ssl-id option.
See: https://cloud.ibm.com/docs/loadbalancer-service?topic=loadbalancer-service-about-ibm-cloud-load-balancer for more details

**Examples**:

	ibmcloud sl loadbal protocol-add --id 1115129 --front-port 443 --front-protocol HTTPS --back-port 80 --back-protocol HTTP --ssl-id 335659 --client-timeout 60 --connections 100
	Creates a new protocol on Load Balancer 1115129 that terminates SSL on port 443, mapping to a backend port 80 HTTP. Using SSL cert 335659


```bash
ibmcloud sl loadbal protocol-add [flags]
```
{: codeblock}


**Command options**:

--back-port
:    Private side port

--back-protocol
:    Protocol type to use when connecting to backend servers: [HTTP|HTTPS|TCP]. Defaults to whatever --front-protocol is

--client-timeout
:    Client side timeout setting, in seconds

--c, connections
:    Maximum number of connections to allow

--front-port
:    Internet side port

--front-protocol
:    Protocol type to use for incoming connections: [HTTP|HTTPS|TCP]. Default: HTTP

--id
:    ID for the load balancer [required]

--m, method
:    Balancing Method: [ROUNDROBIN|LEASTCONNECTION|WEIGHTED_RR]

--server-timeout
:    Server side timeout setting, in seconds

--ssl-id
:    Identifier of the SSL certificate to attach to this protocol. Only valid for HTTPS.

--sticky
:    Use 'cookie' or 'source-ip' to stick

## ibmcloud sl loadbal protocol-delete
{: #sl_loadbal_protocol_delete}

Delete a protocol

ibmcloud sl loadbal protocol-delete (--lb-id LOADBAL_ID) (--protocol-uuid PROTOCOL_UUID)

```bash
ibmcloud sl loadbal protocol-delete [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

--lb-id
:    ID for the load balancer [required]

--protocol-uuid
:    UUID for the protocol [required]

## ibmcloud sl loadbal protocol-edit
{: #sl_loadbal_protocol_edit}

Edit load balancer protocol

Use 'ibmcloud sl loadbal detail' to find the --protocol-uuid values for a loadbalancer
**Examples**:

	ibmcloud sl loadbal protocol-add --id 1115129 --protocol-uuid 8ec8911a-c32d-4678-89fe-979f182c822f --ssl-id 123
	This command changes the SSL certificate


```bash
ibmcloud sl loadbal protocol-edit [flags]
```
{: codeblock}


**Command options**:

--back-port
:    Private side port

--back-protocol
:    Protocol type to use when connecting to backend servers: [HTTP|HTTPS|TCP]. Defaults to whatever --front-protocol is

--client-timeout
:    Client side timeout setting, in seconds

--c, connections
:    Maximum number of connections to allow

--front-port
:    Internet side port

--front-protocol
:    Protocol type to use for incoming connections: [HTTP|HTTPS|TCP]. Default: HTTP

--id
:    ID for the load balancer [required]

--m, method
:    Balancing Method: [ROUNDROBIN|LEASTCONNECTION|WEIGHTED_RR]

--protocol-uuid
:    UUID of the protocol you want to edit.

--server-timeout
:    Server side timeout setting, in seconds

--ssl-id
:    Identifier of the SSL certificate to attach to this protocol. Only valid for HTTPS.

--sticky
:    Use 'cookie' or 'source-ip' to stick
