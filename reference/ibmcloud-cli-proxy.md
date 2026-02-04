---

copyright:
  years: 2021, 2026
lastupdated: "2026-02-04"

keywords: IBM Cloud CLI, proxy, ibmcloud cli, ibmcloud, Golang

subcollection: cli

---

{{site.data.keyword.attribute-definition-list}}

# Using a proxy with the {{site.data.keyword.cloud_notm}} CLI
{: #ibmcloud-cli-proxy}

You can use the HTTPS_PROXY environment variable to set a proxy for requests from the {{site.data.keyword.cloud}} CLI.
{: shortdesc}

With the HTTPS_PROXY environment variable, you can set the host and port of your proxy for use by the {{site.data.keyword.cloud}} CLI.

## Before you begin
{: #ibmcloud-cli-proxy-prereq}

* [Install the {{site.data.keyword.cloud_notm}} CLI](https://cloud.ibm.com/docs/cli?topic=cli-getting-started).

## Setting the HTTPS_PROXY environment variable
{: #ibmcloud-cli-proxy-usage}

To set the proxy, export the environment variable before using the  {{site.data.keyword.cloud}} CLI in the terminal. Enter the following command:

Mac or Linux&trade
```bash
  export HTTPS_PROXY=https://your-server:your-port
```
{: codeblock}

Windows&trade
```bash
  set HTTPS_PROXY=https://your-server:your-port
```
{: codeblock}

Windows PowerShell&trade
```bash
  $env:HTTPS_PROXY = "https://your-server:your-port"
```
{: codeblock}


For more information about environment variables for the {{site.data.keyword.cloud_notm}} CLI, see [Tips and Tricks for Using the {{site.data.keyword.cloud_notm}} CLI](https://www.ibm.com/think){: external} and [{{site.data.keyword.cloud_notm}} CLI (ibmcloud) environment variables](/docs/cli?topic=cli-ibmcloud_env_var).
