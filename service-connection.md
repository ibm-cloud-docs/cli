---

copyright:
  years: 2020, 2024
lastupdated: "2024-08-06"

keywords: isolation for IBM Cloud CLI, service endpoints for IBM Cloud CLI, private network for IBM Cloud CLI, network isolation in IBM Cloud CLI, non-public routes for IBM Cloud CLI, private connection for IBM Cloud CLI, private endpoints, regions that support private endpoints, private service endpoints, cli private endpoints

subcollection: cli

---

{{site.data.keyword.attribute-definition-list}}

# Securing your connection when using the {{site.data.keyword.cloud_notm}} CLI
{: #service-connection}

To ensure that you have enhanced control and security over your data when you use the {{site.data.keyword.cloud}} Command Line Interface, you have the option of using private routes to {{site.data.keyword.cloud_notm}} endpoints. Private routes are not accessible or reachable over the internet. By using the {{site.data.keyword.cloud_notm}} private endpoints feature, you can protect your data from threats from the public network and logically extend your private network.
{: shortdesc}

The CLI uses the private endpoint support that is provided by the {{site.data.keyword.cloud_notm}} platform. Platform services that are used by the core CLI, such as IAM, provide private endpoint support.

If your deployment uses the VPC environment of {{site.data.keyword.cloud_notm}}, private endpoints are exposed through global endpoints. If your deployment uses the Classic environment, regional support is provided for a limited number of CLI commands. The following regions support private endpoints in Classic environments:
* `us-south`
* `us-east`

## Log in using One time passcode
{: #cli-passcode}

You can access a one-time passcode to log into your IBM Cloud account from the command line. You will need to have [installed the CLI](https://cloud.ibm.com/docs/cli?topic=cli-install-ibmcloud-cli) or [OpenShift CLI](https://www.ibm.com/docs/en/software-hub/5.1.x?topic=workstation-installing-openshift-cli) in your development console.

To use the passcode:

1. Log in to your IBM Cloud account
2. Under your profile icon in the upper right of the IBM Cloud home page, select the **Log in to CLI or API** menu item.
3. Copy the command line and paste into your developer console.

To streamline your login, you may want to add your prefered region and target resource group to the command line, such as:

```sh
ibmcloud login -a https://cloud.ibm.com -u passcode -p thepasscode -r us-south -g MyResourceGroup
```

## Enabling virtual routing and forwarding
{: #cli-private-vrf}

First, enable virtual routing and forwarding in your account, and then you can enable the use of {{site.data.keyword.cloud_notm}} private service endpoints. For more information about setting up your account to support the private connectivity option, see [Enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint).

To learn more about private connections on {{site.data.keyword.cloud_notm}}, see [Secure access to services using service endpoints](/docs/account?topic=account-service-endpoints-overview).

## Logging in to the CLI with a private endpoint
{: #cli-private-login}

You can log in to either a private endpoint for Classic or for VPC. To log in using Classic infrastructure, [log in](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login) to a private endpoint by using the CLI by using the following command:

```text
ibmcloud login -a private.cloud.ibm.com
```

To [log in](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login) by using the VPC infrastructure, add the `--vpc` flag to the command:

```text
ibmcloud login -a private.cloud.ibm.com --vpc
```

## Targeting a supported region (required for Classic use)
{: #cli-private-region}

To use private endpoints for deployments in the Classic environment, a region must be targeted when a private endpoint is set in the {{site.data.keyword.cloud_notm}} CLI.

To [target](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_target) a supported region, use the following command:

```text
ibmcloud target -r [region]
```

## Creating a private endpoint gateway (required for VPC use)
{: #cli-private-vpc}

To use private endpoints for deployments in the VPC environment, you must create a virtual private endpoint gateway. For more information, see [About virtual private endpoint gateways](/docs/vpc?topic=vpc-about-vpe).

A list of all {{site.data.keyword.cloud_notm}} services that are configurable through a virtual private endpoint gateway is at [VPE Supported Services](/docs/vpc?topic=vpc-vpe-supported-services).

To ensure basic CLI capability against the private endpoint, you must configure the gateway to include these services:
* Account Management: Endpoint URL `(https://private.accounts.cloud.ibm.com)`{: external}
* Cloud Object Storage (use `direct`): [Endpoint URL](/docs/cloud-object-storage?topic=cloud-object-storage-endpoints)
* Identity and Access Management: [Endpoint URL](/apidocs/iam-identity-token-api#endpoints)
* Global Catalog: [Endpoint URL](/apidocs/resource-catalog/global-catalog#endpoint-url)
* Global Search: [Endpoint URL](/apidocs/search#endpoint-url)
* Global Tagging: [Endpoint URL](/apidocs/tagging#endpoint-url)
* Usage Metering: [Endpoint URL](/apidocs/usage-metering#endpoint)
* Enterprise Management: [Endpoint URL](/apidocs/enterprise-apis/enterprise#endpoint-url)
* Resource Controller: [Endpoint URL](/apidocs/resource-controller/resource-controller#endpoint-url)
* User Management: [Endpoint URL](/apidocs/user-management#endpoint-url)

## Determining which CLI plug-ins support private endpoints
{: #cli-private-plugins}

The [`ibmcloud plugin list`](/docs/cli?topic=cli-ibmcloud_commands_settings#ibmcloud_plugin_list) command reports whether an installed CLI plug-in supports private endpoints. If a plug-in that you use does not show private support, you must continue to use it with your API set to the public endpoint `cloud.ibm.com`.

## Installing CLI plug-ins over a private connection
{: #cli-private-plugins-install}

To configure the CLI to install plug-ins over a private connection, you must set up the API of the CLI. Follow the [login instructions](#cli-private-login) to set up the API and indicate VPC as applicable.

## Determining which commands support private endpoints
{: #cli-private-commands}

The following commands support private endpoints:
- `api`
- `login`
- `target`
- `logout`

Most commands under the following namespaces work when you are using private endpoints:
- `account`
- `billing`
- `iam`
- `resource`
- `catalog`

If the CLI is set to access private endpoints and you try to run a command or plug-in that does not yet support private endpoints, you might see an error.
{: note}

The following core commands do not yet support private endpoints:

```text
account
billing
  org-usage
catalog
  template-run
sl
  all commands
app (deprecated)
  all commands
service (deprecated)
  all commands
```
