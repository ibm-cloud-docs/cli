


## ibmcloud sl cdn create
{: #sl_cdn_create}

Create a new CDN domain mapping

ibmcloud sl cdn create
**Examples**:

ibmcloud sl cdn create --hostname www.example.com --origin 123.45.67.8 --http 80

```bash
ibmcloud sl cdn create [flags]
```
{: codeblock}


**Command options**:

--bucket-name
:    Bucket name

--cname
:    Enter a globally unique subdomain. The full URL becomes the CNAME we use to configure your DNS. If no value is entered, we will generate a CNAME for you.

--header
:    The edge server uses the host header in the HTTP header to communicate with the Origin host. It defaults to Hostname.

--hostname
:    To route requests to your website, enter the hostname for your website, for example, www.example.com or app.example.com. [required]

--http
:    Http port

--https
:    Https port

--origin
:    Your server IP address or hostname. [required]

--origin-type
:    The origin type. [Permit: server, storage] Note: If OriginType is storage then OriginHost is take as Endpoint

--path
:    Give a path relative to the domain provided, which can be used to reach this Origin. For example, 'articles/video' => 'www.example.com/articles/video

--ssl
:    A DV SAN Certificate allows HTTPS traffic over your personal domain, but it requires a domain validation to prove ownership. A wildcard certificate allows HTTPS traffic only when using the CNAME given. [Permit: dvSan, wilcard]

## ibmcloud sl cdn delete
{: #sl_cdn_delete}

Delete a CDN domain mapping.

ibmcloud sl cdn delete

```bash
ibmcloud sl cdn delete IDENTIFIER
```
{: codeblock}


## ibmcloud sl cdn detail
{: #sl_cdn_detail}

Detail a CDN Account.

ibmcloud sl cdn detail

```bash
ibmcloud sl cdn detail [flags]
```
{: codeblock}


**Command options**:

--history
:    Bandwidth, Hits, Ratio counted over history number of days ago. 89 is the maximum.

## ibmcloud sl cdn edit
{: #sl_cdn_edit}

Edit a CDN Account.

ibmcloud sl cdn edit

```bash
ibmcloud sl cdn edit [flags]
```
{: codeblock}


**Command options**:

--cache
:    Cache key optimization. These are the valid options to choose: 'include-all', 'ignore-all', 'include-specified', 'ignore-specified'. If you select 'include-specified' or 'ignore-specified' please add to option cache-description.

--cache-description
:    In cache option, if you select 'include-specified' or 'ignore-specified', please add a description too using this option e.g --cache include-specified --cache-description description.

--header
:    Host header.

--http-port
:    HTTP port.

--https-port
:    HTTPS port.

--origin
:    Origin server address.

--performance-configuration
:    Optimize for, 'General web delivery', 'Large file optimization', 'Video on demand optimization', the Dynamic content acceleration option is not added because this has a special configuration.

--respect-headers
:    Respect headers. The value 1 is On and 0 is Off.

## ibmcloud sl cdn list
{: #sl_cdn_list}

List all CDN accounts.

ibmcloud sl cdn list

```bash
ibmcloud sl cdn list
```
{: codeblock}


## ibmcloud sl cdn origin-add
{: #sl_cdn_origin_add}

Create an origin path for an existing CDN mapping.

ibmcloud sl cdn origin-add
**Examples**:

ibmcloud sl cdn origin-add --origin 123.123.123.123 --path /example/videos --http 80

```bash
ibmcloud sl cdn origin-add IDENTIFIER [flags]
```
{: codeblock}


**Command options**:

--bucket-name
:    Bucket name.

--cache-key
:    Cache query rules with the following formats: 'include-all', 'ignore-all', 'include: query-names', 'ignore: query-names'. example query-names = 'uuid=1234567 issue=important'.

--compression
:    Enable or disable compression of JPEG images for requests over certain network conditions.

--dynamic-path
:    The path that Akamai edge servers periodically fetch the test object from. example = /detection-test-object.html

--file-extensions
:    Specify the file extensions that can be stored on the CDN service, separated by commas. For example, 'jpg, pdf, jpeg, png' is a valid list. Leave the flag empty to allow all extensions.

--header
:    The edge server uses the host header in the HTTP header to communicate with the Origin host. It defaults to Hostname.

--http
:    Http port. [http or https is required]

--https
:    Https port. [http or https is required]

--optimize
:    Performance configuration. [Permit: web, video, file, dynamic]

--origin
:    Your server IP address or hostname. [required]

--origin-type
:    The origin type. [Permit: server, storage] Note: If OriginType is storage then OriginHost is take as Endpoint.

--path
:    Give a path relative to the domain provided, which can be used to reach this Origin. For example, 'articles/video' => 'www.example.com/articles/video [required]

--prefetching
:    Enable or disable the embedded object prefetching feature.

## ibmcloud sl cdn origin-list
{: #sl_cdn_origin_list}

List origin path for an existing CDN mapping.

List origin path for an existing CDN mapping. ibmcloud sl cdn origin-list

```bash
ibmcloud sl cdn origin-list IDENTIFIER
```
{: codeblock}


## ibmcloud sl cdn origin-remove
{: #sl_cdn_origin_remove}

Removes an origin path for an existing CDN mapping.

Removes an origin path for an existing CDN mapping. ibmcloud sl cdn origin-remove
**Examples**:

ibmcloud sl cdn origin-remove 123456789 "/path/*"

```bash
ibmcloud sl cdn origin-remove IDENTIFIER PATH
```
{: codeblock}


## ibmcloud sl cdn purge
{: #sl_cdn_purge}

Creates a purge record and also initiates the purge call.

Creates a purge record and also initiates the purge call. For more information see the following documentation: https://cloud.ibm.com/docs/infrastructure/CDN?topic=CDN-manage-your-cdn#purging-cached-content ibmcloud sl cdn purge
**Examples**:

ibmcloud sl cdn purge 9779455 /article/file.txt"

```bash
ibmcloud sl cdn purge IDENTIFIER PATH
```
{: codeblock}

