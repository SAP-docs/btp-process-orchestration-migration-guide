<!-- loioaeb106f049144c71a0b7814a2ffedc3f -->

# Customizing the Pipeline Concept

You can apply the pipeline concept as a template and fit it to your custom needs. For example, implement your own exception handling, or define a different global maximum number of retries.

The pipeline concept package provided on the SAP Business Accelerator Hub supports some extension points that allow you to customize the message processing behavior without having to change the standard generic integration flows. This way, you can ensure that the standard integration content still receives updates. See [Updates for SAP's Integration Packages](https://help.sap.com/docs/integration-suite/sap-integration-suite/updates-for-sap-s-integration-packages).

The following extensions and standard customizations are supported:

-   You can implement your own custom exception handling. See [Custom Exception Handling](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md#loioed9b82cb928049e6990a4d784aa6aac7__section_pm1_ggs_5bc).

-   You can implement your own custom receiver determination instead of performing the routing conditions in an XSLT retrieved from the Partner Directory. See [Custom Receiver Determination](customizing-the-pipeline-concept-aeb106f.md#loioaeb106f049144c71a0b7814a2ffedc3f__section_jqy_xh2_pdc).
-   You can implement your own custom interface determination instead of performing the interface split conditions in an XSLT retrieved from the Partner Directory. See [Custom Interface Determination](customizing-the-pipeline-concept-aeb106f.md#loioaeb106f049144c71a0b7814a2ffedc3f__section_tbp_vh2_pdc).
-   You can configure the message end event type in case messages are stored in a dead letter queue. The default is *Escalated*. See [Standard Retry Handling](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md#loioed9b82cb928049e6990a4d784aa6aac7__section_l3k_qrn_j1c).

-   You can configure a pipeline JMS queue prefix, which simplifies configuring queue names if you create another set of generic integration flows.

-   As all adapter parameters of the generic integration flows have been externalized, you can configure their adapters.

-   You can pass a list of name and value pairs to the generic integration flows to create custom header properties. This way, you can search for message processing logs based on payload data. See [Custom Header Properties](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md#loioed9b82cb928049e6990a4d784aa6aac7__section_c4h_dkz_zcc).

-   You can pass any header starting with the prefix `dc` to the generic integration flows as dynamic configuration parameters. In addition to the payload-based routing conditions, this allows you to support header-based routing conditions.

-   You can customize the options of determining the partner ID. By default, only the recommended option using an alternative partner is supported. For compatibility reasons, you can switch on the fallback option using a combination of sender component and sender interface separated by a tilde. See [Using the Partner Directory in the Pipeline Concept](using-the-partner-directory-in-the-pipeline-concept-9ec7d2d.md).

> ### Caution:  
> Depending on your needs, you can modify the provided standard package. However, if you modify the standard integration flows, you won't receive any updates SAP provides for the pipeline concept package.

> ### Note:  
> If the message body is not in XML format, you can use header-based routing conditions instead of xpath conditions in the XSLT mapping. Still, the XSLT runtime expects an XML body - otherwise it runs into an error. To avoid a processing error, a dummy XML body is defined right before running the XSLT and the original body is retrieved afterwards.



<a name="loioaeb106f049144c71a0b7814a2ffedc3f__section_jqy_xh2_pdc"/>

## Custom Receiver Determination

As an alternative to the standard receiver determination based on an XSLT from the Partner Directory, you can implement your own custom receiver determination. The generic Receiver Determination integration flow supports a custom exit you can use to run your own custom logic without changing the delivered generic integration flows. To do so, you must implement a separate scenario-specific integration flow that's called instead of the standard receiver determination.

To enable the custom receiver determination for your scenario, define a Partner Directory entry with object ID `CustomXRDEndpoint` that points to the `ProcessDirect` endpoint of the scenario-specific custom receiver determination flow.

You can either create your custom receiver determination flow from scratch or use the provided integration flow `Pipeline Template Step04 - Custom Receiver Determination` as template. The template contains the schema Receivers as local reference. The generic Receiver Determination integration flow expects an XML message containing the list of receivers \(and eventually the list of receiver interfaces\) in the format of the schema Receivers as response from the custom receiver determination. You can use a transformation program of your choice to create such an XML message. For example, you can create a message mapping or a Groovy script.



<a name="loioaeb106f049144c71a0b7814a2ffedc3f__section_tbp_vh2_pdc"/>

## Custom Interface Determination

As an alternative to the standard interface determination based on an XSLT from the Partner Directory, you can implement your own custom interface determination. The generic Interface Determination integration flow supports a kind of custom exit that you can use to run your own custom logic without changing the delivered generic integration flows. To do so, you must implement a separate integration flow that's called instead of the standard interface determination.

To enable the custom interface determination for your scenario, you need to define a Partner Directory entry with object ID `CustomXIDEndpoint` that points to the `ProcessDirect` endpoint of the scenario-specific custom interface determination flow.

You can either create your custom interface determination flow from scratch or use the provided integration flow `Pipeline Template Step05 - Custom Interface Determination` as template. The template contains the schema Interfaces as local reference. The generic Interface Determination integration flow expects an XML message containing the list of interfaces in the format of the schema Interfaces as response from the custom interface determination. You can use a transformation program of your choice to create such an XML message. For example, you can create a message mapping or a Groovy script.

