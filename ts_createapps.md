---

copyright:
  years: 2015, 2024
lastupdated: "2024-09-04"

keywords: cli, troubleshoot cli, debug app cli, developer tools debug, ibmcloud cli debug, ibmcloud help, ibmcloud dev help, cli debug, command line, command-line, developer tools troubleshoot

subcollection: cli

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting for the {{site.data.keyword.cloud_notm}} CLI
{: #troubleshoot}

See solutions to common problems with using the {{site.data.keyword.cloud}} Command Line Interface. Often, you can recover from these problems by following a few easy steps.
{: shortdesc}

## Why do I get a failure when updating the CLI, updating a plug-in, or installing a plug-in?
{: #ts-cli-version-1-failure}
{: troubleshoot}
{: support}

If you are attempting to update the {{site.data.keyword.cloud_notm}} CLI, or update or install a plug-in with a CLI version lower than 2.0.0, you see an error similar to the following message.
{: tsSymptoms}

```text
An error occurred when fetching latest CLI info:
invalid character '<' looking for beginning of value
```
{: screen}

This error is caused by the older CLI version attempting to reach the deprecated CLI repo infrastructure.
{: tsCauses}

Download and install or replace the older CLI with the latest CLI version by using these [instructions](/docs/cli?topic=cli-install-ibmcloud-cli).
{: tsResolve}

## Why do I get a failure with the plug-in update or install command after it has downloaded the binary?
{: #ts-cli-plugin-update-failure}
{: troubleshoot}
{: support}

If you are attempting to update or install a plug-in and the default downloads folder for your system lacks access rights, you see an error similar to the following message.
{: tsSymptoms}

```text
FAILED
Unable to obtain plug-in's metadata. Error: fork/exec/tmp/... : permission denied
```
{: screen}

This error is caused by the download folder or the temp folder on your system not having exec privileges.
{: tsCauses}

There are multiple resolutions depending on your scenario: 

- If the problem is with a download folder accessed with the `plugin download` command, modify the folder to have exec privileges. 
- If the problem is with the default download folder and you are unable to change the permissions, use the [plugin download command](/docs/cli?topic=cli-ibmcloud_commands_settings#ibmcloud_plugin_download) to download to an alternate directory. Then use the [plugin install command](/docs/cli?topic=cli-ibmcloud_commands_settings#ibmcloud_plugin_install) to install by using the downloaded binary file. 
- If the temp folder on your system lacks executable privileges and cannot be modified, specify a different temp folder during plug-in installation or update. Set the environment variable `$TMPDIR` for Mac or Linux, and `%TMP%` for Windows.
{: tsResolve}


## Why do I get a service broker error when I add the {{site.data.keyword.objectstorageshort}} capability?
{: #ts-cli-object-storage}
{: troubleshoot}

The following error might be displayed if you use the CLI to create two apps with the {{site.data.keyword.objectstorageshort}} capability:

```text
FAILED
Service broker error: {"description"=>"You can not create this Object Storage instance. Each organization using the Object Storage service is limited to one instance of the Free plan."}
```
{: screen}
{: tsSymptoms}

This error is due to the {{site.data.keyword.objectstorageshort}} service, which provides only one instance of the free {{site.data.keyword.objectstorageshort}} plan.
{: tsCauses}

Select a different plan.
{: tsResolve}

## Why does the ibmcloud catalog search command fail?
{: #ts-cli-catalog-search-error}
{: troubleshoot}

Running the `ibmcloud catalog search` command displays the following error:

```text
FAILED
'search' is not a registered command. See 'C:\Program Files\IBM\Cloud\bin\ibmcloud.exe catalog help'.
```
{: screen}
{: tsSymptoms}

The `ibmcloud catalog search` command was moved to a separate plug-in in v1.0.0.
{: tsCauses}

To use this command, you must install the catalogs-management plug-in. For more information, see the [Catalogs management CLI plug-in](/docs/cli?topic=cli-manage-catalogs-plugin).
{: tsResolve}
