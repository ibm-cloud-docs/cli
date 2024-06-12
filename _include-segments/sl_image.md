


## ibmcloud sl image datacenter
{: #sl_image_datacenter}

Add/Remove datacenter of an image.

ibmcloud sl image datacenter IDENTIFIER [OPTIONS] 

**Examples**:

	ibmcloud sl image datacenter 12345678 --add dal05 --remove sjc03
	This command Add/Remove datacenter of an image.

```bash
ibmcloud sl image datacenter IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--add
:    To add Datacenter

--remove
:    To remove Datacenter

## ibmcloud sl image delete
{: #sl_image_delete}

Delete an image 



```bash
ibmcloud sl image delete IDENTIFIER
```
{: codeblock}


## ibmcloud sl image detail
{: #sl_image_detail}

Get details for an image



```bash
ibmcloud sl image detail IDENTIFIER
```
{: codeblock}


## ibmcloud sl image edit
{: #sl_image_edit}

Edit details of an image

ibmcloud sl image edit IDENTIFIER [OPTIONS]

**Examples**:
 
   ibmcloud sl image edit 12345678 --name ubuntu16 --note testing --tag staging
   This command edits an image with ID 12345678 and set its name to "ubuntu16", note to "testing", and tag to "staging".

```bash
ibmcloud sl image edit IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--name
:    Name of the image

--note
:    Add notes for the image

--tag
:    Tags for the image

## ibmcloud sl image export
{: #sl_image_export}

Export an image to an object storage

IDENTIFIER: ID of the image
URI: The URI for an object storage object (.vhd/.iso file) of the format: cos://regionName/bucketName/objectPath
API_KEY: The IBM Cloud API Key with access to IBM Cloud Object Storage instance.

```bash
ibmcloud sl image export IDENTIFIER URI API_KEY
```
{: codeblock}


## ibmcloud sl image import
{: #sl_image_import}

Import an image from an object storage

ibmcloud sl image import NAME URI API_KEY [--note NOTE] [--os-code OS_CODE] [--root-key-crn ROOT_KEY_CRN] [--wrapper-dek WRAPPER_DEK] [--cloud-init] [--byol] [--is-encrypted]
    NAME: The image name
    URI: The URI for an object storage object (.vhd/.iso file) of the format: cos://regionName/bucketName/objectPath
    API_KEY: The IBM Cloud API Key with access to IBM Cloud Object Storage instance.

```bash
ibmcloud sl image import NAME URI API_KEY [flags]
```
{: codeblock}


**Command options**:

--byol
:    Specifies if image is bring your own license

--cloud-init
:    Specifies if image is cloud-init

--is-encrypted
:    Specifies if image is encrypted

--note
:    The note to be applied to the imported template

--os-code
:    The referenceCode of the operating system software description for the imported VHD, ISO, or RAW image

--root-key-crn
:    CRN of the root key in your KMS instance

--wrapped-dek
:    Wrapped Data Encryption Key provided by IBM KeyProtect. For more info see: https://console.bluemix.net/docs/services/key-protect/wrap-keys.html#wrap-keys

## ibmcloud sl image list
{: #sl_image_list}

List all images on your account



```bash
ibmcloud sl image list [flags]
```
{: codeblock}


**Command options**:

--name
:    Filter on image name

--private
:    Display only private images

--public
:    Display only public images

## ibmcloud sl image share
{: #sl_image_share}

Share an image template with another account.



```bash
ibmcloud sl image share IDENTIFIER ACCOUNT ID
```
{: codeblock}


## ibmcloud sl image share-deny
{: #sl_image_share_deny}

Deny sharing of an image template with another account.



```bash
ibmcloud sl image share-deny IDENTIFIER ACCOUNT ID
```
{: codeblock}

