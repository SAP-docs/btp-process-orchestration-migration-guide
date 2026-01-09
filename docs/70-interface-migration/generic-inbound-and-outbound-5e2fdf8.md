<!-- loio5e2fdf8dfb8e457087ffd39bdd55781b -->

# Generic Inbound and Outbound

For scenarios that use the IDoc or XI protocol, you can simplify the configuration of your scenarios by leveraging generic integration flows for the following:

-   For XI inbound, see [XI Sender Adapter](generic-inbound-and-outbound-5e2fdf8.md#loio5e2fdf8dfb8e457087ffd39bdd55781b__section_vcg_m1f_j1c).
-   For IDoc inbound, see [IDoc Sender Adapter](generic-inbound-and-outbound-5e2fdf8.md#loio5e2fdf8dfb8e457087ffd39bdd55781b__section_tjw_z3f_j1c).
-   For XI outbound, see [XI Receiver Adapter](generic-inbound-and-outbound-5e2fdf8.md#loio5e2fdf8dfb8e457087ffd39bdd55781b__section_kjy_1jf_j1c).
-   For IDoc outbound, see [IDoc Receiver Adapter](generic-inbound-and-outbound-5e2fdf8.md#loio5e2fdf8dfb8e457087ffd39bdd55781b__section_idoc_receiver_adapter).



<a name="loio5e2fdf8dfb8e457087ffd39bdd55781b__section_vcg_m1f_j1c"/>

## XI Sender Adapter

For scenarios in which sender systems connect to Cloud Integration using the XI message protocol, you can use the generic inbound integration flow `Pipeline v2 Generic Step01 - Inbound Processing for XI` from the integration package `Cloud Integration Pipeline - Generic Inbound` to act as the single entry point for your XI proxy inbound scenarios.

> ### Note:  
> The generic XI inbound processing flow supports both asynchronous and synchronous scenarios.

As in the integration flow [Inbound Processing \(Scenario-Specific\)](fully-decoupled-pipeline-f8e69f4.md#loiof8e69f43059a44cdb891892f4ff083d8__section_cfy_myk_31c), you must set the message headers for holding the sender system name and sender interface name. You can derive them from the headers provided by the XI sender adapter.

In a content modifier step, define the headers as follows:


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

Source Type

</th>
<th valign="top">

Source Value

</th>
</tr>
<tr>
<td valign="top">

`SAP_Sender`

</td>
<td valign="top">

Header

</td>
<td valign="top">

`sapsenderservice`

</td>
</tr>
<tr>
<td valign="top">

`SAP_SenderInterface`

</td>
<td valign="top">

Header

</td>
<td valign="top">

`sapinterfacename`

</td>
</tr>
<tr>
<td valign="top">

`SAP_MessageType`

</td>
<td valign="top">

Header

</td>
<td valign="top">

`sapinterfacename`

</td>
</tr>
<tr>
<td valign="top">

`SAP_ApplicationID`

</td>
<td valign="top">

Expression

</td>
<td valign="top">

`${header.SapMessageIdEx.toUpperCase()}`

</td>
</tr>
</table>

The header `SAP_ApplicationID` holds the XI message ID that was passed from the integration engine of the sender system. It allows you to search for a particular message ID in the message monitoring. The ID is converted to upper case to make it easier to track a message sent from the sender system to Cloud Integration.

In the *Delivery Assurance* tab of the XI sender adapter, select `Handled by Integration Flow` for *Quality of Service* to support both asynchronous and synchronous message processing.

For asynchronous messages, put the JMS receiver send step to write the message to the JMS queue within your sequence of flows into an idempotent process call.

In the *Processing* tab of the idempotent process call step, set the idempotent conditions details to the following:

-   *Message ID*: `${header.SapMessageIdEx}`

-   *Skip Process Call for Duplicates*: select the checkbox


The idempotent process uses the exchange property `CamelDuplicateMessage` to identify duplicates. If the property isn't set, the message is sent to the JMS queue. If this succeeds, for all following calls of the idempotent process with the same unique ID, the exchange property `CamelDuplicateMessage` has the value `true`. In this case, the message isn't forwarded to the JMS queue again. Instead, the custom status is set to `DuplicateDiscarded`, which is displayed in the message processing log in the message monitor.

Next, as the outbound JMS queue, configure the queue name of the first JMS queue in the sequence of flows, namely the inbound processing queue. For the fully decoupled pipeline, the default queue name is `PIPQ01`, and for the integrated messaging runtime, the default queue name is `PIPX01`. If you want to overwrite your configuration for a specific scenario, you need to maintain the string parameter `InboundQueue` in the Partner Directory. See [Message Processing Behavior](using-the-partner-directory-in-the-pipeline-concept-9ec7d2d.md#loio9ec7d2dce72d423abff80543f11b2091__section_bxk_wty_31c).

> ### Note:  
> The default inbound processing queue is defined as `PIPX01`, following the recommendation of using the integrated messaging runtime. Before, the default value was `PIPQ01`.

For synchronous content-based router scenarios, send the messages to the synchronous integrated messaging runtime using the ProcessDirect adapter. When you're using synchronous point-to-point scenarios, the pipeline can be bypassed, and the message directly routed to the corresponding scenario-specific outbound flow.



<a name="loio5e2fdf8dfb8e457087ffd39bdd55781b__section_tjw_z3f_j1c"/>

## IDoc Sender Adapter

For scenarios in which sender systems connect to Cloud Integration using the IDoc sender adapter, use the generic inbound flow `Pipeline v2 Generic Step01 - Inbound Processing for Idoc` from the integration package `Cloud Integration Pipeline - Generic Inbound`, acting as one single entry point for your IDoc inbound scenarios.

As in the scenario-specific inbound integration flow, the message headers for holding the sender system name and sender interface name must be set. You can derive them from the IDoc control header.

In a content modifier step, the message headers are defined as follows:


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

Source Type

</th>
<th valign="top">

Source Value

</th>
<th valign="top">

Data Type

</th>
</tr>
<tr>
<td valign="top">

`SAP_Sender` 

</td>
<td valign="top">

XPath

</td>
<td valign="top">

`//EDI_DC40/SNDPRN` 

</td>
<td valign="top">

java.lang.String

</td>
</tr>
<tr>
<td valign="top">

`testMode` 

</td>
<td valign="top">

XPath

</td>
<td valign="top">

`//*:TEST != ''`

</td>
<td valign="top">

java.lang.Boolean

</td>
</tr>
<tr>
<td valign="top">

`SAP_IDoc_EDIDC_MESTYP` 

</td>
<td valign="top">

XPath

</td>
<td valign="top">

`//*:MESTYP`

</td>
<td valign="top">

java.lang.String

</td>
</tr>
<tr>
<td valign="top">

`SAP_IDoc_EDIDC_IDOCTYP` 

</td>
<td valign="top">

XPath

</td>
<td valign="top">

`//*:IDOCTYP`

</td>
<td valign="top">

java.lang.String

</td>
</tr>
<tr>
<td valign="top">

`SAP_IDoc_EDIDC_CIMTYP` 

</td>
<td valign="top">

XPath

</td>
<td valign="top">

`//*:CIMTYP`

</td>
<td valign="top">

java.lang.String

</td>
</tr>
</table>

If you want to run your scenario in test mode, for example, for scenario regression tests, you can set the IDoc control header field `TEST` in the sender system. This action sets the `testMode` header to `true`and passes the header through the sequence of integration flows. You can then use it to define the processing behavior for scenario tests, for example, when sending the message to a mocked receiver instead of the actual receiver.

In a Groovy script, `SAP_SenderInterface` is concatenated as a combination of the previously created headers `SAP_IDoc_EDIDC_MESTYP`, `SAP_IDoc_EDIDC_IDOCTYP`, and `SAP_IDoc_EDIDC_CIMTYP`. The latter is only added if the IDoc control header field `CIMTYP` isn't empty.

The partner ID with which you read the Partner Directory is derived from `SAP_Sender`, `SAP_SenderInterface` and the fixed namespace `urn:sap-com:document:sap:idoc:messages`. It's used to read the scenario-specific retry handling. See [Partner ID](using-the-partner-directory-in-the-pipeline-concept-9ec7d2d.md#loio9ec7d2dce72d423abff80543f11b2091__section_oy4_t1p_hcc).

For improved monitoring of IDoc bulk messages, all IDoc numbers are stored in a custom header property. The leading zeros are removed from the IDoc numbers to make it easier to search for a message in the message monitor. Also, IDoc bulk messages are split using an IDoc Splitter step, unless you've defined the string parameter **KeepBulk** in the Partner Directory. See [Message Processing Behavior](using-the-partner-directory-in-the-pipeline-concept-9ec7d2d.md#loio9ec7d2dce72d423abff80543f11b2091__section_bxk_wty_31c).

> ### Note:  
> You can configure the way IDoc numbers of IDoc bulk messages are displayed in the message processing log in the message monitor. By default, each IDoc number is displayed as an individual header property. If you'd prefer to display all IDoc numbers as array, change the configuration parameter `IDocIndividualHeaderInBulk` of the integration flow `Pipeline v2 Generic Step01 - Inbound Processing for Idoc` to `false`.

Put the JMS receiver send step to write the message to the JMS queue within your sequence of integration flows into an idempotent process call. This way, if the sender resends the same IDoc message, you guarantee exactly once delivery.

In the *Processing* tab of the idempotent process call step, set the idempotent conditions details as follows. The exchange property unique ID is a combination of the sender partner number and the IDoc document number.

-   *Message ID*: `${property.uniqueID}`

-   *Skip Process Call for Duplicates*: leave checkbox empty


The idempotent process uses the exchange property `CamelDuplicateMessage` to identify duplicates. If the property hasn’t been set yet, the message is sent to the JMS queue. If this succeeds, for all subsequent calls of the idempotent process with the same unique ID, the exchange property `CamelDuplicateMessage` has the value `true`. In this case, the message isn't forwarded to the JMS queue again. Instead, the custom status is set to `DuplicateDiscarded`, which is displayed in the message processing log in the message monitor.

> ### Note:  
> For testing purposes, you can disable the duplicate check, which is enabled by default. To do so, change the configuration parameter `CustomXTest_SkipDuplicateCheck` of the generic IDoc inbound flow from `false` to `true`.

As the outbound JMS queue, configure the queue name of the first JMS queue in the sequence of flows, namely the inbound processing queue. For the fully decoupled pipeline, the default queue name is `PIPQ01`, and for the integrated messaging runtime, the default queue name is `PIPX01`. If you want to overwrite your configuration for a specific scenario, maintain the string parameter `InboundQueue` in the Partner Directory. See [Message Processing Behavior](using-the-partner-directory-in-the-pipeline-concept-9ec7d2d.md#loio9ec7d2dce72d423abff80543f11b2091__section_bxk_wty_31c).

> ### Note:  
> The default inbound processing queue is defined as `PIPX01`, following the recommendation of using the integrated messaging runtime. Before, the default value was `PIPQ01`.



<a name="loio5e2fdf8dfb8e457087ffd39bdd55781b__section_kjy_1jf_j1c"/>

## XI Receiver Adapter

For scenarios in which Cloud Integration connects to receiver systems using the XI message protocol, you can use the generic outbound integration flow `Pipeline v2 Generic Step08 - Outbound Processing for XI` from the integration package `Cloud Integration Pipeline - Generic Outbound`. Here, the generic XI outbound flow supports both asynchronous and synchronous communication.

The following options are supported: either use a single generic XI outbound integration flow across all your receiving systems or set up a generic XI outbound integration flow for each receiving system. In both cases, the generic XI outbound integration flow allows you to set up your XI outbound scenarios in a common way including built-in support for guaranteed delivery and error handling.

> ### Note:  
> If you set up a generic XI outbound integration flow for each receiving system, you need to copy the integration package `Cloud Integration Pipeline - Generic Outbound`, which you can find in SAP Integration Suite at *Discover* \> *Integrations*. By providing a corresponding suffix for the copied package and integration flows, you ensure that the copied packages receive the regular updates.

If you use an XI outbound scenario, like for any other scenario, you need to create a scenario-specific outbound processing flow. For this integration flow, use the template `Pipeline v2 Template Step07 - Outbound Processing Point-to-Point to Generic XI Outbound` from the integration package **Cloud Integration Pipeline - Templates**. You can use the template for both synchronous and asynchronous communication. In this flow, you run your mappings and transformation steps, if any, and eventually configure the XI receiver adapter. However, instead of an XI receiver adapter, you need to create a ProcessDirect receiver adapter to pass the message to the generic XI outbound integration flow. The generic XI outbound integration flow then takes care of delivering the message to the actual receiver using the XI protocol.

> ### Note:  
> By default, the ProcessDirect endpoint of the generic XI outbound integration flow equals */generic/step08/xi*. Before deploying the generic flow, change the endpoint to your preferences. If you create multiple generic XI outbound integration flows, ensure to configure a unique endpoint, respectively. Otherwise, deployment fails.

Because we use a generic flow across multiple scenarios, the XI receiver adapter parameters and the XI header attributes are dynamically set during runtime. The following configuration options are supported:

-   Configuring externalized parameters of the generic XI outbound integration flow.
-   Maintaining Partner Directory parameters. For the connectivity-related parameters, maintain the partner ID representing the business system or business system alias, respectively. For the XI service interface and namespace, maintain the partner ID representing the configuration scenario.
-   Maintaining message headers in the scenario-specific outbound processing flow.

You can also combine the configuration options, depending on your specific requirements, instead of using one option for your whole scenario. However, the following hierarchical rules apply:

-   By default, the externalized parameters of the generic XI outbound integration flow are used.
-   You can override the externalized parameters by maintaining the corresponding Partner Directory parameters.
-   At the end, you can override all previously configured parameters by maintaining the corresponding message headers in the scenario-specific flows.



### Configuration Option 1: Externalized Parameters

For the generic XI outbound integration flow, you can configure the following **connection parameters**:


<table>
<tr>
<th valign="top">

Externalized Parameter

</th>
<th valign="top">

Value

</th>
</tr>
<tr>
<td valign="top">

`XI_Address`

</td>
<td valign="top">

XI endpoint of the receiving system, for example, `https://<host name>:<port>/sap/xi/engine?type=receiver&sap-client=<client>` 

</td>
</tr>
<tr>
<td valign="top">

`XI_ProxyType`

</td>
<td valign="top">

`On-Premise` or `Internet`

</td>
</tr>
<tr>
<td valign="top">

`LocationID`

</td>
<td valign="top">

If proxy type is `On-Premise`: Cloud Connector location ID

</td>
</tr>
<tr>
<td valign="top">

`XI_AuthenticationType`

</td>
<td valign="top">

`None`, `Basic`, `ClientCertificate`, or `PrincipalPropagation`

</td>
</tr>
<tr>
<td valign="top">

`CredentialName`

</td>
<td valign="top">

If authentication type is `Basic`: credential alias

</td>
</tr>
<tr>
<td valign="top">

`XI_PrivateKeyAlias`

</td>
<td valign="top">

If authentication type is `ClientCertificate`: Private key alias

</td>
</tr>
</table>

For the generic XI outbound integration flow, you can configure the following **XI header parameters**:


<table>
<tr>
<th valign="top">

Externalized Parameter

</th>
<th valign="top">

Value

</th>
</tr>
<tr>
<td valign="top">

`XI_Sender` 

</td>
<td valign="top">

Sender component name

</td>
</tr>
<tr>
<td valign="top">

`XI_SenderParty` 

</td>
<td valign="top">

Sender party name

</td>
</tr>
<tr>
<td valign="top">

`XI_Receiver` 

</td>
<td valign="top">

Receiver component name

</td>
</tr>
<tr>
<td valign="top">

`XI_ReceiverParty` 

</td>
<td valign="top">

Receiver party name

</td>
</tr>
</table>



### Configuration Option 2: Partner Directory

In the Partner Directory, you can configure the connection parameters of the receiving systems. As a prerequisite for this option, set up your landscape stages. See [Landscape Stages](landscape-stages-05cace1.md).

1.  First, maintain the configuration parameters for the partner ID representing the business system alias. To distinguish between the different stages, you need to add the actual business system name as a suffix to the parameters.

2.  Then, for each business system, configure the following string parameters in the Partner Directory:


    <table>
    <tr>
    <th valign="top">

    String Parameter
    
    </th>
    <th valign="top">

    Value
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    `XIEndpoint_<business system name>`
    
    </td>
    <td valign="top">
    
    XI endpoint of the receiving system, for example, `https://<host name>:<port>/sap/xi/engine?type=receiver&sap-client=<client>`
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `XIProxyType_<business system name>`
    
    </td>
    <td valign="top">
    
    `On-Premise` or `Internet`
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `XICCLocationId_<business system name>`
    
    </td>
    <td valign="top">
    
    If proxy type is `On-Premise`: Cloud Connector location ID
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `XIAuthenticationType_<business system name>`
    
    </td>
    <td valign="top">
    
    `None`, `Basic`, `ClientCertificate`, `PrincipalPropagation`
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `XICredentialName_<business system name>`
    
    </td>
    <td valign="top">
    
    If authentication type is `Basic`: Credential alias
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `XIPrivateKeyAlias_<business system name>`
    
    </td>
    <td valign="top">
    
    If authentication type is `Client Certificate`: Private key alias
    
    </td>
    </tr>
    </table>
    
3.  Finally, maintain the XI integration scenario-related configuration parameters \(`Service Interface` and `Service Interface Namespace`\) in the partner ID representing the configuration scenario:


    <table>
    <tr>
    <th valign="top">

    String Parameter
    
    </th>
    <th valign="top">

    Value
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    `InterfaceNameDetermination_<receiver system alias>` 
    
    </td>
    <td valign="top">
    
    Enter the name of the `Receiver Interface` or `Service Interface` that is part of the XI Identifiers for the receiver in the XI Receiver adapter. This parameter can be helpful in point-to-point scenarios \(bypass option\) when receiver and outbound service are also set as string parameters.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `InterfaceNamespaceDetermination_<service interface name>` 
    
    </td>
    <td valign="top">
    
    Specify the namespace of the service interface used in the XI identifiers for the receiver within the XI Receiver adapter. This parameter is optional since the namespace can also be assigned dynamically using XPath. The suffix refers to the service interface name configured in the previous parameter.
    
    </td>
    </tr>
    </table>
    



### Configuration Option 3: Message Headers

In the scenario-specific outbound processing flow, you can configure both connection and XI header parameters by creating and maintaining message headers in a content modifier flow step.

Most of the XI headers are passed from the generic pipeline flows, such as `SAP_Sender`, `SAP_SenderParty`, `SAP_SenderInterface`, `SAP_Receiver`, `SAP_ReceiverParty`, and `SAP_ReceiverInterface`. The latter is set only if you've maintained the receiver interface in the XSLT for determining the receivers and receiver interfaces, which is optional. Hence, unless you like to override those headers, there's no need to create those headers in the scenario-specific outbound processing flow.

You can create the following connection-related headers and maintain them in the scenario-specific outbound processing flows:


<table>
<tr>
<th valign="top">

Message Header

</th>
<th valign="top">

Value

</th>
</tr>
<tr>
<td valign="top">

`SAP_Receiver_XIEndpoint` 

</td>
<td valign="top">

XI endpoint of the receiving system, for example, `https://<host name>:<port>/sap/xi/engine?type=receiver&sap-client=<client>` 

</td>
</tr>
<tr>
<td valign="top">

`SAP_Receiver_XIProxyType` 

</td>
<td valign="top">

`On-Premise`, `Internet` 

</td>
</tr>
<tr>
<td valign="top">

`SAP_Receiver_XICCLocationId` 

</td>
<td valign="top">

If proxy type is `On-Premise`: Cloud Connector location ID

</td>
</tr>
<tr>
<td valign="top">

`SAP_Receiver_XIAuthenticationType` 

</td>
<td valign="top">

`None`, `Basic`, `ClientCertificate`, `PrincipalPropagation` 

</td>
</tr>
<tr>
<td valign="top">

`SAP_Receiver_XICredentialName` 

</td>
<td valign="top">

If authentication is `Basic`: Credential alias

</td>
</tr>
<tr>
<td valign="top">

`SAP_Receiver_XIPrivateKeyAlias`

</td>
<td valign="top">

If authentication is `Client Certificate`: Private key alias

</td>
</tr>
<tr>
<td valign="top">

`SapQualityOfService`

</td>
<td valign="top">

`ExactlyOnce`, `BestEffort`

</td>
</tr>
</table>

You can configure the following XI header-related headers and maintain them in the scenario-specific outbound processing flows:


<table>
<tr>
<th valign="top">

Message Header

</th>
<th valign="top">

Value

</th>
</tr>
<tr>
<td valign="top">

`SAP_Sender` 

</td>
<td valign="top">

Sender component name

</td>
</tr>
<tr>
<td valign="top">

`SAP_SenderParty` 

</td>
<td valign="top">

Sender party name

</td>
</tr>
<tr>
<td valign="top">

`SAP_Receiver` 

</td>
<td valign="top">

Receiver component name

</td>
</tr>
<tr>
<td valign="top">

`SAP_ReceiverParty` 

</td>
<td valign="top">

Receiver party name

</td>
</tr>
<tr>
<td valign="top">

`SAP_ReceiverInterface` 

</td>
<td valign="top">

Receiver interface name

</td>
</tr>
<tr>
<td valign="top">

`SAP_ReceiverInterfaceNamespace`

</td>
<td valign="top">

Receiver interface namespace

</td>
</tr>
</table>



### Duplicate Handling

Duplicate handling in the XI receiver adapter of the generic XI outbound flow is based on the header **UniqueID**. The header is passed from the generic outbound processing flow and routed through the scenario-specific outbound processing flow to the generic XI outbound flow. By default, the header `UniqueID` equals the message processing log ID \(header `SAP_MessageProcessingLogID`\) of the generic outbound processing flow. If an error happens during the sequence of flows, the generic outbound processing flow handles the retry of the failed message while the message processing log ID for this particular message remains the same.

If you prefer using a functional ID, such as an order ID or an invoice ID, instead of the technical ID, you can override the header `UniqueID` in your scenario-specific outbound processing flow.



### One Global XI Outbound or XI Outbound for Each Receiver System

Depending on whether you use a single generic XI outbound integration flow across all your receiving systems or set up one generic XI outbound integration flow for each receiving system, the configuration can differ.

You can always apply the third configuration option, that is, maintaining headers in the scenario-specific outbound processing flow, because here you can configure all connection and XI header parameters. However, you can end up with a high degree of redundancy.

In any case, you need to create and maintain the message headers `SAP_ReceiverInterface`, `SAP_ReceiverInterfaceNamespace`, and `SapQualityOfService` in the scenario-specific outbound processing flow.

For the connection parameters, the following guidelines apply:

-   If there's a single generic XI outbound integration flow across all scenarios, don't use externalized parameters \(option 1\). Instead, either set up the connection parameters as **message headers \(option 3\)** or as **Partner Directory parameters \(option 2\)**.

-   If there's one generic XI outbound integration flow for each receiving system, configure the connection parameters either as **externalized parameters \(option 1\)** or as **Partner Directory parameters \(option 2\)**.




<a name="loio5e2fdf8dfb8e457087ffd39bdd55781b__section_idoc_receiver_adapter"/>

## IDoc Receiver Adapter

For scenarios in which Cloud Integration connects to receiver systems exchanging IDoc messages, use the generic outbound integration flow `Pipeline v2 Generic Step08 - Outbound Processing for IDoc` from the integration package `Cloud Integration Pipeline - Generic Outbound`.

Both options are supported: either use a single generic IDoc outbound integration flow across all your receiving systems or set up a generic IDoc outbound integration flow for each receiving system. In any case, the generic IDoc outbound integration flow allows you to set up your IDoc outbound scenarios in a common way including built-in support for guaranteed delivery and error handling.

> ### Note:  
> For the latter case, copy the integration package `Cloud Integration Pipeline - Generic Outbound`, which you can find in SAP Integration Suite at *Discover* \> *Integrations*, and provide a corresponding suffix for the copied package and integration flows. This way, you ensure that the copied packages receive the regular updates.

For IDoc outbound scenarios, as for any other scenario, you need to create a scenario-specific outbound processing flow. For this integration flow, use the template `Pipeline v2 Template Step07 - Outbound Processing Point-to-Point to Generic IDoc Outbound` from the integration package **Cloud Integration Pipeline - Templates**. In this flow, you run your mappings and transformation steps, if any, and configure the IDoc receiver adapter. However, instead of an IDoc receiver adapter, you need to create a ProcessDirect receiver adapter to pass the message to the generic XI outbound integration flow. The generic IDoc outbound integration flow then takes care of delivering the message to the actual receiver using the IDoc protocol.

> ### Note:  
> By default, the ProcessDirect endpoint of the generic IDoc outbound integration flow equals `/generic/step08/idoc`. Before deploying the generic flow, change the endpoint to your preference. If you create multiple generic IDoc outbound integration flows, make sure to configure a unique endpoint for each. Otherwise, the deployment fails.

Since we use a generic flow across multiple scenarios, the IDoc receiver adapter parameters and the IDoc control headers are dynamically set during runtime. The following configuration options are supported:

-   Configuring externalized parameters of the generic IDoc outbound integration flow
-   Maintaining Partner Directory parameters. For the connectivity-related parameters, maintain the partner ID representing the business system or business system alias, respectively. For the IDoc control header, maintain the partner ID that represents the configuration scenario.
-   Maintaining message headers in the scenario-specific outbound processing flow
-   Defining the IDoc control header in the message body in the scenario-specific outbound processing flow

You can also combine the configuration options, depending on your requirements, instead of using one option for your whole scenario. However, the following hierarchical rules apply for the connectivity-related parameters:

-   By default, the externalized parameters of the generic IDoc outbound integration flow are used.
-   You can override the externalized parameters by maintaining the corresponding Partner Directory parameters.
-   At the end, you can override all previously configured parameters by maintaining the corresponding message headers in the scenario-specific flows.

For the IDoc control header, the behavior differs slightly. We assume that, by default, the IDoc control header is defined in the message body. If you want to override the IDoc control header, create a message header `SAP_IDoc_EDIDC_overrideControlRecordParameters` in the scenario-specific outbound processing flow to specify which control headers should be overridden. As value, maintain the IDoc control headers as a comma-separated list. If the message header is empty, the IDoc control header isn't overridden. Otherwise, the following rules for overriding the control headers apply:

-   For any control header listed in the message header above, it's firstly checked if any corresponding message header is defined in the scenario-specific flow.
-   If not already overridden, it's checked whether any corresponding Partner Directory parameters are defined.
-   If not already overridden, it's checked whether any externalized parameters of the generic IDoc outbound integration flow are configured.



### Configuration Option 1: Externalized Parameters

For the generic IDoc outbound integration flow, you can configure the following connection parameters:


<table>
<tr>
<th valign="top">

Externalized Parameter

</th>
<th valign="top">

Value

</th>
</tr>
<tr>
<td valign="top">

`IDoc_Address`

</td>
<td valign="top">

IDoc endpoint of the receiving system, for example, `https://<host name>:<port>/sap/bc/idoc_xml?sap-client=<client>` 

</td>
</tr>
<tr>
<td valign="top">

`IDoc_ProxyType`

</td>
<td valign="top">

`On-Premise` or `Internet` 

</td>
</tr>
<tr>
<td valign="top">

`LocationID`

</td>
<td valign="top">

If proxy type is `On-Premise`: Cloud Connector location ID

</td>
</tr>
<tr>
<td valign="top">

`IDoc_AuthenticationType`

</td>
<td valign="top">

`None`, `Basic`, `ClientCertificate`, or `PrincipalPropagation` 

</td>
</tr>
<tr>
<td valign="top">

`IDoc_CredentialName`

</td>
<td valign="top">

If authentication type is `Basic`: Credential alias

</td>
</tr>
<tr>
<td valign="top">

`IDoc_PrivateKeyAlias`

</td>
<td valign="top">

If authentication type is `Client Certificate`: Private key alias

</td>
</tr>
<tr>
<td valign="top">

`IDoc_ContentType`

</td>
<td valign="top">

`Application/x-sap.idoc` or `Text/XML` 

</td>
</tr>
</table>

For the generic IDoc outbound integration flow, you can configure the following IDoc control header parameters:


<table>
<tr>
<th valign="top">

Externalized Parameter

</th>
<th valign="top">

Value

</th>
</tr>
<tr>
<td valign="top">

`Default_SNDPOR`

</td>
<td valign="top">

Sender port

</td>
</tr>
<tr>
<td valign="top">

`Default_SNDPRN`

</td>
<td valign="top">

Sender partner name

</td>
</tr>
<tr>
<td valign="top">

`Default_SNDPRT`

</td>
<td valign="top">

Sender partner type

</td>
</tr>
<tr>
<td valign="top">

`Default_RCVPOR`

</td>
<td valign="top">

Receiver port

</td>
</tr>
<tr>
<td valign="top">

`Default_RCVPRN`

</td>
<td valign="top">

Receiver partner name

</td>
</tr>
<tr>
<td valign="top">

`Default_RCVPRT`

</td>
<td valign="top">

Receiver partner type

</td>
</tr>
<tr>
<td valign="top">

`Default_EDIDC_List_Names`

</td>
<td valign="top">

Specifies the names of the control record fields for which default values can be assigned. The field names must be provided as a comma-separated string, for example, `SNDPFC,RCVPFC`.

</td>
</tr>
<tr>
<td valign="top">

`Default_EDIDC_List_Values`

</td>
<td valign="top">

Specifies the default values to be assigned to the corresponding control record fields. The values must be provided as a comma-separated string, matching the order of the field names, for example, `LF,AG`.

</td>
</tr>
</table>



### Configuration Option 2: Partner Directory

In the Partner Directory, you can configure the connection parameters of the receiving systems and the IDoc control header of the configuration scenarios. As a prerequisite for maintaining the connection parameters, set up your landscape stages. See [Landscape Stages](landscape-stages-05cace1.md).

You maintain the connectivity-related configuration parameters in the partner ID representing the business system alias. To distinguish between the different stages, add the actual business system name as a suffix to the parameters.

For each business system, you can configure the following string parameters in the Partner Directory:


<table>
<tr>
<th valign="top">

String Parameter

</th>
<th valign="top">

Value

</th>
</tr>
<tr>
<td valign="top">

`IDocEndpoint_<business system name>`

</td>
<td valign="top">

IDoc endpoint of the receiving system, for example, `https://<host name>:<port>/sap/bc/idoc_xml?sap-client=<client>` 

</td>
</tr>
<tr>
<td valign="top">

`IDocProxyType_<business system name>`

</td>
<td valign="top">

`On-Premise` or `Internet` 

</td>
</tr>
<tr>
<td valign="top">

`IDocCCLocationId_<business system name>`

</td>
<td valign="top">

If proxy type is `On-Premise`: Cloud Connector location ID

</td>
</tr>
<tr>
<td valign="top">

`IDocAuthenticationType_<business system name>`

</td>
<td valign="top">

`None`, `Basic`, `ClientCertificate`, or `PrincipalPropagation` 

</td>
</tr>
<tr>
<td valign="top">

`IDocCredentialName_<business system name>`

</td>
<td valign="top">

If authentication type is `Basic`: Credential alias

</td>
</tr>
<tr>
<td valign="top">

`IDocPrivateKeyAlias_<business system name>`

</td>
<td valign="top">

If authentication type is `Client Certificate`: Private key alias

</td>
</tr>
<tr>
<td valign="top">

`IDocLogicalSystem_<business system name>`

</td>
<td valign="top">

Logical system

</td>
</tr>
<tr>
<td valign="top">

`IDocContentType_<business system name>`

</td>
<td valign="top">

`Application/x-sap.idoc` or `Text/XML` 

</td>
</tr>
</table>

Maintain the IDoc control header-related configuration parameters in the partner ID representing the configuration scenario. By default, the parameters are defined in the Partner Directory for each receiver interface. For this, you need to add the receiver interface name as a suffix to the parameters.

> ### Note:  
> The receiver interface name for IDoc messages is derived from the IDoc message type `MESTYP`, the IDoc basic type `IDOCTYP`, and the extension type `CIMTYP`. The latter is only added if the corresponding IDoc control header isn’t empty.
> 
> This behavior is defined in the generic IDoc outbound flow as externalized parameter `pidParameterReadSuffixPattern` with value `MESTYP.IDOCTYP.CIMTYP`. If you want to change the default behavior, change the parameter value accordingly.

If you use the default behavior, for each receiver interface, maintain the IDoc control header that should be overridden as string parameter, for example, string parameter ID equaling `RCVPRN_INVOIC.INVOIC02` with value equaling the receiver partner number.

> ### Note:  
> The prerequisite for this behavior is that the IDoc control header is maintained in the message header `SAP_IDoc_EDIDC_overrideControlRecordParameters`, as mentioned previously.



### Configuration Option 3: Message Headers

In the scenario-specific outbound processing flow, you can configure both connection and IDoc control header parameters by creating and maintaining message headers in a content modifier flow step.

In the scenario-specific outbound processing flows, you can create and maintain the following connection-related headers:


<table>
<tr>
<th valign="top">

Message Header

</th>
<th valign="top">

Value

</th>
</tr>
<tr>
<td valign="top">

`SAP_Receiver_IDocEndpoint`

</td>
<td valign="top">

IDoc endpoint of the receiving system, for example, `https://<host name>:<port>/sap/bc/idoc_xml?sap-client=<client>` 

</td>
</tr>
<tr>
<td valign="top">

`SAP_Receiver_IDocProxyType`

</td>
<td valign="top">

`On-Premise` or `Internet` 

</td>
</tr>
<tr>
<td valign="top">

`SAP_Receiver_IDocCCLocationId`

</td>
<td valign="top">

If proxy type is `On-Premise`: Cloud Connector location ID

</td>
</tr>
<tr>
<td valign="top">

`SAP_Receiver_IDocAuthenticationType`

</td>
<td valign="top">

`None`, `Basic`, `ClientCertificate`, or `PrincipalPropagation` 

</td>
</tr>
<tr>
<td valign="top">

`SAP_Receiver_IDocCredentialName`

</td>
<td valign="top">

If authentication type is `Basic`: Credential alias

</td>
</tr>
<tr>
<td valign="top">

`SAP_Receiver_IDocPrivateKeyAlias`

</td>
<td valign="top">

If authentication type is `Client Certificate`: Private key alias

</td>
</tr>
<tr>
<td valign="top">

`SAP_Receiver_IDocContentType`

</td>
<td valign="top">

`Application/x-sap.idoc` or `Text/XML` 

</td>
</tr>
</table>

For each IDoc control header that should be overridden, create a message header with suffix `SAP_IDoc_EDIDC_`, for example, message header name `SAP_IDoc_EDIDC_SNDPRT` with value `LS`.

> ### Note:  
> The prerequisite for this behavior is that the IDoc control header is maintained in the message header `SAP_IDoc_EDIDC_overrideControlRecordParameters`, as mentioned previously.



### Configuration Option 4: IDoc Control Header in Message Body

In the scenario-specific outbound processing flow, you can maintain the IDoc control header directly in the message body. You can do this directly in a content modifier step, using message mapping, an XSLT mapping, or your preferred technology.



### Duplicate Handling

Duplicate handling in the IDoc receiver adapter of the generic IDoc outbound flow is based on the header `UniqueID`. This header is passed from the generic outbound processing flow and routed through the scenario-specific outbound processing flow to the generic IDoc outbound flow. By default, the header `UniqueID` equals the message processing log ID \(header `SAP_MessageProcessingLogID`\) of the generic outbound processing flow. If an error occurs during the sequence of flows, the generic outbound processing flow handles the retry of the failed message while the message processing log ID for this particular message remains the same.

If you prefer using a functional ID, such as an order ID or an invoice ID, instead of the technical ID, you can override the header `UniqueID` in your scenario-specific outbound processing flow.



### Monitoring

For improved monitoring of the processed IDoc messages, custom header properties that display additional information in the message processing log are created. This additional information includes, for example, the IDoc number or all IDoc numbers in case of IDoc bulk messages, the transfer ID, sender partner details, receiver partner details, and information about which control headers were overridden.

> ### Note:  
> You can configure the way IDoc numbers of IDoc bulk messages are displayed in the message processing log in the message monitor. By default, each IDoc number is displayed as individual header property. If you'd prefer to display all IDoc numbers as array, change the configuration parameter `IDocIndividualHeaderInBulk` of the integration flow `Pipeline v2 Generic Step08 - Outbound Processing for IDoc` to `false`.

