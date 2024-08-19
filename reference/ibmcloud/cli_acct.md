---

copyright:
  years: 2018, 2024
lastupdated: "2024-08-16"

keywords: cli, ibmcloud account cli, managing accounts cli, managing users cli, account, account update command

subcollection: cli

---

{{site.data.keyword.attribute-definition-list}}

# Managing accounts and users (ibmcloud account)
{: #ibmcloud_commands_account}

Use the following commands from the {{site.data.keyword.cloud}} Command Line Interface to manage accounts and users in an account.
{: shortdesc}

## ibmcloud account show
{: #ibmcloud_account_show}

Show account details:
```bash
ibmcloud account show
```
{: codeblock}

### Examples
{: #ibmcloud_account_show_examples}

Show details of the currently targeted account:
```bash
ibmcloud account show
```
{: codeblock}

## ibmcloud account list 
{: #ibmcloud_account_list}

### List accounts
{: #ibmcloud_account_list_accounts}

```bash
ibmcloud account list [--active | --exclude EXCLUDE_STATES] [-o, --output FORMAT] [-q, --quiet]
```
{: codeblock}

### Command options
{: #ibmcloud_account_list_options}

--active 
:   Active. List only the accounts that are active. Exclude states: `CANCEL_PENDING`, `CANCELED`, and `SUSPENDED`

--exclude value *EXCLUDE_VALUE*
:   Exclude value. Comma-delimited list of account states to exclude. Example: `SUSPENDED,CANCEL_PENDING`

-o, --output
:   Specify output format. Only 'JSON' is supported.

-q, --quiet
:   Suppress verbose output.

## ibmcloud account update
{: #ibmcloud_account_update}

Update a specific account:
```bash
ibmcloud account update (--service-endpoint-enable true | false)
```
{: codeblock}

### Command options
{: #ibmcloud_account_update_options}

--service-endpoint-enable true | false
:   Enable or disable service endpoints connectivity for a SoftLayer account.


### Examples
{: #ibmcloud_account_update_examples}

Enable service endpoint connectivity for current account:
```bash
ibmcloud account update --service-endpoint-enable true
```
{: codeblock}

## Classic infrastructure account audit-logs
{: #classic_account_audit_logs}

List SoftLayer account audit logs:
```bash
account audit-logs [-u, --user-name USER_NAME] [-t, --object-type OBJECT_TYPE] [-o, --object OBJECT] [-a, --action ACTION] [-s, --start-date START_DATE] [-e, --end-date END_DATE]
```
{: codeblock}

### Command options
{: #classic_account_audit_logs_options}

-a, --action *ACTION*
:   Action. List audit logs with the action.

-e, --end-date *END_DATE*
:   End date. List audit logs before the end date. Supported formats are yyyy-MM-ddTHH:mm:ss.

o, --object *OBJECT*
:   Object. List audit logs with the object.

t, --object-type *OBJECT_TYPE*
:   Object type. List audit logs with the object type.

s, --start-date *START_DATE*
:   Start date. List audit logs after the start date. Supported formats are yyyy-MM-ddTHH:mm:ss.

u, --user-name *USER_NAME*
:   User name. List audit logs with the username.

### Examples
{: #classic_account_audit_logs_examples}

List audit logs:
```bash
ibmcloud account audit-logs
```
{: codeblock}

## ibmcloud account audit-logs
{: #ibmcloud_account_audit_logs}

List account audit logs:
```bash
ibmcloud account audit-logs [--user-name USER_NAME] [--object-type OBJECT_TYPE] [--object OBJECT] [--action ACTION] [--start-date START_DATE] [--end-date END_DATE]
```
{: codeblock}

### Command options
{: #ibmcloud_account_audit_logs_options}

--user-name *USER_NAME* (optional)
:   List audit logs with the user name.

--object-type *OBJECT_TYPE* (optional)
:   List audit logs with the object type.

--object *OBJECT* (optional)
:   List audit logs with the object.

--action *ACTION* (optional)
:   List audit logs with the action.

--start-date *START_DATE* (optional)
:   List audit logs after the start date. Supported formats are yyyy-MM-ddTHH:mm:ss.

--end-date *END_DATE* (optional)
:   List audit logs before the end date. Supported formats are yyyy-MM-ddTHH:mm:ss.


## ibmcloud account users
{: #ibmcloud_account_users}

Displays users that are associated with the account. To view the required permissions to run this command,
see [Retrieve users in the account](/apidocs/user-management#list-users).
```bash
ibmcloud account users [-c, --account-id ACCOUNT_ID]
```
{: codeblock}

### Command options
{: #ibmcloud_account_users_options}

-c (optional)
:   Account ID. If not specified, default to the current account.

## ibmcloud account user-remove
{: #ibmcloud_account_user_remove}

Remove a user from an account (account owner only).
```bash
ibmcloud account user-remove USER_ID [-c ACCOUNT_ID] [-f, --force]
```
{: codeblock}

### Command options
{: #ibmcloud_account_user_remove_options}

USER_ID (required)
:   User ID

-c ACCOUNT_ID
:   Account ID. If not specified, default to the current account.

-f, --force
:   Force removal without confirmation.

## ibmcloud account user-invite
{: #ibmcloud_account_user_invite}

Invite a user to the account:
```bash
ibmcloud account user-invite USER_EMAIL [-o ORG [--org-role ORG_ROLE] [-s SPACE, --space-role SPACE_ROLE]] [-r, --region REGION]
```
{: codeblock}

### Command options
{: #ibmcloud_account_user_invite_options}

USER_EMAIL (required)
:   The email of the user to be invited.

-o, --org ORG (deprecated)
:   Organization to invite user to.

--org-role ORG_ROLE (deprecated)
:   Organization role. Valid inputs are: `OrgManager`, `BillingManager`, `OrgAuditor`, and `OrgUser`. If omitted, the `OrgUser` role is set.

-s, --space SPACE (deprecated)
:   Space to invite user to.

--space-role SPACE_ROLE (deprecated)
:   Space role. Valid inputs are: `SpaceManager`, `SpaceDeveloper`, and `SpaceAuditor`.

-r, --region REGION (deprecated)
:   Region name. Defaults to current region if not specified.


If you aren't ready to assign access, or want to assign an IAM policy, you can invite a user and assign it later. For more information about assigning access to users, see [Managing access to resources](/docs/account?topic=account-assign-access-resources).
{: tip}

## ibmcloud account user-reinvite
{: #ibmcloud_account_user_reinvite}

Resend invitation to a user (account admin):
```bash
ibmcloud account user-reinvite USER_EMAIL
```
{: codeblock}

### Command options
{: #ibmcloud_account_user_reinvite_options}

USER_EMAIL (required)
:   The email of the user to be invited again.

## ibmcloud account user-preference
{: #ibmcloud_account_user_preference}

Show user preference details:
```bash
ibmcloud account user-preference
```
{: codeblock}

## ibmcloud account user-preference-update
{: #ibmcloud_account_user_preference_update}

Update user preferences:
```bash
ibmcloud account user-preference-update (--position NEW_POSITION)
```
{: codeblock}

### Command options
{: #ibmcloud_account_user_preference_update_options}

--position *NEW_POSITION* (optional)
:   Set a user's position, such as `manager` or `student`.

## ibmcloud account user-status
{: #ibmcloud_account_user_status}

Show the user's status:
```bash
ibmcloud account user-status [USER_ID] [--output FORMAT] [-q, --quiet]
```
{: codeblock}

### Command options
{: #ibmcloud_account_user_status_options}

USER_ID
:   User ID. If not specified, default to the current user.

--output FORMAT
:   Specify the output format. Only 'JSON' is supported.

-q, --quiet
:   Suppress verbose output.

## ibmcloud account user-status-update
{: #ibmcloud_account_user_status_update}

Update the user's status:
```bash
ibmcloud account user-status-update USER_ID NEW_STATUS [--output FORMAT] [-q, --quiet]
```
{: codeblock}

### Command options
{: #ibmcloud_account_user_status_update_options}

USER_ID (required)
:   User ID.

NEW_STATUS (required)
:   Set a user's status, such as `SUSPENDED` or `ACTIVE`. For more information, see [User account status](https://cloud.ibm.com/apidocs/user-management#user-states) for a list of possible statuses. This option can also take in values in lowercase such as `suspended` or `active`.

--output FORMAT
:   Specify the output format. Only 'JSON' is supported.

-q, --quiet
:   Suppress verbose output.

### Examples
{: #ibmcloud_account_user_status_update_examples}

Suspend user `user@ibm.com`:
```bash
ibmcloud account user-status-update user@ibm.com SUSPENDED
```

## ibmcloud account platform-notification-subscribe
{: #ibmcloud_account_platform_notification_subscribe}

Subscribe platform notification:
```bash
ibmcloud account platform-notification-subscribe (--type TYPE)
```
{: codeblock}

### Command options
{: #ibmcloud_account_platform_notification_subscribe_options}

--type *TYPE* (optional)
:   Notification type, one of `unplanned_events`, `planned_maintenance`.

## ibmcloud account platform-notification-unsubscribe
{: #ibmcloud_account_platform_notification_unsubscribe}

Unsubscribe platform notification:
```bash
ibmcloud account platform-notification-unsubscribe (--type TYPE)
```
{: codeblock}

### Command options
{: #ibmcloud_account_platform_notification_unsubscribe_options}

--type *TYPE* (optional)
:   Notification type, one of `unplanned_events`, `planned_maintenance`.
