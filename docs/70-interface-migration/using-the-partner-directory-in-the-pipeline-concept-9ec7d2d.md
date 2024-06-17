<!-- loio9ec7d2dce72d423abff80543f11b2091 -->

# Using the Partner Directory in the Pipeline Concept

In the pipeline concept, most generic integration flows rely on the Partner Directory. This topic discusses parameters in the Partner Directory that help to define the message processing behavior and the XSLTs that are stored in the Partner Directory as binaries and used to dynamically determine receivers and interfaces.

For an overview of the Partner Directory API, see [Partner Directory](https://help.sap.com/docs/integration-suite/sap-integration-suite/partner-directory).



<a name="loio9ec7d2dce72d423abff80543f11b2091__section_jjh_gty_31c"/>

## Accessing the Partner Directory

> ### Note:  
> The REST client used in the tests for the pipeline concept is **Visual Studio Code**, so the example requests follow the syntax of this extension for Visual Studio Code.

In Visual Studio Code, you can define a settings file in which you maintain the environment variables holding the required URLs and credentials. As a prerequisite, you have setup the service instance and service key. See [Setting Up Inbound HTTP Connections \(for API Clients\)](https://help.sap.com/docs/integration-suite/sap-integration-suite/setting-up-inbound-http-connections-for-api-clients).

You need the following environment variables, which you can retrieve from your service key:

-   `apitokenurl`

-   `api_clientid` and `api_clientsecret`

-   `apihost`


For a request towards the Partner Directory API, authenticate yourself towards the token service to fetch an access token:

```
### fetch access token
# @name getAccessToken
GET {{apitokenurl}}?grant_type=client_credentials HTTP/1.1
Authorization: Basic {{api_clientid}}:{{api_clientsecret}}
```

Store the returned token in a variable:

```
###
@accesstoken = {{getAccessToken.response.body.access_token}}
```

For POST requests, fetch an XSRF token. Authentication is done using the bearer token that you fetched before:

```
### fetch XSRF token
# @name getXSRFToken
GET https://{{apihost}}/api/v1 HTTP/1.1
X-CSRF-Token: fetch
Authorization: Bearer {{accesstoken}}
```

Again, store the returned XSRF token in a variable:

```
###
@xsrftoken = {{getXSRFToken.response.headers.x-csrf-token}}
```

Use both tokens for writing data into the Partner Directory. The following is an example for a string parameter:

```
### create string parameter
POST https://{{apihost}}/api/v1/StringParameters
content-type: application/json
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{xsrftoken}}

{
    "Pid": "your partner ID",
    "Id": "ID of the object",
    "Value": "Value of the object"
}
```

The following example shows how to read a string parameter:

```
### read string parameter
GET https://{{apihost}}/api/v1/StringParameters(Pid='your partner ID',Id='ID of the object')
Authorization: Bearer {{accesstoken}}
```

The following example shows how to delete a string parameter:

```
### delete string parameter
DELETE https://{{apihost}}/api/v1/StringParameters(Pid='your partner ID',Id='ID of the object')
Authorization: Bearer {{accesstoken}}
```



<a name="loio9ec7d2dce72d423abff80543f11b2091__section_bxk_wty_31c"/>

## Message Processing Behavior

The following table lists the different required string parameters that are used to dynamically define the message processing behavior:


<table>
<tr>
<th valign="top">

Pid

</th>
<th valign="top">

Id

</th>
<th valign="top">

Value

</th>
<th valign="top">

Mandatory/Optional

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`<Sender system>~<Sender interface>`

</td>
<td valign="top">

`InboundConversionEndpoint`

</td>
<td valign="top">

`ProcessDirect endpoint`

</td>
<td valign="top">

Optional

</td>
<td valign="top">

ProcessDirect endpoint of inbound conversion integration flow, if required

</td>
</tr>
<tr>
<td valign="top">

`<Sender system>~<Sender interface` 

</td>
<td valign="top">

`MaxJMSRetries`

</td>
<td valign="top">

`integer`

</td>
<td valign="top">

Optional, default is unlimited

</td>
<td valign="top">

Maximum number of retries

</td>
</tr>
<tr>
<td valign="top">

`<Sender system>~<Sender interface>`

</td>
<td valign="top">

`ReuseXRDEndpoint`

</td>
<td valign="top">

`ProcessDirect endpoint`

</td>
<td valign="top">

Optional

</td>
<td valign="top">

ProcessDirect endpoint of extended receiver determination integration flow, if required

</td>
</tr>
<tr>
<td valign="top">

`<Sender system>~<Sender interface>`

</td>
<td valign="top">

`ReceiverNotDeterminedType`

</td>
<td valign="top">

`Error`, `Ignore`, or `Default`

</td>
<td valign="top">

Should be set if `ReuseXRDEndpoint` exists, if not set default as *Error*

</td>
<td valign="top">

Behavior if receiver can't be determined

</td>
</tr>
<tr>
<td valign="top">

`<Sender system>~<Sender interface>`

</td>
<td valign="top">

`ReceiverNotDeterminedDefault`

</td>
<td valign="top">

`String`

</td>
<td valign="top">

Required if `ReceiverNotDeterminedType` equals *Default*

</td>
<td valign="top">

Default receiver system name

</td>
</tr>
<tr>
<td valign="top">

`<Receiver system>`

</td>
<td valign="top">

`ReceiverSpecificQueue`

</td>
<td valign="top">

`String`

</td>
<td valign="top">

Optional

</td>
<td valign="top">

Queue name for receiver system-specific outbound queue

</td>
</tr>
</table>



### Inbound Conversion

To determine whether your specific scenario needs an inbound conversion, create a string parameter holding the ProcessDirect endpoint of your scenario-specific inbound conversion flow.

The partner ID is a combination of the sender system name and the sender interface name, separated with `~`.

The following is an example of a partner ID \(`pid`\):

```
@pid = Sender_1~Interface_1
```

If you need inbound conversion, define a Partner Directory entry with object ID `InboundConversionEndpoint`, which points to the ProcessDirect endpoint of the scenario-specific integration flow for inbound conversion.

```
### create string parameter: InboundConversionEndpoint
POST https://{{apihost}}/api/v1/StringParameters
content-type: application/json
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{token}}

{
    "Pid": "{{pid}}",
    "Id": "InboundConversionEndpoint",
    "Value": "/pip/03/scenario1"
}
```



### Maximum Number of JMS Retries

For each scenario, you can define a maximum number of retries to handle the retry behavior of your scenarios individually. This parameter is optional and the default is unlimited. You can edit the provided Groovy script and change the default to any valid global value. See [readRetryHandlingFromPD](script-collection-for-pipeline-concept-05d9f8d.md#loio05d9f8d85d7945af8d610dca81375b43__section_jjn_gy2_j1c).

Again, the partner ID is a combination of the sender system name and the sender interface name, separated with `~`.

```
@pid = Sender_1~Interface_1
```

The object ID is `MaxJMSRetries`. In the following example, the maximum number of retries is set to `3`.

```
### create string parameter: MaxJMSRetries
POST https://{{apihost}}/api/v1/StringParameters
content-type: application/json
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{token}}

{
    "Pid": "{{pid}}",
    "Id": "MaxJMSRetries",
    "Value": "3"
}
```



### Reuse Extended Receiver Determination

If your integrated configuration object in SAP Process Orchestration already uses the extended receiver determination feature, you can reuse the mapping instead of using the default option, which is an XSLT mapping stored in the Partner Directory. If you choose to reuse, you must create a string parameter that holds the ProcessDirect endpoint of your integration flow carrying out the mapping. Also, create a string parameter that defines the `Receiver not determined` behavior, which is alternatively defined within the XSLT mapping. If `Receiver not determined` type equals default, you must also define a string parameter that holds the default receiver system name.

Again, the partner ID is a combination of the sender system name and the sender interface name, separated with `~`.

```
@pid = Sender_1~Interface_1
```

Define a Partner Directory entry with object ID ReuseXRDEndpoint as follows:

```
POST https://{{apihost}}/api/v1/StringParameters
content-type: application/json
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{token}}

{
    "Pid": "{{pid}}",
    "Id": "ReuseXRDEndpoint",
    "Value": "/pip/04/scenario4"
}
```

If you've defined an endpoint, you also need to define another Partner Directory entry with object ID `ReceiverNotDeterminedType`. The default value is *Error*.

```
POST https://{{apihost}}/api/v1/StringParameters
content-type: application/json
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{token}}

{
    "Pid": "{{pid}}",
    "Id": "ReceiverNotDeterminedType",
    "Value": "Default"
}
```

If `ReceiverNotDeterminedType` equals *Default*, define another Partner Directory entry with object ID `ReceiverNotDeterminedDefault`.

```
POST https://{{apihost}}/api/v1/StringParameters
content-type: application/json
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{token}}

{
    "Pid": "{{pid}}",
    "Id": "ReceiverNotDeterminedDefault",
    "Value": "Receiver_1"
}
```



### Receiver-Specific Outbound Queue

By default, each scenario uses the same set of generic JMS queues. For receivers for which you want to control the outbound delivery, you can define receiver-specific JMS queues.

This time, the partner ID is the receiver system name.

```
@pid = Receiver_3
```

The object ID is `ReceiverSpecificQueue`. This parameter is optional. If not set, the default outbound queue is used.

```
POST https://{{apihost}}/api/v1/StringParameters
content-type: application/json
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{token}}

{
    "Pid": "{{pid}}",
    "Id": "ReceiverSpecificQueue",
    "Value": "PIPQ04_R3"
}

```



<a name="loio9ec7d2dce72d423abff80543f11b2091__section_thd_scz_31c"/>

## XSLT Mappings

This section discusses the different XSLTs that are used to execute the xpath conditions for either determining the receivers or the interfaces.



### XSLT Mapping for Determining Receivers

Unless you reuse the extended receiver determination mapping, you must create an XSLT in the Partner Directory for each scenario. The XSLT mapping carries out the xpath routing conditions to determine the list of receivers. For an example, see [Receiver Determination \(Generic\)](pipeline-steps-f8e69f4.md#loiof8e69f43059a44cdb891892f4ff083d8__section_qbb_wyk_31c).

> ### Note:  
> The XSLT mapping is stored as binary, so you need to encode the XSLT before uploading to the Partner Directory.

For the receiver determination XSLT, the partner ID is a combination of the sender system name and the sender interface name, separated with `~`.

```
@pid = Sender_1~Interface_1
```

The object ID is `receiverDetermination`. Let's assume that the encoded XSLT mapping is stored in the variable binary.

```
POST https://{{apihost}}/api/v1/BinaryParameters
content-type: application/json
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{token}}

{
  "Pid": "{{pid}}",
  "Id": "receiverDetermination",
  "ContentType": "xsl",
  "Value": "{{binary}}"
}
```



### XSLT Mapping for Determining Interfaces

For each receiver of your scenario, you need to create an XSLT in the Partner Directory that carries out the xpath routing conditions to determine the interfaces. For an example, see [Interface Determination \(Generic\)](pipeline-steps-f8e69f4.md#loiof8e69f43059a44cdb891892f4ff083d8__section_drs_wyk_31c).

> ### Note:  
> The XSLT mapping is stored as binary, so you need to encode the XSLT before uploading to the Partner Directory.

For the interface determination XSLT, the partner ID is a combination of the sender system name, the sender interface name, and the receiver system name, separated with `~`.

```
@pid = Sender_1~Interface_1~Receiver_3
```

The object ID is `interfaceDetermination`. Let's assume that the encoded XSLT mapping is stored in the variable binary.

```
POST https://{{apihost}}/api/v1/BinaryParameters
content-type: application/json
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{token}}

{
  "Pid": "{{pid}}",
  "Id": "interfaceDetermination",
  "ContentType": "xsl",
  "Value": "{{binary}}"
}
```

