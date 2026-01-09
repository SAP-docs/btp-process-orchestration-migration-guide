<!-- loiod3f428d2e52e4f4eba5853a22b308cf8 -->

# Pipelines

The pipeline concept works with a fixed sequence of integration flows, the pipeline steps.

You can find the generic integration flows and a set of templates for the scenario-specific integration flows in the following integration packages on the [SAP Business Accelerator Hub](https://help.sap.com/docs/link-disclaimer?site=https%3A%2F%2Fhub.sap.com%2F):

-   [Cloud Integration Pipeline - Generic Inbound](https://hub.sap.com/package/CloudIntegrationPipelineGenericInbound/overview) contains the generic IDoc and XI inbound flows.
-   [Cloud Integration Pipeline - Generic Pipelines](https://hub.sap.com/package/CloudIntegrationPipelineGenericPipelines/overview) contains the main generic pipeline steps.
-   [Cloud Integration Pipeline - Generic Outbound](https://hub.sap.com/package/CloudIntegrationPipelineGenericOutbound/overview) contains the generic outbound processing flow.
-   [Cloud Integration Pipeline - Templates](https://hub.sap.com/package/CloudIntegrationPipelineTemplates/overview) contains all templates for the scenario-specific flows and custom extensions, and a script collection with scripts that help you implement the scenario-specific flows.

> ### Caution:  
> The Cloud Integration pipeline integration packages replace the [Process Integration Pipeline - Generic Integration Flows and Templates](https://hub.sap.com/package/PIPipelineGenericIntegrationFlows/overview) package, which was split into the four packages listed previously. This way, it allows you more flexibility in setting up your different pipelines, sender-specific IDoc and XI inbound flows, receiver-specific IDoc and XI outbound flows, and receiver-specific outbound flows, if required. For the same reason, the script collection for the generic flows was also replaced with local scripts. For the scenario-specific integration flows, a new script collection has been added to the template package. Not all template integration flows require a script: for those that do, the scripts from the new script collection are referenced.
> 
> The previous integration package has been deprecated. All new feature increments will only be shipped with the new integration packages.
> 
> If you've been using the previously provided package, switch to the new packages as soon as possible. To do so, perform the following steps:
> 
> -   **Undeploy** all generic flows from the deprecated package. In the new Cloud Integration packages, the name and IDs of the integration flows have the addition "v2". It's important that the old integration flows and the new integration flows must not be deployed together because they compete on reading from the same JMS queues.
> -   **Configure and deploy** the required generic flows \(depending on which pipeline you use, see the following\) provided by the new Cloud Integration pipeline packages.
> -   If you've used scripts from the old script collection in your scenario-specific flows, replace them with the scripts from the new script collection. As long as you haven't replaced all scripts, it's still recommended to run the old script collection. Once you're done, you can then also **undeploy** the old script collection.

You can deploy the generic integration flows on your tenant as they are, but you can also adapt them to your own needs. You can create the scenario-specific integration flows by copying the templates. In this case, you also need to deploy the script collection provided in the templates package.

> ### Note:  
> The templates aren't complete but function as examples. For example, you must add the end points as they aren't included, especially for templates with ProcessDirect. Copy or replicate the templates to use them in your system with your custom details.

The pipeline concept distinguishes between the following pipelines:

-   **[Fully decoupled pipeline](fully-decoupled-pipeline-f8e69f4.md)**: Separate pipeline steps for inbound processing including inbound conversion, receiver determination, interface determination, and outbound processing including mapping and outbound conversion.
-   **[Integrated messaging runtime - asynchronous](integrated-messaging-runtime-asynchronous-21b45fc.md)**: Combines inbound conversion, receiver determination, and interface determination in one single pipeline step
-   **[Integrated messaging runtime - synchronous](integrated-messaging-runtime-synchronous-0dfede9.md)**: Combines receiver determination and interface determination in one single pipeline step for handling synchronous content-based router scenarios.



<a name="loiod3f428d2e52e4f4eba5853a22b308cf8__section_q3h_ljf_g2c"/>

## When to Use Which Pipeline

The **asynchronous integrated messaging runtime** has been evolved from the fully decoupled pipeline. It combines inbound conversion, receiver determination, and interface determination in a single pipeline step. This way, less tenant resources are needed compared to the fully decoupled pipeline, such as a lower number of JMS queues and only one XSLT mapping to carry out the routing conditions. The reduced number of resources eventually leads to lower maintenance effort and an improved runtime behavior compared to the fully decoupled pipeline. Furthermore, it reduces the number of message processing logs in the message monitor.

An advantage of the **fully decoupled pipeline** is that it separates the pipeline steps, which makes it easier to single out a pipeline step if errors occur. However, this separation comes at the cost of a higher number of processing logs.

The following table compares the two pipelines based on their features:

****


<table>
<tr>
<th valign="top">

Use case/feature

</th>
<th valign="top">

Fully decoupled pipeline

</th>
<th valign="top">

Integrated messaging runtime

</th>
</tr>
<tr>
<td valign="top">

**Combined receiver & interface determination**

</td>
<td valign="top">

yes

</td>
<td valign="top">

yes \(by default\)

</td>
</tr>
<tr>
<td valign="top">

**Header-based routing**

</td>
<td valign="top">

yes

</td>
<td valign="top">

yes

</td>
</tr>
<tr>
<td valign="top">

**Extended receiver determination**

</td>
<td valign="top">

yes

</td>
<td valign="top">

yes \(using custom receiver determination\)

</td>
</tr>
<tr>
<td valign="top">

**Custom receiver determination**

</td>
<td valign="top">

yes

</td>
<td valign="top">

yes \(combined only\)

</td>
</tr>
<tr>
<td valign="top">

**Custom interface determination**

</td>
<td valign="top">

yes

</td>
<td valign="top">

No \(see [When to Use Which Pipeline](pipelines-d3f428d.md#loiod3f428d2e52e4f4eba5853a22b308cf8__section_q3h_ljf_g2c)\)

</td>
</tr>
<tr>
<td valign="top">

**Point-to-point bypass option**

</td>
<td valign="top">

yes

</td>
<td valign="top">

yes

</td>
</tr>
<tr>
<td valign="top">

**Bypassing receiver determination**

</td>
<td valign="top">

yes

</td>
<td valign="top">

no

</td>
</tr>
<tr>
<td valign="top">

**Bypassing interface determination**

</td>
<td valign="top">

yes

</td>
<td valign="top">

yes \(by default\)

</td>
</tr>
<tr>
<td valign="top">

**Custom error handling**

</td>
<td valign="top">

yes

</td>
<td valign="top">

yes

</td>
</tr>
<tr>
<td valign="top">

**Receiver-specific outbound**

</td>
<td valign="top">

yes

</td>
<td valign="top">

yes

</td>
</tr>
<tr>
<td valign="top">

**Sender wildcard**

</td>
<td valign="top">

yes

</td>
<td valign="top">

yes

</td>
</tr>
</table>

-   **[Fully Decoupled Pipeline](fully-decoupled-pipeline-f8e69f4.md "The fully decoupled pipeline consists of separate pipeline steps for the inbound
		processing, the receiver determination, the interface determination, and the outbound
		processing.")**  
The fully decoupled pipeline consists of separate pipeline steps for the inbound processing, the receiver determination, the interface determination, and the outbound processing.
-   **[Integrated Messaging Runtime \(Asynchronous\)](integrated-messaging-runtime-asynchronous-21b45fc.md "The asynchronous integrated messaging runtime combines inbound conversion, receiver
		determination, and interface determination in one single pipeline step.")**  
The asynchronous integrated messaging runtime combines inbound conversion, receiver determination, and interface determination in one single pipeline step.
-   **[Integrated Messaging Runtime \(Synchronous\)](integrated-messaging-runtime-synchronous-0dfede9.md "The synchronous integrated messaging runtime is used for handling synchronous
		content-based router scenarios. Unlike the asynchronous messaging, the synchronous pipeline
		doesn't use JMS queues, but instead connects the pipeline steps using the ProcessDirect
		adapter, which is synchronous by nature.")**  
The synchronous integrated messaging runtime is used for handling synchronous content-based router scenarios. Unlike the asynchronous messaging, the synchronous pipeline doesn't use JMS queues, but instead connects the pipeline steps using the ProcessDirect adapter, which is synchronous by nature.
-   **[Generic Inbound and Outbound](generic-inbound-and-outbound-5e2fdf8.md "For scenarios that use the IDoc or XI protocol, you can simplify the configuration of
		your scenarios by leveraging generic integration flows for the following:")**  
For scenarios that use the IDoc or XI protocol, you can simplify the configuration of your scenarios by leveraging generic integration flows for the following:

**Related Information**  


[Fully Decoupled Pipeline](fully-decoupled-pipeline-f8e69f4.md "The fully decoupled pipeline consists of separate pipeline steps for the inbound processing, the receiver determination, the interface determination, and the outbound processing.")

[Integrated Messaging Runtime \(Asynchronous\)](integrated-messaging-runtime-asynchronous-21b45fc.md "The asynchronous integrated messaging runtime combines inbound conversion, receiver determination, and interface determination in one single pipeline step.")

[Integrated Messaging Runtime \(Synchronous\)](integrated-messaging-runtime-synchronous-0dfede9.md "The synchronous integrated messaging runtime is used for handling synchronous content-based router scenarios. Unlike the asynchronous messaging, the synchronous pipeline doesn't use JMS queues, but instead connects the pipeline steps using the ProcessDirect adapter, which is synchronous by nature.")

