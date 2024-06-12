


## ibmcloud sl security cert-add
{: #sl_security_cert_add}

Add and upload SSL certificate details

ibmcloud sl security cert-add [OPTIONS]

**Examples**:

   ibmcloud sl security cert-add --crt ~/ibm.com.cert --key ~/ibm.com.key 
   This command adds certificate file: ~/ibm.com.cert and private key file ~/ibm.com.key for domain ibm.com.

```bash
ibmcloud sl security cert-add [flags]
```
{: codeblock}


**Command options**:

--crt
:    Certificate file

--csr
:    Certificate Signing Request file

--icc
:    Intermediate Certificate file

--key
:    Private Key file

--notes
:    Additional notes

## ibmcloud sl security cert-download
{: #sl_security_cert_download}

Download SSL certificate and key files

ibmcloud sl security cert-download IDENTIFIER [OPTIONS]

**Examples**:

   ibmcloud sl security cert-download 12345678
   This command downloads four files to current directory for certificate with ID 12345678. The four files are: certificate file, certificate signing request file, intermediate certificate file and private key file.

```bash
ibmcloud sl security cert-download IDENTIFIER
```
{: codeblock}


## ibmcloud sl security cert-edit
{: #sl_security_cert_edit}

Edit SSL certificate

ibmcloud sl security cert-edit IDENTIFIER [OPTIONS]

**Examples**:

   ibmcloud sl security cert-edit 12345678 --key ~/ibm.com.key 
   This command edits certificate with ID 12345678 and updates its private key with file: ~/ibm.com.key.

```bash
ibmcloud sl security cert-edit IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--crt
:    Certificate file

--csr
:    Certificate Signing Request file

--icc
:    Intermediate Certificate file

--key
:    Private Key file

--notes
:    Additional notes

## ibmcloud sl security cert-list
{: #sl_security_cert_list}

List SSL certificates on your account

ibmcloud sl security cert-list [OPTIONS]

**Examples**:

   ibmcloud sl security cert-list --status valid --sortby days_until_expire
   This command lists all valid certificates on current account and sort them by validity days.

```bash
ibmcloud sl security cert-list [flags]
```
{: codeblock}


**Command options**:

--sortby
:    Column to sort by. Options are: id,common_name,days_until_expire,note

--status
:    Show certificates with this status, default is: all, options are: all,valid,expired

## ibmcloud sl security cert-remove
{: #sl_security_cert_remove}

Remove SSL certificate

ibmcloud sl security cert-remove IDENTIFIER [OPTIONS]

**Examples**:

   ibmcloud sl security cert-remove 12345678 
   This command removes certificate with ID 12345678.

```bash
ibmcloud sl security cert-remove IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation

## ibmcloud sl security sshkey-add
{: #sl_security_sshkey_add}

Add a new SSH key

ibmcloud sl security sshkey-add LABEL [OPTIONS]

**Examples**:

   ibmcloud sl security sshkey-add my_sshkey -f ~/.ssh/id_rsa.pub --note mykey
   This command adds an SSH key from file ~/.ssh/id_rsa.pub with a note "mykey".

```bash
ibmcloud sl security sshkey-add LABEL [flags]
```
{: codeblock}


**Command options**:

--f, in-file
:    The id_rsa.pub file to import for this key

--k, key
:    The actual SSH key

--note
:    Extra note to be associated with the key

## ibmcloud sl security sshkey-edit
{: #sl_security_sshkey_edit}

Edit an SSH key

ibmcloud sl security sshkey-edit IDENTIFIER [OPTIONS]

**Examples**:

   ibmcloud sl security sshkey-edit 12345678 --label IBMCloud --note testing
   This command updates the SSH key with ID 12345678 and sets label to "IBMCloud" and note to "testing".

```bash
ibmcloud sl security sshkey-edit IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--label
:    The new label for the key

--note
:    New notes for the key

## ibmcloud sl security sshkey-list
{: #sl_security_sshkey_list}

List SSH keys on your account

ibmcloud sl security sshkey-list [OPTIONS]

**Examples**:

   ibmcloud sl security sshkey-list --sortby label
   This command lists all SSH keys on current account and sorts them by label.

```bash
ibmcloud sl security sshkey-list [flags]
```
{: codeblock}


**Command options**:

--sortby
:    Column to sort by. Options are: id,label,fingerprint,note

## ibmcloud sl security sshkey-print
{: #sl_security_sshkey_print}

Prints out an SSH key to the screen

ibmcloud sl security sshkey-print IDENTIFIER [OPTIONS]

**Examples**:

   ibmcloud sl security sshkey-print 12345678 -f ~/mykey.pub
   This command shows the ID, label and notes of SSH key with ID 12345678 and write the public key to file: ~/mykey.pub.

```bash
ibmcloud sl security sshkey-print [flags]
```
{: codeblock}


**Command options**:

--f, out-file
:    The public SSH key will be written to this file

## ibmcloud sl security sshkey-remove
{: #sl_security_sshkey_remove}

Permanently removes an SSH key

ibmcloud sl security sshkey-remove IDENTIFIER [OPTIONS]

**Examples**:

   ibmcloud sl security sshkey-remove 12345678 -f 
   This command removes the SSH key with ID 12345678 without asking for confirmation.

```bash
ibmcloud sl security sshkey-remove IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--f, force
:    Force operation without confirmation
