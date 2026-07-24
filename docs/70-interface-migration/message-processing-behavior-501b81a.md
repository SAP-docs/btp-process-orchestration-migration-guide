<!-- loio501b81a050ad4f0fb421cdac5581011e -->

# Message Processing Behavior

The following table lists the different required string parameters that are used to dynamically define the message processing behavior. They're read from the Partner Directory using the partner ID \(pid\) as defined in [Partner ID](partner-id-7b226f5.md).


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

`KeepBulk`

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

`CustomXPreEnabled`

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

`CustomXPreEndpoint`

</td>
<td valign="top">

`String`

</td>
<td valign="top">

Required if `CustomXPreEnabled` is maintained

</td>
<td valign="top">

ProcessDirect endpoint of custom exit integration flow, if required

</td>
</tr>
<tr>
<td valign="top">

`PassMessageIdFromE2E`

</td>
<td valign="top">

`Boolean`

</td>
<td valign="top">

Optional, default is **false**

</td>
<td valign="top">

Only relevant for XI to XI scenarios. Set to *true* if the XI message ID from sender should be passed to the XI receiver.

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



<a name="loio501b81a050ad4f0fb421cdac5581011e__section_inbound_conversion"/>

## Inbound Conversion

To determine whether your specific scenario needs an inbound conversion, create a string parameter holding the ProcessDirect endpoint of your scenario-specific inbound conversion flow. This can be defined either scenario-specific or for each sender system.

If you need inbound conversion and you only have one sender for your configuration scenario, create one scenario-specific inbound conversion flow. Then, configure a string parameter in the Partner Directory that points to the ProcessDirect endpoint of the scenario-specific integration flow.

If there are sender wildcard scenarios, that is, scenarios in which the same configuration applies to different sender systems, you have two options. If your inbound conversion is the same for each sender system, create a single scenario-specific inbound conversion flow, which means you only have to maintain one configuration parameter. If the inbound conversion differs depending on the sender systems, create scenario-specific inbound conversion flows for each sender system, which means you can maintain configuration parameters for each sender system.

The partner ID is derived from the sender system name and the sender interface name, either using an alternative partner or a combination of the sender system name and the sender interface name. See [Partner ID](partner-id-7b226f5.md).

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



<a name="loio501b81a050ad4f0fb421cdac5581011e__section_max_jms_retries"/>

## Maximum Number of JMS Retries

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



<a name="loio501b81a050ad4f0fb421cdac5581011e__section_reuse_ext_receiver_det"/>

## Reuse Extended Receiver Determination

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



<a name="loio501b81a050ad4f0fb421cdac5581011e__section_custom_receiver_det"/>

## Custom Receiver Determination

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



<a name="loio501b81a050ad4f0fb421cdac5581011e__section_customer_interface_det"/>

## Custom Interface Determination

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



<a name="loio501b81a050ad4f0fb421cdac5581011e__section_inbound_processing_queue"/>

## Scenario-Specific Inbound Processing Queue

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



<a name="loio501b81a050ad4f0fb421cdac5581011e__section_keep_idoc_bulk"/>

## Keep IDoc Bulk

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



<a name="loio501b81a050ad4f0fb421cdac5581011e__section_custom_preprocessing_exit"/>

## Custom Preprocessing Exit

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



<a name="loio501b81a050ad4f0fb421cdac5581011e__section_pass_message_e2e"/>

## Pass Message ID From End-to-End

For integration scenarios with XI sender adapter and XI receiver adapter, you can pass the XI message from the sender system to the receiver system. This allows you to track the same XI message ID from end to end. To enable this feature for your specific configuration scenario, create a string parameter with the value *true*. This parameter is optional and the default is *false*.

The object ID is `PassMessageIdFromE2E`. In the following example, the parameter is set to `true`.

```
### create string parameter: PassMessageIdFromE2E
POST https://{{apihost}}/api/v1/StringParameters
content-type: application/json
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{token}}

{
    "Pid": "{{pid}}",
    "Id": "PassMessageIdFromE2E",
    "Value": "true"
}
```



<a name="loio501b81a050ad4f0fb421cdac5581011e__section_outbound_queue"/>

## Receiver-Specific Outbound Queue

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

