---

copyright:
  years: 2019, 2025
lastupdated: "2025-05-21"

keywords: cli, catalogs management, catalog

subcollection: cli

---

{{site.data.keyword.attribute-definition-list}}

# Catalogs management CLI plug-in
{: #manage-catalogs-plugin}

The {{site.data.keyword.cloud}} catalogs management command-line interface (CLI) provides additional capabilities for working with products in the {{site.data.keyword.cloud_notm}} catalog and the private catalogs in your account. You can use this CLI plug-in to manage your private catalogs, onboard private software products, and manage catalog visibility between the public catalog and your private catalogs.
{: shortdesc}

## Before you begin
{: #prereqs-managecatalogs}

* Install the {{site.data.keyword.cloud_notm}} CLI. For more information, see [Getting started with the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started). The prefix for running commands by using the {{site.data.keyword.cloud_notm}} CLI is `ibmcloud`.
* Before you run the registry commands, log in to {{site.data.keyword.cloud_notm}} with the `ibmcloud login` command to generate an access token and authenticate your session.

## Installing the catalogs management plug-in
{: #install-managecatalogs}

To install the catalogs management plug-in, run the following command:

```bash
ibmcloud plugin install catalogs-management
```
{: codeblock}

In the command line, you are notified when updates to the `ibmcloud` CLI and `catalogs-management` CLI plug-in are available. Ensure that you keep your CLI up to date so that you can use all the available commands and flags.

If you want to view the current version of your `catalogs-management` CLI plug-in, run `ibmcloud plugin list`.

To maintain privacy and security, don't put personal information in your catalog names or catalog descriptions.
{: important}

## ibmcloud catalog account add-approval-access
{: #catalog-account-add-approval}

Run the following command to add approval access to your catalog account.

```bash
ibmcloud catalog account add-approval-access [--account-ids IDS] [--object-kind KIND]
```
{: codeblock}

### Command options
{: #catalog-account-add-approval-access}

--object-kind VALUE

:   Provide the object kind.  Options are `offering`, `vpe`, `proxy_source`, or `preset_configuration`.

--account-ids VALUE

:   Provide a comma-separated list of account IDs prefixed with one of the following.  `-acct-` for regular accounts, `-ent-` for enterprise accounts, and `-entgrp-` for enterprise account groups.

## ibmcloud catalog account delete-approval-access
{: #catalog-account-delete-approval}

Run the following command to delete approval access to your catalog account.

```bash
ibmcloud catalog account delete-approval-access [--account-ids IDS] [--object-kind KIND]
```
{: codeblock}

### Command options
{: #catalog-account-delete-approval-access}

--object-kind VALUE

:   Provide the object kind.  Options are `offering`, `vpe`, `proxy_source`, or `preset_configuration`.

--account-ids VALUE

:   Provide a comma-separated list of account IDs prefixed with one of the following.  `-acct-` for regular accounts, `-ent-` for enterprise accounts, and `-entgrp-` for enterprise account groups.

## ibmcloud catalog account get-approval-list
{: #catalog-account-get-list}

Run the following command to get an approval list for your catalog account.

```bash
ibmcloud catalog account get-approval-list [--object-kind KIND]
```
{: codeblock}

### Command options
{: #catalog-account-get-approval-list}

--object-kind VALUE

:   Provide the object kind.  Options are `offering`, `vpe`, `proxy_source`, or `preset_configuration`.

## ibmcloud catalog account get-approval-list-source
{: #catalog-account-get-source}

Run the following command to get all target accounts pointing to a source.

```bash
ibmcloud catalog account get-approval-list-source [--approval-state STATE] [--enterprise-id ID] [--object-kind KIND]
```
{: codeblock}

### Command options
{: #catalog-account-get-approval-list-source}

--object-kind VALUE

:   Provide the object kind.  Options are `offering`, `vpe`, `proxy_source`, or `preset_configuration`.

--approval-state VALUE

:   Provide the approval state.  Options are `approved`, `pending`, or `rejected`.

--enterprise-id VALUE (optional)

:   Provide an enterprise or enterprise account group ID to view or manage requests for the enterprise. Prefix the ID with `-ent-` for an enterprise and `-entgrp` for an account group.

## ibmcloud catalog account set-approval-state-source
{: #catalog-account-set-source}

Run the following command to set the approval state for target accounts that point to a source.

```bash
ibmcloud catalog account set-approval-state-source [--account-ids IDS] [--approval-state STATE] [--enterprise-id ID] [--object-kind KIND]
```
{: codeblock}

### Command options
{: #catalog-account-set-approval-state-source}

--object-kind VALUE

:   Provide the object kind.  Options are `offering`, `vpe`, `proxy_source`, or `preset_configuration`.

--approval-state VALUE

:   Provide the approval state.  Options are `approved`, `pending`, or `rejected`.

--account-ids VALUE

:   Provide a comma-separated list of account IDs prefixed with one of the following. `-acct-` for regular accounts, `-ent-` for enterprise accounts, and `-entgrp-` for enterprise account groups.

--enterprise-id VALUE (optional)

:   Provide an enterprise or enterprise account group ID to view or manage requests for the enterprise. Prefix the ID with `-ent-` for an enterprise and `-entgrp` for an account group.

## ibmcloud catalog create
{: #create-catalog}

Use this command to create a new private catalog in your account. A private catalog is used to organize a set of products, private ones you add, or references to products in the {{site.data.keyword.cloud_notm}} catalog. A user must have access to your private catalog through an IAM access policy and the resource group that contains your private catalog to view and work with the products.

Target a resource group to create a catalog because the catalog exists in the context of a particular resource group. To get the list of resource groups, you can run the `ibmcloud resource groups` command, and then the `ibmcloud target -g "resource group"` command.
{: important}

```bash
ibmcloud catalog create --name CATALOG [--catalog-description "DESCRIPTION"]
```
{: codeblock}

### Command options
{: #create-catalog-options}

--name CATALOG

:   The catalog name.

--catalog-description DESCRIPTION (optional)

:   Short description for the new catalog.


### Example
{: #create-example}

Create a catalog called `dev-catalog` with the description `a catalog for development and testing purpsoses`.

```bash
ibmcloud catalog create --name dev-catalog --catalog-description "a catalog for development and testing purposes"
```
{: codeblock}

## ibmcloud catalog list
{: #get-catalogs}

Run the following command to retrieve the list of catalogs in this particular account.

```bash
ibmcloud catalog list [--output FORMAT]
```
{: codeblock}

### Command options
{: #get-catalogs-options}

--output FORMAT (optional)

:   Specifies output format. The default is terminal compatible and the only supported alternative is JSON. For example, `--output json`.

### Output
{: #get-catalogs-output}

The command returns the following output:

```bash
Name                                           ID                                     Description                   Last Updated
dev-catalog                                    93f592fb-e09b-4a53-bbd9-92f6ab9e253b   short-description             2019-11-21 21:28:28.347 +0000 UTC
ABDemoTestCatalog                              7a246530-e191-45e2-87cc-07c8c7033d2b   short-description             2019-08-19 17:43:48.59 +0000 UTC
```
{: screen}


## ibmcloud catalog get
{: #get-catalog}

Run the following command to retrieve information for a particular catalog in the account.

```bash
ibmcloud catalog get --catalog CATALOG [--output FORMAT]
```
{: codeblock}

### Command options
{: #get-catalog-options}


--catalog CATALOG

:   The catalog name or ID.

--output FORMAT (optional)

:   Specifies output format. The default is terminal compatible and the only supported alternative is JSON. For example, `--output json`.

### Output
{: #get-catalog-output}

The command returns the following output:

```bash
Name                                     Current State   Version Locator
dev-catalog
|__dev-offering
|  |__Openshift
|     |__1.0.0                           Draft           480fb4e3-d7ba-4e9b-9d4c-42f0ab811040.fd8f91a3-8027-4919-ad6d-c5189a4a8ee
```
{: screen}

## ibmcloud catalog delete
{: #delete-catalog}

Run the following command to delete a particular catalog in the account.

```bash
ibmcloud catalog delete --catalog CATALOG
```
{: codeblock}

### Command options
{: #delete-catalog-options}

--catalog CATALOG

:   The catalog name or ID.

## ibmcloud catalog search
{: #search-catalog}

Run the following command to search the public catalog for published products, including services and software.

```bash
ibmcloud catalog search <QUERY> [--catalog CATALOG] [--type TYPE] [-r, --region REGION] [-k, --kind KIND] [--fields FIELDS] [-p, --price PRICE] [-t, --tag TAG] [--sort-by PROPERTY] [--col COLUMNS] [--reverse] [--output TYPE] [--global]
```
{: codeblock}

### Command options
{: #search-catalog-options}


--type TYPE (optional)

:   Optional. Default is `services`. Valid options are `services` and `software`.

--catalog CATALOG (optional)

:   Search for the software published by your account. Specify the catalog name or ID to search by.

--output FORMAT (optional)

:   Specifies output format. Default is terminal compatible and the only alternative options are `json` and `csv`.

--kind KIND (optional)

:   The flag is only valid for searching services. Provide a comma-separated list of types of products.

--region REGION (optional)

:   The flag is only valid for searching services. Provide a comma-separated list of regions. Run `ibmcloud cs regions` to return a valid list.

--price PRICE (optional)

:   The flag is only valid for searching services. Provide a comma-separated list of pricing types.

--tag TAG (optional)

:   The flag is only valid for searching services. Provide a comma-separated list of tags.

--global (optional)

:   The flag is only valid for searching services. Use it to operate in a global scope.

--sort-by TYPE (optional)

:   The flag is only valid for searching services and used to order the search result. Available options are `name`, `displayname`, `kind`, `provider`, `created`, and `updated`.

--reverse (optional)

:   The flag is only valid for searching services. Use it to reverse the sorting order.

--fields FIELDS (optional)

:   The flag is only valid for searching services. Customize the table, for example, `--fields name,kind,metadata.service.iam_compatible`.


### Output
{: #search-catalog-output}

The command returns the following output:

```bash
Name                                       ID                                                    Category
2 Zone VPC                                 f10d9ae9-ac94-4718-b24a-3994241ae2a4-global           Networking
Apache                                     Qml0bmFtaS1hcGFjaGU=-global                           Developer Tools
Apache Airflow                             Qml0bmFtaS1haXJmbG93-global                           Databases
Apache Airflow                             Qml0bmFtaS1haXJmbG93-global                           Developer Tools
```
{: screen}

## ibmcloud catalog filter get
{: #get-filter}

Run the following command to retrieve filter details for either the account or a particular catalog.

```bash
ibmcloud catalog filter get --catalog CATALOG [--output FORMAT]
```
{: codeblock}

### Command options
{: #get-filter-options}


--catalog CATALOG

:   The catalog name or ID.

--account-group ACCOUNT GROUP

:   The account group name or ID. This field applies only to enterprise accounts.

--output FORMAT (optional)

:   Specifies output format. The default is terminal compatible and the only supported alternative is JSON. For example, `--output json`.


### Output
{: #get-filter-output}

The command returns the following output:

```text
Account: The IBM Cloud catalog is visible to all users in this account.

Filter:
Including IBM Cloud catalog

Type           Include   Tags
Pricing plan   false     Free
Provider       false     Third Party
```
{: screen}

## ibmcloud catalog filter create
{: #create-filter}

Run the following command to create a new filter. If a filter exists, this command overrides the current filter.

```bash
ibmcloud catalog filter create [--catalog CATALOG] [--category CATEGORY] [--compliance COMPLIANCE] [--deployment-target TARGET] [--exclude-list LIST] [--include-all ALL] [--include-list LIST] [--offering-format FORMAT] [--pricing-plan PLAN] [--provider PROVIDER] [--release RELEASE] [--type TYPE]
```
{: codeblock}

### Command options
{: #create-filter-options}

--catalog CATALOG (optional)

:   Specify the catalog name or ID. If not specified, the filter is created at the account level.

--account-group ACCOUNT GROUP

:   The account group name or ID. This option applies only to enterprise accounts.

--hide-ibm-catalog (optional)

:   By default, the catalog is visible to all users in this account. By providing this flag, you can make products available only to the users you choose by turning off visibility to the {{site.data.keyword.cloud_notm}} catalog and adding the products to your private catalogs.

--include-all BOOLEAN (optional)

:   Default is true if flag is not provided. Valid values are `true` and `false`. If set to true, the filter defaults to include the entire public catalog, and subsequent filters are excluded. If set to false, the filter excludes the entire public catalog, and subsequent flags are included. For more information, see [Managing catalog settings](/docs/account?topic=account-filter-account).

--offering-format FORMAT (optional)

--category CATEGORY (optional)

:   Provide the category that best fits how users might use your product. Categories are used to organize products in the catalog based on common solutions, function, or use. You can select only one category. Run the `ibmcloud catalog offering category-options` command to view all options. Default is `Developer tools`.

--compliance TYPE (optional)

:   Provide a comma-separated list of compliance categories that you want to include or exclude. Run the `ibmcloud catalog filter options` command to view all options.

--deployment-target TARGET (optional)

:   Provide a comma-separated list of deployment targets that you want to include or exclude. Run the `ibmcloud catalog filter options` command to view all options.

--exclude-list LIST (optional)

:   Provide a comma-separated list of product IDs or names that must be excluded in the filtered public catalog.

--include-list LIST (optional)

:   Provide a comma-separated list of product IDs or names that must be included in the filtered public catalog.
:   Provide a comma-separated list of product formats that you want to include or exclude. Run the `ibmcloud catalog filter options` command to view all options.

--pricing-plan PLAN (options)

:   Provide a comma-separated list of pricing plans that you want to include or exclude. Run the `ibmcloud catalog filter options` command to view all options.

--provider PROVIDER (optional)

:   Provide a comma-separated list of providers that you want to include or exclude. Run the `ibmcloud catalog filter options` command to view all options.

--release RELEASE (optional)

:   Provide a comma-separated list of categories that you want to include or exclude. Run the `ibmcloud catalog filter options` command to view all options.

--type TYPE (optional)

:   Provide a comma-separated list of software types that you want to include or exclude. Run the `ibmcloud catalog filter options` command to view all options.

## ibmcloud catalog filter delete
{: #delete-filter}

Run the following command to delete an applied filter. This filter defaults to the account level unless a catalog is specified. As a result, the filter is reset to include all products in the public catalog.

```bash
ibmcloud catalog filter delete --catalog CATALOG
```
{: codeblock}

### Command options
{: #delete-filter-options}


--catalog CATALOG

:   The catalog name or ID.

--account-group ACCOUNT GROUP

:   The account group name or ID. This option applies only to enterprise accounts.

## ibmcloud catalog filter offering
{: #offering-filter}

Update the filter to include or exclude a particular product and any applicable pricing plans. This filter defaults to the account level unless a catalog or account group is specified.

```bash
ibmcloud catalog filter offering --offering PRODUCT-NAME
```
{: codeblock}

### Command options
{: #get-filter-offering-options}


--catalog CATALOG

:   The catalog name or ID.

--account-group ACCOUNT GROUP

:   The account group name or ID. This option applies only to enterprise accounts.

--plans-list PLANS LIST

:   A comma-separated list of plan IDs or names to include or exclude.

--offering OFFERING

:   The product name or ID.

--include

:   The default value is true if a flag is not provided. Valid values are `true` and `false`. If set to true, the product and plans provided are visible to users in the account. If set to false, the product and plans aren't visible to users in the account.

## ibmcloud catalog filter hide-ibm-public-catalog
{: #hide-filter}

By default, the {{site.data.keyword.cloud_notm}} catalog is visible to all users in the account. You can make products available only to the users you choose by turning off visibility to the {{site.data.keyword.cloud_notm}} catalog and adding the products to your private catalogs.

```bash
ibmcloud catalog filter hide-ibm-public-catalog
```
{: codeblock}

## ibmcloud catalog filter show-ibm-public-catalog
{: #show-filter}

By default, the {{site.data.keyword.cloud_notm}} catalog is visible to all users in the account. You can make products available only to the users you choose by turning off visibility to the {{site.data.keyword.cloud_notm}} catalog and adding the products to your private catalogs.

```bash
ibmcloud catalog filter show-ibm-public-catalog
```
{: codeblock}

## ibmcloud catalog filter options
{: #options-filter}

Run the following command to retrieve the filter options for each filter category.

```bash
ibmcloud catalog filter options
```
{: codeblock}

### Command options
{: #options-filter-options}

--all

:   Includes industry, solution type, and pricing plan in the list of filters.

--output FORMAT (optional)

:   Specifies output format. The default is terminal compatible and the only supported alternative is JSON. For example, `--output json`.


### Output
{: #options-filter-output}

The command returns the following output:

```bash
Deployment target              ID
IBM Cloud Kubernetes Service   target_iks
IBM Cloud Schematics           target_terraform
Red Hat OpenShift              target_roks
VMware vCenter Server          target_vcenter
Virtual private cloud          target_vpc-x86
Power Systems Virtual Server   target_power-iaas

Provider      ID
Third party   ibm_third_party
Community     ibm_community
IBM           ibm_created

Release      ID
Beta         ibm_beta
Deprecated   ibm_deprecated

Works with             ID
SAP Certified          sap_certified
Quantum Technologies   quantum_tech
Satellite Enabled      satellite_enabled
HPC                    hpc

Support                 ID
Third party supported   support_third_party
Community supported     support_community
IBM supported           support_ibm

Delivery method   ID
Cloud Paks        cloud_pak
Helm charts       helm
Operators         operator
OVA Images        ova
Starter kits      template
Terraform         terraform
Server Images     vsi_image
Blueprint         blueprint
Toolchains        toolchain

Compliance                     ID
EU Supported                   eu_access
Financial Services Validated   fs_ready
HIPAA Enabled                  hipaa
IAM-enabled                    rc_compatible
Service Endpoint Supported     service_endpoint_supported

Category                   ID                   Tags
Compute                    compute              compute,compute_classic,content,openwhisk,runtime,virtualservers,compute_baremetal
Containers                 containers           containers,clusters,registry
Networking                 network              network,network_vpc,network_classic,network_edge,network_interconnectivity
Storage                    storage              storage,storage_vpc,storage_classic,storage_datamovement
Converged infrastructure   converged_infra      converged_infra
Enterprise applications    enterprise_app       enterprise_app
AI / Machine Learning      ai                   watson,ai
Analytics                  analytics            data_analytics,business_analytics,analytics
Blockchain                 blockchain           blockchain
Databases                  databases            data_management,database
Developer tools            devops               dev_ops
Logging and monitoring     logging_monitoring   logging_monitoring
Migration                  migration_tools      migration_tools
Integration                integration          integration,api
Internet of Things         iot                  internet_of_things
Security                   security             security
Mobile                     mobile               mobile,web_and_app
```
{: screen}

## ibmcloud catalog offering create
{: #create-offering}

Run the following command to add a product to a private catalog in the account.

```bash
ibmcloud catalog offering create [--catalog CATALOG_NAME] [--zipurl URL] [--include-config] [--target-version VERSION] [--token TOKEN] [--vpc-body BODY]
```
{: codeblock}

### Command options
{: #create-offering-options}

--catalog CATALOG_NAME

:   The catalog name or ID.

--zipurl URL (optional)

:   URL pointing to the .zip file of the product.

--target-version VERSION

:   Specify the version of the product.

--include-config (optional)

:   If provided, all configuration values are included and available when you add the product.

--token TOKEN (optional)

:   Specify the personal access token for a private repository.

--vpc-body BODY (optional)

:   Provide the information to import a virtual server image for VPC, including a name, label, install kind, target kind, version, sha, tags, and metadata.

### Virtual server image for VPC Example #1
{: #import-offering-example-1}

Import a virtual server image for VPC as an offering to a catalog with ID `51c9e0db-2911-45a6-adb0-ac5332d27cf2`.

```bash
ibmcloud catalog offering create --catalog 51c9e0db-2911-45a6-adb0-ac5332d27cf2 --vpc-body '{
    "name": "virtual-server-image",
    "label": "virtual server image",
    "install_kind": "instance",
    "target_kinds": ["vpc-x86"],
    "version": "0.0.10",
    "sha": "64245e5f3f1e9c4048b18db3abd1450d4b6f9e263ac1b33df6fc1ae96fcbdebb",
    "tags": ["virtualservers"],
    "metadata": {
        "operating_system": {
            "dedicated_host_only": false,
            "vendor": "CentOS",
            "name": "centos-7-amd64",
            "href": "https://us-south-stage01.iaasdev.cloud.ibm.com/v1/operating_systems/centos-7-amd64",
            "display_name": "CentOS 7.x - Minimal Install (amd64)",
            "family": "CentOS",
            "version": "7.x - Minimal Install",
            "architecture": "amd64"
        },
        "minimum_provisioned_size": 100,
        "file": {
            "size": 1
        },
        "images": [{"id": "r134-14903434-faf0-4a66-b861-7b35198de393", "name": "virtual-server-image", "region": "us-south"}]
    }
}'
```
{: codeblock}

### Virtual server image for VPC Example #2
{: #import-offering-example-2}

Import a virtual server image for VPC as an offering to a catalog with ID `2bdc3974-dfcf-4711-b298-cd238f7d3734`.

```bash
ibmcloud catalog offering create --catalog 2bdc3974-dfcf-4711-b298-cd238f7d3734 --vpc-body '{
"name": "virtual-server-image-s390x",
"label": "virtual-server-image-s390x",
"install_kind": "instance",
"target_kinds": ["vpc-z"],
"version": "0.0.10",
"sha": "4739f1eaeeebc69ad5d48f9191fcc0d23960cb720bb16c67e915e5556c1da9b2",
"tags": ["virtualservers"],
"metadata": {
    "operating_system": {
        "dedicated_host_only": false,
        "vendor": "SUSE Linux Enterprise Server",
        "name": "sles-15-sp2-s390x-byol",
        "href": "https://us-south-stage01.iaasdev.cloud.ibm.com/v1/operating_systems/sles-15-s390x",
        "display_name": "Suse enterprise server(s390x)",
        "family": "SUSE",
        "version": "15-sp2",
        "architecture": "s390x"
    },
    "minimum_provisioned_size": 100,
    "file": {
        "size": 1
    },
    "images": [{"id": "r134-f20e2e4e-3133-423c-afa2-365afa14c4dc", "name": "virtual-server-image-s390x", "region": "us-south"}]
}
```

## ibmcloud catalog offering list
{: #list-offering}

Run the following command to get details about the products in your private catalogs. This command provides a filter by private catalog, product, and version.

```bash
ibmcloud catalog offering list [--catalog CATALOG] [--offering OFFERING_NAME] [--version VERSION] [--output FORMAT]
```
{: codeblock}

### Command options
{: #list-offering-options}


--catalog CATALOG

:   The catalog name or ID.

--output FORMAT (optional)

:   Specifies output format. The default is terminal compatible and the only supported alternative is JSON, for example, `--output json`.


### Example
{: #get-example}

List all of the products that are in the `dev-catalog` catalog.

```bash
ibmcloud catalog offering list --catalog dev-catalog
```
{: codeblock}

### Output
{: #list-offering-output}

The command returns the following output:

```bash
Name                                   ID                                     Current State   Version Locator
Cloud Pak for Automation               cb90274e-398b-4373-9b28-d6428d3302df
|__OpenShift
   |__19.0.2                                                                  New             7b7e590f-259b-437b-b1f4-39e8615ed837.21d1d712-80ab-4318-9d05-73c6caaaee23
Cloud Pak for Data                     8993c7b1-1794-4447-9275-db83faa08ee4
|__OpenShift
   |__2.1.0.2                                                                 New             7b7e590f-259b-437b-b1f4-39e8615ed837.ab6ba56f-788d-4d6b-b880-a1001fca8451
harbor                                 927adb44-6784-4bec-a771-f639900f07f1
|__Kubernetes
   |__1.9.1                                                                   New             7b7e590f-259b-437b-b1f4-39e8615ed837.e437b06c-273f-49de-8c44-f55e408abf78
IBM Starter Collection for Openshift   fd1857f4-cf17-4e97-9443-b615bc71f6a0
|__OpenShift
   |__0.0.1                                                                   New             7b7e590f-259b-437b-b1f4-39e8615ed837.72e0f636-9dc4-49ae-b3c2-7a5de90487b9
tf_cloudless_sleepy-2.0                c260a67a-1b25-49fc-9896-46e7e6212990
|__
   |__1.0.0                                                                   New             7b7e590f-259b-437b-b1f4-39e8615ed837.965df91d-5760-4872-adf6-4019796c06b0
   |__1.0.1                                                                   New             7b7e590f-259b-437b-b1f4-39e8615ed837.aff4cecb-4c9b-41ba-ae3d-71f4217dc0bc
```
{: screen}

## ibmcloud catalog offering search
{: #search-catalog-offering-search}

Run the following command to get details about the products in your private catalogs. This command provides a filter by private catalog, product, and version.

```bash
ibmcloud catalog offering search [--catalog CATALOG] [--offering OFFERING_NAME] [--version VERSION] [--output FORMAT]
```
{: codeblock}

### Command options
{: #search-offering-options}


--catalog CATALOG (optional)

:   The catalog name or ID.

--offering OFFERING (optional)

:   The product name or ID.

--version VERSION (optional)

:   The version name or ID.

--output FORMAT (optional)

:   Specifies output format. The default is terminal compatible and the only supported alternative is JSON, for example, `--output json`.


### Example
{: #search-example}

List all of the products that are in the `dev-catalog` catalog.

```bash
ibmcloud catalog offering list --catalog dev-catalog
```
{: codeblock}

### Output
{: #search-offering-output}

The command returns the following output:

```bash
Name                                     Current State          Version Locator
dev-catalog
|__dev-offering
|  |__Kubernetes
|     |__1.0.0                           Validated              b636d651-8489-4425-bd6a-f30af1603577.17ac792e-a603-4f1a-a1b6-48e90a46940c
|__dev-offering-2.0
|  |__Kubernetes
|     |__1.0.0                           Published to account   b636d651-8489-4425-bd6a-f30af1603577.decdb0e1-46d2-401a-b482-80f9d6855f98
```
{: screen}

## ibmcloud catalog offering get
{: #get-offering}

Run the following command to get details about a specific product in the catalog.

```bash
ibmcloud catalog offering get --catalog CATALOG --offering OFFERING_NAME [--output FORMAT]
```
{: codeblock}

### Command options
{: #get-offering-options}


--catalog CATALOG
:   The catalog name or ID.

--offering OFFERING_NAME
:   The product name or ID.

--output FORMAT (optional)
:   Specifies output format. The default is terminal compatible and the only supported alternative is JSON, for example, `--output json`.


### Output
{: #get-offering-output}

The command returns the following output:

```bash
Name           Current State   Version Locator
dev-offering
|__
   |__1.0.0    Draft           480fb4e3-d7ba-4e9b-9d4c-42f0ab811040.a92f5409-ebd9-413c-88ae-7ed311c1b793
```
{: screen}


## ibmcloud catalog offering import-version
{: #import-offering-version}

Run the following command to import a new version of a product in your private catalog.

```bash
ibmcloud catalog offering import-version --catalog CATALOG --offering OFFERING_NAME [--zipurl URL] [--target-version APP_VERSION] [--include-config] [--vpc-body BODY]
```
{: codeblock}

### Command options
{: #import-offering-version-options}


--catalog CATALOG
:   The catalog name or ID.

--offering OFFERING_NAME
:   :   The product name or ID.

--zipurl URL (optional)
:   The URL pointing to the .zip file of the product.

--target-version APP_VERSION (optional)
:   The application version of the \"tgz\" being imported.

--include-config (optional)
:   If provided, all configurations values are included and available when you import the new version.

--vpc-body BODY (optional)
:   Provide the information to import a virtual server image for VPC, including a name, label, install kind, target kind, version, sha, tags, and metadata.

### Virtual server image for VPC Example
{: #import-version-example}

Import a virtual server image for VPC to an existing offering with to a catalog with ID `51c9e0db-2911-45a6-adb0-ac5332d27cf2` and offering ID `97cdaf1b-62b2-48e2-8589-10b31023866d`.

```bash
ibmcloud catalog offering import-version --catalog 51c9e0db-2911-45a6-adb0-ac5332d27cf2 --offering 97cdaf1b-62b2-48e2-8589-10b31023866d --vpc-body '{
    "name": "virtual-server-image",
    "label": "virtual server image",
    "install_kind": "instance",
    "target_kinds": ["vpc-x86"],
    "version": "0.0.10",
    "sha": "64245e5f3f1e9c4048b18db3abd1450d4b6f9e263ac1b33df6fc1ae96fcbdebb",
    "tags": ["virtualservers"],
    "metadata": {
        "operating_system": {
            "dedicated_host_only": false,
            "vendor": "CentOS",
            "name": "centos-7-amd64",
            "href": "https://us-south-stage01.iaasdev.cloud.ibm.com/v1/operating_systems/centos-7-amd64",
            "display_name": "CentOS 7.x - Minimal Install (amd64)",
            "family": "CentOS",
            "version": "7.x - Minimal Install",
            "architecture": "amd64"
        },
        "minimum_provisioned_size": 100,
        "file": {
            "size": 1
        },
        "images": [{"id": "r134-14903434-faf0-4a66-b861-7b35198de393", "name": "virtual-server-image", "region": "us-south"}]
    }
}''
```
{: codeblock}

## ibmcloud catalog offering update
{: #update-offering}

To update a product in your private catalog, you first need to get the product and then you can update.

Run the `offering get` command. For more information, see the [ibmcloud catalog offering get](#get-offering).

```bash
ibmcloud catalog offering get -c <CATALOGID> -o <OFFERINGID> --output json
```
{: codeblock}

Run the `offering update` command.

```bash
ibmcloud catalog offering update -c <CATALOGID> -o <OFFERINGID> --updated-offering <UPDATED_OFFERING.json>
```
{: codeblock}



## ibmcloud catalog offering version preinstall
{: #preinstall-offering}

Run the following command to run the preinstallation script for a particular product.

```bash
ibmcloud catalog offering version preinstall --version-locator VERSION_NUMBER --cluster CLUSTER_ID --namespace NAME
```
{: codeblock}

### Command options
{: #preinstall-offering-options}


--version-locator VERSION_NUMBER
:   To get the version locator for this product, run the `ibmcloud catalog offering list` command and locate the specified product and version that you'd like to use.

--cluster CLUSTER_ID
:   Provide the cluster ID of the cluster where you want to install the product.

--namespace NAME
:   Provide the namespace that you'd like to use. You can specify a new one and it is automatically created as part of the preinstallation.


### Example
{: #preinstall-example}

Run the preinstallation script for a product with a version locator number of `b636d651-8489-4425-bd6a-f30af1603577.18aad484-c78b-4269-808b-52027621abd4` in cluster with ID `bn5ebho206o7fg45f2e0` in the namespace called `test-namespace`.

```bash
ibmcloud catalog offering version preinstall --version-locator b636d651-8489-4425-bd6a-f30af1603577.18aad484-c78b-4269-808b-52027621abd4 --cluster bn5ebho206o7fg45f2e0 --namespace test-namespace
```
{: codeblock}

## ibmcloud catalog offering version preinstall-status
{: #preinstall-status-offering}

Run the following command to get the status of an ongoing preinstallation.

```bash
ibmcloud catalog offering version preinstall-status --version-locator VERSION_NUMBER --cluster CLUSTER_ID --namespace NAME [--output FORMAT]
```
{: codeblock}

### Command options
{: #preinstall-status-offering-options}


--version-locator VERSION_NUMBER
:   To get the version locator for the product, run the `ibmcloud catalog offering list` command and locate the specified product and version that you'd like to use.

--cluster CLUSTER_ID
:   Provide the cluster ID of the cluster where the preinstallation was run.

--namespace NAME
:   Provide the namespace used for the preinstallation.

--output FORMAT (optional)
:   Specifies output format. The default is terminal compatible and the only supported alternative is JSON, for example, `--output json`.


## ibmcloud catalog offering version validate
{: #validate-offering}

Run the following command to validate a new version of a product in your private catalog. Products must be validated to ensure that they work as expected before they can be published to the account for other users to create an instance from the private catalog.

```bash
ibmcloud catalog offering version validate --version-locator VERSION_NUMBER --cluster CLUSTER_ID --namespace NAME [--timeout TIMEOUT] [--wait WAIT] [--override-values VALUES|FILENAME] [--workspace-tf-version VERSION] [--workspace-region REGION] [--workspace-rg-id ID][--schematics-destroy][--schematics-delete]
```
{: codeblock}

### Command options
{: #validate-offering-options}


--version-locator VERSION_NUMBER
:   To get the version locator for the product, run the `ibmcloud catalog offering list` command and locate the specified product and version you'd like to use.

--cluster CLUSTER_ID
:   Provide the cluster ID of the cluster where you want to install the product.

--namespace NAME
:   Provide the namespace that you'd like to use. You can specify a new one and it is automatically created as part of the preinstallation.

--timeout TIMEOUT
:   Specify in seconds how long the {{site.data.keyword.bpshort}} workspace waits it installs. Default is `180`.

--wait WAIT
:   Wait and track the progress of the {{site.data.keyword.bpshort}} workspace job. If `true`, installation waits. If `false`, the software installs immediately. Default is `true`.

--override-values VALUES|FILENAME (optional)
:   Provide any custom configurations for the installation. You can provide this value either inline or by using a JSON or TXT file.
For example, `override-values values.json`. When validating a virtual server image for VPC, the following fields must be provided:
vsi_instance_name, vsi_id, vpc_profile, subnet_id, vpc_id, subnet_zone, ssh_key_id, vpc_region

--workspace-tf-version VERSION (optional)
:   Provide a workspace terraform version.

--workspace-region REGION (optional)
:   Provide a workspace region.

--workspace-rg-id ID (optional)
:   Provide a workspace resource group ID.

--schematics-destroy (optional)
:   Provide this flag to delete the workspace resources after validation and installation.

--schematics-delete VALUE (optional)
:   Provide this flag to delete the {{site.data.keyword.bpshort}} workspace after validation and installation.

### Example validating a product that uses a cluster
{: #validate-example}

Validate a product with the version locator `b636d651-8489-4425-bd6a-f30af1603577.18aad484-c78b-4269-808b-52027621abd4` in a cluster with the ID `bn5ebho206o7fg45f2e0` within a namespace called `test-namespace`. This installation has custom configurations, so the values are provided by using a `values.json` file.

```bash
ibmcloud catalog offering version validate --version-locator b636d651-8489-4425-bd6a-f30af1603577.18aad484-c78b-4269-808b-52027621abd4 --cluster bn5ebho206o7fg45f2e0 --namespace test-namespace --override-values values.json
```
{: codeblock}

Override values example format from the `values.json` file:

```bash
{
  "username": "provision-test-1",
  "password": "passw0rd"
}
```
{: codeblock}

### Virtual server image for VPC Example
{: #vs-image-example}

Validate a product with the version locator `51c9e0db-2911-45a6-adb0-ac5332d27cf2.ecebffdc-f1f8-4a85-965f-9cbe31920542` in
a VPC with the ID `r134-476cbb67-a6c2-4957-9806-3fcbac3498be`.

```bash
ibmcloud catalog offering version validate --version-locator 51c9e0db-2911-45a6-adb0-ac5332d27cf2.ecebffdc-f1f8-4a85-965f-9cbe31920542 --workspace-region=us-south --workspace-rg-id Default --override-values '{
  "vsi_instance_name": "instance-name-1",
  "vsi_id": "r134-14903434-faf0-4a66-b861-7b35198de393",
  "vpc_profile": "bx2-2x8",
  "subnet_id": "0716-d799c449-466c-4844-902c-a5d3f8948d7d",
  "vpc_id": "r134-476cbb67-a6c2-4957-9806-3fcbac3498be",
  "subnet_zone": "us-south-1",
  "ssh_key_id": "r134-0c53e7f2-771f-4d0e-a19e-39f2e6e6949c",
  "vpc_region": "us-south"
}
```
{: codeblock}

## ibmcloud catalog offering version validate-status
{: #validate-status-offering}

Run the following command to get the status of an ongoing validation.

```bash
ibmcloud catalog offering version validate-status --version-locator VERSION_NUMBER [--output FORMAT]
```
{: codeblock}

### Command options
{: #validate-status-offering-options}


--version-locator VERSION_NUMBER
:   To get the version locator for the product, run the `ibmcloud catalog offering list`command and locate the specified product or version you want to use.

--output FORMAT (optional)
:   Specifies output format. The default is terminal compatible and the only supported alternative is JSON, for example, `--output json`.



## ibmcloud catalog offering category-options
{: #category-options-offering}

Run the following command to retrieve the list of category choices.

```bash
ibmcloud catalog offering category-options [--output FORMAT]
```
{: codeblock}

### Command options
{: #category-options-offering-options}


--output FORMAT (optional)
:   Specifies output format. The default is terminal compatible and the only supported alternative is JSON, for example, `--output json`.


### Example
{: #category-options-offering-example}

```bash
ibmcloud catalog offering category-options
```
{: codeblock}


### Output
{: #category-options-offering-output}

The command returns the following output:

```bash
Name                    Tags                                                  Description
VPC Infrastructure      vpc                                                   Fully customizable, software-defined virtual network with superior isolation.
Compute                 compute,content,containers,openwhisk,vmware,runtime   Build your virtual environments
Containers              containers,clusters,registry                          Get started by creating a Kubernetes cluster, or manage your Docker images in the registry.
Networking              network                                               Order network.
Storage                 storage                                               Order storage.
```
{: screen}

## ibmcloud catalog offering add-category
{: #add-category-offering}

Run the following command to add a category tag to a product. You can provide the category name, which you can find by running the `ibmcloud catalog offering category-options` command. The products must be placed in a category to be visible in the catalog. Default is `Developer tools`.

```bash
ibmcloud catalog offering category-options [--output FORMAT]
```
{: codeblock}

### Command options
{: #add-category-offering-options}


--catalog CATALOG
:   The catalog name or ID.

--offering OFFERING
:   The product name or ID.

--category CATEGORY
:  Provide the category that best fits how users might use your product. Categories are used to organize products in the catalog based on common solutions, function, or use. You can select only one category. Run the `ibmcloud catalog offering category-options` command to view all options. Default is `Developer tools`.


### Example
{: #add-category-offering-example}

```bash
ibmcloud catalog offering add-category --catalog dev-catalog --offering dev-offering --category dev_ops
```
{: codeblock}

## ibmcloud catalog offering categories
{: #categories-offering}

Run the following command to retrieve the category of a product version.

```bash
ibmcloud catalog offering version categories [--catalog CATALOG] [--offering OFFERING] [--output OUTPUT]
```
{: codeblock}

### Command options
{: #categories-offering-options}

--catalog CATALOG
:   The catalog name or ID.

--offering OFFERING
:   The product name or ID.

--output FORMAT (optional)
:   Specifies output format. The default is terminal compatible and the only supported alternative is JSON. For example, `--output json`.

### Example
{: #categories-offering-example}

Retrieve the category of a product that is called `dev-offering` and located in the `dev-catalog`.

```bash
ibmcloud catalog offering version categories --catalog dev-catalog --offering dev-offering
```
{: codeblock}

## ibmcloud catalog offering version get-claims
{: #get-claims}

Run the following command to retrieve the security and compliance information that a version claimed.

```bash
  ibmcloud catalog offering version get-claims [--output OUTPUT] [--version-locator LOCATOR]
```
{: codeblock}

### Command options
{: #get-claims-options}

--version-locator LOCATOR
:   To get the version locator for the product, run the `ibmcloud catalog offering list` command and locate the specified product or version you want to use.

--output value (optional)
:   Specifies output format. The default is terminal compatible and the only supported alternative is JSON, for example, `--output json`.

## ibmcloud catalog offering version update-claims
{: #update-claims}

Run the following command to update the security and compliance claims of a version.

```bash
  ibmcloud catalog offering version update-claims [--claims CLAIMS] [--version-locator LOCATOR]
```
{: codeblock}

### Command options
{: #update-claims-options}

--claims CLAIMS
:   Specify the claims data for a version as a JSON object or file.

--version-locator LOCATOR
:   To get the version locator for the product, run the `ibmcloud catalog offering list` command and locate the specified product or version you want to use.

## ibmcloud catalog offering version scc-apply
{: #scc-apply}

Run the following command to add a Security and Compliance Center scan to your version. Add security and compliance information to your version and validate your version before you can add a scan.

```bash
  ibmcloud catalog offering version scc-apply [--instance-region REGION] [--scan SCAN] [--service-instance INSTANCE] [--target-account-name NAME] [--target-api-key KEY] [--timeout TIMEOUT] [--version-locator LOCATOR] [--wait WAIT]
```
{: codeblock}

### Command options
{: #scc-apply-options}

--instance-region REGION
:   The region of the instance.

--scan SCAN
:   The ID of a Security and Compliance Center scan.

--service-instance INSTANCE
:   Provide the Security and Compliance Center instance ID.

--target-account-name NAME (optional)
:   Provide the name of the target account.

--target-api-key KEY (optional)
:   Provide an API key if you want to use an alternative account (target account) to apply a scan to your source account. For more information, see [Setting up a target account](/docs/account?topic=account-catalog-cross-validation).

--timeout TIMEOUT
:   Specify in seconds how long you want to wait for the scan to be applied to the version before the command returns. The default value is 600 (10 minutes).

--version-locator LOCATOR
:   To get the version locator for the product, run the `ibmcloud catalog offering list` command and locate the specified product or version you want to use.

--wait WAIT
:   Wait and track the progress of a scan application. Default is true if flag is not provided. If `true`, the command tracks the progress of the scan application. If `false`, the command returns immediately.

## ibmcloud catalog offering version scc-apply-status
{: #scc-apply-status}

Run the following command to see the status of a Security and Compliance Center scan application to your version.

```bash
  ibmcloud catalog offering version scc-apply-status [--scan SCAN] [--version-locator LOCATOR]
```
{: codeblock}

### Command options
{: #scc-apply-status-options}

--scan SCAN
:   The ID of a Security and Compliance Center scan.

--version-locator LOCATOR
:   To get the version locator for the product, run the `ibmcloud catalog offering list` command and locate the specified product or version you want to use.

## ibmcloud catalog offering version get-scans
{: #get-scans}

Run the following command to retrieve the Security and Compliance Center scans that are added to your version.

```bash
  ibmcloud catalog offering version get-scans [--instance-region REGION] [--output OUTPUT] [--profiles PROFILES] [--service-instance INSTANCE] [--target-account-name NAME] [--target-api-key KEY]
```
{: codeblock}

### Command options
{: #get-scans-options}

--instance-region REGION
:   Provide the region of the instance.

--output OUTPUT (optional)
:   Specifies output format. The default is terminal compatible and the only supported alternative is JSON. For example, `--output json`.

--profiles PROFILES
:   Provide a comma-separated list of profile names with versions, for example, `"IBM Cloud for Financial Services::1.2.0"`.

--service-instance INSTANCE
:   Provide the Security and Compliance Center instance ID.

--target-account-name NAME (optional)
:   Provide the name of the target account.

--target-api-key KEY (optional)
:   Provide an API key if you want to use an alternative account (target account) to apply a scan to your source account. For more information, see [Setting up a target account](/docs/account?topic=account-catalog-cross-validation).

## ibmcloud catalog offering get-scan-results
{: #get-scan-results}

Run the following command to generate a report of your version's Code Risk Analyzer and Security and Compliance Center scan results. To generate a full report, you must run the Code Risk Analyzer and Security and Compliance Center scans. 

```bash
ibmcloud catalog offering get-scan-results [--version-locator LOCATOR]
```
{: codeblock}

### Command options
{: #get-scan-results-options}

--version-locator LOCATOR
:   To get the version locator for the product, run the `ibmcloud catalog offering list` command and locate the specified product or version you want to use.

## ibmcloud catalog offering version create-draft
{: #create-offering-draft}

Run the following command to create a draft of an existing version. This command is useful for changing an existing version that you want to publish without introducing a new version. Some changes, like changing the source file, require you to revalidate the product.

```bash
ibmcloud catalog offering version create-draft --version-locator VERSION_NUMBER [--output FORMAT]
```
{: codeblock}

### Command options
{: #create-offering-draft-options}


--version-locator VERSION_NUMBER
:   To get the version locator for the product, run the `ibmcloud catalog offering list` command and locate the specified product or version you want to use.

--output FORMAT (optional)
:   Specifies output format. The default is terminal compatible and the only supported alternative is JSON. For example, `--output json`.

## ibmcloud catalog offering version delete-version
{: #offering-delete-version}

Run the following command to delete a version of a product.

```bash
ibmcloud catalog offering version delete-version --version-locator VERSION_NUMBER [--output FORMAT]
```
{: codeblock}

### Command options
{: ##offering-delete-version-options}


--version-locator VERSION_NUMBER
:   To get the version locator for the product, run the `ibmcloud catalog offering list` command and locate the specified product or version you want to use.

--output FORMAT (optional)
:   Specifies output format. The default is terminal compatible and the only supported alternative is JSON. For example, `--output json`.

## ibmcloud catalog offering version deprecate-version
{: #publish-version-deprecate}

Run the following command to deprecate a previously published product version from the {{site.data.keyword.cloud_notm}} catalog.

```bash
ibmcloud catalog offering version deprecate-version --version-locator VERSION_NUMBER
```
{: codeblock}

### Command options
{: #publish-version-deprecate-options}


--version-locator VERSION_NUMBER
:   To get the version locator for the product, run the `ibmcloud catalog offering list` command and locate the specified product or version you want to use.

## ibmcloud catalog offering version refresh-version
{: #refresh-offering-version}

Run the following command to create a change in the source file of a draft version. This command is useful for updating an existing version.

```bash
ibmcloud catalog offering version refresh-version --version-locator VERSION_NUMBER --zipurl URL [--include-config]
```
{: codeblock}

### Command options
{: #refresh-offering-version-options}


--version-locator VERSION_NUMBER
:   To get the version locator for the product, run the `ibmcloud catalog offering list` command and locate the specified product or version you want to use.

--zipurl URL
:   The URL pointing to the compressed file of the product.

--include-config (optional)
:   If provided, all configuration values are included and available when you add the product.


## ibmcloud catalog offering version merge-draft
{: #merge-offering-draft-version}

Run the following command to merge a draft version of a product.

```bash
ibmcloud catalog offering version merge-draft --version-locator VERSION_NUMBER
```
{: codeblock}

### Command options
{: #merge-offering-draft-version-options}

--version-locator VERSION_NUMBER
:   To get the version locator for the product, run the `ibmcloud catalog offering list` command and locate the specified product or version you want to use.

## ibmcloud catalog offering enable-sharing
{: #share-offering}

Run the following command to enable your product to be shared.

```bash
ibmcloud catalog offering enable-sharing --catalog CATALOG --offering OFFERING
```
{: codeblock}

### Command options
{: #share-offering-options}

--catalog CATALOG
:   The catalog name or ID.

--offering OFFERING
:   The product name or ID.

## ibmcloud catalog offering ready
{: #ready-offering}

Run the following command to mark your product as ready to share or publish.

```bash
ibmcloud catalog offering ready --version-locator VERSION_NUMBER
```
{: codeblock}

### Command options
{: #ready-offering-options}

--version-locator VERSION_NUMBER
:   To get the version locator for the product, run the `ibmcloud catalog offering list` command and locate the specified product or version you want to use.

## ibmcloud catalog offering delete
{: #delete-offering}

Run the following command to delete a product from your private catalog. You cannot delete a product that is published in the {{site.data.keyword.cloud_notm}} catalog. To deprecate a published product from the {{site.data.keyword.cloud_notm}} catalog, see [`ibmcloud catalog offering deprecate-offering`](/docs/cli?topic=cli-manage-catalogs-plugin#publish-offering-deprecate).

```bash
ibmcloud catalog offering delete --catalog CATALOG --offering OFFERING
```
{: codeblock}

### Command options
{: #delete-offering-options}

--catalog CATALOG
:   The catalog name or ID.

--offering OFFERING
:   The product name or ID.


## ibmcloud catalog offering publish account
{: #publish-offering-to-account}

Run the following command to publish a product from your private catalog to an account. After the product is published, users in the account that have access to the private catalog. Its containing resource group can create an instance and start to use it.

```bash
ibmcloud catalog offering publish account [--catalog CATALOG][--offering OFFERING]
```
{: codeblock}

### Command options
{: #publish-offering-to-account-options}

--catalog CATALOG
:   The catalog name or ID.

--offering OFFERING
:   The product name or ID.

## ibmcloud catalog offering publish allowlist
{: #publish-offering-allowllist}

Run the following command to publish a product from your private catalog to a set of allowlisted accounts. After the product is published, users in the allowlisted accounts can create an instance and start to use it.

```bash
ibmcloud catalog offering publish allowlist [--catalog CATALOG][--offering OFFERING][--account-ids ACCOUNT-IDS]
```
{: codeblock}

### Command options
{: #publish-offering-allowlist-options}

--catalog CATALOG
:   The catalog name or ID.

--offering OFFERING
:   The product name or ID.

--account-ids ACCOUNT-IDS
:   The account IDs.


## ibmcloud catalog offering publish enterprise
{: #publish-offering-enterprise}

Run the following command to publish a product to an enterprise. After the product is published, users within the enterprise can create an instance of the product.

```bash
ibmcloud catalog offering publish enterprise [--catalog CATALOG][--offering OFFERING]
```
{: codeblock}

### Command options
{: #publish-offering-enterprise-options}


--catalog CATALOG
:   The catalog name or ID.

--offering OFFERING
:   The product name or ID.

## ibmcloud catalog offering suspend-offering
{: #suspend-offering}

Run the following command to suspend a product from the catalog. You can suspend it for a short time without permanently deleting or deprecating it. Suspending a product can be useful if, for example, you discover a bug or a vulnerability in your product that must be investigated before more customers install it.

```bash
ibmcloud catalog offering suspend-offering [--catalog CATALOG][--offering OFFERING]
```
{: codeblock}

### Command options
{: #suspend-offering-options}


--catalog CATALOG
:   The catalog name or ID.

--offering OFFERING
:   The product name or ID.

## ibmcloud catalog offering version suspend-version
{: #suspend-version}

Run the following command to suspend a version of a product from the catalog. You can suspend the version for a short time without permanently deleting or deprecating it.

```bash
ibmcloud catalog offering version suspend-version [--version-locator VERSION_NUMBER]
```
{: codeblock}

### Command options
{: #suspend-version-options}


--version-locator VERSION_NUMBER

:   To get the version locator for this offering, run `ibmcloud catalog offering list` and locate the version that you want to use.

## ibmcloud catalog offering workspaces
{: #get-workspaces}

Run the following command to get the {{site.data.keyword.bpshort}} workspaces for a product version.

```bash
ibmcloud catalog offering workspaces [--version-locator VERSION_NUMBER] [output FORMAT]
```
{: codeblock}

### Command options
{: #get-workspaces-options}

--version-locator VERSION_NUMBER

:   To get the version locator for this offering, run `ibmcloud catalog offering list` and locate the specified version that you want to use.

--output FORMAT (optional)

:   Specifies output format. The default is terminal compatible and the only supported alternative is JSON. For example, `--output json`.

## ibmcloud catalog install
{: #install-software-version}

Run the following command to install a software version from the {{site.data.keyword.cloud_notm}} catalog.

```bash
ibmcloud catalog install [--version-locator VERSION_NUMBER] [--cluster CLUSTER_ID] [--namespace NAME] [--override-values VALUES] [--timeout TIMEOUT] [--wait WAIT] [--workspace-name NAME] [--workspace-tags TAGS] [--workspace-tf-version VERSION] [--workspace-region REGION] [--workspace-rg-id ID] [schematics-delete VALUE]
```
{: codeblock}

### Command options
{: #install-software-version-options}

--version-locator VERSION_NUMBER

:   To get the version locator for this offering, run `ibmcloud catalog offering list` and locate the version that you want to use.

--cluster CLUSTER_ID

:   Specify the cluster name or ID.

--namespace NAME

:   Specify the namespace that you'd like to use.

--override-values VALUES

:   Provide any custom configurations for the installation. You can provide this value either inline or by using a JSON or TXT file. For example, `override-values values.json`.

--timeout TIMEOUT

:   Specify in seconds how long the {{site.data.keyword.bpshort}} workspace waits before it installs. Default is `180`.

--wait WAIT

:   Wait and track the progress of the {{site.data.keyword.bpshort}} workspace job. If `true`, installation waits. If `false`, the software installs immediately. Default is `true`.

--workspace-name NAME (optional)

:   Provide a workspace name. Default is `OfferingName-Date`.

--workspace-tags TAGS (optional)
:   Provide a comma-separated list of tags.

--workspace-tf-version VERSION (optional)
:   Provide a workspace terraform version.

--workspace-region REGION (optional)
:   Provide a workspace region.

--workspace-rg-id ID (optional)
:   Provide a workspace resource group ID.

--schematics-delete VALUE (optional)
:   Provide this flag to delete the {{site.data.keyword.bpshort}} workspace after validation and installation.

### Example
{: #install-software-version-example}

Install the software version `1` by using cluster `A`, namespace `install`, and the override values JSON `values.json`.

```bash
ibmcloud catalog install [--version-locator 1] [--cluster A] [--namespace install] [--override-values values.json]
```
{: codeblock}

Override values example format from the `values.json` file:

```bash
{
  "username": "install-test-1",
  "password": "passw0rd"
}
```
{: codeblock}


## ibmcloud catalog pricing
{: #catalog-pricing}

Run the following command to get pricing information for catalog offerings.

```bash
ibmcloud catalog pricing [-r, --region REGION] [-k, --kind KIND] [-p, --price PRICE] [--tag TAG] [--country COUNTRY] [--global] [--iam] [--json] [--csv] [-f, --file FILENAME]
```

### Command options
{: #pricing-options}

-r, --region (optional)
:   Filter by geo.

-k, --kind (optional)
:   Filter by the kind of resources. Currently `service` (default), `iaas`, `runtime`, `template`, and `geography` are supported

-p, --price (optional)
:   Filter by price. Currently `free`, `paygo`, and `subscription` are supported

-t, --tag (optional)
:   Filter by tag. This flag is repeatable and results in a logical OR of all the tags specified.

--co, --country (optional)
:   Filter by a country. Output to CSV or JSON may use the value `ALL` to get values for all countries.

--json (optional)
:   Output a JSON response.

--csv (optional)
:   Output a CSV file.

-f, --file (optional)
:   Specify a file name for the csv output.

--global (optional)
:   Operate in global scope.

--iam (optional)
:   Filter by IAM compatible offerings.

### Example
{: #pricing-example}

Get pricing information for Virtual Server for VPC for a Pay-As-You-Go account.

```bash
ibmcloud catalog pricing is.instance [--price paygo]
```
{: codeblock}

## ibmcloud catalog private-endpoint regions
{: #catalog-private-endpoint-regions}

Run the following command to retrieve the list of regions that support private endpoints for a specified service.

```bash
ibmcloud catalog private-endpoint regions [--service ID] 
```
{: codeblock}

### Command options
{: #catalog-private-endpoint-regions-options}

--service

:   Provide the ID or programmatic name of the service to see its regions that support private endpoint

## ibmcloud catalog private-endpoint services
{: #catalog-private-endpoint-services}

Run the following command to retrieve the list of services that support private endpoints for a specified region.

```bash
ibmcloud catalog private-endpoint services [--region REGION] 
```
{: codeblock}

### Command options
{: #catalog-private-endpoint-services-options}

--region or -r

:   Provide the REGION to see which services support private endpoints in that region


## ibmcloud catalog utility create-product-from-workspace
{: #publish-utility-create}

Run the following command to create a deployable architecture tile from a [{{site.data.keyword.bpshort}} workspace](/docs/schematics?topic=schematics-sch-create-wks&interface=ui) that was created directly from the Git repository. The deployable architecture [creates a project](/docs/cli?topic=cli-projects-cli#project-cli-create-command) so that you can continue to develop and maintain the deployable architecture with the future version.

The command requires a `GIT_TOKEN` environment variable to authenticate with your source repository so a catalog manifest can be added. The command pushes to a new branch in the Git repository that is found in the {{site.data.keyword.bpshort}} workspace and creates a release that is used for onboarding.

```bash
ibmcloud catalog utility create-product-from-workspace [--workspace-id ID] [--api-key KEY] [--trusted-profile-id ID] [--catalog-label LABEL] [--offering-label LABEL] [--project-name NAME] [--project-resource-group GROUP] [--target-version VERSION] [--variation-label LABEL]
```
{: codeblock}

### Command options
{: #publish-utility-create-options}

--api-key or --ak API KEY

:   Provide an API key that is used to link the catalog and project. Mutually exclusive with '--trusted-profile-id'.

--catalog-label CATALOG LABEL (optional)

:   Provide the label of an existing catalog to import into or the name of a new catalog to create. The default is 'Migrated DAs'.

--offering-label OFFERING LABEL (optional)

:    Provide the label of an existing offering to import into or the name of a new offering to create. The default is 'Migrated <workspace_name>'. The label overwrites the existing offering label if the workspace is created from a catalog offering.

--project-name NAME (optional)

:   Provide a project name that is linked to the onboarded catalog. If the project does not exist, it is created. The default name is 'Dev Migration Project'.

--project-resource-group (optional)
:   Provide a resource group for the project that is created. The default resource group is 'Default'.

--target-version VERSION (optional)

:   Provide the target version for the migrated offering. The default is '1.0.0'.

--trusted-profile-id or --tpi TRUSTED PROFILE ID

:   Provide a trusted profile ID that is used to link the catalog and project. Mutually exclusive with '--api-key'.

--variation-label VARIATION LABEL (optional)

:   Provide a variation label for the version to be onboarded. The default is 'Standard'. The label overwrites the existing version label if the workspace is created from a catalog offering.

--workspace-id WORKSPACE ID

:   Provide a {{site.data.keyword.bpshort}} workspace ID. To get the workspace ID, you must create the {{site.data.keyword.bpshort}} workspace. For more information, see [`ibmcloud schematics workspace new`](/docs/schematics?topic=schematics-schematics-cli-reference#schematics-workspace-new).

## ibmcloud catalog utility netrc
{: #generate-netrc}

Run the following command to create a `.netrc` file, generate the machine name in your `.netrc` file, or update the credential in your `.netrc` file. A `.netrc` file stores the required login information that is needed to use Terraform modules from the {{site.data.keyword.cloud_notm}} catalog.

By running this command, you configure a `.netrc` file for the machine name `cm.globalcatalog.cloud.ibm.com` with `iamtoken` as the username and your IAM token as the password.

You need version 1.2.7 or higher of the catalogs management CLI plug-in to run the `.netrc` command.
{: note}

```bash
ibmcloud catalog utility netrc
```
{: codeblock}

## ibmcloud catalog utility update-module-references
{: #utility-module-references}

Run the following command to check your working directory's Terraform modules for updates from the catalog and update the source attribute to the latest version. The README.md is also updated.

```bash
ibmcloud catalog utility update-module-references
```
{: codeblock}

## ibmcloud catalog offering unpublish account
{: #unpublish-offering-account}

Run the following command to unpublish a product from your account. After the product is unpublished, users in your account cannot create an instance of the product.

```bash
ibmcloud catalog offering unpublish account [--catalog CATALOG][--offering OFFERING]
```
{: codeblock}

### Command options
{: #unpublish-offering-account-options}


--catalog CATALOG
:   The catalog name or ID.

--offering OFFERING
:   The product name or ID.

## ibmcloud catalog offering unpublish allowlist
{: #unpublish-offering-allowlist}

Run the following command to remove account IDs from the product's allowlist. Accounts that are removed from the allowlist cannot create an instance of the product.

```bash
ibmcloud catalog offering unpublish allowlist [--catalog CATALOG][--offering OFFERING][--account-ids ACCOUNT-IDS]
```
{: codeblock}

### Command options
{: #unpublish-offering-allowlist-options}


--catalog CATALOG
:   The catalog name or ID.

--offering OFFERING
:   The product name or ID.

--account-ids ACCOUNT-IDS
:   The account IDs.

## ibmcloud catalog offering unpublish enterprise
{: #unpublish-offering-enterprise}

Run the following command to unpublish a product from an enterprise. After the product is unpublished, the enterprise cannot create an instance of the product.

```bash
ibmcloud catalog offering unpublish enterprise [--catalog CATALOG][--offering OFFERING]
```
{: codeblock}

### Command options
{: #unpublish-offering-enterprise-options}


--catalog CATALOG
:   The catalog name or ID.

--offering OFFERING
:   The product name or ID.

## ibmcloud catalog offering unpublish ibm
{: #unpublish-offering-ibm}

Run the following command to unpublish a product from {{site.data.keyword.IBM_notm}}. After the product is unpublished, {{site.data.keyword.IBM_notm}} employees cannot create an instance of the product.

```bash
ibmcloud catalog offering unpublish ibm [--catalog CATALOG][--offering OFFERING]
```
{: codeblock}

### Command options
{: #unpublish-offering-ibm-options}

--catalog CATALOG
:   The catalog name or ID.

--offering OFFERING
:   The product name or ID.



## ibmcloud catalog offering publish ibm
{: #publish-offering-to-ibm}

Run the following command to publish an offering that is already available in your account to all {{site.data.keyword.IBM_notm}}ers. This part of the publication process creates a tile in the staging and production catalogs that is visible only to {{site.data.keyword.IBM_notm}}ers. By publishing an offering to {{site.data.keyword.IBM_notm}}ers, you can test the offering in production before you make it available to all users in the {{site.data.keyword.cloud_notm}} catalog.

```bash
ibmcloud catalog offering publish ibm [--catalog CATALOG][--offering OFFERING]
```
{: codeblock}

### Command options
{: #publish-offering-to-ibm-options}


--catalog CATALOG
:   The catalog name or ID.

--offering OFFERING
:   The product name or ID.


## ibmcloud catalog offering publish public
{: #publish-offering-to-public}

Run the following command to publish your private offering to the {{site.data.keyword.cloud_notm}} catalog for all users to see and use. To get to this step in the publication process, you must first publish the offering to your account and to all IBMers to complete the testing process. After your testing is complete, you can run this command.

This option requires approval. When your approval is complete, your tile is available for all {{site.data.keyword.cloud_notm}} customers.
{: important}

```bash
ibmcloud catalog offering publish public [--catalog CATALOG][--offering OFFERING]
```
{: codeblock}

### Command options
{: #publish-offering-to-public-options}

--catalog CATALOG
:   The catalog name or ID.

--offering OFFERING
:   The product name or ID.

## ibmcloud catalog offering deprecate-offering
{: #publish-offering-deprecate}

Run the following command to deprecate a previously published offering version in the {{site.data.keyword.cloud_notm}} catalog.

```bash
ibmcloud catalog offering deprecate-offering [--catalog CATALOG][--offering OFFERING]
```
{: codeblock}

### Command options
{: #publish-offering-deprecate-options}


--catalog CATALOG
:   The catalog name or ID.

--offering OFFERING
:   The product name or ID.

## ibmcloud catalog offering restore-offering
{: #publish-offering-restore}

Run the following command to restore a previously deprecated product in the {{site.data.keyword.cloud_notm}} catalog. After you validate a version of your product, you can restore it to the published state that it was in before it was deprecated.

```bash
ibmcloud catalog offering restore-offering [--catalog CATALOG][--offering OFFERING]
```
{: codeblock}

### Command options
{: #publish-offering-restore-options}

--catalog CATALOG
:   The catalog name or ID.

--offering OFFERING
:   The product name or ID.

## ibmcloud catalog offering version restore-version
{: #publish-version-restore}

Run the following command to restore a previously deprecated version of a product in the {{site.data.keyword.cloud_notm}} catalog. Restoring it places the version in a draft state. After you validate it, you can restore the original version to the published state that it was in before it was deprecated.

```bash
ibmcloud catalog offering version restore-version [--catalog CATALOG][--offering OFFERING] [--include-config]
```
{: codeblock}

### Command options
{: #publish-version-restore-options}

--catalog CATALOG
:   The catalog name or ID.

--offering OFFERING
:   The product name or ID.

--include-config (optional)

:   If provided, all configuration values are included and available when you add the product.



## ibmcloud catalog object create vpe
{: #create-object}

Run the following command to add an object to a private catalog in the account.

```bash
ibmcloud catalog object create vpe [--catalog CATALOG] [--crn CRN] [endpoint-type TYPE] [--fqdn FQDN] [--name NAME] [--region REGION]
```
{: codeblock}

## Command options
{: #create-object-options}

--catalog CATALOG

:   Specify the catalog name or ID.

--crn CRN

:   Provide the Cloud Resource Name (CRN).

--endpoint-type TYPE

:   Specify the VPE endpoint type.

--fqdn FQDN

:   Provide a comma-separated list of fully qualified domain names.

--name NAME

:   Specify the name of the object.

--region REGION

:   Specify the region for the VPE endpoint.

## ibmcloud catalog object delete
{: #delete-object}

Run the following command to delete the object.

```bash
ibmcloud catalog object delete [--catalog CATALOG] [--name NAME]
```
{: codeblock}

### Command options
{: #delete-object-options}

--catalog CATALOG

:   Specify the catalog name or ID.

--name NAME

:   Provide the name of the object.

## ibmcloud catalog object update vpe
{: #update-object}

Run the following command to update the object.

```bash
ibmcloud catalog object update vpe [--catalog CATALOG] [--name NAME] [--crn CRN] [--endpoint-type TYPE] [--fqdn FQDN] [--region REGION]
```
{: codeblock}

### Command options
{: #update-object-options}

--catalog CATALOG

:   Specify the catalog name or ID.

--name NAME

:   Specify the name of the object.

--crn CRN (optional)

:   Provide the Cloud Resource Name (CRN).

--endpoint-type TYPE (optional)

:   Specify the VPE endpoint type.

--fqdn FQDN (optional)

:   Provide a comma-separated list of fully qualified domain names.

--region REGION (optional)

:   Specify the region for the VPE endpoint.

## ibmcloud catalog object get
{: #get-object}

Run the following command to retrieve information for a particular object.

```bash
ibmcloud catalog object get [--catalog CATALOG] [--name NAME] [--output OUTPUT]
```
{: codeblock}

### Command options
{: #get-object-options}

--catalog CATALOG

:   Specify the catalog name or ID.

--name NAME

:   Provide the name of the object.

--output OUTPUT (optional)

: Specifies output format. The default is terminal compatible and the only supported alternative is JSON. For example, `--output json`

## ibmcloud catalog object list
{: #list-object}

Run the following command to retrieve a list of objects in a catalog.

```bash
ibmcloud catalog object list [--catalog CATALOG] [--output OUTPUT]
```
{: codeblock}

### Command options
{: #list-object-options}

--catalog CATALOG

:   Specify the catalog name or ID.

--output OUTPUT (optional)

:   Specifies output format. The default is terminal compatible and the only supported alternative is JSON. For example, `--output json`

## ibmcloud catalog object search
{: #search-object}

Run the following command to search objects by using Lucene query syntax.

```bash
ibmcloud catalog object search [--query QUERY] [--output OUTPUT]
```
{: codeblock}

### Command options
{: #search-object-options}

--query QUERY

:   Provide the Lucene query string.

--output OUTPUT (optional)

:   Specifies output format. The default is terminal compatible and the only supported alternative is JSON. For example, `--output json`

## ibmcloud catalog object ready
{: #ready-object}

Run the following command to mark your object as ready to share or publish.

```bash
ibmcloud catalog object ready [--catalog CATALOG] [--name NAME]
```
{: codeblock}

### Command options
{: #ready-object-options}

--catalog CATALOG
:   Specify the catalog name or ID.

--name NAME
:   Specify the name of the object.

## ibmcloud catalog object enable-sharing
{: #enable-share-object}

Run the following command to enable sharing of a Partner Center managed object. Enable sharing before you can share an object to an account or access list.

```bash
ibmcloud catalog object enable-sharing [--catalog CATALOG] [--name NAME]
```
{: codeblock}

### Command options
{: #enable-share-object-options}

--catalog CATALOG
:   Specify the catalog name or ID.

--name NAME
:   Specify the name of the object.


## ibmcloud catalog object publish
{: #publish-object}

Run the following command to publish the object to an access list, your account, {{site.data.keyword.IBM_notm}} employees, or {{site.data.keyword.cloud_notm}} catalog for all users to see and use.

```bash
ibmcloud catalog object publish COMMAND [--catalog CATALOG] [--name NAME]
```
{: codeblock}

### Command options
{: #publish-object-options}

Command

:   Specify where you want to publish the object. Valid values are `accesslist`, `account`, `ibm`, or `public`.

--catalog CATALOG

:   Specify the catalog name or ID.

--name NAME

:   Provide the name of the object.

### Example
{: #publish-object-example}

Publish an object called `dev-object` that's in the catalog `dev-catalog` to {{site.data.keyword.IBM_notm}} employees.
```bash
ibmcloud catalog object publish ibm --catalog dev-catalog --name dev-object
```
{: codeblock}

## ibmcloud catalog object access-list add
{: #add-accesslist-object}

Run the following command to add account IDs to an object's access list.

```bash
ibmcloud catalog object access-list add [--account-id ID] [--catalog CATALOG] [--name NAME]
```
{: codeblock}

### Command options
{: #add-accesslist-object-options}

--account-id ID

:   Provide a comma-separated list of account IDs.

--catalog CATALOG

:   Specify the catalog name or ID.

--name NAME

:   Specify the name of the object.

## ibmcloud catalog object access-list get
{: #get-accesslist-object}

Run the following command to retrieve information for a particular access list for an object.

```bash
ibmcloud catalog object access-list get [--catalog CATALOG] [--name NAME] [--output OUTPUT]
```
{: codeblock}

### Command options
{: #get-accesslist-object-options}

--catalog CATALOG

:   Specify the catalog name or ID.

--name NAME

:   Specify the name of the object.

--output OUTPUT (optional)

:   Specifies output format. The default is terminal compatible and the only supported alternative is JSON. For example, `--output json`

## ibmcloud catalog object access-list rm
{: #remove-object-accesslist}

Run the following command to remove account IDs from the object's access list.

```bash
ibmcloud catalog object access-list rm [--account-id ID] [--catalog CATALOG] [--name NAME]
```
{: codeblock}

### Command options
{: #remove-object-accesslist-options}

--account-id ID

:   Provide a comma-separated list of account IDs.

--catalog CATALOG

:   Specify the catalog name or ID.

--name NAME

:   Specify the name of the object.
