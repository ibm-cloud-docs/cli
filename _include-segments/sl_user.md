


## ibmcloud sl user apikey
{: #sl_user_apikey}

Allows to create, remove or refresh user's API authentication key

Each user can only have a single API key.

```bash
ibmcloud sl user apikey IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--add
:    Create an user's API authentication key

--refresh
:    Refresh an user's API authentication key

--remove
:    Remove an user's API authentication key

## ibmcloud sl user create
{: #sl_user_create}

Creates a user

ibmcloud sl user create USERNAME [OPTIONS] 

**Examples**:
 	
    ibmcloud sl user create my@email.com --email my@email.com --password generate --template '{"firstName": "Test", "lastName": "Testerson"}'
    Remember to set the permissions and access for this new user.

```bash
ibmcloud sl user create USERNAME [flags]
```
{: codeblock}


**Command options**:

--email
:    Email address for this user. Required for creation

--f, force
:    Force operation without confirmation

--from-user
:    Base user to use as a template for creating this user. The default is to use the user that is running this command. Information provided in --template supersedes this template

--password
:    Password to set for this user. If no password is provided, the user is sent an email to generate one, which expires in 24 hours. Specify the '-p generate' option to generate a password for you. Passwords require 8+ characters, uppercase and lowercase, a number and a symbol

--template
:    A json string describing https://softlayer.github.io/reference/datatypes/SoftLayer_User_Customer/

--vpn-password
:    VPN password to set for this user.

## ibmcloud sl user delete
{: #sl_user_delete}

Sets a user's status to CANCEL_PENDING, which will immediately disable the account, and will eventually be fully removed from the account by an automated internal process



```bash
ibmcloud sl user delete USER_ID [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

## ibmcloud sl user detail
{: #sl_user_detail}

User details



```bash
ibmcloud sl user detail USER_ID [flags]
```
{: codeblock}


**Command options**:

--events
:    Show audit log for this user

--hardware
:    Display hardware this user has access to

--keys
:    Show the users API key

--logins
:    Show login history of this user for the last 24 hours

--permissions
:    Display permissions assigned to this user. Master users do not show permissions

--virtual
:    Display virtual guests this user has access to

## ibmcloud sl user detail-edit
{: #sl_user_detail_edit}

Edit a user's details

ibmcloud sl user detail-edit IDENTIFIER [OPTIONS]

**Examples**:
 
    ibmcloud sl user detail-edit USER_ID --template '{"firstName": "Test", "lastName": "Testerson"}'
    This command edit a users details.

```bash
ibmcloud sl user detail-edit USER_ID [flags]
```
{: codeblock}


**Command options**:

--template
:    A json string describing https://softlayer.github.io/reference/datatypes/SoftLayer_User_Customer/

## ibmcloud sl user device-access
{: #sl_user_device_access}

List all devices the user has access and device access permissions.



```bash
ibmcloud sl user device-access IDENTIFIER
```
{: codeblock}


## ibmcloud sl user edit-notifications
{: #sl_user_edit_notifications}

Enable or Disable specific notifications for the active user.

Notification names should be enclosed in quotation marks.
**Examples**:

	slcli user edit-notifications --enable 'Order Approved'
	slcli user edit-notifications --enable 'Order Approved' --enable 'Reload Complete'

```bash
ibmcloud sl user edit-notifications [flags]
```
{: codeblock}


**Command options**:

--disable
:    Disable selected notifications

--enable
:    Enable (DEFAULT) selected notifications

## ibmcloud sl user grant-access
{: #sl_user_grant_access}

Grant access from a user to an specific device



```bash
ibmcloud sl user grant-access IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--dedicated
:    Dedicated Host ID

--hardware
:    Hardware ID

--virtual
:    Virtual Guest ID

## ibmcloud sl user list
{: #sl_user_list}

List Users



```bash
ibmcloud sl user list [flags]
```
{: codeblock}


**Command options**:

--column
:    Column to display. options are: 2FA, classicAPIKey, displayName, email, hardwareCount, id, status, username, virtualGuestCount, vpn. This option can be specified multiple times

## ibmcloud sl user notifications
{: #sl_user_notifications}

List email subscription notifications



```bash
ibmcloud sl user notifications
```
{: codeblock}


## ibmcloud sl user permission-edit
{: #sl_user_permission_edit}

Enable or Disable specific permissions



```bash
ibmcloud sl user permission-edit IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--enable
:    Enable or Disable selected permissions. Accepted inputs are 'true' and 'false'. default is 'true'

--from-user
:    Set permissions to match this user's permissions. Adds and removes the appropriate permissions

--permission
:    Permission keyName to set. Use keyword ALL to select ALL permissions

## ibmcloud sl user permissions
{: #sl_user_permissions}

View user permissions

Some permissions here may also be managed by the IBM IAM service.
See https://cloud.ibm.com/docs/account?topic=account-migrated_permissions for more details.

```bash
ibmcloud sl user permissions USER_ID
```
{: codeblock}


## ibmcloud sl user remove-access
{: #sl_user_remove_access}

Remove access from a user to an specific device



```bash
ibmcloud sl user remove-access IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--dedicated
:    Dedicated Host ID

--hardware
:    Hardware ID

--virtual
:    Virtual Guest ID

## ibmcloud sl user vpn-disable
{: #sl_user_vpn_disable}

Disable vpn for a user.



```bash
ibmcloud sl user vpn-disable USER_ID
```
{: codeblock}


## ibmcloud sl user vpn-enable
{: #sl_user_vpn_enable}

Enable vpn for a user.



```bash
ibmcloud sl user vpn-enable USER_ID
```
{: codeblock}


## ibmcloud sl user vpn-manual
{: #sl_user_vpn_manual}

Enable or disable user vpn subnets manual config.



```bash
ibmcloud sl user vpn-manual USER_ID [flags]
```
{: codeblock}


**Command options**:

--disable
:    Disable vpn subnets manual config.

--enable
:    Enable vpn subnets manual config.

## ibmcloud sl user vpn-password
{: #sl_user_vpn_password}

Set the user VPN password.



```bash
ibmcloud sl user vpn-password IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--password
:    Your new VPN password [required]

## ibmcloud sl user vpn-subnet
{: #sl_user_vpn_subnet}

Add or remove subnet access for a user.



```bash
ibmcloud sl user vpn-subnet USER_ID SUBNET_ID [flags]
```
{: codeblock}


**Command options**:

--add
:    Add access to subnet.

--remove
:    Remove access to subnet.
