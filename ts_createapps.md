---

copyright:
  years: 2015, 2026
lastupdated: "2026-01-22"

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

- If the problem is with a download folder that is accessed with the `plugin download` command, modify the folder to have exec privileges. 
- If the problem is with the default download folder and you are unable to change the permissions, use the [plugin download command](/docs/cli?topic=cli-ibmcloud_commands_settings#ibmcloud_plugin_download) to download to an alternative directory. Then use the [plugin install command](/docs/cli?topic=cli-ibmcloud_commands_settings#ibmcloud_plugin_install) to install by using the downloaded binary file. 
- If the temp folder on your system lacks executable privileges and cannot be modified, specify a different temp folder during plug-in installation or update. Set the environment variable `$TMPDIR` for Mac or Linux, and `%TMP%` for Windows.
{: tsResolve}

## Why does login fail with unsupported protocol scheme on MacOS?
{: #ts-cli-macos-login-failure}
{: troubleshoot}
{: support}

When the MacOS has not restarted for some period of time, the networking on the machine can begin to produce the following types of problems:
{: tsSymptoms}

First example:  **ibmcloud login**

```text
ibmcloud login
API endpoint: https://cloud.ibm.com
Logging in with API key from environment variable...
Authenticating...
Post "iam.cloud.ibm.com/identity/token": unsupported protocol scheme ""
                
API endpoint:   https://cloud.ibm.com
Region:         
Not logged in.
FAILED
Unable to authenticate.
```

Second example:  **ibmcloud login --sso**

```text
ibmcloud login --sso
API endpoint: https://cloud.ibm.com
                
API endpoint:   https://cloud.ibm.com
Region:         
Not logged in.
FAILED
Could not get IAM configuration: Get "iam.cloud.ibm.com/identity/.well-known/openid-configuration": unsupported protocol scheme ""
```

{: screen}

This error is caused by the networking in the MacOS.
{: tsCauses}

Restart the MacOS system to resolve the issue.
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

## Why does the ibmcloud resources command respond with an error 400: Requested result window is too large?
{: #ts-cli-resources-large}
{: troubleshoot}

Running the `ibmcloud resources --output json` command displays the following error:

```text
FAILED
Error response from server. Status code: 400; description: error: {code: GST407E, message: Requested result window is too large, offset +  limit  must be less than or equal to: [ 10000 ] but was [ 11000 ], details: }.
```
{: screen}
{: tsSymptoms}

This error occurs for accounts with a large number of resources because there is a maximum of 10,000 resources to return with this command.
{: tsCauses}

When you need to fetch more than 10,000 resource items, use the `ibmcloud resource search` command with the offset option incremented in units of one thousand, which allows for pagination of results.
{: tsResolve}

**Example**

Search and list resources in batches of 1,000:

```bash
ibmcloud resource search "*"

# Fetch the next 1000 resources
ibmcloud resource search "*" --offset 1001

# Fetch the next 1000 resources
ibmcloud resource search "*" --offset 2001
```
{: codeblock}
