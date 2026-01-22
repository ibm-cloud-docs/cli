---

copyright:
  years: 2023, 2026
lastupdated: "2026-01-22"

subcollection: cli

keywords: project CLI, project command line , project terminal, project shell

---

{{site.data.keyword.attribute-definition-list}}

# Project CLI reference
{: #projects-cli}

The {{site.data.keyword.cloud}} command-line interface (IBM Cloud CLI) provides additional capabilities for service offerings. You can use the {{site.data.keyword.cloud_notm}} CLI to manage projects you have access to.
{: shortdesc}

## Before you begin
{: #projects-cli-prereq}

* Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
* Install the Project CLI by running the following command:

```sh
ibmcloud plugin install project
```
{: pre}

You're notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up to date so that you can use the latest commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
{: tip}

## Projects
{: #project-projects-cli}

Commands for Projects resource.

### `ibmcloud project create`
{: #project-cli-create-command}

Create a project and asynchronously setup the tools to manage it. Add a deployable architecture by customizing the configuration. After the changes are validated and approved, deploy the resources that the project configures. For more information, see [Creating a project](/docs/secure-enterprise?topic=secure-enterprise-setup-project&interface=ui).

```sh
ibmcloud project create [--definition DEFINITION | --definition-name DEFINITION-NAME --definition-description DEFINITION-DESCRIPTION --definition-auto-deploy-mode DEFINITION-AUTO-DEPLOY-MODE --definition-monitoring-enabled=DEFINITION-MONITORING-ENABLED --definition-destroy-on-delete=DEFINITION-DESTROY-ON-DELETE --definition-store DEFINITION-STORE --definition-terraform-engine DEFINITION-TERRAFORM-ENGINE --definition-auto-deploy=DEFINITION-AUTO-DEPLOY] --location LOCATION --resource-group RESOURCE-GROUP [--configs CONFIGS] [--environments ENVIRONMENTS]
```


#### Command options
{: #project-create-cli-options}

`--definition` ([`ProjectPrototypeDefinition`](#cli-project-prototype-definition-example-schema))
:   The definition of the project. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition=@path/to/file.json`.

`--location` (string)
:   The IBM Cloud location where a resource is deployed. Required.

    Allowable values are: `us-south`, `us-east`, `eu-gb`, `eu-de`, `ca-tor`.

`--resource-group` (string)
:   The resource group name where the project's data and tools are created. Required.

    The maximum length is `64` characters. The minimum length is `0` characters. The value must match regular expression `/^(?!\\s)(?!.*\\s$)[^'"`<>{}\\x00-\\x1F]*$/`.

`--configs` ([`ProjectConfigPrototype[]`](#cli-project-config-prototype-example-schema))
:   The project configurations. These configurations are included in the response of creating a project only if a configuration array is specified in the request payload.

    The default value is `[]`. The maximum length is `100` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--configs=@path/to/file.json`.

`--environments` ([`EnvironmentPrototype[]`](#cli-environment-prototype-example-schema))
:   The project environment. These environments are included in the response of creating a project only if an environment array is specified in the request payload.

    The default value is `[]`. The maximum length is `20` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--environments=@path/to/file.json`.

`--definition-name` (string)
:   The name of the project.  It's unique within the account across regions. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The maximum length is `128` characters. The minimum length is `1` character. The value must match regular expression `/^(?!\\s)(?!.*\\s$)[^'"`\/<>{}\\x00-\\x1F]+$/`.

`--definition-description` (string)
:   A brief explanation of the project's use in the configuration of a deployable architecture. A project can be created without providing a description. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The default value is ``. The maximum length is `1024` characters. The minimum length is `0` characters. The value must match regular expression `/^$|^(?!\\s)(?!.*\\s$)[^\\x00-\\x1F]*$/`.

`--definition-auto-deploy-mode` (string)
:   This is an advanced setting to auto deploy to tell how auto deploy should behave when it is enabled. There are 2 options:
> 1. `auto_approval` will automatically approve the configuration after validated without user confirmation.
> 2. `manual_approval` will require user confirmation to approve the configuration after validated before deploying the configuration starts. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The default value is `manual_approval`. Allowable values are: `auto_approval`, `manual_approval`.

`--definition-monitoring-enabled` (bool)
:   A boolean flag to enable automatic drift detection. Use this field to run a daily check to compare the configurations to those deployed resources to detect any difference. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The default value is `false`.

`--definition-destroy-on-delete` (bool)
:   The policy that indicates whether the resources are undeployed or not when a project is deleted. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The default value is `true`.

`--definition-store` ([`ProjectDefinitionStore`](#cli-project-definition-store-example-schema))
:   The details required to custom store project configs. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-store=@path/to/file.json`.

`--definition-terraform-engine` ([`ProjectTerraformEngineSettings`](#cli-project-terraform-engine-settings-example-schema))
:   Experimental schema - this is for prototyping purposes. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-terraform-engine=@path/to/file.json`.

`--definition-auto-deploy` (bool)
:   A boolean flag to enable deploying configurations automatically. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The default value is `false`.

#### Examples
{: #project-create-examples}

```sh
ibmcloud project create \
    --definition '{"name": "acme-microservice", "description": "A microservice to deploy on top of ACME infrastructure.", "auto_deploy_mode": "manual_approval", "monitoring_enabled": false, "destroy_on_delete": true, "store": {"type": "gh", "url": "exampleString", "token": "exampleString", "config_directory": "exampleString"}, "terraform_engine": {"id": "exampleString", "type": "terraform-enterprise"}, "auto_deploy": false}' \
    --location us-south \
    --resource-group Default \
    --configs '[{"definition": {"compliance_profile": {}, "locator_id": "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.018edf04-e772-4ca2-9785-03e8e03bef72-global", "members": [{"name": "exampleString", "config_id": "exampleString"}], "description": "The stage account configuration.", "name": "account-stage", "authorizations": {"trusted_profile_id": "exampleString", "method": "exampleString", "api_key": "exampleString"}, "inputs": {"anyKey": "anyValue"}, "settings": {"anyKey": "anyValue"}, "environment_id": "exampleString"}, "schematics": {"workspace_crn": "crn:v1:staging:public:project:us-south:a/4e1c48fcf8ac33c0a2441e4139f189ae:bf40ad13-b107-446a-8286-c6d576183bb1::"}}]' \
    --environments '[{"definition": {"description": "exampleString", "name": "exampleString", "authorizations": {"trusted_profile_id": "exampleString", "method": "exampleString", "api_key": "exampleString"}, "inputs": {"anyKey": "anyValue"}, "compliance_profile": {}}}]'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud project create \
    --location us-south \
    --resource-group Default \
    --configs '[projectConfigPrototype]' \
    --environments '[environmentPrototype]' \
    --definition-name exampleString \
    --definition-description exampleString \
    --definition-auto-deploy-mode manual_approval \
    --definition-monitoring-enabled=false \
    --definition-destroy-on-delete=true \
    --definition-store projectDefinitionStore \
    --definition-terraform-engine projectTerraformEngineSettings \
    --definition-auto-deploy=false
```
{: pre}

### `ibmcloud project list`
{: #project-cli-list-command}

List existing projects. Projects are sorted by ID.
Note: If the `--all-pages` option is not set, the command will only retrieve a single page of the collection.

```sh
ibmcloud project list [--token TOKEN] [--limit LIMIT]
```


#### Command options
{: #project-list-cli-options}

`--token` (string)
:   The server uses this parameter to determine the first entry that is returned on the next page. If this parameter is not specified, the logical first page is returned.

    The default value is ``. The maximum length is `1536` characters. The minimum length is `0` characters. The value must match regular expression `/^$|^(?!\\s)(?!.*\\s$)[^\\x00-\\x1F]*$/`.

`--limit` (int64)
:   The maximum number of resources to return. The number of resources that are returned is the same, except for the last page.

    The default value is `10`. The maximum value is `100`. The minimum value is `1`.

`--all-pages` (bool)
:   Invoke multiple requests to display all pages of the collection for list.

#### Example
{: #project-list-examples}

```sh
ibmcloud project list \
    --token exampleString \
    --limit 10
```
{: pre}

#### Example output
{: #project-list-cli-output}

An example request to list projects.

```json
{
  "limit" : 10,
  "first" : {
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
  },
  "next" : {
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/12349050-1234-ac97-0000-ba5a12fe9087"
  },
  "projects" : [ {
    "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
    "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
    "created_at" : "2023-02-22T19:51:23.253Z",
    "modified_at" : "2023-02-22T19:51:23.253Z",
    "href" : "https://projects.service.url/v1/projects/cfbf901-ab8e-ac97-b01b-ab5af830be8a",
    "definition" : {
      "description" : "A project example.",
      "name" : "iaas-infra-prestage-env",
      "destroy_on_delete" : false
    },
    "location" : "us-south",
    "state" : "ready",
    "resource_group" : "Default",
    "resource_group_id" : "f37d2637ea814cfd9a1742683a713d24",
    "cumulative_needs_attention_view" : [ {
      "event" : "project.instance.update"
    }, {
      "event_id" : "489f0090-6d7c-4af5-8f20-9106543e4974"
    }, {
      "config_id" : "069ab83e-5016-4bf2-bd50-cc95cf678293"
    }, {
      "config_version" : 1
    } ]
  }, {
    "id" : "1123ed42-4356-efa1-1101-235900fe9087",
    "created_at" : "2023-02-22T19:51:23.253Z",
    "modified_at" : "2023-02-22T19:51:23.253Z",
    "href" : "https://projects.service.url/v1/projects/cfbf901-ab8e-ac97-b01b-ab5af830be8a",
    "definition" : {
      "description" : "A project example.",
      "name" : "iaas-infra-stage-env",
      "destroy_on_delete" : false
    },
    "crn" : "crn:v1:staging:public:project:eu-de:a/06580d923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
    "location" : "eu-gb",
    "state" : "ready",
    "resource_group" : "Default",
    "resource_group_id" : "f37d2637ea814cfd9a1742683a713d24",
    "cumulative_needs_attention_view" : [ ]
  } ]
}
```
{: screen}

#### Default JMESPath
{: #project-list-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `projects[].{id: id, name: definition.name, state: state}` |
| Error | Default | - |
|  | Table | `projects[].{id: id, name: definition.name, state: state}` |
| All pages | Default | - |
|  | Table | `projects[].{id: id, name: definition.name, state: state}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud project get`
{: #project-cli-get-command}

Get information about a project.

```sh
ibmcloud project get --id ID
```


#### Command options
{: #project-get-cli-options}

`--id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

#### Example
{: #project-get-examples}

```sh
ibmcloud project get \
    --id exampleString
```
{: pre}

#### Example output
{: #project-get-cli-output}

A sample response for retrieving a project with configurations.

```json
{
  "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
  "created_at" : "2023-02-22T19:51:23.253Z",
  "modified_at" : "2023-02-22T19:51:23.253Z",
  "href" : "https://projects.service.url/v1/projects/cfbf901-ab8e-ac97-b01b-ab5af830be8a",
  "definition" : {
    "name" : "acme-microservice",
    "description" : "A microservice to deploy on top of ACME infrastructure.",
    "auto_deploy_mode" : "manual_approval",
    "auto_deploy" : false,
    "destroy_on_delete" : true,
    "monitoring_enabled" : false
  },
  "configs" : [ {
    "id" : "673d79e4-52bf-4184-b8e9-d3ca3c110f96",
    "created_at" : "2023-02-22T19:51:23.253Z",
    "deployment_model" : "project_deployed",
    "definition" : {
      "name" : "common-variables",
      "description" : "The common-variables configuration."
    },
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/configs/673d79e4-52bf-4184-b8e9-d3ca3c110f96",
    "is_draft" : true,
    "project" : {
      "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
      "definition" : {
        "name" : "iaas-infra-prestage-env"
      },
      "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
      "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
    },
    "state" : "draft",
    "modified_at" : "2023-02-22T19:51:23.253Z",
    "update_available" : false,
    "version" : 1
  }, {
    "id" : "4a1d4ba2-54ba-43a7-975a-d82b5a7612d1",
    "created_at" : "2023-02-22T19:51:23.253Z",
    "deployment_model" : "project_deployed",
    "definition" : {
      "name" : "account-stage",
      "description" : "The stage account configuration. The stage account hosts test environments prestage, performance, stage. This configuration configures services that are common to all these environments and regions. It's a `terraform_template` type of configuration that points to a GitHub repository that hosts the terraform modules that a Schematics workspace can deploy."
    },
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/configs/4a1d4ba2-54ba-43a7-975a-d82b5a7612d1",
    "is_draft" : true,
    "project" : {
      "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
      "definition" : {
        "name" : "iaas-infra-prestage-env"
      },
      "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
      "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
    },
    "state" : "draft",
    "update_available" : false,
    "modified_at" : "2023-02-22T19:51:23.253Z",
    "version" : 1
  }, {
    "id" : "293c3c36-a094-4115-a12b-de0a9ca39be5",
    "created_at" : "2023-02-22T19:51:23.253Z",
    "deployment_model" : "project_deployed",
    "definition" : {
      "name" : "env-stage",
      "description" : "The stage environment configuration. It includes services that are common to all the environment regions. A blueprint must be used to configure all the services that are common to the stage regions. It's a `terraform_template` type of configuration that points to a GitHub repository that hosts the Terraform modules that a Schematics workspace can deploy."
    },
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/configs/293c3c36-a094-4115-a12b-de0a9ca39be5",
    "is_draft" : true,
    "project" : {
      "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
      "definition" : {
        "name" : "iaas-infra-prestage-env"
      },
      "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
      "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
    },
    "state" : "draft",
    "update_available" : false,
    "modified_at" : "2023-02-22T19:51:23.253Z",
    "version" : 1
  }, {
    "id" : "596e8656-9d4b-41a5-8340-b0cbe8bd374a",
    "created_at" : "2023-02-22T19:51:23.253Z",
    "deployment_model" : "project_deployed",
    "definition" : {
      "name" : "region-us-south-stage",
      "description" : "The stage `us-south` configuration. A blueprint must be used to configure the Virtual Private Cloud and Red Hat OpenShift stage `us-south`."
    },
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/configs/596e8656-9d4b-41a5-8340-b0cbe8bd374a",
    "is_draft" : true,
    "project" : {
      "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
      "definition" : {
        "name" : "iaas-infra-prestage-env"
      },
      "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
      "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
    },
    "state" : "draft",
    "update_available" : false,
    "modified_at" : "2023-02-22T19:51:23.253Z",
    "version" : 1
  }, {
    "id" : "9c7afed6-17fb-4c56-a13d-440a78f936bd",
    "created_at" : "2023-02-22T19:51:23.253Z",
    "deployment_model" : "project_deployed",
    "definition" : {
      "name" : "region-eu-de-stage",
      "description" : "The stage `eu-de` configuration. A blueprint must be used to configure the Virtual Private Cloud and Red Hat OpenShift stage `eu-de`."
    },
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/configs/9c7afed6-17fb-4c56-a13d-440a78f936bd",
    "is_draft" : true,
    "project" : {
      "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
      "definition" : {
        "name" : "iaas-infra-prestage-env"
      },
      "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
      "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
    },
    "state" : "draft",
    "update_available" : false,
    "modified_at" : "2023-02-22T19:51:23.253Z",
    "version" : 1
  } ],
  "environments" : [ {
    "id" : "b0c44146-1ef6-40c2-82ba-74d51149770a",
    "definition" : {
      "name" : "dev-environment",
      "description" : "The development environment."
    },
    "project" : {
      "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
      "definition" : {
        "name" : "iaas-infra-prestage-env"
      },
      "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
      "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
    },
    "created_at" : "2023-02-10T10:05:35.787Z",
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/environments/b0c44146-1ef6-40c2-82ba-74d51149770a"
  } ],
  "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
  "cumulative_needs_attention_view" : [ {
    "event" : "project.instance.update"
  }, {
    "event_id" : "489f0090-6d7c-4af5-8f20-9106543e4974"
  }, {
    "config_id" : "069ab83e-5016-4bf2-bd50-cc95cf678293"
  }, {
    "config_version" : 1
  } ],
  "event_notifications_crn" : "crn:v1:staging:public:event-notifications:us-south:a/06580c923e40314421d3b6cb40c01c68:instance-id::",
  "location" : "us-south",
  "resource_group" : "Default",
  "resource_group_id" : "f37d2637ea814cfd9a1742683a713d24",
  "state" : "ready"
}
```
{: screen}

#### Default JMESPath
{: #project-get-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{id: id, name: definition.name, state: state}` |
| Error | Default | - |
|  | Table | `{id: id, name: definition.name, state: state}` |
| All pages | Default | - |
|  | Table | `{id: id, name: definition.name, state: state}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud project update`
{: #project-cli-update-command}

Update a project by specifying its ID.

```sh
ibmcloud project update --id ID [--definition DEFINITION | --definition-name DEFINITION-NAME --definition-description DEFINITION-DESCRIPTION --definition-auto-deploy-mode DEFINITION-AUTO-DEPLOY-MODE --definition-monitoring-enabled=DEFINITION-MONITORING-ENABLED --definition-destroy-on-delete=DEFINITION-DESTROY-ON-DELETE --definition-store DEFINITION-STORE --definition-terraform-engine DEFINITION-TERRAFORM-ENGINE --definition-auto-deploy=DEFINITION-AUTO-DEPLOY]
```


#### Command options
{: #project-update-cli-options}

`--id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--definition` ([`ProjectDefinitionPatch`](#cli-project-definition-patch-example-schema))
:   The definition of the project. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition=@path/to/file.json`.

`--definition-name` (string)
:   The name of the project.  It's unique within the account across regions. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The maximum length is `128` characters. The minimum length is `1` character. The value must match regular expression `/^(?!\\s)(?!.*\\s$)[^'"`\/<>{}\\x00-\\x1F]+$/`.

`--definition-description` (string)
:   A brief explanation of the project's use in the configuration of a deployable architecture. A project can be created without providing a description. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The maximum length is `1024` characters. The minimum length is `0` characters. The value must match regular expression `/^$|^(?!\\s)(?!.*\\s$)[^\\x00-\\x1F]*$/`.

`--definition-auto-deploy-mode` (string)
:   This is an advanced setting to auto deploy to tell how auto deploy should behave when it is enabled. There are 2 options:
> 1. `auto_approval` will automatically approve the configuration after validated without user confirmation.
> 2. `manual_approval` will require user confirmation to approve the configuration after validated before deploying the configuration starts. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Allowable values are: `auto_approval`, `manual_approval`.

`--definition-monitoring-enabled` (bool)
:   A boolean flag to enable automatic drift detection. Use this field to run a daily check to compare the configurations to the deployed resources to detect any difference. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

`--definition-destroy-on-delete` (bool)
:   The policy that indicates whether the resources are undeployed or not when a project is deleted. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

`--definition-store` ([`ProjectDefinitionStore`](#cli-project-definition-store-example-schema))
:   The details required to custom store project configs. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-store=@path/to/file.json`.

`--definition-terraform-engine` ([`ProjectTerraformEngineSettings`](#cli-project-terraform-engine-settings-example-schema))
:   Experimental schema - this is for prototyping purposes. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-terraform-engine=@path/to/file.json`.

`--definition-auto-deploy` (bool)
:   A boolean flag to enable deploying configurations automatically. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

#### Examples
{: #project-update-examples}

```sh
ibmcloud project update \
    --id exampleString \
    --definition '{"name": "acme-microservice", "description": "A microservice to deploy on top of ACME infrastructure.", "auto_deploy_mode": "auto_approval", "monitoring_enabled": true, "destroy_on_delete": true, "store": {"type": "gh", "url": "exampleString", "token": "exampleString", "config_directory": "exampleString"}, "terraform_engine": {"id": "exampleString", "type": "terraform-enterprise"}, "auto_deploy": true}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud project update \
    --id exampleString \
    --definition-name exampleString \
    --definition-description exampleString \
    --definition-auto-deploy-mode auto_approval \
    --definition-monitoring-enabled=true \
    --definition-destroy-on-delete=true \
    --definition-store projectDefinitionStore \
    --definition-terraform-engine projectTerraformEngineSettings \
    --definition-auto-deploy=true
```
{: pre}

#### Example output
{: #project-update-cli-output}

A sample response for retrieving a project with configurations.

```json
{
  "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
  "created_at" : "2023-02-22T19:51:23.253Z",
  "modified_at" : "2023-02-22T19:51:23.253Z",
  "href" : "https://projects.service.url/v1/projects/cfbf901-ab8e-ac97-b01b-ab5af830be8a",
  "definition" : {
    "name" : "acme-microservice",
    "description" : "A microservice to deploy on top of ACME infrastructure.",
    "auto_deploy_mode" : "manual_approval",
    "auto_deploy" : false,
    "destroy_on_delete" : true,
    "monitoring_enabled" : false
  },
  "configs" : [ {
    "id" : "673d79e4-52bf-4184-b8e9-d3ca3c110f96",
    "created_at" : "2023-02-22T19:51:23.253Z",
    "deployment_model" : "project_deployed",
    "definition" : {
      "name" : "common-variables",
      "description" : "The common-variables configuration."
    },
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/configs/673d79e4-52bf-4184-b8e9-d3ca3c110f96",
    "is_draft" : true,
    "project" : {
      "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
      "definition" : {
        "name" : "iaas-infra-prestage-env"
      },
      "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
      "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
    },
    "state" : "draft",
    "modified_at" : "2023-02-22T19:51:23.253Z",
    "update_available" : false,
    "version" : 1
  }, {
    "id" : "4a1d4ba2-54ba-43a7-975a-d82b5a7612d1",
    "created_at" : "2023-02-22T19:51:23.253Z",
    "deployment_model" : "project_deployed",
    "definition" : {
      "name" : "account-stage",
      "description" : "The stage account configuration. The stage account hosts test environments prestage, performance, stage. This configuration configures services that are common to all these environments and regions. It's a `terraform_template` type of configuration that points to a GitHub repository that hosts the terraform modules that a Schematics workspace can deploy."
    },
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/configs/4a1d4ba2-54ba-43a7-975a-d82b5a7612d1",
    "is_draft" : true,
    "project" : {
      "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
      "definition" : {
        "name" : "iaas-infra-prestage-env"
      },
      "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
      "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
    },
    "state" : "draft",
    "update_available" : false,
    "modified_at" : "2023-02-22T19:51:23.253Z",
    "version" : 1
  }, {
    "id" : "293c3c36-a094-4115-a12b-de0a9ca39be5",
    "created_at" : "2023-02-22T19:51:23.253Z",
    "deployment_model" : "project_deployed",
    "definition" : {
      "name" : "env-stage",
      "description" : "The stage environment configuration. It includes services that are common to all the environment regions. A blueprint must be used to configure all the services that are common to the stage regions. It's a `terraform_template` type of configuration that points to a GitHub repository that hosts the Terraform modules that a Schematics workspace can deploy."
    },
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/configs/293c3c36-a094-4115-a12b-de0a9ca39be5",
    "is_draft" : true,
    "project" : {
      "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
      "definition" : {
        "name" : "iaas-infra-prestage-env"
      },
      "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
      "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
    },
    "state" : "draft",
    "update_available" : false,
    "modified_at" : "2023-02-22T19:51:23.253Z",
    "version" : 1
  }, {
    "id" : "596e8656-9d4b-41a5-8340-b0cbe8bd374a",
    "created_at" : "2023-02-22T19:51:23.253Z",
    "deployment_model" : "project_deployed",
    "definition" : {
      "name" : "region-us-south-stage",
      "description" : "The stage `us-south` configuration. A blueprint must be used to configure the Virtual Private Cloud and Red Hat OpenShift stage `us-south`."
    },
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/configs/596e8656-9d4b-41a5-8340-b0cbe8bd374a",
    "is_draft" : true,
    "project" : {
      "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
      "definition" : {
        "name" : "iaas-infra-prestage-env"
      },
      "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
      "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
    },
    "state" : "draft",
    "update_available" : false,
    "modified_at" : "2023-02-22T19:51:23.253Z",
    "version" : 1
  }, {
    "id" : "9c7afed6-17fb-4c56-a13d-440a78f936bd",
    "created_at" : "2023-02-22T19:51:23.253Z",
    "deployment_model" : "project_deployed",
    "definition" : {
      "name" : "region-eu-de-stage",
      "description" : "The stage `eu-de` configuration. A blueprint must be used to configure the Virtual Private Cloud and Red Hat OpenShift stage `eu-de`."
    },
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/configs/9c7afed6-17fb-4c56-a13d-440a78f936bd",
    "is_draft" : true,
    "project" : {
      "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
      "definition" : {
        "name" : "iaas-infra-prestage-env"
      },
      "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
      "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
    },
    "state" : "draft",
    "update_available" : false,
    "modified_at" : "2023-02-22T19:51:23.253Z",
    "version" : 1
  } ],
  "environments" : [ {
    "id" : "b0c44146-1ef6-40c2-82ba-74d51149770a",
    "definition" : {
      "name" : "dev-environment",
      "description" : "The development environment."
    },
    "project" : {
      "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
      "definition" : {
        "name" : "iaas-infra-prestage-env"
      },
      "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
      "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
    },
    "created_at" : "2023-02-10T10:05:35.787Z",
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/environments/b0c44146-1ef6-40c2-82ba-74d51149770a"
  } ],
  "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
  "cumulative_needs_attention_view" : [ {
    "event" : "project.instance.update"
  }, {
    "event_id" : "489f0090-6d7c-4af5-8f20-9106543e4974"
  }, {
    "config_id" : "069ab83e-5016-4bf2-bd50-cc95cf678293"
  }, {
    "config_version" : 1
  } ],
  "event_notifications_crn" : "crn:v1:staging:public:event-notifications:us-south:a/06580c923e40314421d3b6cb40c01c68:instance-id::",
  "location" : "us-south",
  "resource_group" : "Default",
  "resource_group_id" : "f37d2637ea814cfd9a1742683a713d24",
  "state" : "ready"
}
```
{: screen}

### `ibmcloud project delete`
{: #project-cli-delete-command}

Delete a project document by specifying the ID. A project can be deleted only after deleting all of its resources.

```sh
ibmcloud project delete --id ID
```


#### Command options
{: #project-delete-cli-options}

`--id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

#### Example
{: #project-delete-examples}

```sh
ibmcloud project delete \
    --id exampleString
```
{: pre}

#### Example output
{: #project-delete-cli-output}

The example response to a request to delete a project.

```json
{
  "id" : "4059955c-ccb3-4fd3-aa48-34e3b8334f80"
}
```
{: screen}

## Environments
{: #project-environments-cli}

Commands for Environments resource.

### `ibmcloud project environment-create`
{: #project-cli-environment-create-command}

Create an environment to group related configurations together and share values across them for easier deployment. For more information, see [Creating an environment](/docs/secure-enterprise?topic=secure-enterprise-create-env).

```sh
ibmcloud project environment-create --project-id PROJECT-ID [--definition DEFINITION | --definition-description DEFINITION-DESCRIPTION --definition-name DEFINITION-NAME --definition-authorizations DEFINITION-AUTHORIZATIONS --definition-inputs DEFINITION-INPUTS --definition-compliance-profile DEFINITION-COMPLIANCE-PROFILE]
```


#### Command options
{: #project-environment-create-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--definition` ([`EnvironmentDefinitionRequiredProperties`](#cli-environment-definition-required-properties-example-schema))
:   The environment definition. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition=@path/to/file.json`.

`--definition-description` (string)
:   The description of the environment. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The default value is ``. The maximum length is `1024` characters. The minimum length is `0` characters. The value must match regular expression `/^$|^(?!\\s)(?!.*\\s$)[^\\x00-\\x1F]*$/`.

`--definition-name` (string)
:   The name of the environment. It's unique within the account across projects and regions. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The maximum length is `128` characters. The minimum length is `1` character. The value must match regular expression `/^(?!\\s)(?!.*\\s$)[^'"`<>{}\\x00-\\x1F]+$/`.

`--definition-authorizations` ([`ProjectConfigAuth`](#cli-project-config-auth-example-schema))
:   The authorization details. You can authorize by using a trusted profile or an API key in Secrets Manager. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-authorizations=@path/to/file.json`.

`--definition-inputs` (generic map)
:   The input variables that are used for configuration definition and environment. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-inputs=@path/to/file.json`.

`--definition-compliance-profile` ([`ProjectComplianceProfile`](#cli-project-compliance-profile-example-schema))
:   The profile that is required for compliance. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-compliance-profile=@path/to/file.json`.

#### Examples
{: #project-environment-create-examples}

```sh
ibmcloud project environment-create \
    --project-id exampleString \
    --definition '{"description": "The environment development.", "name": "development", "authorizations": {"trusted_profile_id": "Profile-9ac10c5c-195c-41ef-b465-68a6b6dg5f12", "method": "trusted_profile", "api_key": "exampleString"}, "inputs": {"anyKey": "anyValue"}, "compliance_profile": {"id": "some-profile-id", "instance_id": "some-instance-id", "instance_location": "us-south", "attachment_id": "some-attachment-id", "profile_name": "some-profile-name", "wp_policy_id": "exampleString", "wp_instance_id": "exampleString", "wp_instance_name": "exampleString", "wp_instance_location": "us-south", "wp_zone_id": "exampleString", "wp_zone_name": "exampleString", "wp_policy_name": "exampleString"}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud project environment-create \
    --project-id exampleString \
    --definition-description exampleString \
    --definition-name exampleString \
    --definition-authorizations projectConfigAuth \
    --definition-inputs '{"anyKey": "anyValue"}' \
    --definition-compliance-profile projectComplianceProfile
```
{: pre}

#### Example output
{: #project-environment-create-cli-output}

The sample environment response.

```json
{
  "id" : "env123",
  "definition" : {
    "name" : "development",
    "description" : "The environment development.",
    "authorizations" : {
      "method" : "trusted_profile",
      "trusted_profile_id" : "Profile-9ac10c5c-195c-41ef-b465-68a6b6dg5f12"
    },
    "inputs" : {
      "resource_group" : "stage",
      "region" : "us-south"
    },
    "compliance_profile" : {
      "id" : "some-profile-id",
      "instance_id" : "some-instance-id",
      "instance_location" : "us-south",
      "profile_name" : "some-profile-name",
      "attachment_id" : "some-attachment-id"
    }
  },
  "project" : {
    "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
    "definition" : {
      "name" : "iaas-infra-prestage-env"
    },
    "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
  },
  "created_at" : "2023-06-29T03:28:14.709Z",
  "modified_at" : "2023-06-29T03:28:14.709Z",
  "href" : "https://projects.api.cloud.ibm.com/v1/projects/6fd53106-7ce6-429e-8c57-f22e832d0c4b/environments/2102afed-94c7-46fe-90f2-7fff290637b4"
}
```
{: screen}

### `ibmcloud project environments`
{: #project-cli-environments-command}

List all available environments. For more information, see [Creating an environment](/docs/secure-enterprise?topic=secure-enterprise-create-env).
Note: If the `--all-pages` option is not set, the command will only retrieve a single page of the collection.

```sh
ibmcloud project environments --project-id PROJECT-ID [--token TOKEN] [--limit LIMIT]
```


#### Command options
{: #project-environments-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--token` (string)
:   The server uses this parameter to determine the first entry that is returned on the next page. If this parameter is not specified, the logical first page is returned.

    The default value is ``. The maximum length is `1536` characters. The minimum length is `0` characters. The value must match regular expression `/^$|^(?!\\s)(?!.*\\s$)[^\\x00-\\x1F]*$/`.

`--limit` (int64)
:   The maximum number of resources to return. The number of resources that are returned is the same, except for the last page.

    The default value is `10`. The maximum value is `100`. The minimum value is `1`.

`--all-pages` (bool)
:   Invoke multiple requests to display all pages of the collection for environments.

#### Example
{: #project-environments-examples}

```sh
ibmcloud project environments \
    --project-id exampleString \
    --token exampleString \
    --limit 10
```
{: pre}

#### Example output
{: #project-environments-cli-output}

The sample environment response for a list.

```json
{
  "limit" : 1,
  "first" : {
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/environments?limit=1"
  },
  "next" : {
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/environments?limit=1&token=da969bff-vf9q-3t1t-b677-d6rt5c0de54e"
  },
  "environments" : [ {
    "id" : "env123",
    "definition" : {
      "name" : "development",
      "description" : "The environment development.",
      "authorizations" : {
        "method" : "trusted_profile",
        "trusted_profile_id" : "Profile-9ac10c5c-195c-41ef-b465-68a6b6dg5f12"
      },
      "inputs" : {
        "resource_group" : "stage",
        "region" : "us-south"
      },
      "compliance_profile" : {
        "id" : "some-profile-id",
        "instance_id" : "some-instance-id",
        "instance_location" : "us-south",
        "profile_name" : "some-profile-name",
        "attachment_id" : "some-attachment-id"
      }
    },
    "project" : {
      "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
      "definition" : {
        "name" : "iaas-infra-prestage-env"
      },
      "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
      "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
    },
    "created_at" : "2023-06-29T03:28:14.709Z",
    "modified_at" : "2023-06-29T03:28:14.709Z",
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/6fd53106-7ce6-429e-8c57-f22e832d0c4b/environments/2102afed-94c7-46fe-90f2-7fff290637b4"
  } ]
}
```
{: screen}

### `ibmcloud project environment`
{: #project-cli-environment-command}

Get an environment. [Learn more](/docs/secure-enterprise?topic=secure-enterprise-create-env).

```sh
ibmcloud project environment --project-id PROJECT-ID --id ID
```


#### Command options
{: #project-environment-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The environment ID. Required.

    The maximum length is `256` characters. The minimum length is `1` character. The value must match regular expression `/^(?!\\s)(?!.*\\s$).+$/`.

#### Example
{: #project-environment-examples}

```sh
ibmcloud project environment \
    --project-id exampleString \
    --id exampleString
```
{: pre}

#### Example output
{: #project-environment-cli-output}

The sample environment response.

```json
{
  "id" : "env123",
  "definition" : {
    "name" : "development",
    "description" : "The environment development.",
    "authorizations" : {
      "method" : "trusted_profile",
      "trusted_profile_id" : "Profile-9ac10c5c-195c-41ef-b465-68a6b6dg5f12"
    },
    "inputs" : {
      "resource_group" : "stage",
      "region" : "us-south"
    },
    "compliance_profile" : {
      "id" : "some-profile-id",
      "instance_id" : "some-instance-id",
      "instance_location" : "us-south",
      "profile_name" : "some-profile-name",
      "attachment_id" : "some-attachment-id"
    }
  },
  "project" : {
    "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
    "definition" : {
      "name" : "iaas-infra-prestage-env"
    },
    "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
  },
  "created_at" : "2023-06-29T03:28:14.709Z",
  "modified_at" : "2023-06-29T03:28:14.709Z",
  "href" : "https://projects.api.cloud.ibm.com/v1/projects/6fd53106-7ce6-429e-8c57-f22e832d0c4b/environments/2102afed-94c7-46fe-90f2-7fff290637b4"
}
```
{: screen}

### `ibmcloud project environment-update`
{: #project-cli-environment-update-command}

Update an environment by specifying its ID. [Learn more](/docs/secure-enterprise?topic=secure-enterprise-create-env).

```sh
ibmcloud project environment-update --project-id PROJECT-ID --id ID [--definition DEFINITION | --definition-description DEFINITION-DESCRIPTION --definition-name DEFINITION-NAME --definition-authorizations DEFINITION-AUTHORIZATIONS --definition-inputs DEFINITION-INPUTS --definition-compliance-profile DEFINITION-COMPLIANCE-PROFILE]
```


#### Command options
{: #project-environment-update-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The environment ID. Required.

    The maximum length is `256` characters. The minimum length is `1` character. The value must match regular expression `/^(?!\\s)(?!.*\\s$).+$/`.

`--definition` ([`EnvironmentDefinitionPropertiesPatch`](#cli-environment-definition-properties-patch-example-schema))
:   The environment definition that is used for updates. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition=@path/to/file.json`.

`--definition-description` (string)
:   The description of the environment. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The maximum length is `1024` characters. The minimum length is `0` characters. The value must match regular expression `/^$|^(?!\\s)(?!.*\\s$)[^\\x00-\\x1F]*$/`.

`--definition-name` (string)
:   The name of the environment. It's unique within the account across projects and regions. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The maximum length is `128` characters. The minimum length is `1` character. The value must match regular expression `/^(?!\\s)(?!.*\\s$)[^'"`<>{}\\x00-\\x1F]+$/`.

`--definition-authorizations` ([`ProjectConfigAuth`](#cli-project-config-auth-example-schema))
:   The authorization details. You can authorize by using a trusted profile or an API key in Secrets Manager. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-authorizations=@path/to/file.json`.

`--definition-inputs` (generic map)
:   The input variables that are used for configuration definition and environment. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-inputs=@path/to/file.json`.

`--definition-compliance-profile` ([`ProjectComplianceProfile`](#cli-project-compliance-profile-example-schema))
:   The profile that is required for compliance. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-compliance-profile=@path/to/file.json`.

#### Examples
{: #project-environment-update-examples}

```sh
ibmcloud project environment-update \
    --project-id exampleString \
    --id exampleString \
    --definition '{"description": "The environment development.", "name": "development", "authorizations": {"trusted_profile_id": "Profile-9ac10c5c-195c-41ef-b465-68a6b6dg5f12", "method": "trusted_profile", "api_key": "exampleString"}, "inputs": {"anyKey": "anyValue"}, "compliance_profile": {"id": "some-profile-id", "instance_id": "some-instance-id", "instance_location": "us-south", "attachment_id": "some-attachment-id", "profile_name": "some-profile-name", "wp_policy_id": "exampleString", "wp_instance_id": "exampleString", "wp_instance_name": "exampleString", "wp_instance_location": "us-south", "wp_zone_id": "exampleString", "wp_zone_name": "exampleString", "wp_policy_name": "exampleString"}}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud project environment-update \
    --project-id exampleString \
    --id exampleString \
    --definition-description exampleString \
    --definition-name exampleString \
    --definition-authorizations projectConfigAuth \
    --definition-inputs '{"anyKey": "anyValue"}' \
    --definition-compliance-profile projectComplianceProfile
```
{: pre}

#### Example output
{: #project-environment-update-cli-output}

The sample environment response.

```json
{
  "id" : "env123",
  "definition" : {
    "name" : "development",
    "description" : "The environment development.",
    "authorizations" : {
      "method" : "trusted_profile",
      "trusted_profile_id" : "Profile-9ac10c5c-195c-41ef-b465-68a6b6dg5f12"
    },
    "inputs" : {
      "resource_group" : "stage",
      "region" : "us-south"
    },
    "compliance_profile" : {
      "id" : "some-profile-id",
      "instance_id" : "some-instance-id",
      "instance_location" : "us-south",
      "profile_name" : "some-profile-name",
      "attachment_id" : "some-attachment-id"
    }
  },
  "project" : {
    "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
    "definition" : {
      "name" : "iaas-infra-prestage-env"
    },
    "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
  },
  "created_at" : "2023-06-29T03:28:14.709Z",
  "modified_at" : "2023-06-29T03:28:14.709Z",
  "href" : "https://projects.api.cloud.ibm.com/v1/projects/6fd53106-7ce6-429e-8c57-f22e832d0c4b/environments/2102afed-94c7-46fe-90f2-7fff290637b4"
}
```
{: screen}

### `ibmcloud project environment-delete`
{: #project-cli-environment-delete-command}

Delete an environment in a project by specifying its ID.

```sh
ibmcloud project environment-delete --project-id PROJECT-ID --id ID
```


#### Command options
{: #project-environment-delete-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The environment ID. Required.

    The maximum length is `256` characters. The minimum length is `1` character. The value must match regular expression `/^(?!\\s)(?!.*\\s$).+$/`.

#### Example
{: #project-environment-delete-examples}

```sh
ibmcloud project environment-delete \
    --project-id exampleString \
    --id exampleString
```
{: pre}

#### Example output
{: #project-environment-delete-cli-output}

The sample environment delete response.

```json
{
  "id" : "env123"
}
```
{: screen}

## Configurations
{: #project-configurations-cli}

Commands for Configurations resource.

### `ibmcloud project config-create`
{: #project-cli-config-create-command}

Add a new configuration to a project.

```sh
ibmcloud project config-create --project-id PROJECT-ID [--definition DEFINITION | --definition-compliance-profile DEFINITION-COMPLIANCE-PROFILE --definition-locator-id DEFINITION-LOCATOR-ID --definition-members DEFINITION-MEMBERS --definition-description DEFINITION-DESCRIPTION --definition-name DEFINITION-NAME --definition-authorizations DEFINITION-AUTHORIZATIONS --definition-inputs DEFINITION-INPUTS --definition-settings DEFINITION-SETTINGS --definition-environment-id DEFINITION-ENVIRONMENT-ID --definition-resource-crns DEFINITION-RESOURCE-CRNS] [--schematics SCHEMATICS | --schematics-workspace-crn SCHEMATICS-WORKSPACE-CRN]
```


#### Command options
{: #project-config-create-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--definition` ([`ProjectConfigDefinitionPrototype`](#cli-project-config-definition-prototype-example-schema))
:   This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition=@path/to/file.json`.

`--schematics` ([`SchematicsWorkspace`](#cli-schematics-workspace-example-schema))
:   A Schematics workspace to use for deploying this deployable architecture.
> If importing data from an existing Schematics workspace that is not backed by cart, then a `locator_id` must be provided. If using a Schematics workspace that is backed by cart, a `locator_id` is not required because the Schematics workspace has one.
>
There are 3 scenarios:
> 1. If only a `locator_id` is specified, a new Schematics workspace is instantiated with that `locator_id`.
> 2. If only a schematics `workspace_crn` is specified, a `400` is returned if a `locator_id` is not found in the existing schematics workspace.
> 3. If both a Schematics `workspace_crn` and a `locator_id` are specified, a `400`code  is returned if the specified `locator_id` does not agree with the `locator_id` in the existing Schematics workspace.
>
For more information, see [Creating workspaces and importing the Terraform template](/docs/schematics?topic=schematics-sch-create-wks). This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--schematics=@path/to/file.json`.

`--definition-compliance-profile` ([`ProjectComplianceProfile`](#cli-project-compliance-profile-example-schema))
:   The profile that is required for compliance. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-compliance-profile=@path/to/file.json`.

`--definition-locator-id` (string)
:   A unique concatenation of the catalog ID and the version ID that identify the deployable architecture in the catalog. If importing from an existing Schematics workspace that is not backed by cart, a `locator_id` is required. If using a Schematics workspace that is backed by cart, a `locator_id` is not necessary because the Schematics workspace has one.
> There are 3 scenarios:
> 1. If only a `locator_id` is specified, a new Schematics workspace is instantiated with that `locator_id`.
> 2. If only a schematics `workspace_crn` is specified, a `400` is returned if a `locator_id` is not found in the existing schematics workspace.
> 3. If both a Schematics `workspace_crn` and a `locator_id` are specified, a `400` message is returned if the specified `locator_id` does not agree with the `locator_id` in the existing Schematics workspace.
> For more information of creating a Schematics workspace, see [Creating workspaces and importing the Terraform template](/docs/schematics?topic=schematics-sch-create-wks). This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The maximum length is `512` characters. The minimum length is `1` character. The value must match regular expression `/^(?!\\s)(?!.*\\s$)[\\.0-9a-z-A-Z_-]+$/`.

`--definition-members` ([`StackMember[]`](#cli-stack-member-example-schema))
:   The member deployable architectures that are included in the stack. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The maximum length is `100` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-members=@path/to/file.json`.

`--definition-description` (string)
:   A project configuration description. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The default value is ``. The maximum length is `1024` characters. The minimum length is `0` characters. The value must match regular expression `/^$|^(?!\\s)(?!.*\\s$)[^\\x00-\\x1F]*$/`.

`--definition-name` (string)
:   The configuration name. It's unique within the account across projects and regions. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The maximum length is `128` characters. The minimum length is `1` character. The value must match regular expression `/^[a-zA-Z0-9][a-zA-Z0-9-_ ]*$/`.

`--definition-authorizations` ([`ProjectConfigAuth`](#cli-project-config-auth-example-schema))
:   The authorization details. You can authorize by using a trusted profile or an API key in Secrets Manager. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-authorizations=@path/to/file.json`.

`--definition-inputs` (generic map)
:   The input variables that are used for configuration definition and environment. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-inputs=@path/to/file.json`.

`--definition-settings` (generic map)
:   The Schematics environment variables to use to deploy the configuration. Settings are only available if they are specified when the configuration is initially created. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-settings=@path/to/file.json`.

`--definition-environment-id` (string)
:   The ID of the project environment. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--definition-resource-crns` ([]string)
:   The CRNs of the resources that are associated with this configuration. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The list items must match regular expression `/^(?!\\s)(?!.*\\s$)(crn)[^'"`<>{}\\s\\x00-\\x1F]*$/`. The maximum length is `110` items. The minimum length is `0` items.

`--schematics-workspace-crn` (string)
:   An IBM Cloud resource name that uniquely identifies a resource. This option provides a value for a sub-field of the JSON option 'schematics'. It is mutually exclusive with that option.

    The maximum length is `512` characters. The minimum length is `4` characters. The value must match regular expression `/^(?!\\s)(?!.*\\s$)(crn)[^'"`<>{}\\s\\x00-\\x1F]*$/`.

#### Examples
{: #project-config-create-examples}

```sh
ibmcloud project config-create \
    --project-id exampleString \
    --definition '{"compliance_profile": {}, "locator_id": "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.018edf04-e772-4ca2-9785-03e8e03bef72-global", "members": [{"name": "exampleString", "config_id": "exampleString"}], "description": "The stage environment configuration.", "name": "env-stage", "authorizations": {"trusted_profile_id": "exampleString", "method": "exampleString", "api_key": "exampleString"}, "inputs": {"anyKey": "anyValue"}, "settings": {"anyKey": "anyValue"}, "environment_id": "exampleString"}' \
    --schematics '{"workspace_crn": "crn:v1:staging:public:project:us-south:a/4e1c48fcf8ac33c0a2441e4139f189ae:bf40ad13-b107-446a-8286-c6d576183bb1::"}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud project config-create \
    --project-id exampleString \
    --definition-compliance-profile projectComplianceProfile \
    --definition-locator-id exampleString \
    --definition-members '[stackMember]' \
    --definition-description exampleString \
    --definition-name exampleString \
    --definition-authorizations projectConfigAuth \
    --definition-inputs '{"anyKey": "anyValue"}' \
    --definition-settings '{"anyKey": "anyValue"}' \
    --definition-environment-id exampleString \
    --schematics-workspace-crn crn:v1:staging:public:project:us-south:a/4e1c48fcf8ac33c0a2441e4139f189ae:bf40ad13-b107-446a-8286-c6d576183bb1::
```
{: pre}

### `ibmcloud project configs`
{: #project-cli-configs-command}

Retrieve the collection of configurations.
Note: If the `--all-pages` option is not set, the command will only retrieve a single page of the collection.

```sh
ibmcloud project configs --project-id PROJECT-ID [--token TOKEN] [--limit LIMIT]
```


#### Command options
{: #project-configs-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--token` (string)
:   The server uses this parameter to determine the first entry that is returned on the next page. If this parameter is not specified, the logical first page is returned.

    The default value is ``. The maximum length is `1536` characters. The minimum length is `0` characters. The value must match regular expression `/^$|^(?!\\s)(?!.*\\s$)[^\\x00-\\x1F]*$/`.

`--limit` (int64)
:   The maximum number of resources to return. The number of resources that are returned is the same, except for the last page.

    The default value is `10`. The maximum value is `100`. The minimum value is `1`.

`--all-pages` (bool)
:   Invoke multiple requests to display all pages of the collection for configs.

#### Example
{: #project-configs-examples}

```sh
ibmcloud project configs \
    --project-id exampleString \
    --token exampleString \
    --limit 10
```
{: pre}

#### Example output
{: #project-configs-cli-output}

The example response for a request to get project configurations.

```json
{
  "limit" : 2,
  "first" : {
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/configs?limit=2"
  },
  "next" : {
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/configs?limit=2&token=da969bff-vf9q-3t1t-b677-d6rt5c0de54e"
  },
  "configs" : [ {
    "id" : "293c3c36-a094-4115-a12b-de0a9ca39be5",
    "deployment_model" : "project_deployed",
    "definition" : {
      "name" : "env-stage",
      "description" : "The stage environment configuration."
    },
    "project" : {
      "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
      "definition" : {
        "name" : "iaas-infra-prestage-env"
      },
      "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
      "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
    },
    "version" : 1,
    "state" : "validated",
    "created_at" : "2023-02-22T19:51:23.253Z",
    "modified_at" : "2023-02-22T19:51:23.253Z",
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/db268db0-160b-4911-8f93-89659000a927/configs/293c3c36-a094-4115-a12b-de0a9ca39be5"
  }, {
    "id" : "9c7afed6-17fb-4c56-a13d-440a78f936bd",
    "deployment_model" : "project_deployed",
    "definition" : {
      "name" : "region-eu-de-stage",
      "description" : "The stage `eu-de` configuration."
    },
    "approved_version" : {
      "definition" : {
        "locator_id" : "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.018edf04-e772-4ca2-9785-03e8e03bef72-global"
      },
      "version" : 1,
      "state" : "approved",
      "href" : "https://projects.api.cloud.ibm.com/v1/projects/db268db0-160b-4911-8f93-89659000a927/configs/9c7afed6-17fb-4c56-a13d-440a78f936bd/versions/1"
    },
    "project" : {
      "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
      "definition" : {
        "name" : "iaas-infra-prestage-env"
      },
      "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
      "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
    },
    "version" : 2,
    "state" : "draft",
    "created_at" : "2023-02-22T19:51:23.253Z",
    "modified_at" : "2023-02-22T19:51:23.253Z",
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/db268db0-160b-4911-8f93-89659000a927/configs/9c7afed6-17fb-4c56-a13d-440a78f936bd"
  } ]
}
```
{: screen}

#### Default JMESPath
{: #project-configs-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `configs[].{id: id, name: definition.name, project_name: project.definition.name, state: state, state_code: state_code, version: version}` |
| Error | Default | - |
|  | Table | `configs[].{id: id, name: definition.name, project_name: project.definition.name, state: state, state_code: state_code, version: version}` |
| All pages | Default | - |
|  | Table | `configs[].{id: id, name: definition.name, project_name: project.definition.name, state: state, state_code: state_code, version: version}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud project config`
{: #project-cli-config-command}

Retrieve the specified project configuration in a specific project.

```sh
ibmcloud project config --project-id PROJECT-ID --id ID
```


#### Command options
{: #project-config-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The unique configuration ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

#### Example
{: #project-config-examples}

```sh
ibmcloud project config \
    --project-id exampleString \
    --id exampleString
```
{: pre}

#### Default JMESPath
{: #project-config-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{id: id, name: definition.name, project_name: project.definition.name, state: state, state_code: state_code, version: version}` |
| Error | Default | - |
|  | Table | `{id: id, name: definition.name, project_name: project.definition.name, state: state, state_code: state_code, version: version}` |
| All pages | Default | - |
|  | Table | `{id: id, name: definition.name, project_name: project.definition.name, state: state, state_code: state_code, version: version}` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud project config-update`
{: #project-cli-config-update-command}

Update a configuration in a project by specifying the ID. [Learn more](/docs/secure-enterprise?topic=secure-enterprise-config-project).

```sh
ibmcloud project config-update --project-id PROJECT-ID --id ID [--definition DEFINITION | --definition-compliance-profile DEFINITION-COMPLIANCE-PROFILE --definition-locator-id DEFINITION-LOCATOR-ID --definition-members DEFINITION-MEMBERS --definition-description DEFINITION-DESCRIPTION --definition-name DEFINITION-NAME --definition-authorizations DEFINITION-AUTHORIZATIONS --definition-inputs DEFINITION-INPUTS --definition-settings DEFINITION-SETTINGS --definition-environment-id DEFINITION-ENVIRONMENT-ID --definition-resource-crns DEFINITION-RESOURCE-CRNS]
```


#### Command options
{: #project-config-update-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The unique configuration ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--definition` ([`ProjectConfigDefinitionPatch`](#cli-project-config-definition-patch-example-schema))
:   This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition=@path/to/file.json`.

`--definition-compliance-profile` ([`ProjectComplianceProfile`](#cli-project-compliance-profile-example-schema))
:   The profile that is required for compliance. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-compliance-profile=@path/to/file.json`.

`--definition-locator-id` (string)
:   A unique concatenation of the catalog ID and the version ID that identify the deployable architecture in the catalog. If importing from an existing Schematics workspace that is not backed by cart, a `locator_id` is required. If using a Schematics workspace that is backed by cart, a `locator_id` is not necessary because the Schematics workspace has one.
> There are 3 scenarios:
> 1. If only a `locator_id` is specified, a new Schematics workspace is instantiated with that `locator_id`.
> 2. If only a schematics `workspace_crn` is specified, a `400` is returned if a `locator_id` is not found in the existing schematics workspace.
> 3. If both a Schematics `workspace_crn` and a `locator_id` are specified, a `400` message is returned if the specified `locator_id` does not agree with the `locator_id` in the existing Schematics workspace.
> For more information of creating a Schematics workspace, see [Creating workspaces and importing the Terraform template](/docs/schematics?topic=schematics-sch-create-wks). This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The maximum length is `512` characters. The minimum length is `1` character. The value must match regular expression `/^(?!\\s)(?!.*\\s$)[\\.0-9a-z-A-Z_-]+$/`.

`--definition-members` ([`StackMember[]`](#cli-stack-member-example-schema))
:   The member deployable architectures that are included in the stack. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The maximum length is `100` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-members=@path/to/file.json`.

`--definition-description` (string)
:   A project configuration description. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The maximum length is `1024` characters. The minimum length is `0` characters. The value must match regular expression `/^$|^(?!\\s)(?!.*\\s$)[^\\x00-\\x1F]*$/`.

`--definition-name` (string)
:   The configuration name. It's unique within the account across projects and regions. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The maximum length is `128` characters. The minimum length is `1` character. The value must match regular expression `/^[a-zA-Z0-9][a-zA-Z0-9-_ ]*$/`.

`--definition-authorizations` ([`ProjectConfigAuth`](#cli-project-config-auth-example-schema))
:   The authorization details. You can authorize by using a trusted profile or an API key in Secrets Manager. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-authorizations=@path/to/file.json`.

`--definition-inputs` (generic map)
:   The input variables that are used for configuration definition and environment. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-inputs=@path/to/file.json`.

`--definition-settings` (generic map)
:   The Schematics environment variables to use to deploy the configuration. Settings are only available if they are specified when the configuration is initially created. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-settings=@path/to/file.json`.

`--definition-environment-id` (string)
:   The ID of the project environment. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--definition-resource-crns` ([]string)
:   The CRNs of the resources that are associated with this configuration. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The list items must match regular expression `/^(?!\\s)(?!.*\\s$)(crn)[^'"`<>{}\\s\\x00-\\x1F]*$/`. The maximum length is `110` items. The minimum length is `0` items.

#### Examples
{: #project-config-update-examples}

```sh
ibmcloud project config-update \
    --project-id exampleString \
    --id exampleString \
    --definition '{"compliance_profile": {}, "locator_id": "exampleString", "members": [{"name": "exampleString", "config_id": "exampleString"}], "description": "exampleString", "name": "env-stage", "authorizations": {"trusted_profile_id": "exampleString", "method": "exampleString", "api_key": "exampleString"}, "inputs": {"anyKey": "anyValue"}, "settings": {"anyKey": "anyValue"}, "environment_id": "exampleString"}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud project config-update \
    --project-id exampleString \
    --id exampleString \
    --definition-compliance-profile projectComplianceProfile \
    --definition-locator-id exampleString \
    --definition-members '[stackMember]' \
    --definition-description exampleString \
    --definition-name exampleString \
    --definition-authorizations projectConfigAuth \
    --definition-inputs '{"anyKey": "anyValue"}' \
    --definition-settings '{"anyKey": "anyValue"}' \
    --definition-environment-id exampleString
```
{: pre}

### `ibmcloud project config-delete`
{: #project-cli-config-delete-command}

Delete a configuration in a project by specifying its ID.

```sh
ibmcloud project config-delete --project-id PROJECT-ID --id ID
```


#### Command options
{: #project-config-delete-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The unique configuration ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

#### Example
{: #project-config-delete-examples}

```sh
ibmcloud project config-delete \
    --project-id exampleString \
    --id exampleString
```
{: pre}

#### Example output
{: #project-config-delete-cli-output}

The example response to a request to delete a configuration.

```json
{
  "id" : "293c3c36-a094-4115-a12b-de0a9ca39be5"
}
```
{: screen}

### `ibmcloud project config-force-approve`
{: #project-cli-config-force-approve-command}

Force approve configuration edits to the main configuration with an approving comment.

```sh
ibmcloud project config-force-approve --project-id PROJECT-ID --id ID --comment COMMENT
```


#### Command options
{: #project-config-force-approve-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The unique configuration ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--comment` (string)
:   Notes on the project draft action. If this action is a force approve on the draft configuration, it must include a nonempty comment. Required.

    The maximum length is `1024` characters. The minimum length is `1` character. The value must match regular expression `/^(?!\\s)(?!.*\\s$)[^\\x00-\\x1F]+$/`.

#### Example
{: #project-config-force-approve-examples}

```sh
ibmcloud project config-force-approve \
    --project-id exampleString \
    --id exampleString \
    --comment 'Approving the changes'
```
{: pre}

#### Example output
{: #project-config-force-approve-cli-output}

The example response to a request for a deployable architecture configuration draft.

```json
{
  "id" : "293c3c36-a094-4115-a12b-de0a9ca39be5",
  "definition" : {
    "name" : "env-stage",
    "description" : "The stage environment configuration.",
    "locator_id" : "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.018edf04-e772-4ca2-9785-03e8e03bef72-global",
    "inputs" : {
      "account_id" : "ref:/configs/account-stage/inputs/account_id",
      "resource_group" : "stage",
      "access_tags" : [ "env:stage" ],
      "logdna_name" : "The name of the LogDNA stage service instance.",
      "sysdig_name" : "The name of the SysDig stage service instance."
    }
  },
  "is_draft" : true,
  "version" : 2,
  "outputs" : [ {
    "name" : "resource_group_id"
  }, {
    "name" : "logdna_id"
  }, {
    "name" : "sysdig_id"
  } ],
  "project" : {
    "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
    "definition" : {
      "name" : "iaas-infra-prestage-env"
    },
    "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
  },
  "schematics" : {
    "workspace_crn" : "crn:v1:staging:public:schematics:us-south:a/38acaf4469814090a4e675dc0c317a0d:95ad49de-ab96-4e7d-a08c-45c38aa448e6:workspace:us-south.workspace.service.e0106139"
  },
  "state" : "validated",
  "update_available" : true,
  "needs_attention_state" : [ ],
  "created_at" : "2023-02-22T19:51:23.253Z",
  "modified_at" : "2023-02-22T19:51:23.253Z",
  "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/configs/b0c44146-1ef6-40c2-82ba-74d51149770a",
  "deployment_model" : "project_deployed",
  "references" : { }
}
```
{: screen}

### `ibmcloud project config-approve`
{: #project-cli-config-approve-command}

Approve and merge configuration edits to the main configuration.

```sh
ibmcloud project config-approve --project-id PROJECT-ID --id ID [--comment COMMENT]
```


#### Command options
{: #project-config-approve-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The unique configuration ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--comment` (string)
:   Notes on the project draft action. If this action is a force approve on the draft configuration, it must include a nonempty comment.

    The maximum length is `1024` characters. The minimum length is `1` character. The value must match regular expression `/^(?!\\s)(?!.*\\s$)[^\\x00-\\x1F]+$/`.

#### Example
{: #project-config-approve-examples}

```sh
ibmcloud project config-approve \
    --project-id exampleString \
    --id exampleString \
    --comment 'Approving the changes'
```
{: pre}

#### Example output
{: #project-config-approve-cli-output}

The example response to a request for a deployable architecture configuration draft.

```json
{
  "id" : "293c3c36-a094-4115-a12b-de0a9ca39be5",
  "definition" : {
    "name" : "env-stage",
    "description" : "The stage environment configuration.",
    "locator_id" : "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.018edf04-e772-4ca2-9785-03e8e03bef72-global",
    "inputs" : {
      "account_id" : "ref:/configs/account-stage/inputs/account_id",
      "resource_group" : "stage",
      "access_tags" : [ "env:stage" ],
      "logdna_name" : "The name of the LogDNA stage service instance.",
      "sysdig_name" : "The name of the SysDig stage service instance."
    }
  },
  "is_draft" : true,
  "version" : 2,
  "outputs" : [ {
    "name" : "resource_group_id"
  }, {
    "name" : "logdna_id"
  }, {
    "name" : "sysdig_id"
  } ],
  "project" : {
    "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
    "definition" : {
      "name" : "iaas-infra-prestage-env"
    },
    "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
  },
  "schematics" : {
    "workspace_crn" : "crn:v1:staging:public:schematics:us-south:a/38acaf4469814090a4e675dc0c317a0d:95ad49de-ab96-4e7d-a08c-45c38aa448e6:workspace:us-south.workspace.service.e0106139"
  },
  "state" : "validated",
  "update_available" : true,
  "needs_attention_state" : [ ],
  "created_at" : "2023-02-22T19:51:23.253Z",
  "modified_at" : "2023-02-22T19:51:23.253Z",
  "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/configs/b0c44146-1ef6-40c2-82ba-74d51149770a",
  "deployment_model" : "project_deployed",
  "references" : { }
}
```
{: screen}

### `ibmcloud project config-validate`
{: #project-cli-config-validate-command}

Run a validation check on a specific configuration in the project. The check includes creating or updating the associated Schematics workspace with a plan job, running the CRA scans, and cost estimation.

```sh
ibmcloud project config-validate --project-id PROJECT-ID --id ID
```


#### Command options
{: #project-config-validate-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The unique configuration ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

#### Example
{: #project-config-validate-examples}

```sh
ibmcloud project config-validate \
    --project-id exampleString \
    --id exampleString
```
{: pre}

#### Example output
{: #project-config-validate-cli-output}

The example response to a request for a deployable architecture configuration draft.

```json
{
  "id" : "293c3c36-a094-4115-a12b-de0a9ca39be5",
  "definition" : {
    "name" : "env-stage",
    "description" : "The stage environment configuration.",
    "locator_id" : "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.018edf04-e772-4ca2-9785-03e8e03bef72-global",
    "inputs" : {
      "account_id" : "ref:/configs/account-stage/inputs/account_id",
      "resource_group" : "stage",
      "access_tags" : [ "env:stage" ],
      "logdna_name" : "The name of the LogDNA stage service instance.",
      "sysdig_name" : "The name of the SysDig stage service instance."
    }
  },
  "is_draft" : true,
  "version" : 2,
  "outputs" : [ {
    "name" : "resource_group_id"
  }, {
    "name" : "logdna_id"
  }, {
    "name" : "sysdig_id"
  } ],
  "project" : {
    "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
    "definition" : {
      "name" : "iaas-infra-prestage-env"
    },
    "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
  },
  "schematics" : {
    "workspace_crn" : "crn:v1:staging:public:schematics:us-south:a/38acaf4469814090a4e675dc0c317a0d:95ad49de-ab96-4e7d-a08c-45c38aa448e6:workspace:us-south.workspace.service.e0106139"
  },
  "state" : "validated",
  "update_available" : true,
  "needs_attention_state" : [ ],
  "created_at" : "2023-02-22T19:51:23.253Z",
  "modified_at" : "2023-02-22T19:51:23.253Z",
  "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/configs/b0c44146-1ef6-40c2-82ba-74d51149770a",
  "deployment_model" : "project_deployed",
  "references" : { }
}
```
{: screen}

### `ibmcloud project config-prevalidate`
{: #project-cli-config-prevalidate-command}

Run a validation check a configuration passed via the API. The check includes creating a Schematics workspace with a plan job, running the CRA scans, and cost estimation.

```sh
ibmcloud project config-prevalidate --project-id PROJECT-ID --id ID [--definition DEFINITION | --definition-compliance-profile DEFINITION-COMPLIANCE-PROFILE --definition-locator-id DEFINITION-LOCATOR-ID --definition-members DEFINITION-MEMBERS --definition-description DEFINITION-DESCRIPTION --definition-name DEFINITION-NAME --definition-authorizations DEFINITION-AUTHORIZATIONS --definition-inputs DEFINITION-INPUTS --definition-settings DEFINITION-SETTINGS --definition-environment-id DEFINITION-ENVIRONMENT-ID --definition-resource-crns DEFINITION-RESOURCE-CRNS] [--schematics SCHEMATICS | --schematics-workspace-crn SCHEMATICS-WORKSPACE-CRN]
```


#### Command options
{: #project-config-prevalidate-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The unique configuration ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--definition` ([`ProjectConfigDefinitionPrototype`](#cli-project-config-definition-prototype-example-schema))
:   This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition=@path/to/file.json`.

`--schematics` ([`SchematicsWorkspace`](#cli-schematics-workspace-example-schema))
:   A Schematics workspace to use for deploying this deployable architecture.
> If importing data from an existing Schematics workspace that is not backed by cart, then a `locator_id` must be provided. If using a Schematics workspace that is backed by cart, a `locator_id` is not required because the Schematics workspace has one.
>
There are 3 scenarios:
> 1. If only a `locator_id` is specified, a new Schematics workspace is instantiated with that `locator_id`.
> 2. If only a schematics `workspace_crn` is specified, a `400` is returned if a `locator_id` is not found in the existing schematics workspace.
> 3. If both a Schematics `workspace_crn` and a `locator_id` are specified, a `400`code  is returned if the specified `locator_id` does not agree with the `locator_id` in the existing Schematics workspace.
>
For more information, see [Creating workspaces and importing the Terraform template](/docs/schematics?topic=schematics-sch-create-wks). This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--schematics=@path/to/file.json`.

`--definition-compliance-profile` ([`ProjectComplianceProfile`](#cli-project-compliance-profile-example-schema))
:   The profile that is required for compliance. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-compliance-profile=@path/to/file.json`.

`--definition-locator-id` (string)
:   A unique concatenation of the catalog ID and the version ID that identify the deployable architecture in the catalog. If importing from an existing Schematics workspace that is not backed by cart, a `locator_id` is required. If using a Schematics workspace that is backed by cart, a `locator_id` is not necessary because the Schematics workspace has one.
> There are 3 scenarios:
> 1. If only a `locator_id` is specified, a new Schematics workspace is instantiated with that `locator_id`.
> 2. If only a schematics `workspace_crn` is specified, a `400` is returned if a `locator_id` is not found in the existing schematics workspace.
> 3. If both a Schematics `workspace_crn` and a `locator_id` are specified, a `400` message is returned if the specified `locator_id` does not agree with the `locator_id` in the existing Schematics workspace.
> For more information of creating a Schematics workspace, see [Creating workspaces and importing the Terraform template](/docs/schematics?topic=schematics-sch-create-wks). This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The maximum length is `512` characters. The minimum length is `1` character. The value must match regular expression `/^(?!\\s)(?!.*\\s$)[\\.0-9a-z-A-Z_-]+$/`.

`--definition-members` ([`StackMember[]`](#cli-stack-member-example-schema))
:   The member deployable architectures that are included in the stack. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The maximum length is `100` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-members=@path/to/file.json`.

`--definition-description` (string)
:   A project configuration description. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The default value is ``. The maximum length is `1024` characters. The minimum length is `0` characters. The value must match regular expression `/^$|^(?!\\s)(?!.*\\s$)[^\\x00-\\x1F]*$/`.

`--definition-name` (string)
:   The configuration name. It's unique within the account across projects and regions. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The maximum length is `128` characters. The minimum length is `1` character. The value must match regular expression `/^[a-zA-Z0-9][a-zA-Z0-9-_ ]*$/`.

`--definition-authorizations` ([`ProjectConfigAuth`](#cli-project-config-auth-example-schema))
:   The authorization details. You can authorize by using a trusted profile or an API key in Secrets Manager. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-authorizations=@path/to/file.json`.

`--definition-inputs` (generic map)
:   The input variables that are used for configuration definition and environment. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-inputs=@path/to/file.json`.

`--definition-settings` (generic map)
:   The Schematics environment variables to use to deploy the configuration. Settings are only available if they are specified when the configuration is initially created. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--definition-settings=@path/to/file.json`.

`--definition-environment-id` (string)
:   The ID of the project environment. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--definition-resource-crns` ([]string)
:   The CRNs of the resources that are associated with this configuration. This option provides a value for a sub-field of the JSON option 'definition'. It is mutually exclusive with that option.

    The list items must match regular expression `/^(?!\\s)(?!.*\\s$)(crn)[^'"`<>{}\\s\\x00-\\x1F]*$/`. The maximum length is `110` items. The minimum length is `0` items.

`--schematics-workspace-crn` (string)
:   An IBM Cloud resource name that uniquely identifies a resource. This option provides a value for a sub-field of the JSON option 'schematics'. It is mutually exclusive with that option.

    The maximum length is `512` characters. The minimum length is `4` characters. The value must match regular expression `/^(?!\\s)(?!.*\\s$)(crn)[^'"`<>{}\\s\\x00-\\x1F]*$/`.

#### Examples
{: #project-config-prevalidate-examples}

```sh
ibmcloud project config-prevalidate \
    --project-id exampleString \
    --id exampleString \
    --definition '{"compliance_profile": {}, "locator_id": "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.018edf04-e772-4ca2-9785-03e8e03bef72-global", "members": [{"name": "exampleString", "config_id": "exampleString"}], "description": "The stage environment configuration.", "name": "env-stage", "authorizations": {"trusted_profile_id": "exampleString", "method": "exampleString", "api_key": "exampleString"}, "inputs": {"anyKey": "anyValue"}, "settings": {"anyKey": "anyValue"}, "environment_id": "exampleString"}' \
    --schematics '{"workspace_crn": "crn:v1:staging:public:project:us-south:a/4e1c48fcf8ac33c0a2441e4139f189ae:bf40ad13-b107-446a-8286-c6d576183bb1::"}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud project config-prevalidate \
    --project-id exampleString \
    --id exampleString \
    --definition-compliance-profile projectComplianceProfile \
    --definition-locator-id exampleString \
    --definition-members '[stackMember]' \
    --definition-description exampleString \
    --definition-name exampleString \
    --definition-authorizations projectConfigAuth \
    --definition-inputs '{"anyKey": "anyValue"}' \
    --definition-settings '{"anyKey": "anyValue"}' \
    --definition-environment-id exampleString \
    --schematics-workspace-crn crn:v1:staging:public:project:us-south:a/4e1c48fcf8ac33c0a2441e4139f189ae:bf40ad13-b107-446a-8286-c6d576183bb1::
```
{: pre}

#### Example output
{: #project-config-prevalidate-cli-output}

The result object for prevalidate.

```json
{
  "result_id" : "293c3c36-a094-4115-a12b-de0a9ca39be5"
}
```
{: screen}

### `ibmcloud project get-prevalidate`
{: #project-cli-get-prevalidate-command}

Retrieve the prevalidate results using a key.

```sh
ibmcloud project get-prevalidate --project-id PROJECT-ID --id ID --result-id RESULT-ID
```


#### Command options
{: #project-get-prevalidate-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The unique configuration ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--result-id` (string)
:   The unique identifier to get prevalidate events. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

#### Example
{: #project-get-prevalidate-examples}

```sh
ibmcloud project get-prevalidate \
    --project-id exampleString \
    --id exampleString \
    --result-id exampleString
```
{: pre}

#### Example output
{: #project-get-prevalidate-cli-output}

A response example for get prevalidate results.

```json
{
  "cost_estimate" : { },
  "cra_logs" : {
    "cra_version" : "2.0.4",
    "status" : "passed"
  },
  "job" : {
    "id" : "ba98208b61efa490153b72adfd672251",
    "summary" : {
      "version" : "1.0.5",
      "plan_summary" : { },
      "apply_summary" : { },
      "destroy_summary" : { },
      "message_summary" : { },
      "plan_messages" : { },
      "apply_messages" : { },
      "destroy_messages" : { }
    }
  },
  "result" : "passed"
}
```
{: screen}

### `ibmcloud project config-deploy`
{: #project-cli-config-deploy-command}

Deploy a project's configuration. This operation is asynchronous and can be tracked by using the get project configuration API with full metadata.

```sh
ibmcloud project config-deploy --project-id PROJECT-ID --id ID
```


#### Command options
{: #project-config-deploy-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The unique configuration ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

#### Example
{: #project-config-deploy-examples}

```sh
ibmcloud project config-deploy \
    --project-id exampleString \
    --id exampleString
```
{: pre}

#### Example output
{: #project-config-deploy-cli-output}

The example response to a request for a deployable architecture configuration draft.

```json
{
  "id" : "293c3c36-a094-4115-a12b-de0a9ca39be5",
  "definition" : {
    "name" : "env-stage",
    "description" : "The stage environment configuration.",
    "locator_id" : "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.018edf04-e772-4ca2-9785-03e8e03bef72-global",
    "inputs" : {
      "account_id" : "ref:/configs/account-stage/inputs/account_id",
      "resource_group" : "stage",
      "access_tags" : [ "env:stage" ],
      "logdna_name" : "The name of the LogDNA stage service instance.",
      "sysdig_name" : "The name of the SysDig stage service instance."
    }
  },
  "is_draft" : true,
  "version" : 2,
  "outputs" : [ {
    "name" : "resource_group_id"
  }, {
    "name" : "logdna_id"
  }, {
    "name" : "sysdig_id"
  } ],
  "project" : {
    "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
    "definition" : {
      "name" : "iaas-infra-prestage-env"
    },
    "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
  },
  "schematics" : {
    "workspace_crn" : "crn:v1:staging:public:schematics:us-south:a/38acaf4469814090a4e675dc0c317a0d:95ad49de-ab96-4e7d-a08c-45c38aa448e6:workspace:us-south.workspace.service.e0106139"
  },
  "state" : "validated",
  "update_available" : true,
  "needs_attention_state" : [ ],
  "created_at" : "2023-02-22T19:51:23.253Z",
  "modified_at" : "2023-02-22T19:51:23.253Z",
  "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/configs/b0c44146-1ef6-40c2-82ba-74d51149770a",
  "deployment_model" : "project_deployed",
  "references" : { }
}
```
{: screen}

### `ibmcloud project config-undeploy`
{: #project-cli-config-undeploy-command}

Undeploy a project's configuration resources. The operation undeploys all the resources that are deployed with the specific configuration. The configuration resources can be tracked by using the get project configuration API with full metadata.

```sh
ibmcloud project config-undeploy --project-id PROJECT-ID --id ID
```


#### Command options
{: #project-config-undeploy-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The unique configuration ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

#### Example
{: #project-config-undeploy-examples}

```sh
ibmcloud project config-undeploy \
    --project-id exampleString \
    --id exampleString
```
{: pre}

#### Example output
{: #project-config-undeploy-cli-output}

The example response to a request for a deployable architecture configuration draft.

```json
{
  "id" : "293c3c36-a094-4115-a12b-de0a9ca39be5",
  "definition" : {
    "name" : "env-stage",
    "description" : "The stage environment configuration.",
    "locator_id" : "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.018edf04-e772-4ca2-9785-03e8e03bef72-global",
    "inputs" : {
      "account_id" : "ref:/configs/account-stage/inputs/account_id",
      "resource_group" : "stage",
      "access_tags" : [ "env:stage" ],
      "logdna_name" : "The name of the LogDNA stage service instance.",
      "sysdig_name" : "The name of the SysDig stage service instance."
    }
  },
  "is_draft" : true,
  "version" : 2,
  "outputs" : [ {
    "name" : "resource_group_id"
  }, {
    "name" : "logdna_id"
  }, {
    "name" : "sysdig_id"
  } ],
  "project" : {
    "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
    "definition" : {
      "name" : "iaas-infra-prestage-env"
    },
    "crn" : "crn:v1:staging:public:project:us-south:a/06580c923e40314421d3b6cb40c01c68:cfbf9050-ab8e-ac97-b01b-ab5af830be8a::",
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
  },
  "schematics" : {
    "workspace_crn" : "crn:v1:staging:public:schematics:us-south:a/38acaf4469814090a4e675dc0c317a0d:95ad49de-ab96-4e7d-a08c-45c38aa448e6:workspace:us-south.workspace.service.e0106139"
  },
  "state" : "validated",
  "update_available" : true,
  "needs_attention_state" : [ ],
  "created_at" : "2023-02-22T19:51:23.253Z",
  "modified_at" : "2023-02-22T19:51:23.253Z",
  "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/configs/b0c44146-1ef6-40c2-82ba-74d51149770a",
  "deployment_model" : "project_deployed",
  "references" : { }
}
```
{: screen}

### `ibmcloud project config-sync`
{: #project-cli-config-sync-command}

Sync a project configuration by analyzing the associated pipeline runs and Schematics workspace logs to get the configuration back to a working state.

```sh
ibmcloud project config-sync --project-id PROJECT-ID --id ID [--schematics SCHEMATICS | --schematics-workspace-crn SCHEMATICS-WORKSPACE-CRN]
```


#### Command options
{: #project-config-sync-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The unique configuration ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--schematics` ([`SchematicsWorkspace`](#cli-schematics-workspace-example-schema))
:   A Schematics workspace to use for deploying this deployable architecture.
> If importing data from an existing Schematics workspace that is not backed by cart, then a `locator_id` must be provided. If using a Schematics workspace that is backed by cart, a `locator_id` is not required because the Schematics workspace has one.
>
There are 3 scenarios:
> 1. If only a `locator_id` is specified, a new Schematics workspace is instantiated with that `locator_id`.
> 2. If only a schematics `workspace_crn` is specified, a `400` is returned if a `locator_id` is not found in the existing schematics workspace.
> 3. If both a Schematics `workspace_crn` and a `locator_id` are specified, a `400`code  is returned if the specified `locator_id` does not agree with the `locator_id` in the existing Schematics workspace.
>
For more information, see [Creating workspaces and importing the Terraform template](/docs/schematics?topic=schematics-sch-create-wks). This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--schematics=@path/to/file.json`.

`--schematics-workspace-crn` (string)
:   An IBM Cloud resource name that uniquely identifies a resource. This option provides a value for a sub-field of the JSON option 'schematics'. It is mutually exclusive with that option.

    The maximum length is `512` characters. The minimum length is `4` characters. The value must match regular expression `/^(?!\\s)(?!.*\\s$)(crn)[^'"`<>{}\\s\\x00-\\x1F]*$/`.

#### Examples
{: #project-config-sync-examples}

```sh
ibmcloud project config-sync \
    --project-id exampleString \
    --id exampleString \
    --schematics '{"workspace_crn": "crn:v1:staging:public:schematics:us-south:a/38acaf4469814090a4e675dc0c317a0d:95ad49de-ab96-4e7d-a08c-45c38aa448e6:workspace:us-south.workspace.service.e0106139"}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud project config-sync \
    --project-id exampleString \
    --id exampleString \
    --schematics-workspace-crn crn:v1:staging:public:project:us-south:a/4e1c48fcf8ac33c0a2441e4139f189ae:bf40ad13-b107-446a-8286-c6d576183bb1::
```
{: pre}

### `ibmcloud project config-resources`
{: #project-cli-config-resources-command}

List resources that are deployed by a configuration.

```sh
ibmcloud project config-resources --project-id PROJECT-ID --id ID
```


#### Command options
{: #project-config-resources-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The unique configuration ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

#### Example
{: #project-config-resources-examples}

```sh
ibmcloud project config-resources \
    --project-id exampleString \
    --id exampleString
```
{: pre}

#### Example output
{: #project-config-resources-cli-output}

The example response to a request to get project configuration resources.

```json
{
  "resources" : [ {
    "resource_crn" : "crn:v1:staging:public:toolchain:us-south:a/4e1c48fcf8ac33c0a2441e4139f189ae:bf40ad13-b107-446a-8286-c6d576183bb1::",
    "resource_name" : "toolchain_instance",
    "resource_type" : "ibm_cd_toolchain",
    "resource_tainted" : false,
    "resource_group_name" : "",
    "account_id" : "499b176abb3e1c9727df87ae48b27c7b",
    "location" : "us-south",
    "resource_status" : "active",
    "tags" : [ ],
    "service_tags" : [ ],
    "catalog_tags" : [ ]
  }, {
    "resource_crn" : "crn:v1:staging:public:cloud-object-storage:global:a/4e1c48fcf8ac33c0a2441e4139f189ae:bf40ad13-b107-446a-8286-c6d576183bb1::",
    "resource_name" : "cos_bucket_instance",
    "resource_type" : "ibm_cos_bucket",
    "resource_tainted" : false,
    "resource_group_name" : "",
    "account_id" : "499b176abb3e1c9727df87ae48b27c7b",
    "location" : "us-south",
    "resource_status" : "active",
    "tags" : [ ],
    "service_tags" : [ ],
    "catalog_tags" : [ ]
  } ],
  "resources_count" : 2
}
```
{: screen}

### `ibmcloud project stack-definition-create`
{: #project-cli-stack-definition-create-command}

Defines inputs at the stack level that users need to configure along with input values at the member level. These values are included in the catalog entry when the deployable architecture stack is exported to a private catalog and are required for the deployable architecture stack to deploy. A reference can be added to a value, or add the value explicitly at the member level.

```sh
ibmcloud project stack-definition-create --project-id PROJECT-ID --id ID [--stack-definition STACK-DEFINITION | --stack-definition-inputs STACK-DEFINITION-INPUTS --stack-definition-outputs STACK-DEFINITION-OUTPUTS]
```


#### Command options
{: #project-stack-definition-create-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The unique configuration ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--stack-definition` ([`StackDefinitionBlockPrototype`](#cli-stack-definition-block-prototype-example-schema))
:   The definition block for a stack definition. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--stack-definition=@path/to/file.json`.

`--stack-definition-inputs` ([`StackDefinitionInputVariable[]`](#cli-stack-definition-input-variable-example-schema))
:   Defines the inputs that users need to configure at the stack level. These inputs are included in the catalog entry when the deployable architecture stack is exported to a private catalog. This option provides a value for a sub-field of the JSON option 'stack-definition'. It is mutually exclusive with that option.

    The maximum length is `300` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--stack-definition-inputs=@path/to/file.json`.

`--stack-definition-outputs` ([`StackDefinitionOutputVariable[]`](#cli-stack-definition-output-variable-example-schema))
:   The outputs associated with this stack definition. This option provides a value for a sub-field of the JSON option 'stack-definition'. It is mutually exclusive with that option.

    The maximum length is `100` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--stack-definition-outputs=@path/to/file.json`.

#### Examples
{: #project-stack-definition-create-examples}

```sh
ibmcloud project stack-definition-create \
    --project-id exampleString \
    --id exampleString \
    --stack-definition '{"inputs": [{"name": "region", "type": "string", "description": "The IBM Cloud location where a resource is deployed.", "default": "us-south", "required": true, "hidden": false}], "outputs": [{"name": "vpc_cluster_id", "value": "cluster_id"}]}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud project stack-definition-create \
    --project-id exampleString \
    --id exampleString \
    --stack-definition-inputs '[stackDefinitionInputVariable]' \
    --stack-definition-outputs '[stackDefinitionOutputVariable]'
```
{: pre}

#### Example output
{: #project-stack-definition-create-cli-output}

Sample response from a create stack template operation.

```json
{
  "id" : "293c3c36-a094-4115-a12b-de0a9ca6678a",
  "stack_definition" : {
    "inputs" : [ {
      "name" : "region",
      "type" : "string",
      "required" : true,
      "default" : "us-south",
      "hidden" : false,
      "description" : "The IBM Cloud location where a resource is deployed."
    }, {
      "name" : "resource_group",
      "type" : "string",
      "default" : "Default",
      "required" : true,
      "hidden" : false,
      "description" : "The IBM Cloud resource group where a resource is deployed."
    } ],
    "outputs" : [ {
      "name" : "vpc_cluster_id",
      "value" : "cluster_id"
    } ],
    "members" : [ {
      "name" : "foundation-deployable-architecture",
      "version_locator" : "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.018edf04-e772-4ca2-9785-03e8e03bef72-global",
      "inputs" : [ {
        "name" : "region",
        "value" : "us-south"
      }, {
        "name" : "cluster_name",
        "value" : "foundation-cluster"
      } ]
    }, {
      "name" : "middleware-architecture",
      "version_locator" : "01e1a9ad-534b-4ab9-996a-b8f2a8653d5c.4d86732e-04b9-4dab-bfdc-5b514d86ecd8",
      "inputs" : [ {
        "name" : "kube_version",
        "value" : 1.29
      } ]
    } ]
  },
  "created_at" : "2023-02-22T19:51:23.253Z",
  "modified_at" : "2023-02-22T19:51:23.253Z",
  "configuration" : {
    "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
    "definition" : {
      "name" : "stack-bottom-up-example"
    },
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
  },
  "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/template",
  "references" : { }
}
```
{: screen}

### `ibmcloud project stack-definition`
{: #project-cli-stack-definition-command}

Retrieve the stack definition that is associated to the configuration.

```sh
ibmcloud project stack-definition --project-id PROJECT-ID --id ID
```


#### Command options
{: #project-stack-definition-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The unique configuration ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

#### Example
{: #project-stack-definition-examples}

```sh
ibmcloud project stack-definition \
    --project-id exampleString \
    --id exampleString
```
{: pre}

#### Example output
{: #project-stack-definition-cli-output}

Sample response from a create stack template operation.

```json
{
  "id" : "293c3c36-a094-4115-a12b-de0a9ca6678a",
  "stack_definition" : {
    "inputs" : [ {
      "name" : "region",
      "type" : "string",
      "required" : true,
      "default" : "us-south",
      "hidden" : false,
      "description" : "The IBM Cloud location where a resource is deployed."
    }, {
      "name" : "resource_group",
      "type" : "string",
      "default" : "Default",
      "required" : true,
      "hidden" : false,
      "description" : "The IBM Cloud resource group where a resource is deployed."
    } ],
    "outputs" : [ {
      "name" : "vpc_cluster_id",
      "value" : "cluster_id"
    } ],
    "members" : [ {
      "name" : "foundation-deployable-architecture",
      "version_locator" : "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.018edf04-e772-4ca2-9785-03e8e03bef72-global",
      "inputs" : [ {
        "name" : "region",
        "value" : "us-south"
      }, {
        "name" : "cluster_name",
        "value" : "foundation-cluster"
      } ]
    }, {
      "name" : "middleware-architecture",
      "version_locator" : "01e1a9ad-534b-4ab9-996a-b8f2a8653d5c.4d86732e-04b9-4dab-bfdc-5b514d86ecd8",
      "inputs" : [ {
        "name" : "kube_version",
        "value" : 1.29
      } ]
    } ]
  },
  "created_at" : "2023-02-22T19:51:23.253Z",
  "modified_at" : "2023-02-22T19:51:23.253Z",
  "configuration" : {
    "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
    "definition" : {
      "name" : "stack-bottom-up-example"
    },
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
  },
  "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/template",
  "references" : { }
}
```
{: screen}

### `ibmcloud project stack-definition-update`
{: #project-cli-stack-definition-update-command}

Update the stack definition that is associated with the configuration.

```sh
ibmcloud project stack-definition-update --project-id PROJECT-ID --id ID [--stack-definition STACK-DEFINITION | --stack-definition-inputs STACK-DEFINITION-INPUTS --stack-definition-outputs STACK-DEFINITION-OUTPUTS]
```


#### Command options
{: #project-stack-definition-update-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The unique configuration ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--stack-definition` ([`StackDefinitionBlockPrototype`](#cli-stack-definition-block-prototype-example-schema))
:   The definition block for a stack definition. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--stack-definition=@path/to/file.json`.

`--stack-definition-inputs` ([`StackDefinitionInputVariable[]`](#cli-stack-definition-input-variable-example-schema))
:   Defines the inputs that users need to configure at the stack level. These inputs are included in the catalog entry when the deployable architecture stack is exported to a private catalog. This option provides a value for a sub-field of the JSON option 'stack-definition'. It is mutually exclusive with that option.

    The maximum length is `300` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--stack-definition-inputs=@path/to/file.json`.

`--stack-definition-outputs` ([`StackDefinitionOutputVariable[]`](#cli-stack-definition-output-variable-example-schema))
:   The outputs associated with this stack definition. This option provides a value for a sub-field of the JSON option 'stack-definition'. It is mutually exclusive with that option.

    The maximum length is `100` items. The minimum length is `0` items.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--stack-definition-outputs=@path/to/file.json`.

#### Examples
{: #project-stack-definition-update-examples}

```sh
ibmcloud project stack-definition-update \
    --project-id exampleString \
    --id exampleString \
    --stack-definition '{"inputs": [{"name": "region", "type": "string", "description": "The IBM Cloud location where a resource is deployed.", "default": "eu-gb", "required": true, "hidden": false}], "outputs": [{"name": "exampleString", "value": "exampleString"}]}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud project stack-definition-update \
    --project-id exampleString \
    --id exampleString \
    --stack-definition-inputs '[stackDefinitionInputVariable]' \
    --stack-definition-outputs '[stackDefinitionOutputVariable]'
```
{: pre}

#### Example output
{: #project-stack-definition-update-cli-output}

Sample response from a patch stack template operation.

```json
{
  "id" : "293c3c36-a094-4115-a12b-de0a9ca6678a",
  "stack_definition" : {
    "inputs" : [ {
      "name" : "region",
      "type" : "string",
      "required" : true,
      "default" : "eu-gb",
      "hidden" : false,
      "description" : "The IBM Cloud location where a resource is deployed."
    } ],
    "outputs" : [ {
      "name" : "vpc_cluster_id",
      "value" : "cluster_id"
    } ],
    "members" : [ {
      "name" : "foundation-deployable-architecture",
      "version_locator" : "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.018edf04-e772-4ca2-9785-03e8e03bef72-global",
      "inputs" : [ {
        "name" : "cluster_name",
        "value" : "foundation-cluster"
      } ]
    } ]
  },
  "state" : "draft",
  "created_at" : "2023-02-22T19:51:23.253Z",
  "modified_at" : "2023-02-22T19:51:23.253Z",
  "configuration" : {
    "id" : "cfbf9050-ab8e-ac97-b01b-ab5af830be8a",
    "definition" : {
      "name" : "stack-bottom-up-example"
    },
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a"
  },
  "href" : "https://projects.api.cloud.ibm.com/v1/projects/cfbf9050-ab8e-ac97-b01b-ab5af830be8a/template"
}
```
{: screen}

### `ibmcloud project stack-definition-export`
{: #project-cli-stack-definition-export-command}

Exports the deployable architecture stack to a private catalog. All member deployable architectures within the stack must be validated and deployed before the stack is exported. The stack definition must also exist before the stack is exported. The stack can be exported as a new product, or as a new version of an existing product.

```sh
ibmcloud project stack-definition-export --project-id PROJECT-ID --id ID [--settings SETTINGS | --settings-catalog-id SETTINGS-CATALOG-ID --settings-target-version SETTINGS-TARGET-VERSION --settings-variation SETTINGS-VARIATION --settings-label SETTINGS-LABEL --settings-tags SETTINGS-TAGS --settings-product-id SETTINGS-PRODUCT-ID]
```


#### Command options
{: #project-stack-definition-export-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The unique configuration ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--settings` ([`StackDefinitionExportRequest`](#cli-stack-definition-export-request-example-schema))
:   The payload for the private catalog export request. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--settings=@path/to/file.json`.

`--settings-catalog-id` (string)
:   The catalog ID to publish. This option provides a value for a sub-field of the JSON option 'settings'. It is mutually exclusive with that option.

    The maximum length is `36` characters. The value must match regular expression `/^[\\-0-9a-zA-Z]+$/`.

`--settings-target-version` (string)
:   The semver value of this new version of the product. This option provides a value for a sub-field of the JSON option 'settings'. It is mutually exclusive with that option.

    The maximum length is `60` characters. The minimum length is `5` characters. The value must match regular expression `/^(0|[1-9]\\d*)\\.(0|[1-9]\\d*)\\.(0|[1-9]\\d*)(?:-((?:0|[1-9]\\d*|\\d*[a-zA-Z-][0-9a-zA-Z-]*)(?:\\.(?:0|[1-9]\\d*|\\d*[a-zA-Z-][0-9a-zA-Z-]*))*))?(?:\\+([0-9a-zA-Z-]+(?:\\.[0-9a-zA-Z-]+)*))?$/`.

`--settings-variation` (string)
:   The variation of the current software being onboarded. Only valid if the Product kind is module or solution. See `flavor` in [Catalog's import offering](/apidocs/resource-catalog/private-catalog#import-offering). This option provides a value for a sub-field of the JSON option 'settings'. It is mutually exclusive with that option.

    The maximum length is `128` characters. The value must match regular expression `/^[a-zA-Z0-9][a-zA-Z0-9-_ ]*$/`.

`--settings-label` (string)
:   The product label. This option provides a value for a sub-field of the JSON option 'settings'. It is mutually exclusive with that option.

    The maximum length is `128` characters. The value must match regular expression `/^[a-zA-Z0-9][a-zA-Z0-9-_ ]*$/`.

`--settings-tags` ([]string)
:   Tags associated with the catalog product. This option provides a value for a sub-field of the JSON option 'settings'. It is mutually exclusive with that option.

    The default value is `[]`. The list items must match regular expression `/^[a-zA-Z0-9][a-zA-Z0-9-_]*$/`. The maximum length is `10` items. The minimum length is `0` items.

`--settings-product-id` (string)
:   The product ID to publish. This option provides a value for a sub-field of the JSON option 'settings'. It is mutually exclusive with that option.

    The maximum length is `36` characters. The value must match regular expression `/^[\\-0-9a-zA-Z]+$/`.

#### Examples
{: #project-stack-definition-export-examples}

```sh
ibmcloud project stack-definition-export \
    --project-id exampleString \
    --id exampleString \
    --settings '{"catalog_id": "01e1a9ad-534b-4ab9-996a-b8f2a8653d5c", "target_version": "exampleString", "variation": "exampleString", "label": "Stack Deployable Architecture", "tags": []}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud project stack-definition-export \
    --project-id exampleString \
    --id exampleString \
    --settings-catalog-id exampleString \
    --settings-target-version exampleString \
    --settings-variation exampleString \
    --settings-label exampleString \
    --settings-tags '[]'
```
{: pre}

#### Example output
{: #project-stack-definition-export-cli-output}

Sample response from exporting a stack definition to the private catalog

```json
{
  "catalog_id" : "01e1a9ad-534b-4ab9-996a-b8f2a8653d5c",
  "product_id" : "b60b5876-d074-478a-ac73-f979898c527b",
  "version_locator" : "01e1a9ad-534b-4ab9-996a-b8f2a8653d5c.f9f73bdb-5c7d-4ea6-82ef-9debc6340df8",
  "kind" : "terraform",
  "format" : "stack",
  "tags" : [ ]
}
```
{: screen}

### `ibmcloud project config-versions`
{: #project-cli-config-versions-command}

Retrieve a list of previous and current versions of a project configuration in a specific project.

```sh
ibmcloud project config-versions --project-id PROJECT-ID --id ID
```


#### Command options
{: #project-config-versions-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The unique configuration ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

#### Example
{: #project-config-versions-examples}

```sh
ibmcloud project config-versions \
    --project-id exampleString \
    --id exampleString
```
{: pre}

#### Example output
{: #project-config-versions-cli-output}

The example response to a request to list project configuration drafts.

```json
{
  "versions" : [ {
    "definition" : {
      "locator_id" : "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.018edf04-e772-4ca2-9785-03e8e03bef72-global"
    },
    "version" : 1,
    "state" : "approved",
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/db268db0-160b-4911-8f93-89659000a927/configs/293c3c36-a094-4115-a12b-de0a9ca39be5/versions/1"
  }, {
    "definition" : {
      "locator_id" : "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.018edf04-e772-4ca2-9785-03e8e03bef72-global"
    },
    "version" : 2,
    "state" : "validated",
    "href" : "https://projects.api.cloud.ibm.com/v1/projects/db268db0-160b-4911-8f93-89659000a927/configs/293c3c36-a094-4115-a12b-de0a9ca39be5/versions/2"
  } ]
}
```
{: screen}

#### Default JMESPath
{: #project-config-versions-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `versions` |
| Error | Default | - |
|  | Table | `versions` |
| All pages | Default | - |
|  | Table | `versions` |
{: caption="Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud project config-version`
{: #project-cli-config-version-command}

Retrieve a specific version of a configuration in a project.

```sh
ibmcloud project config-version --project-id PROJECT-ID --id ID --version VERSION
```


#### Command options
{: #project-config-version-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The unique configuration ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--version` (int64)
:   The configuration version. Required.

    The maximum value is `10000`. The minimum value is `0`.

#### Example
{: #project-config-version-examples}

```sh
ibmcloud project config-version \
    --project-id exampleString \
    --id exampleString \
    --version 0
```
{: pre}

## V2 Configurations
{: #project-v2-configurations-cli}

Commands for V2Configurations resource.

### `ibmcloud project config-version-delete`
{: #project-cli-config-version-delete-command}

Delete a configuration version by specifying the project ID.

```sh
ibmcloud project config-version-delete --project-id PROJECT-ID --id ID --version VERSION
```


#### Command options
{: #project-config-version-delete-cli-options}

`--project-id` (string)
:   The unique project ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--id` (string)
:   The unique configuration ID. Required.

    The maximum length is `128` characters. The value must match regular expression `/^[\\.\\-0-9a-zA-Z]+$/`.

`--version` (int64)
:   The configuration version. Required.

    The maximum value is `10000`. The minimum value is `0`.

#### Example
{: #project-config-version-delete-examples}

```sh
ibmcloud project config-version-delete \
    --project-id exampleString \
    --id exampleString \
    --version 0
```
{: pre}

#### Example output
{: #project-config-version-delete-cli-output}

The example response to a request to delete a configuration.

```json
{
  "id" : "293c3c36-a094-4115-a12b-de0a9ca39be5"
}
```
{: screen}

## Schema examples
{: #project-schema-examples}

The following schema examples represent the data that you need to specify for a command option. These examples model the data structure and include placeholder values for the expected value type. When you run a command, replace these values with the values that apply to your environment as appropriate.

### EnvironmentDefinitionPropertiesPatch
{: #cli-environment-definition-properties-patch-example-schema}

The following example shows the format of the EnvironmentDefinitionPropertiesPatch object.

```json

{
  "description" : "The environment development.",
  "name" : "development",
  "authorizations" : {
    "trusted_profile_id" : "Profile-9ac10c5c-195c-41ef-b465-68a6b6dg5f12",
    "method" : "trusted_profile",
    "api_key" : "exampleString"
  },
  "inputs" : {
    "anyKey" : "anyValue"
  },
  "compliance_profile" : {
    "id" : "some-profile-id",
    "instance_id" : "some-instance-id",
    "instance_location" : "us-south",
    "attachment_id" : "some-attachment-id",
    "profile_name" : "some-profile-name",
    "wp_policy_id" : "exampleString",
    "wp_instance_id" : "exampleString",
    "wp_instance_name" : "exampleString",
    "wp_instance_location" : "us-south",
    "wp_zone_id" : "exampleString",
    "wp_zone_name" : "exampleString",
    "wp_policy_name" : "exampleString"
  }
}
```
{: codeblock}

### EnvironmentDefinitionRequiredProperties
{: #cli-environment-definition-required-properties-example-schema}

The following example shows the format of the EnvironmentDefinitionRequiredProperties object.

```json

{
  "description" : "The environment development.",
  "name" : "development",
  "authorizations" : {
    "trusted_profile_id" : "Profile-9ac10c5c-195c-41ef-b465-68a6b6dg5f12",
    "method" : "trusted_profile",
    "api_key" : "exampleString"
  },
  "inputs" : {
    "anyKey" : "anyValue"
  },
  "compliance_profile" : {
    "id" : "some-profile-id",
    "instance_id" : "some-instance-id",
    "instance_location" : "us-south",
    "attachment_id" : "some-attachment-id",
    "profile_name" : "some-profile-name",
    "wp_policy_id" : "exampleString",
    "wp_instance_id" : "exampleString",
    "wp_instance_name" : "exampleString",
    "wp_instance_location" : "us-south",
    "wp_zone_id" : "exampleString",
    "wp_zone_name" : "exampleString",
    "wp_policy_name" : "exampleString"
  }
}
```
{: codeblock}

### EnvironmentPrototype[]
{: #cli-environment-prototype-example-schema}

The following example shows the format of the EnvironmentPrototype[] object.

```json

[ {
  "definition" : {
    "description" : "exampleString",
    "name" : "exampleString",
    "authorizations" : {
      "trusted_profile_id" : "exampleString",
      "method" : "exampleString",
      "api_key" : "exampleString"
    },
    "inputs" : {
      "anyKey" : "anyValue"
    },
    "compliance_profile" : { }
  }
} ]
```
{: codeblock}

### ProjectComplianceProfile
{: #cli-project-compliance-profile-example-schema}

The following example shows the format of the ProjectComplianceProfile object.

```json

{
  "id" : "exampleString",
  "instance_id" : "exampleString",
  "instance_location" : "us-south",
  "attachment_id" : "someattachmentid",
  "profile_name" : "SCCProfilev1.0",
  "wp_policy_id" : "exampleString",
  "wp_instance_id" : "exampleString",
  "wp_instance_name" : "exampleString",
  "wp_instance_location" : "us-south",
  "wp_zone_id" : "exampleString",
  "wp_zone_name" : "exampleString",
  "wp_policy_name" : "exampleString"
}
```
{: codeblock}

### ProjectConfigAuth
{: #cli-project-config-auth-example-schema}

The following example shows the format of the ProjectConfigAuth object.

```json

{
  "trusted_profile_id" : "Profile-9ac10c5c-195c-41ef-b465-68a6b6dg5f12",
  "method" : "trusted_profile",
  "api_key" : "exampleString"
}
```
{: codeblock}

### ProjectConfigDefinitionPatch
{: #cli-project-config-definition-patch-example-schema}

The following example shows the format of the ProjectConfigDefinitionPatch object.

```json

{
  "compliance_profile" : { },
  "locator_id" : "exampleString",
  "members" : [ {
    "name" : "exampleString",
    "config_id" : "exampleString"
  } ],
  "description" : "exampleString",
  "name" : "env-stage",
  "authorizations" : {
    "trusted_profile_id" : "exampleString",
    "method" : "exampleString",
    "api_key" : "exampleString"
  },
  "inputs" : {
    "anyKey" : "anyValue"
  },
  "settings" : {
    "anyKey" : "anyValue"
  },
  "environment_id" : "exampleString"
}
```
{: codeblock}

### ProjectConfigDefinitionPrototype
{: #cli-project-config-definition-prototype-example-schema}

The following example shows the format of the ProjectConfigDefinitionPrototype object.

```json

{
  "compliance_profile" : { },
  "locator_id" : "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.018edf04-e772-4ca2-9785-03e8e03bef72-global",
  "members" : [ {
    "name" : "exampleString",
    "config_id" : "exampleString"
  } ],
  "description" : "The stage environment configuration.",
  "name" : "env-stage",
  "authorizations" : {
    "trusted_profile_id" : "exampleString",
    "method" : "exampleString",
    "api_key" : "exampleString"
  },
  "inputs" : {
    "anyKey" : "anyValue"
  },
  "settings" : {
    "anyKey" : "anyValue"
  },
  "environment_id" : "exampleString"
}
```
{: codeblock}

### ProjectConfigPrototype[]
{: #cli-project-config-prototype-example-schema}

The following example shows the format of the ProjectConfigPrototype[] object.

```json

[ {
  "definition" : {
    "compliance_profile" : { },
    "locator_id" : "1082e7d2-5e2f-0a11-a3bc-f88a8e1931fc.018edf04-e772-4ca2-9785-03e8e03bef72-global",
    "members" : [ {
      "name" : "exampleString",
      "config_id" : "exampleString"
    } ],
    "description" : "The stage account configuration.",
    "name" : "account-stage",
    "authorizations" : {
      "trusted_profile_id" : "exampleString",
      "method" : "exampleString",
      "api_key" : "exampleString"
    },
    "inputs" : {
      "anyKey" : "anyValue"
    },
    "settings" : {
      "anyKey" : "anyValue"
    },
    "environment_id" : "exampleString"
  },
  "schematics" : {
    "workspace_crn" : "crn:v1:staging:public:project:us-south:a/4e1c48fcf8ac33c0a2441e4139f189ae:bf40ad13-b107-446a-8286-c6d576183bb1::"
  }
} ]
```
{: codeblock}

### ProjectDefinitionPatch
{: #cli-project-definition-patch-example-schema}

The following example shows the format of the ProjectDefinitionPatch object.

```json

{
  "name" : "acme-microservice",
  "description" : "A microservice to deploy on top of ACME infrastructure.",
  "auto_deploy_mode" : "auto_approval",
  "monitoring_enabled" : true,
  "destroy_on_delete" : true,
  "store" : {
    "type" : "gh",
    "url" : "exampleString",
    "token" : "exampleString",
    "config_directory" : "exampleString"
  },
  "terraform_engine" : {
    "id" : "exampleString",
    "type" : "terraform-enterprise"
  },
  "auto_deploy" : true
}
```
{: codeblock}

### ProjectDefinitionStore
{: #cli-project-definition-store-example-schema}

The following example shows the format of the ProjectDefinitionStore object.

```json

{
  "type" : "gh",
  "url" : "exampleString",
  "token" : "exampleString",
  "config_directory" : "exampleString"
}
```
{: codeblock}

### ProjectPrototypeDefinition
{: #cli-project-prototype-definition-example-schema}

The following example shows the format of the ProjectPrototypeDefinition object.

```json

{
  "name" : "acme-microservice",
  "description" : "A microservice to deploy on top of ACME infrastructure.",
  "auto_deploy_mode" : "manual_approval",
  "monitoring_enabled" : false,
  "destroy_on_delete" : true,
  "store" : {
    "type" : "gh",
    "url" : "exampleString",
    "token" : "exampleString",
    "config_directory" : "exampleString"
  },
  "terraform_engine" : {
    "id" : "exampleString",
    "type" : "terraform-enterprise"
  },
  "auto_deploy" : false
}
```
{: codeblock}

### ProjectTerraformEngineSettings
{: #cli-project-terraform-engine-settings-example-schema}

The following example shows the format of the ProjectTerraformEngineSettings object.

```json

{
  "id" : "exampleString",
  "type" : "terraform-enterprise"
}
```
{: codeblock}

### SchematicsWorkspace
{: #cli-schematics-workspace-example-schema}

The following example shows the format of the SchematicsWorkspace object.

```json

{
  "workspace_crn" : "crn:v1:staging:public:project:us-south:a/4e1c48fcf8ac33c0a2441e4139f189ae:bf40ad13-b107-446a-8286-c6d576183bb1::"
}
```
{: codeblock}

### StackDefinitionBlockPrototype
{: #cli-stack-definition-block-prototype-example-schema}

The following example shows the format of the StackDefinitionBlockPrototype object.

```json

{
  "inputs" : [ {
    "name" : "region",
    "type" : "string",
    "description" : "The IBM Cloud location where a resource is deployed.",
    "default" : "us-south",
    "required" : true,
    "hidden" : false
  } ],
  "outputs" : [ {
    "name" : "vpc_cluster_id",
    "value" : "cluster_id"
  } ]
}
```
{: codeblock}

### StackDefinitionExportRequest
{: #cli-stack-definition-export-request-example-schema}

The following example shows the format of the StackDefinitionExportRequest object.

```json

{
  "catalog_id" : "01e1a9ad-534b-4ab9-996a-b8f2a8653d5c",
  "target_version" : "exampleString",
  "variation" : "exampleString",
  "label" : "Stack Deployable Architecture",
  "tags" : [ ]
}
```
{: codeblock}

### StackDefinitionInputVariable
{: #cli-stack-definition-input-variable-example-schema}

The following example shows the format of the StackDefinitionInputVariable object.

```json

{
  "name" : "exampleString",
  "type" : "array",
  "description" : "exampleString",
  "default" : "exampleString",
  "required" : false,
  "hidden" : false
}
```
{: codeblock}

### StackDefinitionOutputVariable
{: #cli-stack-definition-output-variable-example-schema}

The following example shows the format of the StackDefinitionOutputVariable object.

```json

{
  "name" : "exampleString",
  "value" : "exampleString"
}
```
{: codeblock}

### StackMember
{: #cli-stack-member-example-schema}

The following example shows the format of the StackMember object.

```json

{
  "name" : "exampleString",
  "config_id" : "exampleString"
}
```
{: codeblock}

## Other relevant commands for {{site.data.keyword.cloud_notm}} projects
{: #project-relevant-commands-other}

The following commands are not a part of the projects CLI plug-in, but you can use them to complete project-related tasks, such as attaching tags to a project. This list is not exhaustive of all of the relevant commands that are available to use with projects. Rather, this list is a starting point for you to explore other commands that you can use with projects.

Some of the following commands might require the installation of their specific plug-ins before you can run them.
{: important}

Run [`ibmcloud resource tag-attach`](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_tag_attach) to attach tags to a project:

```sh
ibmcloud resource tag-attach --tag-names TAG --resource-id PROJECT-CRN
```

Run [`ibmcloud resource search`](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_search) to retrieve all of the resources in an account created by configurations in a project: {: #ibmcloud-resource-tag-search}

```sh
ibmcloud resource search "service_tags:\"schematics::project_id:PROJECT_ID\""
```

Run [`ibmcloud schematics logs`](/docs/cli?topic=cli-schematics-cli-reference#schematics-logs) to retrieve the log files for a {{site.data.keyword.bpshort}} workspace:

```sh
ibmcloud schematics logs --id WORKSPACE_ID [--act-id ACTION_ID]
```
