---

copyright:
  years: "2025"
lastupdated: "2025-06-11"

keywords: cli, context-based restrictions plugin

subcollection: cli

---

{{site.data.keyword.attribute-definition-list}}

# Context-based restrictions CLI plug-in
{: #cbr-plugin}

The {{site.data.keyword.cloud}} context-based restrictions command line interface (CLI) provides extra capabilities for context-based restrictions. You can use this CLI plug-in to manage access restrictions for {{site.data.keyword.cloud}} resources based on the network location of access requests.
{: shortdesc}

## Before you begin
{: #prereqs-cbr-plugin}

* Install the {{site.data.keyword.cloud_notm}} CLI. For more information, see [Getting started with the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started). The prefix for running commands by using the {{site.data.keyword.cloud_notm}} CLI is `ibmcloud`.
* Before you run commands, log in to {{site.data.keyword.cloud_notm}} with the `ibmcloud login` command to generate an access token and authenticate your session.


## Installing the context-based restrictions plug-in
{: #install-cbr-plugin}

To install the context-based restrictions plug-in, run the following command:

```bash
ibmcloud plugin install cbr
```
{: codeblock}

In the command line, you are notified when updates to the `ibmcloud` CLI and `cbr` CLI plug-in are available. Ensure that you keep your CLI up to date so that you can use all the available commands and flags.

If you want to view the current version of your `cbr` CLI plug-in, run `ibmcloud plugin list`.

## Zones
{: #cbr-zones-cli}

Operations on network zones.

### `ibmcloud cbr zone-create`
{: #cbr-cli-zone-create-command}

This operation creates a network zone for the specified account.

```sh
ibmcloud cbr zone-create [--name NAME] [--description DESCRIPTION] [--addresses ADDRESSES] [--vpc VPC] [--service-ref SERVICEREF] [--excluded EXCLUDED] [--empty-address-list] [--file FILE]
```
{: codeblock}

#### Example
{: #cbr-cli-zone-create-example}

```sh
ibmcloud cbr zone-create --name example-zone --description "Example zone description" --addresses 192.0.2.1,3ffe:1900:fe21:4545::,192.2.3.5-192.2.3.10,3ffe:1900:fe21:4547::-3ffe:1900:fe21:6767:

ibmcloud cbr zone-create --name example-zone-with-service-ref --service-ref service_name=kms,location=us-south

ibmcloud cbr zone-create --name example-zone-with-vpc --vpc crn:v1:staging:public:is:us-south:a/12ab34cd56ef78ab90cd12ef34ab56cd::vpc:r123-abc456de-f789-abc1-23de-f456abc789ab
```
{: codeblock}

#### Example output
{: #cbr-cli-zone-create-example-output}

```sh
id                    9adc34f2867a43452a517b3c2de78b95   
crn                   crn:v1:bluemix:public:cbr:global:a/0123456789::zone:9adc34f2867a43452a517b3c2de78b95   
address_count         7   
excluded_count        0   
name                  test   
account_id            0123456789   
description              
Addresses             1 IP Address, 1 IP Range, 1 Subnet, 2 VPCs, 2 Service References                                                                    
Excluded              No addresses       
href                  https://cbr.cloud.ibm.com/v1/zones/9adc34f2867a43452a517b3c2de78b95   
created_at            2024-03-06T22:20:25.000Z   
created_by_id         iam-ServiceId-0123456789
last_modified_at      2024-03-06T22:20:25.000Z   
last_modified_by_id   iam-ServiceId-0123456789
```
{: codeblock}

#### Command options
{: #cbr-zone-create-cli-options}

`--name` (string)
:   The name of the zone.

`--description` (string)
:   The description of the zone.

`--addresses` (string)
:   The list of addresses in the zone. Only addresses of type `ipAddress`, `ipRange`, and `subnet` are allowed in a comma delimited format. IPv4 and IPv6 are supported.

`--service-ref` (string)
:   The service refs in the zone. Input in the form `service_name=VALUE,service_name=VALUE,...`.
:   To find a list of available service refs, run the `ibmcloud cbr service-ref-targets` [command](#cbr-cli-service-ref-targets-command).

`--vpc` (string)
:   The VPCs allowed in the zone. Input in the form `value,value,...`.

`--excluded` (string)
:   The list of excluded addresses in the zone. Only addresses of type `ipAddress`, `ipRange`, and `subnet` are allowed in a comma delimited format.

`--empty-address-list` (bool)
:   Explicitly specifies that the zone will have no addresses. This cannot be used in tandem with the `addresses`, `service-ref`, `vpc`, or `excluded` flags.

`--file` (string)
:   The supplied file is used to create the zone. This flag is unique and cannot be used with other flags. The file needs to follow the JSON schema for the zone create API. For more information, see the [Context-based restrictions API](/apidocs/context-based-restrictions#create-zone-request){: external}.


### `ibmcloud cbr zones`
{: #cbr-cli-zones-command}

This operation lists network zones in the specified account.

```sh
ibmcloud cbr zones [--name NAME] [--sort SORT]
```
{: codeblock}

#### Example
{: #cbr-cli-zones-example}

```sh
ibmcloud cbr zones
```
{: codeblock}

#### Example output
{: #cbr-cli-zones-example-output}

```sh
id                                 name      address_count   excluded_count   
9adc34f2867a43452a517b3c2de78b95   test      7               0
12ab34cd56ef78ab90cd12ef34ab56cd   example   2               0
```
{: codeblock}

#### Command options
{: #cbr-zones-cli-options}

`--name` (string)
:   The name of the zone.

`--sort` (string)
:   Sorts results by using a valid sort field. To learn more, see [Sorting](/docs/api-handbook?topic=api-handbook-sorting).


### `ibmcloud cbr zone`
{: #cbr-cli-zone-command}

This operation retrieves the network zone that is identified by the specified zone ID.

```sh
ibmcloud cbr zone ZONE-ID
```
{: codeblock}

#### Example
{: #cbr-cli-zone-example}

```sh
ibmcloud cbr zone 9adc34f2867a43452a517b3c2de78b95
```
{: codeblock}

#### Example output
{: #cbr-cli-zone-example-output}

```sh
id                    9adc34f2867a43452a517b3c2de78b95   
crn                   crn:v1:bluemix:public:cbr:global:a/0123456789::zone:9adc34f2867a43452a517b3c2de78b95   
address_count         7   
excluded_count        0   
name                  test   
account_id            0123456789   
description              
Addresses             1 IP Address, 1 IP Range, 1 Subnet, 2 VPCs, 2 Service References                                                                    
Excluded              No addresses       
href                  https://cbr.cloud.ibm.com/v1/zones/9adc34f2867a43452a517b3c2de78b95   
created_at            2024-03-06T22:20:25.000Z   
created_by_id         iam-ServiceId-0123456789
last_modified_at      2024-03-06T22:20:25.000Z   
last_modified_by_id   iam-ServiceId-0123456789
```
{: codeblock}

### `ibmcloud cbr zone-update`
{: #cbr-cli-zone-update-command}

This operation replaces the network zone that is identified by the specified zone ID. Partial updates are not supported and the entire network zone object is replaced.

```sh
ibmcloud cbr zone-update ZONE-ID [--name NAME] [--description DESCRIPTION] [--addresses ADDRESSES] [--vpc VPC] [--service-ref SERVICEREF] [--excluded EXCLUDED] [--empty-address-list] [--file FILE]
```
{: codeblock}

#### Example
{: #cbr-zone-update-example}

```shell
ibmcloud cbr zone-update 9adc34f2867a43452a517b3c2de78b95 --name 'Example Zone Name' --addresses 166.22.23.0-166.22.23.108,3ffe:1900:fe21:4545:: --excluded 166.22.23.100

ibmcloud cbr zone-update 9adc34f2867a43452a517b3c2de78b95 --name example-zone-with-service-ref --service-ref service_name=kms,location=us-south

ibmcloud cbr zone-update 9adc34f2867a43452a517b3c2de78b95 --name example-zone-with-vpc --vpc crn:v1:staging:public:is:us-south:a/12ab34cd56ef78ab90cd12ef34ab56cd::vpc:r123-abc456de-f789-abc1-23de-f456abc789ab
```
{: codeblock}

#### Example output
{: #cbr-cli-zone-update-example-output}

```sh
id                    9adc34f2867a43452a517b3c2de78b95   
crn                   crn:v1:bluemix:public:cbr:global:a/0123456789::zone:9adc34f2867a43452a517b3c2de78b95   
address_count         7   
excluded_count        0   
name                  test update   
account_id            0123456789   
description              
Addresses             1 IP Address, 1 IP Range, 1 Subnet, 2 VPCs, 2 Service References                                                                    
Excluded              No addresses       
href                  https://cbr.cloud.ibm.com/v1/zones/9adc34f2867a43452a517b3c2de78b95   
created_at            2024-03-06T22:20:25.000Z   
created_by_id         iam-ServiceId-0123456789
last_modified_at      2024-03-06T22:29:19.000Z   
last_modified_by_id   iam-ServiceId-0123456789
```
{: codeblock}

#### Command options
{: #cbr-zone-update-cli-options}

`--name` (string)
:   The name of the zone.

`--description` (string)
:   The description of the zone.

`--addresses` (string)
:   The list of addresses in the zone. Only addresses of type `ipAddress`, `ipRange`, and `subnet` are allowed in a comma delimited format. IPv4 and IPv6 are supported.

`--service-ref` (string)
:   The service refs in the zone. Input in the form `name=value,name=value,...`.

`--vpc` (string)
:   The VPCs allowed in the zone. Input in the form `value,value,...`.

`--excluded` (string)
:   The list of excluded addresses in the zone. Only addresses of type `ipAddress`, `ipRange`, and `subnet` are allowed in a comma delimited format.

`--empty-address-list` (bool)
:   Explicitly specifies that the zone will have no addresses. This cannot be used in tandem with the `addresses`, `service-ref`, `vpc`, or `excluded` flags.

`--file` (string)
:   The supplied file is used to update the zone. This flag is unique and cannot be used with other flags. The file needs to follow the JSON schema for the zone update API. For more information, see the [Context-based restrictions API](/apidocs/context-based-restrictions#replace-zone-request){: external}.


### `ibmcloud cbr zone-patch`
{: #cbr-cli-zone-patch-command}

This operation performs a partial update of the network zone that is identified by the specified zone ID.

```sh
ibmcloud cbr zone-patch ZONE-ID [--name NAME] [--description DESCRIPTION]
```
{: codeblock}

#### Example
{: #cbr-zone-patch-example}

```shell
ibmcloud cbr zone-patch 9adc34f2867a43452a517b3c2de78b95 --name 'Example Zone Name' --description updated
```
{: codeblock}

#### Example output
{: #cbr-cli-zone-patch-example-output}

```sh
id                    9adc34f2867a43452a517b3c2de78b95   
crn                   crn:v1:bluemix:public:cbr:global:a/0123456789::zone:9adc34f2867a43452a517b3c2de78b95   
address_count         7   
excluded_count        0   
name                  test update   
account_id            0123456789   
description           updated   
Addresses             1 IP Address, 1 IP Range, 1 Subnet, 2 VPCs, 2 Service References                                                                    
Excluded              No addresses       
href                  https://cbr.cloud.ibm.com/v1/zones/9adc34f2867a43452a517b3c2de78b95   
created_at            2024-03-06T22:20:25.000Z   
created_by_id         iam-ServiceId-0123456789
last_modified_at      2024-03-06T22:29:19.000Z   
last_modified_by_id   iam-ServiceId-0123456789
```
{: codeblock}

#### Command options
{: #cbr-zone-patch-cli-options}

`--name` (string)
:   The name of the zone.

`--description` (string)
:   The description of the zone.

### `ibmcloud cbr zone-delete`
{: #cbr-cli-zone-delete-command}

This operation deletes the network zone that is identified by the specified zone ID.

```sh
ibmcloud cbr zone-delete ZONE-ID
```
{: codeblock}

#### Example
{: #cbr-cli-zone-delete-example}

```sh
ibmcloud cbr zone-delete 65810ac762004f22ac19f8f8edf70a34
```
{: codeblock}

### `ibmcloud cbr service-ref-targets`
{: #cbr-cli-service-ref-targets-command}

This operation lists all of the available service reference targets.

```sh
ibmcloud cbr service-ref-targets [--type TYPE]
```
{: codeblock}

#### Example
{: #cbr-cli-service-ref-targets-example}

```sh
ibmcloud cbr service-ref-targets
```
{: codeblock}

#### Example output
{: #cbr-cli-service-ref-targets-example-output}

```sh
service_name                   service_type       locations   
ace                            -                  -   
apprapp                        -                  na, us, dal   
apprapp-dev                    -                  na, us, dal   
cloud-object-storage           -                  na, us, sjc   
cloudantnosqldb                -                  ap, au, syd, +27   
codeengine                     -                  ap, au, syd, +6   
compliance                     platform_service   na, us, dal, +1   
containers-kubernetes          -                  na, us, dal   
directlink                     -                  -   
event-notifications            -                  na, us, dal   
globalcatalog-collection       -                  -   
iam-groups                     platform_service   -   
is                             -                  eu, es, mad, +4   
kms                            -                  -   
logdna                         -                  ap, au, syd, +17   
logdnaat                       -                  ap, au, syd, +17   
messagehub                     -                  eu, uk, lon, +3   
messagehub-vnext-integration   -                  eu, uk, lon, +3   
schematics                     -                  eu, de, fra, +6   
secrets-manager                -                  -   
server-protect                 -                  eu, es, mad, +4   
sysdig-monitor                 -                  eu, uk, lon, +3   
sysdig-secure                  -                  eu, uk, lon, +3   
toolchain                      -                  ap, au, syd, +6   
user-management                platform_service   -   
```
{: codeblock}

#### Command options
{: #cbr-service-ref-targets-cli-options}

`--type` (string)
:   Specifies the types of services to retrieve. The default value is `all`. Allowable values are: `all`, `platform_service`.


### `ibmcloud cbr service-ref-target`
{: #cbr-cli-service-ref-target-command}

This operation gets the service reference target for a specified service name.

```sh
ibmcloud cbr service-ref-target SERVICE-NAME
```
{: codeblock}

#### Example
{: #cbr-cli-service-ref-target-example}

```sh
ibmcloud cbr service-ref-target compliance
```
{: codeblock}

#### Example output
{: #cbr-cli-service-ref-target-example-output}

```sh
Service Name     compliance         
Service Type:    platform_service   
Locations:       
                 Name               Display Name    Kind   
                 na                 North America   geography   
                 us                 United States   country   
                 dal                Dallas          metro   
                 wdc                Washington DC   metro   
```
{: codeblock}

## Rules
{: #cbr-rules-cli}

Operations on context-based restriction rules.

### `ibmcloud cbr rule-create`
{: #cbr-cli-rule-create-command}

This operation creates a rule for the specified account.

```sh
ibmcloud cbr rule-create [--description DESCRIPTION] [--resource-attributes RESOURCES] [--context-attributes CONTEXTS] [--api-types API-TYPES] [--enforcement-mode ENFORCEMENT-MODE] [--service-name SERVICE-NAME] [--service-group-id SERVICE-GROUP-ID] [--service-instance SERVICE-INSTANCE] [--region REGION] [--resource-type RESOURCE-TYPE] [--resource RESOURCE] [--resource-group-id RESOURCE-GROUP-ID] [--tags TAGS] [--zone-id ZONE-ID] [--empty-context-list] [--file FILE]
```
{: codeblock}

#### Example
{: #cbr-cli-rule-create-example}

```sh
ibmcloud cbr rule-create --description 'Example Rule Description' --service-name kms --context-attributes endpointType=private --zone-id 93de8d3f588ab2c457ff576c364d1145

ibmcloud cbr rule-create --service-name example-service --context-attributes mfa=LEVEL2,endpointType=public,networkZoneId=12ab34cd56ef78ab90cd12ef34ab56cd
```
{: codeblock}

#### Example output
{: #cbr-cli-rule-create-example-output}

```sh
id                    2c54cb0fefb0050c88f72d68c400fbec   
crn                   crn:v1:bluemix:public:cbr:global:a/0123456789::rule:2c54cb0fefb0050c88f72d68c400fbec   
description           test   
operations            1 API Type   
contexts              1 Context   
resources                                  
                      serviceInstance   1234567891234   
                      serviceName       cloud-object-storage
  
href                  https://cbr.cloud.ibm.com/v1/rules/2c54cb0fefb0050c88f72d68c400fbec   
created_at            2024-03-07T15:36:52.000Z   
created_by_id         iam-ServiceId-0123456789
last_modified_at      2024-03-07T15:36:52.000Z   
last_modified_by_id   iam-ServiceId-0123456789
enforcement_mode      enabled   

```
{: codeblock}


#### Command options
{: #cbr-rule-create-cli-options}

`--description` (string)
:   The description of the rule.

`--resource-attributes` (string)
:   The resource-attributes this rule applies to in the form of `name=value,name=value,...`. Attribute operators can only be specified using the '--file' flag instead.

`--context-attributes` (string)
:   The context-attributes this rule applies to in the form of `name=value,name=value,...`.

`--api-types` (string)
:   The APIs a rule applies to. For supported service API types, use the `service` command on the resource.

`--enforcement-mode` (string)
:   How the rule is enforced. The CLI accepts the values `enabled` (default), `disabled`, and `report`. For more informaiton about enforcement, see [Rule enforcement](/docs/account?topic=account-context-restrictions-whatis#rule-enforcement).

`--service-name` (string)
:   Shorthand for creating IBM Cloud resource attribute `serviceName`.

`--service-group-id` (string)
:   The `service_group_id` resource attribute.

`--service-instance` (string)
:   GUID of the service instance. This option is exclusive with the --file option.

`--region` (string)
:   Shorthand for creating IBM Cloud resource attribute `region`. For supported regions, run `ibmcloud regions`.

`--resource-type` (string)
:   Shorthand for creating IBM Cloud resource attribute `resourceType`.

`--resource` (string)
:   Shorthand for creating IBM Cloud resource attribute `resource`.

`--resource-group-id` (string)
:   Shorthand for creating IBM Cloud resource attribute `resourceGroupId`.

`--tags` (string)
:   The access tags of the resource in the form of `name:value,name:value,...`.

`--zone-id` (string)
:   Shorthand for adding context attribute `networkZoneId` to the first context.

`--empty-context-list` (bool)
:   Explicitly specifies that the rule will have no contexts. This cannot be used in tandem with the `context-attributes` or `zone-id` flags.

`--file` (string)
:   The supplied file is used to create the rule. This flag is unique and cannot be used with other flags. The file needs to follow the JSON schema for the rule create API. For more information, see the [Context-based restrictions API](/apidocs/context-based-restrictions#create-rule-request){: external}.


### `ibmcloud cbr rules`
{: #cbr-cli-rules-command}

This operation lists rules in the specified account.

```sh
ibmcloud cbr rules [--enforcement-mode ENFORCEMENT-MODE] [--service-name SERVICE-NAME] [--service-group-id SERVICE-GROUP-ID] [--service-instance SERVICE-INSTANCE] [--region REGION] [--resource-type RESOURCE-TYPE] [--resource RESOURCE] [--zone-id ZONE-ID] [--sort SORT]
```
{: codeblock}

#### Example
{: #cbr-cli-rules-example}

```sh
ibmcloud cbr rules
```
{: codeblock}

#### Example output
{: #cbr-cli-rules-example-output}

```sh
id                                 service_name           enforcement   description   
2c54cb0fefb0050c88f72d68c400fbec   cloud-object-storage   enabled       test   
a4135a90bb507bf6d96cf4c6f009d151   kms                    disabled       example   
```
{: codeblock}

#### Command options
{: #cbr-rules-cli-options}

`--enforcement-mode` (string)
:   How the rule is enforced. The CLI accepts the values `enabled` (default), `disabled`, and `report`. For more informaiton about enforcement, see [Rule enforcement](/docs/account?topic=account-context-restrictions-whatis#rule-enforcement).

`--region` (string)
:   The `region` resource attribute.

`--resource` (string)
:   The `resource` resource attribute.

`--resource-type` (string)
:   The `resourceType` resource attribute.

`--service-instance` (string)
:   The GUID of the service instance.

`--service-name` (string)
:   The `serviceName` resource attribute.

`--service-group-id` (string)
:   The `service_group_id` resource attribute.

`--zone-id` (string)
:   The globally unique ID of the zone.

`--sort` (string)
:   Sorts results by using a valid sort field. To learn more, see [Sorting](/docs/api-handbook?topic=api-handbook-sorting).


### `ibmcloud cbr rule`
{: #cbr-cli-rule-command}

This operation retrieves the rule that is identified by the specified rule ID.

```sh
ibmcloud cbr rule RULE-ID
```
{: codeblock}

#### Example
{: #cbr-cli-rule-example}

```sh
ibmcloud cbr rule 30fd58c9b75f40e854b89c432318b4a2
```
{: codeblock}

#### Example output
{: #cbr-cli-rule-example-output}

```sh
id                    2c54cb0fefb0050c88f72d68c400fbec   
crn                   crn:v1:bluemix:public:cbr:global:a/0123456789::rule:2c54cb0fefb0050c88f72d68c400fbec   
description           test   
operations            1 API Type   
contexts              1 Context   
resources                                  
                      serviceInstance   1234567891234   
                      serviceName       cloud-object-storage
  
href                  https://cbr.cloud.ibm.com/v1/rules/2c54cb0fefb0050c88f72d68c400fbec   
created_at            2024-03-07T15:36:52.000Z   
created_by_id         iam-ServiceId-0123456789
last_modified_at      2024-03-07T15:36:52.000Z   
last_modified_by_id   iam-ServiceId-0123456789
enforcement_mode      enabled   

```
{: codeblock}

### `ibmcloud cbr rule-update`
{: #cbr-cli-rule-update-command}

This operation replaces the rule that is identified by the specified rule ID. Partial updates are not supported and the entire rule object is replaced.

```sh
ibmcloud cbr rule-update RULE-ID [--description DESCRIPTION] [--resource-attributes RESOURCES] [--context-attributes CONTEXTS] [--api-types API-TYPES] [--enforcement-mode ENFORCEMENT-MODE] [--service-name SERVICE-NAME] [--service-instance SERVICE-INSTANCE] [--region REGION] [--resource-type RESOURCE-TYPE] [--resource RESOURCE] [--resource-group-id RESOURCE-GROUP-ID] [--tags TAGS] [--zone-id ZONE-ID] [--empty-context-list] [--file FILE]
```
{: codeblock}

#### Example
{: #cbr-cli-rule-update-example}

```sh
ibmcloud cbr rule-update 30fd58c9b75f40e854b89c432318b4a2 --description 'Example rule description' --service-name kms --context-attributes endpointType=private --zone-id 93de8d3f588ab2c457ff576c364d1145
```
{: codeblock}

#### Example output
{: #cbr-cli-rule-update-example-output}

```sh
id                    2c54cb0fefb0050c88f72d68c400fbec   
crn                   crn:v1:bluemix:public:cbr:global:a/0123456789::rule:2c54cb0fefb0050c88f72d68c400fbec   
description           updated   
operations            1 API Type   
contexts              1 Context   
resources                                  
                      serviceInstance   1234567891234   
                      serviceName       cloud-object-storage
  
href                  https://cbr.cloud.ibm.com/v1/rules/2c54cb0fefb0050c88f72d68c400fbec   
created_at            2024-03-07T15:36:52.000Z   
created_by_id         iam-ServiceId-0123456789
last_modified_at      2024-03-07T15:41:18.000Z   
last_modified_by_id   iam-ServiceId-0123456789
enforcement_mode      enabled
```
{: codeblock}

#### Command options
{: #cbr-rule-update-cli-options}

`--description` (string)
:   The description of the rule.

`--resource-attributes` (string)
:   The resource-attributes this rule applies to in the form of `name=value,name=value,...`. Attribute operators can only be specified using the '--file' flag instead.

`--context-attributes` (string)
:   The context-attributes this rule applies to in the form of `name=value,name=value,...`.

`--api-types` (string)
:   The APIs a rule applies to. For supported service API types, use the `service` command on the resource.

`--enforcement-mode` (string)
:   How the rule is enforced. The CLI accepts the values `enabled` (default), `disabled`, and `report`. For more informaiton about enforcement, see [Rule enforcement](/docs/account?topic=account-context-restrictions-whatis#rule-enforcement).

`--service-name` (string)
:   Shorthand for creating IBM Cloud resource attribute `serviceName`.

`--service-group-id` (string)
:   The `service_group_id` resource attribute.

`--service-instance` (string)
:   GUID of the service instance. This option is exclusive with the --file option.

`--region` (string)
:   Shorthand for creating IBM Cloud resource attribute `region`. For supported regions, run `ibmcloud regions`.

`--resource-type` (string)
:   Shorthand for creating IBM Cloud resource attribute `resourceType`.

`--resource` (string)
:   Shorthand for creating IBM Cloud resource attribute `resource`.

`--resource-group-id` (string)
:   Shorthand for creating IBM Cloud resource attribute `resourceGroupId`.

`--tags` (string)
:   The access tags of the resource in the form of `name:value,name:value,...`.

`--zone-id` (string)
:   Shorthand for adding context attribute `networkZoneId` to the first context.

`--empty-context-list` (bool)
:   Explicitly specifies that the rule will have no contexts. This cannot be used in tandem with the `context-attributes` or `zone-id` flags.

`--file` (string)
:   The supplied file is used to create the rule. This flag is unique and cannot be used with other flags. The file needs to follow the JSON schema for the rule create API. For more information, see the [Context-based restrictions API](/apidocs/context-based-restrictions#create-rule-request){: external}.


### `ibmcloud cbr rule-patch`
{: #cbr-cli-rule-patch-command}

This operation performas a partial update of the rule that is identified by the specified rule ID.

```sh
ibmcloud cbr rule-patch RULE-ID [--description DESCRIPTION] [--enforcement-mode ENFORCEMENT-MODE]
```
{: codeblock}

#### Example
{: #cbr-cli-rule-patch-example}

```sh
ibmcloud cbr rule-patch 30fd58c9b75f40e854b89c432318b4a2 --description 'Example rule description' --enforcement-mode disabled
```
{: codeblock}

#### Example output
{: #cbr-cli-rule-patch-example-output}

```sh
id                    2c54cb0fefb0050c88f72d68c400fbec   
crn                   crn:v1:bluemix:public:cbr:global:a/0123456789::rule:2c54cb0fefb0050c88f72d68c400fbec   
description           updated   
operations            1 API Type   
contexts              1 Context   
resources                                  
                      serviceInstance   1234567891234   
                      serviceName       cloud-object-storage
  
href                  https://cbr.cloud.ibm.com/v1/rules/2c54cb0fefb0050c88f72d68c400fbec   
created_at            2024-03-07T15:36:52.000Z   
created_by_id         iam-ServiceId-0123456789
last_modified_at      2024-03-07T15:41:18.000Z   
last_modified_by_id   iam-ServiceId-0123456789
enforcement_mode      enabled
```
{: codeblock}

#### Command options
{: #cbr-rule-patch-cli-options}

`--description` (string)
:   The description of the rule.

`--enforcement-mode` (string)
:   How the rule is enforced. The CLI accepts the values `enabled` (default), `disabled`, and `report`. For more informaiton about enforcement, see [Rule enforcement](/docs/account?topic=account-context-restrictions-whatis#rule-enforcement).


### `ibmcloud cbr rule-delete`
{: #cbr-cli-rule-delete-command}

This operation deletes the rule that is identified by the specified rule ID.

```sh
ibmcloud cbr rule-delete RULE-ID
```
{: codeblock}

#### Example
{: #cbr-cli-rule-delete-example}

```sh
ibmcloud cbr rule-delete 30fd58c9b75f40e854b89c432318b4a2
```
{: codeblock}

## Services 
### `ibmcloud cbr services`
{: #cbr-cli-services-command}

This operation lists services that can create context-based restriction rules.

```sh
ibmcloud cbr services
```
{: codeblock}

#### Example
{: #cbr-cli-services-example}

```sh
ibmcloud cbr services
```
{: codeblock}

#### Example output
{: #cbr-cli-services-example-output}

```sh
Display Name                                         Name                          API Types
Activity Tracker Event Routing                       atracker                      1 API Type
All IAM Account Management Services                  IAM                           3 API Types
App Configuration                                    apprapp                       3 API Types
Catalog Management                                   globalcatalog-collection      3 API Types
Cloud Activity Tracker                               logdnaat                      3 API Types
Cloud Logs                                           logs                          1 API Type
Cloud Monitoring                                     sysdig-monitor                1 API Type
Cloud Object Storage                                 cloud-object-storage          1 API Type
Code Engine                                          codeengine                    3 API Types
Container Registry                                   container-registry            1 API Type
Context-Based Restrictions                           context-based-restrictions    1 API Type
Databases for EDB                                    databases-for-enterprisedb    3 API Types
Databases for Elasticsearch                          databases-for-elasticsearch   3 API Types
Databases for etcd                                   databases-for-etcd            3 API Types
Databases for MongoDB                                databases-for-mongodb         3 API Types
Databases for MySQL                                  databases-for-mysql           3 API Types
Databases for PostgreSQL                             databases-for-postgresql      3 API Types
Databases for Redis                                  databases-for-redis           3 API Types
Direct Link                                          directlink                    1 API Type
DNS Services                                         dns-svcs                      3 API Types
Event Notifications                                  event-notifications           5 API Types
Event Streams                                        messagehub                    1 API Type
Hyper Protect Crypto Services                        hs-crypto                     3 API Types
IAM Access Groups Service                            iam-groups                    1 API Type
IAM Access Management Service                        iam-access-management         1 API Type
IAM Identity Service                                 iam-identity                  3 API Types
Key Protect                                          kms                           3 API Types
Kubernetes Service                                   containers-kubernetes         3 API Types
Log Analysis                                         logdna                        3 API Types
Messages for RabbitMQ                                messages-for-rabbitmq         3 API Types
MQ                                                   mqcloud                       2 API Types
Schematics                                           schematics                    1 API Type
Secrets Manager                                      secrets-manager               3 API Types
Security and Compliance Center                       compliance                    3 API Types
Security and Compliance Center Workload Protection   sysdig-secure                 1 API Type
Tagging Service                                      ghost-tags                    1 API Type
Transit Gateway                                      transit                       1 API Type
User Management                                      user-management               1 API Type
VPC Infrastructure Services                          is                            1 API Type
```
{: codeblock}

### `ibmcloud cbr service`
{: #cbr-cli-service-command}

This operation retrieves a service that can create context-based restriction rules. When querying with a JSON or YAML output, you can view the full list of actions for each API Type.

```sh
ibmcloud cbr service SERVICE [--resource-type RESOURCE-TYPE]
```
{: codeblock}

#### Example
{: #cbr-cli-service-example}

```sh
ibmcloud cbr service context-based-restrictions
```
{: codeblock}

#### Example output
{: #cbr-cli-service-example-output}

```sh
Display Name:     Context-Based Restrictions
Service Name:     context-based-restrictions
API Types:     
                  Name   API Type ID                                                     Type      Actions      Description
                  All    crn:v1:bluemix:public:context-based-restrictions::::api-type:   service   10 actions   Protects all service APIs.
Resource Types:
                  rule
                  zone
```
{: codeblock}

#### Command options
{: #cbr-service-cli-options}

`--resource-type` (string)
:   A sub-resource of the service that has additional context-based restriction rule configurations. Note that not all services have additional sub-resource configurations.

### `ibmcloud cbr rule-options`
{: #cbr-cli-rule-options-command}

This operation gets rule options for a service that can create context-based restriction rules.

```sh
ibmcloud cbr rule-options SERVICE [--api-types API-TYPES] [--resource-type RESOURCE-TYPE] [--full]
```
{: codeblock}

#### Example
{: #cbr-cli-rule-options-example}

```sh
ibmcloud cbr rule-options context-based-restrictions --api-types crn:v1:bluemix:public:context-based-restrictions::::api-type: --full
```
{: codeblock}

#### Example output
{: #cbr-cli-service-example-output}

```sh
Operations:                          
                       API Types:    
                                     crn:v1:bluemix:public:context-based-restrictions::::api-type:
                                     
Enforcement Modes:     disabled, enabled, report
Context Attributes:                                        
                       endpointType                        
                          values:                          
                                     private               
                                     public                
                       mfa                                 
                          values:                          
                                     IAM_ACCOUNT_SETTING   
                                     LEVEL1                
                                     LEVEL2                
                                     LEVEL3                
                       networkZoneId                       
Resource Attributes:                                              
                       accountId                                  
                       resourceGroupId                            
                       resourceType                               
                          values:                                 
                                     rule                         
                                     zone                         
                       serviceName                                
                          values:                                 
                                     context-based-restrictions
```
{: codeblock}

#### Command options
{: #cbr-service-cli-options}

`--api-types` (string)
:   The API types a rule would apply to. Can pass multiple as a comma separated list. This defaults to protecting all service APIs represented by 'crn:v1:bluemix:public:context-based-restrictions::::api-type:' if unspecified.

`--resource-type` (string)
:   A sub-resource of the service that has additional context-based restriction rule configurations. Note that not all services have additional sub-resource configurations.

`--full` (bool)
:   Provides a more detailed output for options, such as valid attribute values and attribute operators. If attribute operators are not listed, the stringEquals operator is supported by default.

### `ibmcloud cbr api-types` [Deprecated]{: tag-deprecated}
{: #cbr-cli-api-types-command}

This command is deprecated. Use `ibmcloud-cbr-service` to get API types instead.
{: deprecated}

[Deprecated] This operation lists all available API types. This operation is now deprecated and it is recommended to use the service command instead.

```sh
ibmcloud cbr api-types {--service-name SERVICE-NAME | --service-group-id SERVICE-GROUP-ID} [--resource-type RESOURCE-TYPE]
```
{: codeblock}

#### Example
{: #cbr-cli-api-types-example}

```sh
ibmcloud cbr api-types --service-name context-based-restrictions
```
{: codeblock}

#### Example output
{: #cbr-cli-api-types-example-output}

```sh
api_type_id                                                     display_name   type      description                  enforcement_modes           actions
crn:v1:bluemix:public:context-based-restrictions::::api-type:   All            service   Protects all service APIs.   disabled, enabled, report   10 actions
```
{: codeblock}

#### Command options
{: #cbr-api-types-cli-options}

`--service-name` (string)
:   Specifes the service to lookup API types for.

`--resource-type` (string)
:   The resource type of the service.

`--service-group-id` (string)
:   Specifes the service group to lookup API types for.
