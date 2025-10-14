---

copyright:
  years: 2018, 2025
lastupdated: "2025-10-14"

keywords: cli, ibmcloud billing, view account, view usage, account usage, resource groups, resources, org-usage

subcollection: cli

---

{{site.data.keyword.attribute-definition-list}}

# Viewing billing and usage information (ibmcloud billing)
{: #ibmcloud_billing}

Use the following commands from the {{site.data.keyword.cloud}} Command Line Interface to retrieve resource usage and billing information. You can use these commands for viewing the monthly usage information for an account, enterprise, and even for a specific resource group.

For more information, see [Viewing your usage](/docs/account?topic=account-viewingusage).

{: shortdesc}

## ibmcloud billing account-usage
{: #ibmcloud_billing_account_usage}

Show monthly usage of all the resources and plans in an account (account admin only). 

To learn more about the account usage summary API, see [Get account usage](/apidocs/metering-reporting#get-account-usage).


```bash
ibmcloud billing account-usage [-d YYYY-MM] [--output FORMAT] [-q, --quiet]
```

### Command options
{: #ibmcloud_billing_account_usage_options}

-d {YEAR-MONTH} (optional)
:   Display data for the month that is specified by using the YYYY-MM format. If not specified, usage of the current month is shown.

--output {FORMAT TYPE} (optional)
:   Specify the output format. Accepted inputs are JSON and CSV.

-q, --quiet (optional)
:   Suppress verbose output.

### Examples
{: #ibmcloud_billing_account_usage_examples}


Show the current account's usage and cost report for June 2024:

```bash
ibmcloud billing account-usage -d 2024-06
```
{: pre}

Show current account's usage and cost report for March 2025 and output to CSV format:

```bash
ibmcloud billing account-usage -d 2024-06 --output CSV
```
{: pre}

## ibmcloud billing resource-group-usage
{: #ibmcloud_billing_resource_group_usage}

Show monthly usage of all the resources and plans for a resource group (account admin or resource group admin only). 

To learn more about the resource group usage API, see [Get resource group usage](/apidocs/metering-reporting#get-resource-group-usage).


```bash
ibmcloud billing resource-group-usage GROUP_NAME [-d YYYY-MM] [--output FORMAT] [-q, --quiet]
```

### Command options
{: #ibmcloud_billing_resource_group_usage_options}

GROUP_NAME (required)
:    Name of the resource group.

-d {YEAR-MONTH} (optional)
:   Display data for the month that is specified by using the YYYY-MM format. If not specified, usage of the current month is shown.

--output {FORMAT} (optional)
:   Specify the output format. Only JSON is supported.

-q, --quiet (optional)
:   Suppress verbose output.

### Examples
{: #ibmcloud_billing_resource_group_usage_examples}

Show the usage for the `dev-test` resource group for the current month and output to JSON format:

```bash
ibmcloud billing resource-group-usage dev-test --output JSON
```
{: pre}

Show the usage for the `dev-test` resource group for July 2025:
```bash
ibmcloud billing resource-group-usage dev-test -d 2025-07
```
{: pre}


## ibmcloud billing resource-instances-usage
{: #ibmcloud_billing_resource_instances_usage}

Show monthly resource instances usage under the current account.

To learn more about the resource instances usage API, see [Get resource instance usage in an account](/apidocs/metering-reporting#get-resource-usage-account).

```bash
ibmcloud billing resource-instances-usage [-o ORG] [-g RESOURCE_GROUP] [-d YYYY-MM] [--output FORMAT] [-q, --quiet]
```

### Command options
{: #ibmcloud_billing_resource_instances_usage_options}

-o {ORG_NAME} (optional)
:   Filter instances by organization.

-g {GROUP_NAME}
:   Filter instance by resource group.

-d {YEAR-MONTH} (optional)
:   Display data for month that is specified by using the YYYY-MM format. If not specified, usage of the current month is shown.

--output {FORMAT} (optional)
:   Specify the output format. Accepted inputs are JSON and CSV.

-q, --quiet (optional)
:   Suppress verbose output.

### Examples
{: #ibmcloud_billing_resource_instances_usage_examples}

Show the usage for resource instances and output to JSON format:

```bash
ibmcloud billing resource-instances-usage --output JSON
```
{: pre}

## ibmcloud billing enterprise-usage
{: #ibmcloud_billing_enterprise_usage}

Show monthly resource usage for an enterprise, a specific account group, or a child account under the enterprise. For more information, see [Viewing usage in an enterprise](/docs/enterprise-management?topic=enterprise-management-enterprise-usage).

```bash
ibmcloud billing enterprise-usage [--account-group ACCOUNT_GROUP_NAME | --account-group-id ACCOUNT_GROUP_ID | --account ACCOUNT_NAME | --account-id ACCOUNT_ID] [--month MONTH] [--children] [--output FORMAT] [-q, --quiet]
```

### Command options
{: #ibmcloud_billing_enterprise_usage_options}

--account {ACCOUNT_NAME} (optional)
:   Name of target account.

--account-id {ACCOUNT_ID} (optional)
:   ID of target account.

--account-group {ACCOUNT_GROUP_NAME} (optional)
:   Name of target account group.

--account-group-id {ACCOUNT_GROUP_ID} (optional)
:   ID of target account group.

--children (optional)
:   Show children usage reports.

--month {MONTH} (optional)
:   Target month. Default to the current month.

--output {FORMAT} (optional)
:   Specify the output format. Only JSON is supported.

-q, --quiet (optional)
:   Suppress verbose output.

### Examples
{: #ibmcloud_billing_enterprise_usage_examples}

Show the current month's usage for an enterprise, including usage from child accounts, and output to JSON format.

```bash
ibmcloud billing enterprise-usage --children --output JSON
```
{: pre}

View usage for the Development account group for July 2024.

```bash
ibmcloud billing enterprise-usage --account-group Development --month 2024-07
```
{: pre}
