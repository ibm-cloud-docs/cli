---

copyright:
  years: 2015, 2025
lastupdated: "2025-04-01"

keywords: command line interface, cli, getting started, getting started with IBM Cloud CLI, getting started with IBM Cloud CLI and developer tools tutorial, IBM Cloud Developer Tools CLI, ibmcloud cli, download cli, cloud cli, cloud command line, developer tools, dev tools, install cloud cli, getting started cli, ibm cloud cli, IBM Cloud CLI installer, installing IBM Cloud CLI, install IBM Cloud CLI
content-type: tutorial
services: 
account-plan: lite
completion-time: 30m
subcollection: cli

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with the {{site.data.keyword.cloud_notm}} CLI
{: #getting-started}
{: toc-content-type="tutorial"} 
{: toc-services=""} 
{: toc-completion-time="30m"}

In this tutorial, you install the latest version of the stand-alone {{site.data.keyword.cloud}} Command Line Interface.
{: shortdesc}

Want to start working with the {{site.data.keyword.cloud_notm}} CLI? Try out {{site.data.keyword.cloud-shell_notm}}, which gives you a personal cloud-based shell workspace with the full {{site.data.keyword.cloud_notm}} CLI and tons of command line tools - no installation needed. To get started, click the {{site.data.keyword.cloud-shell_short}} icon ![{{site.data.keyword.cloud-shell_notm}} icon](../icons/terminal-cloud-shell.svg) in the {{site.data.keyword.cloud_notm}} console menu bar. For more information, see [Getting started with {{site.data.keyword.cloud-shell_notm}}](/docs/cloud-shell?topic=cloud-shell-getting-started).
{: tip}

## Before you begin
{: #idt-prereq}

* Depending on your [{{site.data.keyword.cloud}} account type](/registration){: external}, access to certain resources might be limited or constrained. Depending on your plan limits, certain capabilities that are required by some toolchains might not be available. For more information, see [Setting up your IBM Cloud account](/docs/account?topic=account-account-getting-started).
* For Linux&trade;, install the [curl](https://curl.se/download.html){: external} command for downloading packages through the command line. If `curl` is already installed, the installer updates it to the latest version.

If you need to use a 32-bit version of the CLI, or a previous version other than the latest for {{site.data.keyword.cloud_notm}} dedicated environments, see [{{site.data.keyword.cloud_notm}} CLI releases](https://github.com/IBM-Cloud/ibm-cloud-cli-release/releases/){: external}.
{: note}

## Running the installation command
{: #step1-install-idt}
{: step}

The latest version of the {{site.data.keyword.cloud_notm}} CLI is installed when you run the command. As the CLI installs, keep an eye on the command line to authenticate as needed.

* For MacOS, run the following command:
   ```curl
   curl -fsSL https://clis.cloud.ibm.com/install/osx | sh
   ```
   {: codeblock}

* For Linux&trade;, run the following command:
   ```curl
   curl -fsSL https://clis.cloud.ibm.com/install/linux | sh
   ```
   {: codeblock}

* For Windows&trade;, run the following command in PowerShell as an administrator:
   ```curl
   iex (New-Object Net.WebClient).DownloadString('https://clis.cloud.ibm.com/install/powershell')
   ```
   {: codeblock}

   To open PowerShell, right-click the Windows&trade; PowerShell icon, and select **Run as administrator**.
   {: tip}

* For WSL2 on Windows&trade;, run the following command:
   ```curl
   curl -fsSL https://clis.cloud.ibm.com/install/linux | sh
   ```

## Verifying the installation
{: #step2-verify-idt}
{: step}

To verify that the CLI was installed successfully, run the `help` command:
```text
ibmcloud help
```
{: codeblock}

The output lists the usage instructions, the current version, and the supported commands.

## Installing CLI plug-ins and tools
{: #step3-install-idt-manually}
{: step}

To manually install the CLI plug-ins and tools, see [Extending IBM Cloud CLI with plug-ins](/docs/cli?topic=cli-plug-ins).

## Configuring your environment
{: #step4-configure-idt-env}
{: step}

Log in to {{site.data.keyword.cloud_notm}} with your IBMid. If you have multiple accounts, you are prompted to select which account to use. If you do not specify a region with the `-r` flag, you must also select a region.
   ```text
   ibmcloud login
   ```
   {: codeblock}

If your credentials are rejected, you might be using a federated ID. To log in with a federated ID, use the `--sso` flag. See [Logging in with a federated ID](/docs/account?topic=account-federated_id) for more details.
{: tip}

## Next steps
{: #next-steps}

If you installed the CLI plug-ins and tools, you can start to use {{site.data.keyword.cloud_notm}} resources and services on the CLI. For more information, see [General IBM Cloud CLI (ibmcloud) commands](/docs/cli?topic=cli-ibmcloud_cli). Also, keep in mind the [Getting help and support](/docs/cli?topic=cli-getting-help) page if you have questions or problems.

Stay up to date with the {{site.data.keyword.cloud_notm}} CLI by subscribing to the [{{site.data.keyword.cloud_notm}} CLI releases repository](https://github.com/IBM-Cloud/ibm-cloud-cli-release/releases/){: external}. You'll receive notifications about new {{site.data.keyword.cloud_notm}} CLI releases.

{{site.data.keyword.cloud_notm}} CLI supports a plug-in framework to extend its capability. [Discover and install new CLI plug-ins](/docs/cli?topic=cli-plug-ins)!

Need a hand with remembering {{site.data.keyword.cloud_notm}} CLI commands? Print the [{{site.data.keyword.cloud_notm}} CLI quick reference](https://cloud.ibm.com/media/docs/downloads/IBM%20Cloud%20CLI%20quick%20reference.pdf){: external} to keep commands for common tasks at your fingertips.
{: tip}
