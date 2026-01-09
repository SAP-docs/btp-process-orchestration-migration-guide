<!-- loioaeb106f049144c71a0b7814a2ffedc3f -->

# Customizing the Pipeline Concept

You can apply the pipeline concept as a template and fit it to your custom needs. For example, implement your own exception handling, or define a different global maximum number of retries.

The pipeline concept package provided on the SAP Business Accelerator Hub supports some extension points that allow you to customize the message processing behavior without having to change the standard generic integration flows. This way, you can ensure that the standard integration content still receives updates. See [Updates for SAP's Integration Packages](https://help.sap.com/docs/integration-suite/sap-integration-suite/updates-for-sap-s-integration-packages).

The following extensions and standard customizations are supported:

-   You can implement your own custom exception handling. See [Custom Exception Handling](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md#loioed9b82cb928049e6990a4d784aa6aac7__section_pm1_ggs_5bc).

-   You can implement your own custom preprocessing. See [Custom Preprocessing Exit](customizing-the-pipeline-concept-aeb106f.md#loioaeb106f049144c71a0b7814a2ffedc3f__section_uqy_gdd_kgc).
-   You can implement your own custom receiver determination instead of performing the routing conditions in an XSLT retrieved from the Partner Directory. See [Custom Receiver Determination](customizing-the-pipeline-concept-aeb106f.md#loioaeb106f049144c71a0b7814a2ffedc3f__section_jqy_xh2_pdc).
-   You can implement your own custom interface determination instead of performing the interface split conditions in an XSLT retrieved from the Partner Directory. See [Custom Interface Determination](customizing-the-pipeline-concept-aeb106f.md#loioaeb106f049144c71a0b7814a2ffedc3f__section_tbp_vh2_pdc).
-   You can configure the message end event type in case messages are stored in a dead letter queue. The default is *Escalated*. See [Standard Retry Handling](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md#loioed9b82cb928049e6990a4d784aa6aac7__section_l3k_qrn_j1c).

-   You can configure a pipeline JMS queue prefix, which simplifies configuring queue names if you create another set of generic integration flows.

-   As all adapter parameters of the generic integration flows have been externalized, you can configure their adapters.

-   You can pass a list of name and value pairs to the generic integration flows to create custom header properties. This way, you can search for message processing logs based on payload data. See [Custom Header Properties](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md#loioed9b82cb928049e6990a4d784aa6aac7__section_c4h_dkz_zcc).

-   You can pass any header starting with the prefix `dc` to the generic integration flows as dynamic configuration parameters. In addition to the payload-based routing conditions, this allows you to support header-based routing conditions.

-   You can customize the options of determining the partner ID. By default, only the recommended option using an alternative partner is supported. For compatibility reasons, you can switch on the fallback option using a combination of sender component and sender interface separated by a tilde. See [Using the Partner Directory in the Pipeline Concept](using-the-partner-directory-in-the-pipeline-concept-9ec7d2d.md).
-   Depending on your requirements and preferences, you can bypass the usage of the Partner Directory. See [Custom Scenario Configuration](customizing-the-pipeline-concept-aeb106f.md#loioaeb106f049144c71a0b7814a2ffedc3f__section_ocx_swp_chc).

> ### Caution:  
> Depending on your needs, you can modify the provided standard package. However, if you modify the standard integration flows, you don't receive any updates SAP provides for the pipeline concept package.

> ### Note:  
> If the message body is not in XML format, you can use header-based routing conditions instead of XPath conditions in the XSLT mapping. Still, the XSLT runtime expects an XML body - otherwise it runs into an error. To avoid a processing error, a dummy XML body is defined right before running the XSLT and the original body is retrieved afterwards.



<a name="loioaeb106f049144c71a0b7814a2ffedc3f__section_jqy_xh2_pdc"/>

## Custom Receiver Determination

As an alternative to the standard receiver determination based on an XSLT from the Partner Directory, you can implement your own custom receiver determination. The generic Receiver Determination integration flow supports a custom exit that you can use to run your own custom logic without changing the delivered generic integration flows. To do so, you must implement a separate scenario-specific integration flow that's called instead of the standard receiver determination.

To enable the custom receiver determination for your scenario, define a Partner Directory entry with object ID `CustomXRDEndpoint` that points to the `ProcessDirect` endpoint of the scenario-specific custom receiver determination flow.

You can either create your custom receiver determination flow from scratch or use the following integration flows provided in the integration package **Cloud Integration Pipeline - Templates** as template:

-   `Pipeline v2 Template Step04 - Custom Receiver Determination`
-   `Pipeline v2 Template Step04 - Custom Receiver and Interface Determination via Extended Receiver Determination`
-   `Pipeline v2 Template Step04 - Custom Receiver and Interface Determination via Exchange Properties`



### Custom Receiver Determination in General

The template `Pipeline v2 Template Step04 - Custom Receiver Determination` contains the schema Receivers as local reference. The generic Receiver Determination integration flow expects an XML message containing the list of receivers \(and eventually the list of receiver interfaces\) in the format of the schema Receivers as response from the custom receiver determination. You can use a transformation program of your choice to create such an XML message. For example, you can create a message mapping or a Groovy script.



### Custom Receiver Determination and Interface Determination using Mapping and Exchange Properties

The template `Pipeline v2 Template Step04 - Custom Receiver and Interface Determination via Extended Receiver Determination` gives you the option to implement a combined custom receiver and interface determination. The custom receiver determination is based on a message mapping resulting in an XML message containing the list of receivers. By maintaining exchange properties and running the Groovy script **customInterfaceDeterminationViaXProperties**, the interfaces are added to the beforehand created XML message.

> ### Note:  
> This option can be used as alternative to the [Reuse Extended Receiver Determination](special-cases-1606af9.md#loio1606af9b55bf4391bea01d2f7ee112af__section_kjy_1jf_j1c) in case you want to migrate an integration scenario on SAP Process Orchestration that already uses the extended receiver determination. Other than the **Reuse Extended Receiver Determination** option, this option results into a combined receiver and interface XML message and hence is also supported in the [integrated messaging runtime](integrated-messaging-runtime-asynchronous-21b45fc.md).

When you use a copy of the template, either create a message mapping from scratch or upload an existing message mapping to the **References** section of the integration flow. Then, assign the message mapping to the **Map to Receivers** message mapping flow step.

For the interface determination, maintain the corresponding exchange properties in the **Define interface conditions** content modifier while adhering to the naming convention described in the following.

For each potential receiver that can be listed in the receivers XML message and each interface condition, create the following exchange properties:

****


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

Type

</th>
<th valign="top">

Value

</th>
<th valign="top">

Example

</th>
</tr>
<tr>
<td valign="top">

`SAP-IFDET-<Receiver name>~IFIndex<Index number>`

</td>
<td valign="top">

XPath

</td>
<td valign="top">

Maintain the XPath condition for the corresponding receiver interface.

</td>
<td valign="top">

`SAP-IFDET-Receiver_1~IFIndex1` with value `/*:Order/Item/ProductId = 'XYZ'`

</td>
</tr>
<tr>
<td valign="top">

`SAP-IFENDPT-<Receiver name>~IFIndex<Index number>`

</td>
<td valign="top">

Constant

</td>
<td valign="top">

Maintain the ProcessDirect endpoint of the corresponding scenario-specific outbound flow.

</td>
<td valign="top">

`SAP-IFENDPT-Receiver_1~IFIndex1` with value `/pip/07/scn1/rcv1/ifidx1`

</td>
</tr>
<tr>
<td valign="top">

`SAP-IFNAME-<Receiver name>~IFIndex<Index number>`

</td>
<td valign="top">

Constant

</td>
<td valign="top">

Optionally, maintain the corresponding interface name.

</td>
<td valign="top">

`SAP-IFNAME-Receiver_1~IFIndex1` with value `PurchaseOrderChange`

</td>
</tr>
</table>

Create the following exchange properties to specify the behavior for the case that the receivers XML message doesn't contain any node and no receiver could be determined. The options are **Ignore**, **Error**, or **Default**.

****


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

Type

</th>
<th valign="top">

Value

</th>
<th valign="top">

Example

</th>
</tr>
<tr>
<td valign="top">

`SAP-NOREC-Type`

</td>
<td valign="top">

Constant

</td>
<td valign="top">

Define the receiver not determined behavior.

</td>
<td valign="top">

Values can be **Ignore**, **Error**, or **Default**

</td>
</tr>
<tr>
<td valign="top">

`SAP-NOREC-Default`

</td>
<td valign="top">

Constant

</td>
<td valign="top">

Maintain the default receiver name, only if **SAP-NOREC-Type** equals **Default**.

</td>
<td valign="top">

**SAP-NOREC-Default** with value **Receiver\_2**

</td>
</tr>
</table>

If the default receiver is not in the list of already maintained receivers, create the following exchange properties for each interface condition:

****


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

Type

</th>
<th valign="top">

Value

</th>
<th valign="top">

Example

</th>
</tr>
<tr>
<td valign="top">

`SAP-IFDET-Default~IFIndex<Index number>`

</td>
<td valign="top">

XPath

</td>
<td valign="top">

Only if default receiver is not in the list of already maintained receivers: Maintain the XPath condition for the corresponding default receiver interface

</td>
<td valign="top">

`SAP-IFDET-Default~IFIndex1` with value `/*:Order/Item/ProductId = 'ABC'`

</td>
</tr>
<tr>
<td valign="top">

`SAP-IFENDPT-Default~IFIndex<Index number>`

</td>
<td valign="top">

Constant

</td>
<td valign="top">

Only if default receiver is not in the list of already maintained receivers: Maintain the ProcessDirect endpoint of the corresponding scenario-specific outbound flow

</td>
<td valign="top">

`SAP-IFENDPT-Default~IFIndex1` with value `/pip/07/scn1/rcv2/ifidx1`

</td>
</tr>
<tr>
<td valign="top">

`SAP-IFNAME-Default~IFIndex<Index number>`

</td>
<td valign="top">

Constant

</td>
<td valign="top">

Only if default receiver is not in the list of already maintained receivers: Maintain the corresponding interface name

</td>
<td valign="top">

`SAP-IFNAME-Default~IFIndex1` with value `PurchaseOrderCreate`

</td>
</tr>
</table>

> ### Note:  
> When you use a namespace in the XPath conditions, ensure to maintain the namespace mapping in the runtime configuration of the integration flow.



### Custom Receiver Determination and Interface Determination using Exchange Properties

The  template `Pipeline v2 Template Step04 - Custom Receiver and Interface Determination via Exchange Properties` gives you the option to implement a combined custom receiver and interface determination by maintaining exchange properties and running two Groovy scripts. The first Groovy script `customReceiverDeterminationViaXProperties` creates an XML message containing the list of receivers based on the corresponding configuration parameters. The second Groovy script `customInterfaceDeterminationViaXProperties` adds the interfaces to the previously created XML message based on the corresponding configuration parameters.

For the receiver and interface determination, maintain the corresponding exchange properties in the **Define receiver and interface conditions** content modifier following the naming convention described in the following.

For each receiver, create the following exchange property:

****


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

Type

</th>
<th valign="top">

Value

</th>
<th valign="top">

Example

</th>
</tr>
<tr>
<td valign="top">

`SAP-DYNREC-<Receiver name>`

</td>
<td valign="top">

XPath

</td>
<td valign="top">

Maintain the XPath condition for the corresponding receiver.

</td>
<td valign="top">

`SAP-DYNREC-Receiver_1` with value `/*:Order/Item/Category = 'Software'`

</td>
</tr>
</table>

For each potential receiver and each interface condition, create the following exchange properties:

****


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

Type

</th>
<th valign="top">

Value

</th>
<th valign="top">

Example

</th>
</tr>
<tr>
<td valign="top">

`SAP-IFDET-<Receiver name>~IFIndex<Index number>`

</td>
<td valign="top">

XPath

</td>
<td valign="top">

Maintain the XPath condition for the corresponding receiver interface.

</td>
<td valign="top">

`SAP-IFDET-Receiver_1~IFIndex1` with value `true()`

</td>
</tr>
<tr>
<td valign="top">

`SAP-IFENDPT-<Receiver name>~IFIndex<Index number>`

</td>
<td valign="top">

Constant

</td>
<td valign="top">

Maintain the ProcessDirect endpoint of the corresponding scenario-specific outbound flow.

</td>
<td valign="top">

`SAP-IFENDPT-Receiver_1~IFIndex1` with value `/pip/07/scn1/rcv1/ifidx1`

</td>
</tr>
<tr>
<td valign="top">

`SAP-IFNAME-<Receiver name>~IFIndex<Index number>`

</td>
<td valign="top">

Constant

</td>
<td valign="top">

Optionally, maintain the corresponding interface name.

</td>
<td valign="top">

`SAP-IFNAME-Receiver_1~IFIndex1` with value `PurchaseOrderChange`

</td>
</tr>
</table>

Create the following exchange properties to specify the behavior if no receiver could be determined. The options are **Ignore**, **Error**, or **Default**.

****


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

Type

</th>
<th valign="top">

Value

</th>
<th valign="top">

Example

</th>
</tr>
<tr>
<td valign="top">

`SAP-NOREC-Type`

</td>
<td valign="top">

Constant

</td>
<td valign="top">

Define the receiver not determined behavior.

</td>
<td valign="top">

Values can be **Ignore**, **Error**, or **Default**

</td>
</tr>
<tr>
<td valign="top">

`SAP-NOREC-Default`

</td>
<td valign="top">

Constant

</td>
<td valign="top">

Only if **SAP-NOREC-Type** equals **Default**, maintain the default receiver name.

</td>
<td valign="top">

`SAP-NOREC-Default` with value `Receiver_2`.

</td>
</tr>
</table>

If the default receiver is not in the list of already maintained receivers, create the following exchange properties for each interface condition:

****


<table>
<tr>
<th valign="top">

Name

</th>
<th valign="top">

Type

</th>
<th valign="top">

Value

</th>
<th valign="top">

Example

</th>
</tr>
<tr>
<td valign="top">

`SAP-IFDET-Default~IFIndex<Index number>`

</td>
<td valign="top">

XPath

</td>
<td valign="top">

Only if default receiver is not in the list of already maintained receivers: Maintain the XPath condition for the corresponding default receiver interface.

</td>
<td valign="top">

`SAP-IFDET-Default~IFIndex1` with value `true()`

</td>
</tr>
<tr>
<td valign="top">

`SAP-IFENDPT-Default~IFIndex<Index number>`

</td>
<td valign="top">

Constant

</td>
<td valign="top">

Only if default receiver is not in the list of already maintained receivers: Maintain the ProcessDirect endpoint of the corresponding scenario-specific outbound flow.

</td>
<td valign="top">

`SAP-IFENDPT-Default~IFIndex1` with value `/pip/07/scn1/rcv2/ifidx1`

</td>
</tr>
<tr>
<td valign="top">

`SAP-IFNAME-Default~IFIndex<Index number>`

</td>
<td valign="top">

Constant

</td>
<td valign="top">

Only if default receiver is not in the list of already maintained receivers: Maintain the corresponding interface name.

</td>
<td valign="top">

`SAP-IFNAME-Default~IFIndex1` with value `PurchaseOrderCreate`

</td>
</tr>
</table>

> ### Note:  
> When you use a namespace in the XPath conditions, make sure to maintain the namespace mapping in the runtime configuration of the integration flow.



<a name="loioaeb106f049144c71a0b7814a2ffedc3f__section_tbp_vh2_pdc"/>

## Custom Interface Determination

As an alternative to the standard interface determination based on an XSLT from the Partner Directory, you can implement your own custom interface determination. The generic Interface Determination integration flow supports a kind of custom exit that you can use to run your own custom logic without changing the delivered generic integration flows. To do so, you must implement a separate integration flow that's called instead of the standard interface determination.

To enable the custom interface determination for your scenario, you need to define a Partner Directory entry with object ID `CustomXIDEndpoint` that points to the `ProcessDirect` endpoint of the scenario-specific custom interface determination flow.

You can either create your custom interface determination flow from scratch or use the provided integration flow `Pipeline Template Step05 - Custom Interface Determination` as template. The template contains the schema Interfaces as local reference. The generic Interface Determination integration flow expects an XML message containing the list of interfaces in the format of the schema Interfaces as response from the custom interface determination. You can use a transformation program of your choice to create such an XML message. For example, you can create a message mapping or a Groovy script.



<a name="loioaeb106f049144c71a0b7814a2ffedc3f__section_uqy_gdd_kgc"/>

## Custom Preprocessing Exit

If you want to embed custom logic at the very beginning of the generic pipeline steps, you can call a custom exit integration flow without having to edit the provided generic flows. To do so, you must implement a separate integration flow that can be called at the very beginning of each generic integration flow. Custom preprocessing is supported globally, which means that the custom exit integration flow is called for all of your integration scenarios, or it can be configured scenario-specific.

You can either create your custom exit flow from scratch or use the provided integration flow `Pipeline v2 Template - Custom Exit` from the integration package **Cloud Integration Pipeline - Templates** as template. For the global setting, you can define a custom exit flow for each pipeline step or one single custom exit flow which is used across all pipeline steps. For the scenario-specific setting, the approach is to implement one integration flow per scenario which is used across all pipeline steps to minimize the configuration effort. For this, the template uses the header `customXPipelineStep` in the router conditions, which is then passed from the generic flows to the custom flow to implement your custom logic depending on the pipeline step.



### Global Setting

To enable custom preprocessing globally, configure each generic integration flow that should call the custom preprocessing flow as follows:

1.  In the integration flow configuration, go to the tab *More* and set the parameter *CustomXPreGlobal\_Enabled* to ***true*** \(the default is ***false***\).
2.  Then, maintain the parameter *CustomXPreGlobal\_Endpoint* that points to the ProcessDirect endpoint of the custom exit integration flow. By default, the value is set to ***/pip/custom/preProcessing/global***. You can keep that value or change it to your preference.
3.  Save your configuration changes.
4.  Redeploy your generic integration flow.



### Scenario-Specific Setting

For scenario-specific configuration, you can define for which pipeline steps the custom exit integration flow should be called. For this, you need to create the corresponding parameters in the Partner Directory. See [Message Processing Behavior](using-the-partner-directory-in-the-pipeline-concept-9ec7d2d.md#loio9ec7d2dce72d423abff80543f11b2091__section_bxk_wty_31c).

For each scenario that should call the custom preprocessing flow, configure the Partner Directory as follows:

1.  Create a string parameter `CustomXPreEnabled` in which you define the list of pipeline steps separated by pipe.

    > ### Example:  
    > If your scenario should run in the integrated messaging runtime, you can enable the custom exit for either the generic XI inbound processing or the generic IDoc inbound processing \(both step 01\), the generic integrated messaging runtime \(step 02\) and the generic outbound processing flow \(step 06\). In this case, set the value of the parameter `CustomXPreEnabled` to ***01|02|06***. If you want to enable the custom exit for all pipeline steps of the fully decoupled pipeline, that's the generic inbound processing flow \(step 02\), the generic receiver determination flow \(step 04\), the generic interface determination flow \(step 05\) and the generic outbound processing flow \(step 06\) including the generic XI and IDoc inbound processing flows. Set the value to ***01|02|04|05|06***.

2.  Create a string parameter `CustomXPreEndpoint`, which points to the ProcessDirect endpoint of the custom exit integration flow.



<a name="loioaeb106f049144c71a0b7814a2ffedc3f__section_ocx_swp_chc"/>

## Custom Scenario Configuration

If you don't want to use the Partner Directory, you can configure most of the parameters defining your configuration scenario as custom parameters in your scenario-specific inbound processing flows. The custom parameters are then passed to the generic pipeline flows and if they exist, the Partner Directory is not called.

Although the Partner Directory is not called, you must still define the header **partnerID** in your scenario-specific inbound processing flow for compatibility reasons. Choose any value. If the header exists, the generic pipeline won't try to map the sender component name and the sender interface name to a partner ID in the Partner Directory. Otherwise, your message fails.

Since the Partner Directory should not be leveraged here, content-based router and recipient list scenarios must implement custom receiver and interface determination. This means that you must call a custom integration flow to determine the receivers and interfaces instead of calling an XSLT from the Partner Directory. In such a scenario, create the following mandatory headers:

-   **partnerID** with any value
-   **customXRDEndpoint** with the value being the ProcessDirect endpoint of the custom receivers and interfaces integration flow

Additionally, you can create the following optional headers based on your requirements:

-   **customXInboundConversionEndpoint** with the value being the ProcessDirect endpoint of the integration flow performing the inbound conversion if any
-   **maxJMSRetries** if you want to define a scenario-specific maximum number of retries
-   **customXPreEnabled** specifying the pipeline steps for which you want to call a custom pre-processing flow, if at all
-   **customXPreEndpoint** with the value being the ProcessDirect endpoint of the custom pre-processing flow, if any

In a Point-to-Point scenario in which the pipeline is bypassed, define the following headers in the scenario-specific inbound processing flows:

-   **partnerID** with any value
-   **SAP\_OutboundProcessingEndpoint** with the value being the ProcessDirect endpoint of the scenario-specific outbound processing flow

> ### Note:  
> Not all scenarios and features are supported here. Since you can't define custom parameters in the generic XI and generic IDoc inbound processing flows, XI inbound and IDoc inbound scenarios require Partner Directory access. Furthermore, tenant staging, receiver-specific queues, and reuse of Extended Receiver Determination are not supported either.

