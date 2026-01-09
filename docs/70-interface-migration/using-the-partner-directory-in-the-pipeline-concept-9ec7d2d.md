<!-- loio9ec7d2dce72d423abff80543f11b2091 -->

# Using the Partner Directory in the Pipeline Concept

In the pipeline concept, most generic integration flows rely on the Partner Directory. This topic discusses parameters in the Partner Directory that help to define the message processing behavior and the XSLTs that are stored in the Partner Directory as binaries and used to dynamically determine receivers and interfaces.

To create and maintain Partner Directory entries for setting up the integration scenarios for the Cloud Integration pipeline, you can either use the **Partner Directory API** or the new **Partner Directory user interface**.

For an overview of the Partner Directory API, see [Partner Directory](https://help.sap.com/docs/integration-suite/sap-integration-suite/partner-directory). For an overview of the Partner Directory user interface, see [Managing Partner Directory Entries](https://help.sap.com/docs/integration-suite/sap-integration-suite/managing-partner-directory-entries).



<a name="loio9ec7d2dce72d423abff80543f11b2091__section_jjh_gty_31c"/>

## Accessing the Partner Directory Using API

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

The following example shows how to create an alternative partner:

```
### create alternative partner 
POST https://{{apihost}}/api/v1/AlternativePartners 
content-type: application/json 
Authorization: Bearer {{accesstoken}} 
X-CSRF-Token: {{xsrftoken}} 

{ 
    "Agency": "your agency", 
    "Scheme": "your identification scheme", 
    "Id": "identifier for the partner issued by the agency", 
    "Pid": "your internal ID of the partner" 
} 
```

The following example shows how to create a binary parameter:

```
### create string parameter 
POST https://{{apihost}}/api/v1/BinaryParameters 
content-type: application/json 
Authorization: Bearer {{accesstoken}} 
X-CSRF-Token: {{xsrftoken}} 

{ 
    "Pid": "your partner ID", 
    "Id": "ID of the object", 
    "ContentType": "content type such as xml, xsl, xsd, etc.", 
    "Value": "Base64 encoded value of your binary" 
} 
```



<a name="loio9ec7d2dce72d423abff80543f11b2091__section_oy4_t1p_hcc"/>

## Partner ID



### 

The partner ID unambiguously determines the configuration scenario. It’s based on the sender system name and the sender interface information. The following approaches are supported:

-   **Recommended option**: You define the partner ID as **configuration scenario name**, and you map **sender system name** and **sender interface name** to the partner ID using an **alternative partner**.
-   **Alternative option**: You define the partner ID as a combination of the **sender system name** and the **sender interface name**.

> ### Note:  
> The recommended option has been extended for higher flexibility during the setup of your configuration scenario. This means you define the partner ID as **configuration scenario name**, and map **sender system name**, **sender interface name**, and **sender interface namespace** to the partner ID using an **alternative partner**. Since the alternative partner is defined differently compared to the standard option, this option is only supported if the sender interface name doesn't exceed 120 characters.

During runtime, the generic inbound processing flow first checks if an alternative partner exists that matches the headers `SAP_Sender`, `SAP_SenderInterface`, and `SapInterfaceNamespace`, which are passed from the scenario-specific inbound flows to the generic flows. If there's a match, the associated partner ID is used to read the Partner Directory parameters. If such an alternative partner doesn’t exist in the Partner Directory, in a second attempt, the standard option is applied. The standard option checks for an alternative partner that matches only the **sender system name** and the **sender interface name**.

For the generic XI inbound processing flow, in a first attempt, the partner ID is determined based on the headers `SapSenderService`, `SapInterfaceName` and `SapInterfaceNamespace`. These headers are passed from the XI sender adapter. If such an alternative partner doesn’t exist in the Partner Directory, in a second attempt, the standard option is applied, which checks for an alternative partner that matches the headers `SapSenderService` and `SapInterfaceName`.

For the generic IDoc inbound processing flow, in a first attempt, the partner ID is determined based on the **sender system name**, **sender interface name**, and the constant namespace `urn:sap-com:document:sap:idoc:messages`. The **sender system name** and the **sender interface name** are derived from the IDoc control header. The **sender system name** equals the sender partner number `SNDPRN` whereas the **sender interface name** is defined as combination of the message type `MESTYP`, the IDoc type `IDOCTYP` and eventually the extension type `CIMTYP`. The latter is only added if the IDoc control header field `CIMTYP` isn't empty.

If such an alternative partner doesn’t exist in the Partner Directory, in a second attempt, the standard option is applied.

If the partner ID still couldn't be determined, in a third attempt, the partner ID is constructed as a combination of the two header values **sender system name** and **sender interface name**, unless the option is switched off, as described in the following.

> ### Note:  
> You should only use the **recommended option** of using an alternative partner since the alternative option of using a combination of sender system and sender interface is only supported for compatibility reasons.
> 
> With the recommended option, not only are you less likely to run into any length restrictions of the partner ID, but it also supports sender wildcard scenarios, and allows you to group all your entries in the Partner Directory user interface using a scenario ID. Furthermore, only the recommended option supports the landscape stages feature.

> ### Note:  
> The alternative option of using a combination of sender system and sender interface is **switched off by default**. This way, if the partner ID can’t be determined based on an alternative partner, for example, due to inconsistencies or missing configuration in the Partner Directory, the processed message goes into an error instead of unintentionally constructing a wrong partner ID.
> 
> If you still want to use a combination of sender system and sender interface, you must configure the externalized parameter `CustomXPid_SwitchOffTilde` by changing from the default value `true` to `false` for the following integration flows:
> 
> -   `Pipeline v2 Generic Step01 - Inbound Processing for Idoc`
> -   `Pipeline v2 Generic Step01 - Inbound Processing for XI`
> -   `Pipeline v2 Generic Step02 - Inbound Processing`
> -   `Pipeline v2 Generic Step02 - Integrated Messaging Runtime Async`
> -   `Pipeline v2 Generic Step02 - Integrated Messaging Runtime Sync`



### Recommended option: Using alternative partner

The alternative partner allows you to be more flexible in defining the partner ID. Firstly, you're less likely to run into any length restrictions: Agency and scheme have a maximum length of 120, while the external ID can be up to 255 characters. Secondly, so-called sender wildcard scenarios are supported more easily, which means you can map multiple sender systems to the same partner ID, assuming that the configuration is the same.

To define an alternative partner, follow the following naming conventions:

-   **Agency** equals sender system name

-   **Scheme** is constant SenderInterface

-   **ID** holds the sender interface name

-   As **partner ID \(pid\)**, you can define a configuration scenario name


The following is an example of an alternative partner:

```
### create alternative partner for Scenario 1 
POST https://{{apihost}}/api/v1/AlternativePartners 
content-type: application/json 
Authorization: Bearer {{accesstoken}} 
X-CSRF-Token: {{xsrftoken}} 
					
{ 
	"Agency": "Sender_1", 
	"Scheme": "SenderInterface", 					
	"Id": "Interface_1", 
	"Pid": "Scenario_1"
} 
```

For XI inbound scenarios, you can define an alternative partner as follows:

-   **Agency** equals the sender system name
-   **Scheme** holds the sender interface name
-   **ID** holds the sender interface namespace
-   As **partner ID \(pid\)**, define a configuration scenario name

The following is an example of an alternative partner:

```
### create alternative partner for Scenario 2  
POST https://{{apihost}}/api/v1/AlternativePartners  
content-type: application/json  
Authorization: Bearer {{accesstoken}}  
X-CSRF-Token: {{xsrftoken}}  
					 
{
	"Agency": "Sender_2",  
	"Scheme": "Interface_2", 					 
	"Id": "http://namespace_2.com",  
	"Pid": "Scenario_2" 
}
```

For IDoc inbound scenarios, you can define an alternative partner as follows:

-   **Agency** equals the sender partner number.
-   **Scheme** holds the sender interface name.
-   **ID** holds the sender interface namespace `urn:sap-com:document:sap:idoc:messages`.
-   As **partner ID \(pid\)**, define a configuration scenario name.

The following is an example of an alternative partner:

```
### create alternative partner for Scenario 3  
POST https://{{apihost}}/api/v1/AlternativePartners  
content-type: application/json  
Authorization: Bearer {{accesstoken}}  
X-CSRF-Token: {{xsrftoken}}  
					 
{
	"Agency": "SNDCLNT100",  
	"Scheme": "MATMAS.MATMAS05", 					 
	"Id": "urn:sap-com:document:sap:idoc:messages",
	"Pid": "Scenario_3" 
}
```



### Alternative option: Combination of sender system and sender interface

The partner ID can be defined as the combination of the sender system name and the sender interface name, separated with "~".

The following is an example of a partner ID \(pid\):

```
@pid = Sender_1~Interface_1
```

> ### Note:  
> The partner ID is restricted to a maximum length of 60 characters. Depending on your naming conventions for the sender system and the sender interface, you may exceed the maximum length. In this case, use an **alternative partner**. For information on length restrictions, see [Partner Directory](https://help.sap.com/docs/integration-suite/sap-integration-suite/partner-directory).



<a name="loio9ec7d2dce72d423abff80543f11b2091__section_bxk_wty_31c"/>

## Message Processing Behavior

The following table lists the different required string parameters that are used to dynamically define the message processing behavior. They're read from the Partner Directory using the partner ID \(pid\) as defined in [Partner ID](using-the-partner-directory-in-the-pipeline-concept-9ec7d2d.md#loio9ec7d2dce72d423abff80543f11b2091__section_oy4_t1p_hcc).


<table>
<tr>
<th valign="top">

ID

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

`MaxJMSRetries`

</td>
<td valign="top">

`integer`

</td>
<td valign="top">

Optional, default is 5

</td>
<td valign="top">

Maximum number of retries

</td>
</tr>
<tr>
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

`CustomXRDEndpoint`

</td>
<td valign="top">

`String`

</td>
<td valign="top">

Optional

</td>
<td valign="top">

ProcessDirect endpoint of custom receiver determination integration flow, if required

</td>
</tr>
<tr>
<td valign="top">

`CustomXIDEndpoint`

</td>
<td valign="top">

`String`

</td>
<td valign="top">

Optional

</td>
<td valign="top">

ProcessDirect endpoint of custom interface determination integration flow, if required

</td>
</tr>
<tr>
<td valign="top">

`InboundQueue`

</td>
<td valign="top">

`String`

</td>
<td valign="top">

Optional

</td>
<td valign="top">

Overwriting the default inbound processing JM queue, if required

</td>
</tr>
<tr>
<td valign="top">

**KeepBulk**

</td>
<td valign="top">

`Boolean`

</td>
<td valign="top">

Optional, default is **false**

</td>
<td valign="top">

Only relevant for IDoc bulk messages. Set to *true* if the IDoc bulk message should not be split into single IDoc messages.

</td>
</tr>
<tr>
<td valign="top">

**CustomXPreEnabled**

</td>
<td valign="top">

`String`

</td>
<td valign="top">

Optional

</td>
<td valign="top">

List of pipeline steps for which a custom exit integration flow for preprocessing should be called

</td>
</tr>
<tr>
<td valign="top">

**CustomXPreEndpoint**

</td>
<td valign="top">

`String`

</td>
<td valign="top">

Required if *CustomXPreEnabled* is maintained

</td>
<td valign="top">

ProcessDirect endpoint of custom exit integration flow, if required

</td>
</tr>
</table>

The following table lists the details for the required string parameter that is used to dynamically define the message processing behavior with partner ID equals receiver name:


<table>
<tr>
<th valign="top">

ID

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

To determine whether your specific scenario needs an inbound conversion, create a string parameter holding the ProcessDirect endpoint of your scenario-specific inbound conversion flow. This can be defined either scenario-specific or for each sender system.

If you need inbound conversion and you only have one sender for your configuration scenario, create one scenario-specific inbound conversion flow. Then, configure a string parameter in the Partner Directory that points to the ProcessDirect endpoint of the scenario-specific integration flow.

If there are sender wildcard scenarios, that is, scenarios in which the same configuration applies to different sender systems, you have two options. If your inbound conversion is the same for each sender system, create a single scenario-specific inbound conversion flow, which means you only have to maintain one configuration parameter. If the inbound conversion differs depending on the sender systems, create scenario-specific inbound conversion flows for each sender system, which means you can maintain configuration parameters for each sender system.

The partner ID is derived from the sender system name and the sender interface name, either using an alternative partner or a combination of the sender system name and the sender interface name. See [Partner ID](using-the-partner-directory-in-the-pipeline-concept-9ec7d2d.md#loio9ec7d2dce72d423abff80543f11b2091__section_oy4_t1p_hcc).

If there's a single inbound conversion for your configuration scenario, define a Partner Directory entry with the object ID `InboundConversionEndpoint`, which points to the ProcessDirect endpoint of the scenario-specific integration flow for inbound conversion.

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

If you need multiple inbound conversions for your scenario depending on the sender systems, for each sender system, define a Partner Directory entry with the object ID being a combination of the constant identifier `InboundConversionEndpoint` and the sender system name, separated by an underscore "\_". As value, enter the ProcessDirect endpoint of the corresponding scenario-specific integration flow for inbound conversion.

```
### create string parameter: InboundConversionEndpoint
POST https://{{apihost}}/api/v1/StringParameters
content-type: application/json
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{token}}

{
    "Pid": "{{pid}}",
    "Id": "InboundConversionEndpoint_Sender_2",
    "Value": "/pip/03/scenario1/sender2"
}
```



### Maximum Number of JMS Retries

For each scenario, you can define a maximum number of retries to handle the retry behavior of your scenarios individually. This parameter is optional and the default is 5.

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



### Custom Receiver Determination

Instead of using the default option, which is an XSLT mapping stored in the Partner Directory, you can implement custom receiver determination. To do this, you must create a string parameter that holds the ProcessDirect endpoint of your integration flow that carries out the receiver determination logic.

> ### Note:  
> For both options, the custom receiver determination and the reuse of extended receiver determination, you can determine a list of receivers by calling a scenario-specific integration flow. You use the reuse of extended receiver determination option when migrating from SAP Process Orchestration in case your source Integrated Configuration already uses the extended receiver determination. With the custom receiver determination, you're more flexible compared to the reuse of extended receiver determination because here you can also define the `receiver not determined` behavior and eventually the list of receiver interfaces within the custom flow.

Define a Partner Directory entry with object ID `CustomXRDEndpoint` as follows:

```
POST https://{{apihost}}/api/v1/StringParameters 
content-type: application/json 
Authorization: Bearer {{accesstoken}} 
X-CSRF-Token: {{token}} 
 
{ 
    "Pid": "{{pid}}", 
    "Id": "CustomXRDEndpoint", 
    "Value": "/pip/04/xrd/scenario4" 
} 
```



### Custom Interface Determination

Instead of using the default option, which is an XSLT mapping stored in the Partner Directory, you can implement custom interface determination. To do this, you must create a string parameter that holds the ProcessDirect endpoint of your integration flow that carries out the interface determination logic.

Define a Partner Directory entry with object ID `ReuseXIDEndpoint` as follows:

```
POST https://{{apihost}}/api/v1/StringParameters 
content-type: application/json 
Authorization: Bearer {{accesstoken}} 
X-CSRF-Token: {{token}} 

{ 
    "Pid": "{{pid}}", 
    "Id": "CustomXIDEndpoint", 
    "Value": "/pip/05/xid/scenario4" 
} 
```



### Scenario-Specific Inbound Processing Queue

Instead of using the default inbound processing queue, you can define a scenario-specific inbound processing queue which routes the message to the corresponding pipeline. To do so, you must create a string parameter holding the name of the inbound processing JMS queue.

> ### Note:  
> This option is only needed for scenarios with either XI or IDoc sender adapter using the generic XI or IDoc inbound flows. For all other scenarios, you can simply define the inbound processing queue in the scenario-specific inbound processing flow.

Define a Partner Directory entry with object ID `InboundQueue` as follows:

```
POST https://{{apihost}}/api/v1/StringParameters
content-type: application/json
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{token}}

{
    "Pid": "{{pid}}", 
    "Id": "InboundQueue", 
    "Value": "PIPX01" 
}
```



### Keep IDoc Bulk

For IDoc inbound scenarios, by default, IDoc bulk messages are split into single IDoc messages. Each single IDoc message is passed to the next pipeline step. If you want to keep the IDoc bulk and not split the IDoc bulk message for a specific scenario, create a string parameter with value *true*. This parameter is optional and the default is *false*.

The object ID is `KeepBulk`. In the following example, the parameter is set to `true`.

```
### create string parameter: KeepBulk
POST https://{{apihost}}/api/v1/StringParameters
content-type: application/json
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{token}}

{
    "Pid": "{{pid}}",
    "Id": "KeepBulk",
    "Value": "true"
}
```



### Custom Preprocessing Exit

If you want to embed custom logic at the very beginning of the pipeline steps, you can call a custom exit integration flow without having to edit the provided generic flows. Custom preprocessing is supported globally, which means that the custom exit integration flow is called for all of your integration scenarios, or it can be configured scenario-specific. For scenario-specific configuration, you can define for which pipeline steps the custom exit integration flow should be called. For this, create a string parameter **CustomXPreEnabled** in which you define the list of pipeline steps separated by pipe.

Assuming that you want to enable the custom exit for the generic XI inbound processing \(step 01\), the generic integrated messaging runtime \(step 02\) and the generic outbound processing flow \(step 06\), define a Partner Directory entry with object ID **CustomXPreEnabled** as follows:

```
POST https://{{apihost}}/api/v1/StringParameters
content-type: application/json
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{token}}

{
    "Pid": "{{pid}}",
    "Id": "CustomXPreEnabled",
    "Value": "01|02|06"
}
```

If you've defined such a string parameter, you also need to define another Partner Directory entry with object ID `CustomXPreEndpoint`, which points to the ProcessDirect endpoint of the custom exit integration flow.

```
POST https://{{apihost}}/api/v1/StringParameters
content-type: application/json
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{token}}

{
    "Pid": "{{pid}}",
    "Id": "CustomXPreEndpoint",
    "Value": "/pip/custom/preProcessing/scenario4"
}
```



### Receiver-Specific Outbound Queue

By default, each scenario uses the same set of generic JMS queues. For receivers for which you want to control the outbound delivery, you can define receiver-specific JMS queues. This can be either defined globally or scenario specific. For the latter, you can define different receiver-specific queues for the same receiver depending on your particular configuration scenario. The scenario-specific setting overrides the global setting.

To use a receiver-specific JMS outbound queue across all your scenarios, use the partner ID as the receiver system name.

```
@pid = Receiver_3
```

The object ID is `ReceiverSpecificQueue`. As value, enter the receiver-specific queue name. This parameter is optional. If not set, the default outbound queue is used.

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

To define a receiver-specific JMS outbound queue for a particular configuration scenario only, use the partner ID as the configuration scenario name.

```
@pid = Scenario_2
```

In this case, the object ID is a combination of the constant identifier `ReceiverSpecificQueue` and the business system name, separated by an underscore "\_". As value, enter the receiver-specific queue name. This parameter is optional. If not set, the default outbound queue is used.

```
POST https://{{apihost}}/api/v1/StringParameters
content-type: application/json
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{token}}

{
    "Pid": "{{pid}}",
    "Id": "ReceiverSpecificQueue_Receiver_3",
    "Value": "PIPQ04_CS2R3"
}

```



<a name="loio9ec7d2dce72d423abff80543f11b2091__section_thd_scz_31c"/>

## XSLT Mappings

This section discusses the different XSLTs that are used to execute the XPath conditions for either determining the receivers or the interfaces.



### XSLT Mapping for Determining Receivers

Unless you reuse the extended receiver determination mapping, you must create an XSLT in the Partner Directory for each scenario. The XSLT mapping carries out the XPath routing conditions to determine the list of receivers. For an example, see [Receiver Determination \(Generic\)](fully-decoupled-pipeline-f8e69f4.md#loiof8e69f43059a44cdb891892f4ff083d8__section_qbb_wyk_31c).

> ### Note:  
> The XSLT mapping is stored as binary. When using the API, you need to encode the XSLT before uploading to the Partner Directory. When you upload the XSLT using the Partner Directory user interface, selecting the content type `xsl` and the encoding `UTF-8` automatically encodes the XSLT.

For the receiver determination XSLT, the object ID is `receiverDetermination`. Let's assume that the encoded XSLT mapping is stored in the variable binary.

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

For each receiver of your scenario, you need to create an XSLT in the Partner Directory that carries out the XPath routing conditions to determine the interfaces. For an example, see [Interface Determination \(Generic\)](fully-decoupled-pipeline-f8e69f4.md#loiof8e69f43059a44cdb891892f4ff083d8__section_drs_wyk_31c).

> ### Note:  
> The XSLT mapping is stored as binary. When using the API, you need to encode the XSLT before uploading to the Partner Directory. When you upload the XSLT using the Partner Directory user interface, selecting the content type `xsl` and the encoding `UTF-8` automatically encodes the XSLT.

For the interface determination XSLT, the object ID is a combination of a constant identifier `interfaceDetermination` and the receiver system name, separated with an underscore "\_". Let's assume that the encoded XSLT mapping is stored in the variable binary.

> ### Note:  
> From version 1.0.6 of the provided standard integration package onwards, the partner ID \(pid\) and the identifier \(Id\) used to upload the interface determination XSLT to the Partner Directory have been changed to overcome the partner ID restrictions. This change is an incompatible change. Hence, you must change your code and update the Partner Directory entries accordingly.

```
POST https://{{apihost}}/api/v1/BinaryParameters
content-type: application/json
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{token}}

{
  "Pid": "{{pid}}",
  "Id": "interfaceDetermination_Receiver_1",
  "ContentType": "xsl",
  "Value": "{{binary}}"
}
```



<a name="loio9ec7d2dce72d423abff80543f11b2091__section_lsh_hkp_hcc"/>

## Special Cases: Bypass Options

In some cases, you can bypass one or more pipeline steps and improve your runtime behavior. You have the following bypass options:

-   Point-to-Point Scenarios
-   Combined receiver and interface determination in a single XSLT
-   Bypass interface determination
-   Bypass receive determination

See also [Pipeline Bypass Options](special-cases-1606af9.md#loio1606af9b55bf4391bea01d2f7ee112af__section_bdm_kc3_hcc).



### Point-to-Point Scenarios

For Point-to-Point scenarios, you can bypass the two pipeline steps receiver determination and interface determination. In this case, you don't need to upload XSLT mappings to determine the list of receivers and receiver interfaces. Instead, create corresponding string parameters in the Partner Directory. See [Pipeline Bypass Options](special-cases-1606af9.md#loio1606af9b55bf4391bea01d2f7ee112af__section_bdm_kc3_hcc).

Define a Partner Directory string parameter with object ID `receiverDetermination` as follows:

```
POST https://{{apihost}}/api/v1/StringParameters 
content-type: application/json 
Authorization: Bearer {{accesstoken}} 
X-CSRF-Token: {{token}} 

{ 
    "Pid": "{{pid}}", 
    "Id": "receiverDetermination", 
    "Value": "Receiver_1" 
} 
```

Additionally, define a Partner Directory string parameter with the object ID as combination of the constant identifier `interfaceDetermination` and the receiver system name, separated with an underscore "\_". As value, enter the `ProcessDirect` endpoint of the scenario-specific integration flow for outbound processing. The following is an example for this definition:

```
POST https://{{apihost}}/api/v1/StringParameters 
content-type: application/json 
Authorization: Bearer {{accesstoken}} 
X-CSRF-Token: {{token}} 

{ 
    "Pid": "{{pid}}", 
    "Id": "interfaceDetermination_Receiver_1", 
    "Value": "/pip/07/scenario1" 
} 
```



### Combined Receiver and Interface Determination in a Single XSLT

In general, you can combine the receiver determination and the interface determination in one single XSLT instead of defining separate XSLTs for the receiver determination and an interface determination for each receiver. This allows you to only upload one single XSLT that carries out the XPath routing conditions to determine the list of receivers and the XPath conditions to determine the list of receiver interfaces. This way, you can bypass the interface determination step.

For the combined receiver and interface determination XSLT, the object ID is `receiverDetermination`, same as for the receiver determination XSLT. Assume that the encoded XSLT mapping is stored in the variable binary.

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



### Bypass Interface Determination

This bypass option is a subset of the combined receiver and interface determination option. It applies to Recipient List scenarios without interface split, that is, scenarios in which each receiver has only a single receiver interface. This way, you can bypass the interface determination step.

The configuration is similar to the combined receiver and interface determination option. You only need to upload a single XSLT that carries out the XPath routing conditions to determine the list of receivers. However, you must define a fixed receiver interface in the XSLT for each receiver.



### Bypass Receiver Determination

For interface split scenarios with only a single receiver, you can bypass the receiver determination step. In this case, you don't need to upload an XSLT mapping to determine the list of receivers. Instead, create a corresponding string parameter in the Partner Directory. However, for the interface determination, you must create an XSLT in the Partner Directory that carries out the XPath routing conditions to determine the interfaces.

Define a Partner Directory string parameter with object ID `receiverDetermination` as follows:

```
POST https://{{apihost}}/api/v1/StringParameters  
content-type: application/json  
Authorization: Bearer {{accesstoken}}  
X-CSRF-Token: {{token}}  

{  
    "Pid": "{{pid}}",  
    "Id": "receiverDetermination",  
    "Value": "Receiver_1"  
}  
```

Additionally, define an interface determination XSLT. When you upload the XSLT, the object ID is a combination of a constant identifier `interfaceDetermination` and the receiver system name, separated by an underscore "\_". Assume that the encoded XSLT mapping is stored in the variable binary.

```
POST https://{{apihost}}/api/v1/BinaryParameters 
content-type: application/json 
Authorization: Bearer {{accesstoken}} 
X-CSRF-Token: {{token}} 

{ 
  "Pid": "{{pid}}", 
  "Id": "interfaceDetermination_Receiver_1", 
  "ContentType": "xsl", 
  "Value": "{{binary}}" 
} 
```

