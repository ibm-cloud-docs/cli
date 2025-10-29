---

copyright:
  years: 2018, 2025
lastupdated: "2025-10-29"

keywords: cli, ibmcloud billing, view account, view usage, account usage, resource groups, resources, org-usage

subcollection: cli

---

{{site.data.keyword.attribute-definition-list}}

# Viewing billing and usage information (ibmcloud billing)
{: #ibmcloud_billing}

Use the following commands from the {{site.data.keyword.cloud}} Command Line Interface to retrieve resource usage and billing information. You can use these commands for viewing the monthly usage information for an account, enterprise, and even for a specific resource group.
{: shortdesc}

## ibmcloud billing account-usage
{: #ibmcloud_billing_account_usage}

Show monthly usage of the current account (account admin only):

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

Get the account's usage report that you're currently logged into for the month of June 2024 (2024-06):

```bash
ibmcloud billing account-usage -d 2024-06
```

## ibmcloud billing resource-group-usage
{: #ibmcloud_billing_resource_group_usage}

Show monthly usage for resources in a specific resource group (account admin or resource group admin only):

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

If you have a resource group named `devteam`, you can use the following command to view the current month's usage for the resources that are in the `devteam` resource group in your account:

```bash
ibmcloud billing resource-group-usage devteam
```

## ibmcloud billing resource-instances-usage
{: #ibmcloud_billing_resource_instances_usage}

Show monthly resource instances usage under the current account:
```bash
ibmcloud billing resource-instances-usage [-g RESOURCE_GROUP] [-d YYYY-MM] [--output FORMAT] [-q, --quiet]
```

### Command options
{: #ibmcloud_billing_resource_instances_usage_options}

-g {GROUP_NAME}
:   Filter instance by resource group.

-d {YEAR-MONTH} (optional)
:   Display data for month that is specified by using the YYYY-MM format. If not specified, usage of the current month is shown.

--output {FORMAT} (optional)
:   Specify the output format. Accepted inputs are JSON and CSV.

-q, --quiet (optional)
:   Suppress verbose output.

## ibmcloud billing enterprise-usage
{: #ibmcloud_billing_enterprise_usage}

Show enterprise usage reports:
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
