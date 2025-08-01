---

copyright:
  years: 2022, 2025
lastupdated: "2025-05-30"

keywords: cli, command line, command-line, login, cli login, compute resource, compute resource identity, compute resource identities, vsi, vpc, trusted profiles, cri

subcollection: cli

---

{{site.data.keyword.attribute-definition-list}}

# Logging in as a Virtual Server Instance Compute Resource Identity
{: #vsi-cri-login}

You can use a trusted profile to set up fine-grained authorization for applications that are running in compute resources. As a result, you aren't required to create service IDs or API keys for the compute resources. The {{site.data.keyword.cloud_notm}} CLI supports logging in and authenticating to {{site.data.keyword.cloud_notm}} by using an {{site.data.keyword.cloud_notm}} Virtual Server Instance (VSI) for VPC compute resource.
{: shortdesc}

For more information about managing trusted profiles and establishing trust with compute resources, see [Establishing trust with compute resources](/docs/account?topic=account-create-trusted-profile&interface=ui#create-profile-compute).

## Using the CLI to log in
{: #vpc-cli-login}

To use the {{site.data.keyword.cloud_notm}} CLI Virtual Server Instance for VPC compute resource identity login feature, you must enable the Instance Metadata service for VPC service on the VSI and link the instance to a trusted profile. For more information about enabling the Instance Metadata service, see [About Instance Metadata for VPC](/docs/vpc?topic=vpc-imd-about&interface=ui). After it's enabled and the VSI is linked to a trusted profile, the CLI can use the [Instance Identity token service](/docs/vpc?topic=vpc-imd-about&interface=ui#imd-vpc-access-token) to acquire a JSON web token and exchange it for an IAM token.

Certain {{site.data.keyword.cloud_notm}} Kubernetes Service CLI commands are currently not supported when logged in as a VPC compute resource including [ibmcloud ks cluster config](/docs/containers?topic=containers-kubernetes-service-cli#cs_cluster_config).
{: note}

### Log in with the CLI
{: #vpcvsiflag_login}

When you use the VPC VSI option to log in, you can optionally specify the trusted profile parameter to enter at login. If provided, the CLI uses this trusted profile to authenticate to IBM Cloud. Otherwise, the VSI's default linked trusted profile that is linked during instance provisioning is used.

You can log in as a VSI compute resource by using the CLI in any of the following ways:

* Provide a trusted profile by parameter:
   1. Specify the `--vpc-cri` option with the `ibmcloud login` command.
   2. Specify the `--profile` option with the `ibmcloud login` command, and provide the ID or CRN of the trusted IAM profile that the instance is linked to.

   ```bash
   ibmcloud login --vpc-cri --profile <profile_id_or_crn_string>
   ```
   {: codeblock}

* Provide a trusted profile by using the `IBMCLOUD_CR_PROFILE` environment variable. 
  
   You can provide a trusted profile by setting the environment variable on your system. For example, set `IBMCLOUD_CR_PROFILE=profile_id_or_crn`, where `profile_id_or_crn` is the ID or CRN of the IAM trusted profile that the VSI is linked to. After the environment variable is set, you can simply specify `ibmcloud login --vpc-cri` from the CLI.

* Use the Virtual Service Instance's default linked trusted profile:
   1. Specify the `--vpc-cri` option with the `ibmcloud login` command.

   ```bash
   ibmcloud login --vpc-cri
   ```
   {: codeblock}

If your [VPC instance metadata service](/docs/vpc?topic=vpc-imd-about) is configured for secure access, override the default URL for the service before you log in by setting the environment variable `IBMCLOUD_CR_VPC_URL=https://api.metadata.cloud.ibm.com`.

If you want to log in as a VSI compute resource by using private endpoints for VPC, you must also provide the ``--vpc`` flag
and set the API endpoint to ``private.cloud.ibm.com``. In the example, the trusted profile was provided by setting the environment variable `IBMCLOUD_CR_PROFILE=profile_id_or_crn`:
 ```bash
   ibmcloud login --vpc-cri --vpc -a private.cloud.ibm.com
   ```
   {: codeblock}

For more information about logging in to the CLI with a private endpoint, see [Logging in to the CLI with a private endpoint](/docs/cli?topic=cli-service-connection#cli-private-vpc). For information about configuring a VPC connection to use a private API endpoint, see [Configuring a private endpoint gateway (required for VPC use)](/docs/cli?topic=cli-service-connection#cli-private-vpc).

The resulting login session is valid for 60 minutes.
{: note}
