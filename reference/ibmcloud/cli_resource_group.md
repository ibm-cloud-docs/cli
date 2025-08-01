---

copyright:
  years: 2018, 2025
lastupdated: "2025-07-16"

keywords: cli, manage resources, resource group, ibmcloud resource group, ibmcloud resource, service-instance, quotas, resource group cli, resource cli

subcollection: cli

---

{{site.data.keyword.attribute-definition-list}}

# Working with resources and resource groups (ibmcloud resource)
{: #ibmcloud_commands_resource}

A resource group is a way for you to organize your account resources in customizable groupings. Use the following commands from the {{site.data.keyword.cloud}} Command Line Interface to manage {{site.data.keyword.cloud_notm}} resources in a resource group.
{: shortdesc}

## ibmcloud resource groups
{: #ibmcloud_resource_groups}

List resource groups.
```bash
ibmcloud resource groups [--default]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_groups_options}

--default
:   Get the default group of the current account.

### Examples
{: #ibmcloud_resource_groups_examples}

List all resource groups under the currently targeted account:
```bash
ibmcloud resource groups
```
{: codeblock}

List the default group of currently targeted account:
```bash
ibmcloud resource groups --default
```
{: codeblock}

## ibmcloud resource group
{: #ibmcloud_resource_group}

Show details of a resource group
```bash
ibmcloud resource group NAME [--id]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_group_options}

NAME (required)
:   Name of the resource group

--id
:   Show ID only


### Examples
{: #ibmcloud_resource_group_examples}

Show resource group `example-group`:
```bash
ibmcloud resource group example-group
```
{: codeblock}

Show only ID of resource group `example-group`:
```bash
ibmcloud resource group example-group --id
```
{: codeblock}

## ibmcloud resource group-create
{: #ibmcloud_resource_group_create}

Create a resource group:
```bash
ibmcloud resource group-create NAME
```
{: codeblock}

### Command options
{: #ibmcloud_resource_group_create_options}

NAME (required)
:   Name of the resource group

### Examples
{: #ibmcloud_resource_group_create_examples}

Create a resource group `example-group`:
```bash
ibmcloud resource group-create example-group
```
{: codeblock}

## ibmcloud resource group-update
{: #ibmcloud_resource_group_update}

Update an existing resource group
```bash
ibmcloud resource group-update NAME [-n, --name NEW_NAME] [-f, --force]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_group_update_options}

NAME (required)
:   Name of the target resource group

-n, --name
:   New name of the resource group

-f, --force
:   Force update without confirmation



### Examples
{: #ibmcloud_resource_group_update_examples}

Rename resource group `example-group` to `trial-group`:
```bash
ibmcloud resource group-update example-group -n trial-group
```
{: codeblock}

## ibmcloud resource group-delete
{: #ibmcloud_resource_group_delete}

Delete an existing resource group
```bash
ibmcloud resource group-delete NAME [-f, --force]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_group_delete_options}

NAME (required)
:   Name of the target resource group

-f, --force
:   Force deletion without confirmation



### Examples
{: #ibmcloud_resource_group_delete_examples}

Delete resource group `example-group`:
```bash
ibmcloud resource group-delete example-group -f
```
{: codeblock}

## ibmcloud resource quotas
{: #ibmcloud_resource_quotas}

List all quota definitions.
```bash
ibmcloud resource quotas
```
{: codeblock}

### Examples
{: #ibmcloud_resource_quotas_examples}

List all quota definitions:
```bash
ibmcloud resource quotas
```
{: codeblock}

## ibmcloud resource quota
{: #ibmcloud_resource_quota}

Show details of a quota definition.
```bash
ibmcloud resource quota NAME
```
{: codeblock}

### Command options
{: #ibmcloud_resource_quota_options}

NAME (required)
:   Name of the quota



### Examples
{: #ibmcloud_resource_quota_examples}

Show details of quota `free`:
```bash
ibmcloud resource quota free
```
{: codeblock}

## ibmcloud resource service-instances
{: #ibmcloud_resource_service_instances}

List service instances.
```bash
ibmcloud resource service-instances [--service-name SERVICE_NAME] [--location LOCATION] [--type INSTANCE_TYPE] [-g RESOURCE_GROUP | --all-resource-groups] [--long] [--limit LIMIT] [--offset OFFSET] [--output FORMAT] [-q, --quiet]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_service_instances_options}

--service-name *SERVICE_NAME*
:   Name of belonging to service

--location *LOCATION*
:   Filter by location

--type *INSTANCE_TYPE*
:   Type of instances. The `service_instance` type is used if not specified. Use all to list all types of instances.

-g *RESOURCE_GROUP*
:   Resource group name

--all-resource-groups
:   Query all resource groups

--long
:   Show more fields in output

--limit LIMIT
:   Number of resources to return

--offset OFFSET
:   Starting resource position number

--output FORMAT
:   Specify the output format. Only JSON is supported now.

-q, --quiet
:   Suppress verbose output.


### Examples
{: #ibmcloud_resource_service_instances_examples}

List service instances of service `test-service`:
```bash
ibmcloud resource service-instances --service-name test-service
```

List next page of service instances with 10 records per page.
```bash
ibmcloud resource service-instances --offset 1 --limit 10
```
{: codeblock}

## ibmcloud resource service-instance
{: #ibmcloud_resource_service_instance}

Show details of a service instance.

```bash
ibmcloud resource service-instance (NAME|ID) [--location LOCATION] [--id]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_service_instance_options}

NAME (required), exclusive with ID
:   Name of the service instance

ID (required), exclusive with NAME
:   ID of the service instance

--location
:   Filter by location

--id
:   Display the ID of the service instance



### Examples
{: #ibmcloud_resource_service_instance_examples}

Show details of service instance `my-service-instance`:
```bash
ibmcloud resource service-instance my-service-instance
```
{: codeblock}

## ibmcloud resource service-instance-create
{: #ibmcloud_resource_service_instance_create}

Create a service instance.
```bash
ibmcloud resource service-instance-create NAME (SERVICE_NAME | SERVICE_ID) SERVICE_PLAN_NAME LOCATION [-d, --deployment DEPLOYMENT_NAME] [-p, --parameters @JSON_FILE | JSON_STRING ] [-g RESOURCE_GROUP] [--service-endpoints SERVICE_ENDPOINTS_TYPE] [--allow-cleanup] [--lock] [--subscription SUBSCRIPTION_ID]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_service_instance_create_options}

NAME (required)
:   Name of the service instance

SERVICE_NAME or SERVICE_ID (required)
:   Name or ID of the service. To list service offerings, use the `ibmcloud catalog service-marketplace`[command](/docs/cli?topic=cli-ibmcloud_catalog#ibmcloud_catalog_service_marketplace).

SERVICE_PLAN_NAME or SERVICE_PLAN_ID (required)
:   Name or ID of the service plan

LOCATION (required)
:   Target location or environment to create the service instance

-d, --deployment *DEPLOYMENT_NAME*
:   Name of the deployment

-p, --parameters *@JSONFILE or JSON_STRING*
:   JSON file or JSON string of parameters to create service instance

-g *RESOURCE_GROUP*
:   Resource group name

--service-endpoints *SERVICE_ENDPOINTS_TYPE*
:   Types of the service endpoints. Possible values are 'public', 'private', 'public-and-private'. The default value for service endpoints is the type that is configured by the service in {{site.data.keyword.cloud}}.

--allow-cleanup
:   Whether the service instance should be deleted (cleaned up) during the processing of a region instance delete call

--lock
:   Whether to create the service instance with locked state

--subscription
:   Subscription ID associated with this service and plan



### Examples
{: #ibmcloud_resource_service_instance_create_examples}

Create a service instance that is named `my-service-instance` that uses service plan `test-service-plan` of service `test-service` on location `eu-gb`:
```bash
ibmcloud resource service-instance-create my-service-instance test-service test-service-plan eu-gb
```
{: codeblock}

## ibmcloud resource service-instance-update
{: #ibmcloud_resource_service_instance_update}

Update service instance.
```bash
ibmcloud resource service-instance-update ( NAME | ID ) [-n, --name NEW_NAME] [--service-plan-id SERVICE_PLAN_ID] [-p, --parameters @JSON_FILE | JSON_STRING ] [-g RESOURCE_GROUP] [--service-endpoints SERVICE_ENDPOINTS_TYPE] [-f, --force]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_service_instance_update_options}

Name (required)
:   Name of the service instance, exclusive with ID

ID (required)
:   ID of the service instance, exclusive with NAME

-n, --name *NEW_NAME*
:   New service instance name

--service-plan-id *SERVICE_PLAN_ID*
:   New Service Plan ID

-p, --parameters *@JSON_FILE | JSON_STRING*
:   JSON file or JSON string of parameters to create service instance

-g *RESOURCE_GROUP*
:   Resource group name

--service-endpoints *SERVICE_ENDPOINTS_TYPE*
:   Types of the service endpoints. Possible values are 'public', 'private', 'public-and-private'.

-f, --force
:   Force update without confirmation



### Examples
{: #ibmcloud_resource_service_instance_update_examples}

Update service instance `my-service-instance`, change its name to `new-service-instance`:
```bash
ibmcloud resource service-instance-update my-service-instance -n new-service-instance
```
{: codeblock}

## ibmcloud resource service-instance-delete
{: #ibmcloud_resource_service_instance_delete}

Delete the service instance. If provisioning is in progress, the command attempts to cancel the provisioning process. Some services might not support cancellation.
```bash
ibmcloud resource service-instance-delete (NAME|ID) [-f, --force] [--recursive]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_service_instance_delete_options}

Name (required)
:   Name of the service instance, exclusive with ID

ID (required)
:   ID of the service instance, exclusive with NAME

-f, --force
:   Force deletion without confirmation

--recursive
:   Delete all belonging resources



### Examples
{: #ibmcloud_resource_service_instance_delete_examples}

Delete resource service-instance `my-service-instance`:
```bash
ibmcloud resource service-instance-delete my-service-instance
```
{: codeblock}

## ibmcloud resource service-instance-lock
{: #ibmcloud_resource_service_instance_lock}

Lock service instance.
```bash
ibmcloud resource service-instance-lock ( NAME | ID ) [-g RESOURCE_GROUP] [-f, --force]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_service_instance_lock_options}

Name (required)
:   Name of the service instance, exclusive with ID

ID (required)
:   ID of the service instance, exclusive with NAME

-g *RESOURCE_GROUP*
:   Resource group name

-f, --force
:   Force locking without confirmation



### Examples
{: #ibmcloud_resource_service_instance_lock_examples}

Lock resource service-instance `my-service-instance`:
```bash
ibmcloud resource service-instance-lock my-service-instance
```
{: codeblock}

## ibmcloud resource service-instance-unlock
{: #ibmcloud_resource_service_instance_unlock}

Unlock the service instance.
```bash
ibmcloud resource service-instance-unlock ( NAME | ID ) [-g RESOURCE_GROUP] [-f, --force]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_service_instance_unlock_options}

Name (required)
:   Name of the service instance, exclusive with ID

ID (required)
:   ID of the service instance, exclusive with NAME

-g *RESOURCE_GROUP*
:   Resource group name

-f, --force
:   Force locking without confirmation



### Examples
{: #ibmcloud_resource_service_instance_unlock_examples}

Unlock resource service-instance `my-service-instance`:
```bash
ibmcloud resource service-instance-unlock my-service-instance
```
{: codeblock}

## ibmcloud resource service-keys
{: #ibmcloud_resource_service_keys}

List service keys of service instance.
```bash
ibmcloud resource service-keys [ --instance-id ID | --instance-name NAME ]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_service_keys_options}

--instance-id
:   Service Instance ID

--instance-name
:   Service Instance Name


### Examples
{: #ibmcloud_resource_service_keys_examples}

List service keys of service instance `my-service-instance`:
```bash
ibmcloud resource service-keys --instance-name my-service-instance
```
{: codeblock}

## ibmcloud resource service-key
{: #ibmcloud_resource_service_key}

Displays the details of any number of service keys, where the first *n* characters of the service key name matches the supplied KEY_NAME.
```bash
ibmcloud resource service-key (NAME | ID) [-g RESOURCE_GROUP] [--id]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_service_key_options}

NAME
:   Name of the key

ID
:   ID of the key

-g
:   Resource group name

--id
:   Display the ID of the service key. This option is exclusive with '--output'.

-g RESOURCE_GROUP
:   Resource group name

### Examples
{: #ibmcloud_resource_service_key_examples}

Show details of service keys `my-service-key`:
```bash
ibmcloud resource service-key my-service-key
```
{: codeblock}

Show details of service key with ID `crn:v1:bluemix:public:cloudantnosqldb:us-south:a/537860630a5ba7115be954e8d5aa5689:cc2a6d6c-8f5e-4038-b975-b09b51d1d8dc:resource-key:9057f12e-fbf5-421d-8865-764422217a79`:

```bash
ibmcloud resource service-key crn:v1:bluemix:public:cloudantnosqldb:us-south:a/537860630a5ba7115be954e8d5aa5689:cc2a6d6c-8f5e-4038-b975-b09b51d1d8dc:resource-key:9057f12e-fbf5-421d-8865-764422217a79
```
{: codeblock}

## ibmcloud resource service-key-create
{: #ibmcloud_resource_service_key_create}

Create a service key.
```bash
ibmcloud resource service-key-create NAME [ROLE_NAME] ( --instance-id SERVICE_INSTANCE_ID | --instance-name SERVICE_INSTANCE_NAME) [--service-id SERVICE_ID] [-p, --parameters @JSON_FILE | JSON_TEXT] [-g RESOURCE_GROUP] [--service-endpoint SERVICE_ENDPOINT_TYPE] [-f, --force] [-f, --force] [-q, --quiet]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_service_key_create_options}

NAME (required)
:   Name of the key.

ROLE_NAME (optional)
:   Name of the IAM service role. The specified role cannot be one of the default platform roles. You can verify the eligibility of any role for use with this option by running `ibmcloud iam roles --service <your-service>` and checking that `serviceRole` appears in the role's CRN.

--instance-id *SERVICE_INSTANCE_ID*
:   Service instance ID.

--instance-name *SERVICE_INSTANCE_NAME*
:   Service instance name.

--service-id *SERVICE_ID*
:   Name or UUID of the service ID, which the role belongs to. Can be set only when `ROLE_NAME` is omitted or is set to `None`.

-p, --parameters *@JSON_FILE | JSON_TEXT*
:   Parameters JSON file or JSON string.

-g *RESOURCE_GROUP*
:   Resource group name.

--service-endpoint *SERVICE_ENDPOINT_TYPE*
:   Type of the service endpoint. Possible values are 'public' or 'private'.

--output FORMAT (optional)
:   Specify the output format. Only JSON is supported.

-f, --force
:   Force creation without confirmation

-q, --quite
:   Suppress verbose output.



### Examples
{: #ibmcloud_resource_service_key_create_examples}

Create a service key named `my-service-key` with role `Administrator` for service instance `my-service-instance`:
```bash
ibmcloud resource service-key-create my-service-key Administrator --instance-name my-service-instance
```
{: codeblock}

Create a service key named `my-service-key` without any role for a non-iam-enabled service instance `my-service-instance`:
```bash
ibmcloud resource service-key-create my-service-key --instance-name my-service-instance
```
{: codeblock}

## ibmcloud resource service-key-update
{: #ibmcloud_resource_service_key_update}

Update a service key.
```bash
ibmcloud resource service-key-update ( NAME | ID ) [-n, --name NEW_NAME] [-g RESOURCE_GROUP] [-f, --force]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_service_key_update_options}

NAME | ID
:   Name or ID of the key

-n, --name NEW_NAME
:   New name of the key

-g RESOURCE_GROUP
:   ID of the resource group to which the key belongs

-f, --force
:   Force update without confirmation



### Examples
{: #ibmcloud_resource_service_key_update_examples}

Update a service key named `my-service-key`, give it a new name `my-service-key-2`:
```bash
ibmcloud resource service-key-update my-service-key -n my-service-key-2
```
{: codeblock}

## ibmcloud resource service-key-delete
{: #ibmcloud_resource_service_key_delete}

Delete a service key.
```bash
ibmcloud resource service-key-delete ( KEY_NAME | KEY_ID ) [-f, --force]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_service_key_delete_options}

KEY_NAME | KEY_ID
:   Name of the key or the ID of the key

-f, --force
:   Force deletion without confirmation



### Examples
{: #ibmcloud_resource_service_key_delete_examples}

Delete service key `my-service-key`:
```bash
ibmcloud resource service-key-delete my-service-key
```
{: codeblock}

## ibmcloud resource search
{: #ibmcloud_resource_search}

Search resources by using Lucene query syntax.
```bash
ibmcloud resource search LUCENE_QUERY [-o, --offset OFFSET] [-l, --limit LIMIT] [-s, --sort-by (name, family, region, type, crn)] [-p, --provider PROVIDER] [-ir, --is-reclaimed (false, true, any)] [--output FORMAT]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_search_options}

-ir, --is-reclaimed
:   Search for account resources that have been reclaimed. However, by default the search returns only active resources. You can set is-reclaimed to any to search for resources whether they are reclaimed or not. Set this option to `true` to apply the search criteria only to reclaimed resources. Set this option to `false` to search only for active resources. `false` is the default behavior.

-o, -offset
:   Starting resource position number

-l, -limit
:   Number of resources to return, up to a maximum of 10000.

-s, --sort-by
:   Property to sort by. Accepted values are `name`, `family`, `region`, `type`, `crn`.

-p, --provider
:   Display classic infrastructure resources. The only supported value is `classic-infrastructure`.

### Searchable attributes
{: #ibmcloud_resource_search_attributes}

You can search for many attributes to scope your search. A few examples are:

name
:   The user-defined name of the resource.

region
:   The geographical location where the resource is provisioned. For example: us-south, us-east, au-syd, eu-gb, eu-de, and jp-tok.

service_name
:   The name of the service as it appears in the Name column of the output of 'ibmcloud catalog service-marketplace'.

creation_date
:   The date on which the resource is created.

modification_date
:   The last modification date of the resource.

For the complete list of attributes that you can search for, see [Searching for resources](/docs/account?topic=account-manage_resource&interface=cli#searching-for-resources).

### Examples
{: #ibmcloud_resource_search_examples}

Search for Resource Controller resources in the specified location (that is, in us-south region):
```bash
ibmcloud resource search "region:us-south AND family:resource_controller"
```
{: codeblock}

Search for resource groups with name default:
```bash
ibmcloud resource search "name:default AND type:resource-group"
```
{: codeblock}

Search for a resource with the specified Cloud Resource Name (CRN):
```bash
ibmcloud resource search "crn:\"crn:v1:bluemix:public:cloudantnosqldb:us-south:s/4948af7e-cc78-4321-998a-e549dd5e9210:41a031cd-e9e5-4c46-975d-9e4a6391322e:cf-service-instance:\""
```
{: codeblock}

Search for a resource with the specified tag:
```bash
ibmcloud resource search "tags:\"mykey:myvalue\""
```
{: codeblock}

Search for Classic Infrastructure Virtual Guest resource with the specified id (only with -p classic-infrastructure):
```bash
ibmcloud resource search "id:12345678 _objectType:SoftLayer_Virtual_Guest"
```
{: codeblock}

Search for Classic Infrastructure Hardware resource with the specified tag name (only with -p classic-infrastructure):
```bash
ibmcloud resource search "tagReferences.tag.name:name _objectType:SoftLayer_Hardware"
```
{: codeblock}

## ibmcloud resource subscription
{: #ibmcloud_resource_subscription}

Show details of a subscription.

```bash
ibmcloud resource subscription SUBSCRIPTION_ID
```
{: codeblock}

### Command options
{: #ibmcloud_resource_subscription_options}

SUBSCRIPTION_ID (required)
:   SUBSCRIPTION_ID field of a subscription


### Examples
{: #ibmcloud_resource_subscription_examples}

Show details of subscription `my-subscription-id`:
```bash
ibmcloud resource subscription my-subscription-id
```
{: codeblock}

## ibmcloud resource subscriptions
{: #ibmcloud_resource_subscriptions}

List subscriptions for your account

```bash
ibmcloud resource subscriptions [--output FORMAT] 
```
{: codeblock}

### Command options
{: #ibmcloud_resource_subscriptions_options}

--output value
:   Specify the output format. Only JSON is supported now.


## ibmcloud resource tags
{: #ibmcloud_resource_tags}

List all tags in your billing account

```bash
ibmcloud resource tags [-o, --offset OFFSET] [-l, --limit LIMIT]  [-p, --provider classic-infrastructure] [-d, --details true] [-a, --attached true] [--output FORMAT] [--tag-type TAG_TYPE] [--account-id ACCOUNT_ID]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_tags_options}

--offset value, -o value
:   Starting resource position number (default: 0).

--limit value, -l value
:   Number of resources to return (maximum 1000) (default: 100).

--provider value, -p value
:   Display Classic Infrastructure resources, the only value that is allowed is: classic-infrastructure. Use it for resources of type SoftLayer_Hardware, SoftLayer_Network_Application_Delivery_Controller, SoftLayer_Network_Subnet_IpAddress or SoftLayer_Network_Vlan.

--details value, -d value
:   Show additional attributes for each tag, only value allowed is true.

--attached value, -a value
:   Show only filtered tags attached to a resource, only value allowed is true.

--tag-type value
:   Type of the tag. Only allowed values are: user, service, or access (default value : user).

--account-id value
:   The ID of the account that owns the tags that you want to list (required if tag-type is set to service).

--output value
:   Specify the output format. Only JSON is supported now.

-q, --quiet
:   Suppress verbose output.

## ibmcloud resource tag-create
{: #ibmcloud_resource_tag_create}

Create an access management tag:
```bash
ibmcloud resource tag-create --tag-names TAG_NAMES
```
{: codeblock}

### Command options
{: #ibmcloud_resource_tag_create_options}

--tag-names value
:   Comma-separated list of tag names.

-q, --quiet
:   Suppress verbose output.

This command is only valid for access management tags. For example:

* Run the following command to create the access management tag `project:myproject`:
   ```bash
   ibmcloud resource tag-create —tag-names “project:myproject”
   ```
   {: codeblock}

## ibmcloud resource tag-attach
{: #ibmcloud_resource_tag_attach}

Attach one or more tags to a resource:
```bash
ibmcloud resource tag-attach --tag-names TAG_NAMES (--resource-name NAME | --resource-id RESOURCE_ID | --resources-query RESOURCES_QUERY) [--resource-type RESOURCE_TYPE] [--tag-type TAG_TYPE] [--account-id ACCOUNT_ID] [--replace] [--update]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_tag_attach_options}

--tag-names value
:   Comma-separated list of tag names.

--resources-query value
:   Global Search query string to retrieve the resources on which the tags should be attached

--resource-name value
:   The name of the resource on which the tags must be attached.

--resource-id value
:   CRN of the resource on which the tags should be attached (for Classic Infrastructure resource, it is the ID of the resource).

--resource-type value
:   Type of the tag. Only allowed values are: user, service or access (default value : user).

--tag-type value
:   The type of the tag. The only allowed values are `user` or `service`. The default value is `user`.

--account-id value
:   The ID of the account that owns the resources to be tagged (required if tag-type is set to service).

--replace
:   The list of tag names replaces the current list of tag names that are attached to the resource.

--update
:   The tag names in the format `key:value` will be updated. The option has no effect on tag names that are not in that format.

-q, --quiet
:   Suppress verbose output.

### Examples
{: #ibmcloud_resource_tag_attach_examples}

* To attach `my-tag` user tag to a Kubernetes cluster named `MyCluster`, first identify the CRN of the cluster:
    ```bash
    ibmcloud resource search 'type:k8\-cluster AND name:MyCluster'
    ```
    {: codeblock}

    Take note of the CRN, which is a string similar to the following example:
    ```bash
    crn:v1:bluemix:public:containers-kubernetes:us-south:a/a27a4741a57dcf5c965939adb66fe1c7:a46242e638ca47b09f10e9a3cbe5687a::
    ```
    {: screen}

    To attach the tag, run the following command:
    ```bash
    ibmcloud resource tag-attach --tag-names my-tag --resource-id rn:v1:bluemix:public:containers-kubernetes:us-south:a/a27a4741a57dcf5c965939adb66fe1c7:a46242e638ca47b09f10e9a3cbe5687a::
    ```
    {: codeblock}

* To attach `my-tag` user tag to a resource named `MyResource`:
    ```bash
    ibmcloud resource tag-attach --tag-name my-tag --resource-name  'MyResource'
    ```
    {: codeblock}

* To attach `my-tag-1` and `my-tag-2` user tags to all the Kubernetes clusters deployed in `us-south`, run the following command:
    ```bash
    ibmcloud resource tag-attach --tag-names my-tag-1,my-tag-2 --resources-query 'service_name:containers-kubernetes AND region:us-south'
    ```
    {: codeblock}

    The command initially retrieves all Kubernetes clusters in us-south that you can view, and subsequently attaches the two specified tags to each.
    It then displays the outcome of the operation for every Kubernetes cluster.

* To attach `my-tag` user tag to a classic infrastructure virtual guest named `MyVM`, identify the virtual guest's ID:
    ```bash
    ibmcloud resource search 'fullyQualifiedDomainName:MyVM  _objectType:SoftLayer_Virtual_Guest' -p classic-infrastructure
    ```
    {: codeblock}

    Take a note of the ID, which is a string similar to `48373549`.

    To attach the tag, run the following command:
    ```bash
    ibmcloud resource tag-attach --tag-names my-tag --resource-id 48373549 --resource-type SoftLayer_Virtual_Guest
    ```
    {: codeblock}

* To attach the access management tag `project:myproject`, that you previously created, to an instance of IBM Cloud Object Storage called `Project data`, run the following command:
    ```bash
    ibmcloud resource tag-attach --tag-names "project:myproject" --resource-name Project data -—tag-type access
    ```
    {: codeblock}

* To update to `production` the value of the `env` user tag on a resource named `MyResource` run the following command:

    ```bash
    ibmcloud resource tag-attach --tag-names 'env:production' --resource-name 'MyResource' --update
    ```
    {: codeblock}

* To update to `production` the value of the `env` access management tag on a resource named `MyResource` run the following command:

    ```bash
    ibmcloud resource tag-attach --tag-names 'env:production' --resource-name 'MyResource' --update --tag-type access
    ```
    {: codeblock}

* To replace all user tags of `MyResource` with a new set of tags `tag1`, `tag2`, and `tag3` run the following command:

    ```bash
    ibmcloud resource tag-attach --tag-names 'tag1,tag2,tag3' --resource-name 'MyResource' --replace
    ```
    {: codeblock}

* To replace all access management tags of `MyResource` with the tag `compliance:hipaa` run the following command:

    ```bash
    ibmcloud resource tag-attach --tag-names 'compliance:hipaa' --resource-name 'MyResource' --replace --tag-type access
    ```
    {: codeblock}

## ibmcloud resource tag-detach
{: #ibmcloud_resource_tag_detach}

Detaching one or more tags from a resource:
```bash
ibmcloud resource tag-detach --tag-names TAG_NAMES (--resource-name NAME | --resource-id RESOURCE_ID | --resources-query RESOURCES_QUERY) [--resource-type RESOURCE_TYPE] [--tag-type TAG_TYPE] [--account-id ACCOUNT_ID]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_tag_detach_options}

--tag-names value
:   Comma-separated list of tag names.

--resources-query value
:   Global Search query string to retrieve the resources on which the tags should be detached

--resource-name value
:   The name of the resource on which the tags should be attached.

--resource-id value
:   CRN of the resource on which the tags should be attached (for Classic Infrastructure resource, it is the ID of the resource).

--resource-type value
:   Resource type on which the tags should be attached (required for Classic Infrastructure resource of type SoftLayer_Hardware, SoftLayer_Network_Application_Delivery_Controller, SoftLayer_Network_Subnet_IpAddress or SoftLayer_Network_Vlan only).

--tag-type value
:   Type of the tag. Only allowed values are: user, service, or access (default value : user).

--account-id value
:   The ID of the account that owns the resources to be detached (required if tag-type is set to service).

-q, --quiet
:   Suppress verbose output.

### Examples
{: #ibmcloud_resource_tag_detach_examples}

* To detach `my-tag` user tag from a Kubernetes cluster named `MyCluster`, first identify the CRN of the cluster:
    ```bash
    ibmcloud resource search 'type:k8\-cluster AND name:MyCluster'
    ```
    {: codeblock}

    Take note of the CRN, which is a string similar to the following example:
    ```bash
    crn:v1:bluemix:public:containers-kubernetes:us-south:a/a27a4741a57dcf5c965939adb66fe1c7:a46242e638ca47b09f10e9a3cbe5687a::
    ```
    {: screen}

    To detach the tag, run the following command:
    ```bash
    ibmcloud resource tag-detach --tag-names my-tag --resource-id crn:v1:bluemix:public:containers-kubernetes:us-south:a/a27a4741a57dcf5c965939adb66fe1c7:a46242e638ca47b09f10e9a3cbe5687a::
    ```
    {: codeblock}

* To detach `my-tag` user tag from a resource named `MyResource`:
    ```bash
    ibmcloud resource tag-detach --tag-name my-tag --resource-name 'MyResource'
    ```
    {: codeblock}

* To detach the user tags `my-tag-1` and `my-tag-2` from all the Kubernetes clusters deployed in `us-south`, run the following command:
    ```bash
    ibmcloud resource tag-detach --tag-names my-tag-1,my-tag-2 --resources-query 'service_name:containers-kubernetes AND region:us-south'
    ```
    {: codeblock}

    The command initially retrieves all Kubernetes clusters in us-south that you can view, and subsequently detaches the two specified tags from each.
    It then displays the outcome of the operation for every Kubernetes cluster.

* To detach `my-tag` user tag from a classic infrastructure virtual guest named `MyVM`, first look for the ID of the virtual guest you would like to detach the tag from:
    ```bash
    ibmcloud resource search 'fullyQualifiedDomainName:MyVM  _objectType:SoftLayer_Virtual_Guest' -p classic-infrastructure
    ```
    {: codeblock}

    Take a note of the ID, which is a string similar to `48373549`.

    To detach the tag, run the following command:
    ```bash
    ibmcloud resource tag-detach --tag-names my-tag --resource-id 48373549 --resource-type SoftLayer_Virtual_Guest
    ```
    {: codeblock}

* To detach the access management tag `project:myproject` from an instance of IBM Cloud Object Storage called `Project data`, run the following command:
    ```bash
    ibmcloud resource tag-detach --tag-names "project:myproject" --resource-name Project data -—tag-type access
    ```
    {: codeblock}

* To detach the `env:value` tag from `MyResource`, regardless of its value, run the following command:

    ```bash
    ibmcloud resource tag-detach --tag-names 'env:*' —resource-name 'MyResource'
    ```
    {: codeblock}

* To detach all tags from `MyResource` run the following command:

    ```bash
    ibmcloud resource tag-detach --tag-names '*' —resource-name 'MyResource'
    ```
    {: codeblock}

## ibmcloud resource tag-delete
{: #ibmcloud_resource_tag_delete}

Delete a tag:
```bash
ibmcloud resource tag-delete (--tag-name TAG_NAME | -a, --all  [-f, --force]) [-p, --provider PROVIDER] [--tag-type TAG_TYPE] [--account-id ACCOUNT_ID]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_tag_delete_options}

--tag-name value
:   Tag name to be deleted.

--provider value, -p value
:   Delete the tag in the specified provider (the only supported value is classic-infrastructure). Use it for resources of type SoftLayer_Hardware, SoftLayer_Network_Application_Delivery_Controller, SoftLayer_Network_Subnet_IpAddress or SoftLayer_Network_Vlan.

--tag-type value
:   Type of the tag. Only allowed values are: user, service, or access (default value : user).

account-id value
:   The ID of the account that owns the tags to be deleted (required if tag-type is set to service).

--force, -f
:   Delete the tags without confirmation.

--all, -a
:   Delete all tags that are not attached to any resources.

-q, --quiet
:   Suppress verbose output.



A tag can be deleted only if it isn't attached to any resource.

### Examples
{: #ibmcloud_resource_tag_delete_examples}

* To delete the user tag `my-tag` from the account:
    ```bash
    ibmcloud resource tag-delete --tag-name "my-tag"
    ```
    {: codeblock}

* To delete the access management tag `project:myproject` from the account:
    ```bash
    ibmcloud resource tag-delete --tag-name "project:myproject" --tag-type access
    ```
    {: codeblock}

* To delete all unused user tags from the account:
    ```bash
    ibmcloud resource tag-delete -a
    ```
    {: codeblock}

* To delete all unused access management tags from the account:
    ```bash
    ibmcloud resource tag-delete -a --tag-type access
    ```
    {: codeblock}


## ibmcloud resource reclamations
{: #ibmcloud_resource_reclamations}

List reclaimed resources that can be restored or deleted:
```bash
ibmcloud resource reclamations [--resource-instance-id INSTANCE_ID]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_reclamations_options}

--resource-instance-id
:   The globally unique ID (GUID) of the resource instance

### Examples
{: #ibmcloud_resource_reclamations_examples}

List all resource reclamations:
```bash
ibmcloud resource reclamations
```
{: codeblock}

List resource reclamations of a particular service instance:
```bash
ibmcloud resource reclamations --resource-instance-id abcd1234-ef56-486e-b293-22d6c7eb6699
```
{: codeblock}

## ibmcloud resource reclamation
{: #ibmcloud_resource_reclamation}

Show details of a resource reclamation:
```bash
ibmcloud resource reclamation RECLAMATION_ID
```
{: codeblock}

### Command options
{: #ibmcloud_resource_reclamation_options}

RECLAMATION_ID
:   Resource reclamation ID


### Examples
{: #ibmcloud_resource_reclamation_examples}

Show details of a resource reclamation:
```bash
ibmcloud resource reclamation daf12d343ef
```
{: codeblock}

## ibmcloud resource reclamation-restore
{: #ibmcloud_resource_reclamation_restore}

Restore a reclaimed resource so that the resource is available again:
```bash
ibmcloud resource reclamation-restore ID [--comment COMMENT]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_reclamation_restore_options}

ID
:   ID of the resource reclamation

--comment
:   Comments about the action


### Examples
{: #ibmcloud_resource_reclamation_restore_examples}

Restore a resource reclamation with ID `d9fendfwlw`:
```bash
ibmcloud resource reclamation-restore "d9fendfwlw"
```
{: codeblock}

Restore a resource reclamation with ID `d9fendfwlw`, leave a comment of `need to use for another 3 months`, and show JSON output:

```bash
ibmcloud resource reclamation-restore "d9fendfwlw" --comment "need to use for another 3 months" --output JSON
```
{: codeblock}

## ibmcloud resource reclamation-delete
{: #ibmcloud_resource_reclamation_delete}

Delete a reclaimed resource so that the resource can no longer be restored:
```bash
ibmcloud resource reclamation-delete ID [--comment COMMENT] [--f, --force]
```
{: codeblock}

### Command options
{: #ibmcloud_resource_reclamation_delete_options}

ID
:   ID of the resource reclamation

--comment
:   Comments about the action

-f, --force
:   Force deletion without confirmation


### Examples
{: #ibmcloud_resource_reclamation_delete_examples}

Delete a resource reclamation with ID `d9fendfwlw`:
```bash
ibmcloud resource reclamation-delete "d9fendfwlw"
```
{: codeblock}

Delete a resource reclamation with ID `d9fendfwlw` and leave a comment of `no longer needed` without confirmation:

```bash
ibmcloud resource reclamation-delete "d9fendfwlw" --comment "no longer needed" -f
```
{: codeblock}
