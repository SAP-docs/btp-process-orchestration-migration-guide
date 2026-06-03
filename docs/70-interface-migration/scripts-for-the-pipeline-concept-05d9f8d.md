<!-- loio05d9f8d85d7945af8d610dca81375b43 -->

# Scripts for the Pipeline Concept

Use the scripts collected in this section to read the Partner Directory and to perform pipeline-specific tasks.

> ### Note:  
> The script collection of the deprecated package [Process Integration Pipeline - Generic Integration Flows & Templates](https://hub.sap.com/package/PIPipelineGenericIntegrationFlows/scriptcollection) has been replaced by local scripts for the generic flows and a new script collection for the template integration flows to give your more flexibility when setting up your pipeline. You can access the local scripts from within the generic flows. Each generic integration flow provided only contains required scripts. The script collection in the templates package only contains the scripts that may be required in the scenario-specific integration flows.

The following table describes the scripts included in the generic integration flows and the script collection, respectively:


<table>
<tr>
<th valign="top">

Script Name

</th>
<th valign="top">

Description

</th>
<th valign="top">

Where Used

</th>
</tr>
<tr>
<td valign="top">

`addCalledByPipelineStep` 

</td>
<td valign="top">

Use this script  to add the pipeline step number to the custom header properties.

</td>
<td valign="top">

This script is provided in the template `Pipeline v2 Template - Custom Exit` as an indication about which pipeline step called the exit.

</td>
</tr>
<tr>
<td valign="top">

`addCustomHeaderProperties` 

</td>
<td valign="top">

Use this script  to add custom header properties to the message processing log so you can search for message logs based on payload data.

</td>
<td valign="top">

This script is called by all generic flows and can also be added in your scenario-specific flows.

</td>
</tr>
<tr>
<td valign="top">

`addPartyForXIInbound` 

</td>
<td valign="top">

Use this script to add the party name to the header SAP\_Sender when the XI header contains a sender party.

</td>
<td valign="top">

This script is called by the integration flow `Pipeline v2 Generic Step01 - Inbound Processing for XI`.

</td>
</tr>
<tr>
<td valign="top">

`attachAdditionalInformation` 

</td>
<td valign="top">

Use this script to add information about the queue names to the message processing log if the message is parked in a dead letter queue. In addition, the log level is set to `DEBUG`.

</td>
<td valign="top">

This script is called by all generic flows as part of the standard error handling.

</td>
</tr>
<tr>
<td valign="top">

`checkWellFormedXML` 

</td>
<td valign="top">

Use this script to check if the message body is in a well-formed XML format.

</td>
<td valign="top">

This script is called by the generic receiver determination flow and by the integrated messaging flows for both asynchronous and synchronous message processing.

</td>
</tr>
<tr>
<td valign="top">

`createHeadersFromSapDynamicConfiguration`

</td>
<td valign="top">

Use this script to convert the exchange properties that were created based on the dynamic XI header of the incoming message to message headers to pass the values to the subsequent pipeline steps.

</td>
<td valign="top">

This script is called by the integration flow `Pipeline v2 Generic Step01 - Inbound Processing for XI`.

</td>
</tr>
<tr>
<td valign="top">

`createSapDynamicConfigurationFromHeaders`

</td>
<td valign="top">

Use this script to convert the dynamic configuration headers passed to the generic XI outbound flow to exchange properties that are in the format that the XI receiver adapter expects to add the corresponding dynamic XI headers to the outgoing XI message.

</td>
<td valign="top">

This script is called by the integration flow `Pipeline v2 Generic Step08 - Outbound Processing for XI`.

</td>
</tr>
<tr>
<td valign="top">

`customInterfaceDeterminationViaXProperties` 

</td>
<td valign="top">

Use this script to implement custom interface determination by maintaining exchange properties. This is an alternative to running an XSLT mapping read from the Partner Directory.

</td>
<td valign="top">

This script is used in the templates `Pipeline v2 Template Step04 - Custom Receiver and Interface Determination via Exchange Properties` and `Pipeline v2 Template Step04 - Custom Receiver and Interface Determination via Extended Receiver Determination`.

</td>
</tr>
<tr>
<td valign="top">

`customReceiverDeterminationViaXProperties` 

</td>
<td valign="top">

Use this script to implement custom receiver determination by maintaining exchange properties. This is an alternative to running an XSLT mapping read from the Partner Directory.

</td>
<td valign="top">

This script is used in the template `Pipeline v2 Template Step04 - Custom Receiver and Interface Determination via Exchange Properties`.

</td>
</tr>
<tr>
<td valign="top">

`determinePartnerID` 

</td>
<td valign="top">

Use this script  to set the header partner ID either based on an alternative partner or as a combination of the sender component and the sender interface.

</td>
<td valign="top">

This script is called by most of the generic inbound flows and by the integrated messaging flows for both asynchronous and synchronous message processing.

</td>
</tr>
<tr>
<td valign="top">

`determinePartnerIDForIDocInbound`

</td>
<td valign="top">

Use this script  for IDoc inbound scenarios to set the header partner ID based on the IDoc control record of the incoming IDoc message.

</td>
<td valign="top">

This script is called by the integration flow `Pipeline v2 Generic Step01 - Inbound Processing for Idoc`.

</td>
</tr>
<tr>
<td valign="top">

`determinePartnerIDForXIInbound`

</td>
<td valign="top">

This script has been replaced by the `determinePartnerID` script.

</td>
<td valign="top">

Not in use

</td>
</tr>
<tr>
<td valign="top">

`displayBulkIDs` 

</td>
<td valign="top">

Use this script  to display all IDoc numbers of an IDoc bulk message in the message monitor.

</td>
<td valign="top">

This script is called by the integration flow `Pipeline v2 Generic Step01 - Inbound Processing for Idoc` flow.

</td>
</tr>
<tr>
<td valign="top">

`logOutboundProcessingEndpoint` 

</td>
<td valign="top">

Use this script to add outbound processing information to the pipeline processing log.

</td>
<td valign="top">

This script is called by the generic interface determination flow and the integrated messaging flows for both asynchronous and synchronous message processing.

</td>
</tr>
<tr>
<td valign="top">

`mapMessageTypeToOperation` 

</td>
<td valign="top">

Use this script to determine the service interface operation based on the message type.

</td>
<td valign="top">

This script has been added to all templates for scenario-specific inbound processing and the template for inbound conversion.

</td>
</tr>
<tr>
<td valign="top">

`mapReceiverAliasToBusinessSystemName`

</td>
<td valign="top">

Use this script to map the alias of the receiver system to the actual receiver business system name.

</td>
<td valign="top">

This script is called by the generic receiver determination flow and the integrated messaging flows for both asynchronous as well as synchronous message processing.

</td>
</tr>
<tr>
<td valign="top">

`mapSenderStageToReceiverStage`

</td>
<td valign="top">

Use this script to read the stage rule from the Partner Directory and to map the sender landscape stage to the receiver landscape stage, if applicable.

</td>
<td valign="top">

This script is called by the integration flows `Pipeline v2 Generic Step02 - Integrated Messaging Runtime Async`, `Pipeline v2 Generic Step02 - Integrated Messaging Runtime Sync` and `Pipeline v2 Generic Step04 - Receiver Determination`.

</td>
</tr>
<tr>
<td valign="top">

`PipelineLogger` 

</td>
<td valign="top">

Use this script to add pipeline processing information to a header passed to the attachAdditionalInformation script.

</td>
<td valign="top">

This script is called within the majority of scripts.

</td>
</tr>
<tr>
<td valign="top">

`readBypassOptionFromPD` 

</td>
<td valign="top">

Use this script  to check if the integration scenario follows the pattern Point-to-Point. If it does, the pipeline steps `receiver determination` and `interface determination` are skipped.

</td>
<td valign="top">

This script is called by the generic inbound processing flow and by the integrated messaging flows for both asynchronous and synchronous message processing.

</td>
</tr>
<tr>
<td valign="top">

`readCustomInterfaceDeterminationFromPD` 

</td>
<td valign="top">

Use this script to check if a custom interface determination flow should be used by reading the corresponding ProcessDirect endpoint from the Partner Directory.

</td>
<td valign="top">

This script is called by the generic interface determination flow and by the integrated messaging flows for both asynchronous and synchronous message processing.

</td>
</tr>
<tr>
<td valign="top">

`readCustomReceiverDeterminationFromPD` 

</td>
<td valign="top">

Use this script to check whether a custom receiver determination flow or an extended receiver determination mapping should be used by reading the corresponding ProcessDirect endpoint from the Partner Directory.

</td>
<td valign="top">

This script is called by the generic receiver determination flow and by the integrated messaging flows for both asynchronous and synchronous message processing.

</td>
</tr>
<tr>
<td valign="top">

`readCustomXFromPD` 

</td>
<td valign="top">

Use this script to check if a custom exit should be called by reading the corresponding string parameters from the Partner Directory

</td>
<td valign="top">

This script is called by all generic integration flows.

</td>
</tr>
<tr>
<td valign="top">

`readInboundConversionFromPD` 

</td>
<td valign="top">

Use this script to check if an inbound conversion is needed by reading the corresponding ProcessDirect endpoint from the Partner Directory.

</td>
<td valign="top">

This script is called by the generic inbound processing flow and by the integrated messaging flow for asynchronous message processing.

</td>
</tr>
<tr>
<td valign="top">

`readInboundQueueFromPD`

</td>
<td valign="top">

Use this script to read the scenario-specific inbound processing queue from the Partner Directory.

</td>
<td valign="top">

This script is called by the integration flows `Pipeline v2 Generic Step01 - Inbound Processing for Idoc` and the `Pipeline v2 Generic Step01 - Inbound Processing for XI`.

</td>
</tr>
<tr>
<td valign="top">

`readKeepBulkSettingFromPD`

</td>
<td valign="top">

Use this script to check if an IDoc bulk message should be kept or split into single IDoc messages \(default\) by reading the corresponding string parameter from the Partner Directory.

</td>
<td valign="top">

This script is called by the integration flow `Pipeline v2 Generic Step01 - Inbound Processing for Idoc`.

</td>
</tr>
<tr>
<td valign="top">

`readReceiverNotDeterminedFromPD` 

</td>
<td valign="top">

Use this script to read the type of receiver-not-determined behavior from the Partner Directory if you're reusing an extended receiver determination mapping.

</td>
<td valign="top">

This script is called by the integration flow `Pipeline v2 Generic Step04 - Receiver Determination`.

</td>
</tr>
<tr>
<td valign="top">

`readReceiverSpecificQueueFromPD` 

</td>
<td valign="top">

Use this script to read the outbound queue name from the Partner Directory if you need a receiver-specific queue.

</td>
<td valign="top">

This script is called by the generic interface determination flow and by the integrated messaging flow for asynchronous message processing.

</td>
</tr>
<tr>
<td valign="top">

`readRetryHandlingFromPD` 

</td>
<td valign="top">

Use this script to read the maximum number of retries from the Partner Directory.

</td>
<td valign="top">

This script is called by the generic inbound processing flow and by the integrated messaging flow for asynchronous message processing.

</td>
</tr>
<tr>
<td valign="top">

`removeLeadingZerosFromApplicationID` 

</td>
<td valign="top">

Use this script to remove the leading zeros from the application ID.

</td>
<td valign="top">

This script is used in the integration flow `Pipeline v2 Generic Step01 - Inbound Processing for Idoc`.

</td>
</tr>
<tr>
<td valign="top">

`setIDocSenderInterface` 

</td>
<td valign="top">

Use this script  to concatenate the sender interface based on the IDoc control headers `MESTYP`, `IDOCTYP` and `CIMTYP`. In addition, the sender interface namespace and the quality of service are set as well.

</td>
<td valign="top">

This script is called by the integration flow `Pipeline v2 Generic Step01 - Inbound Processing for Idoc`.

</td>
</tr>
<tr>
<td valign="top">

`throwException`

</td>
<td valign="top">

Use this script to throw an exception with the provided exception message.

</td>
<td valign="top">

This script is used in the majority of generic flows.

</td>
</tr>
</table>

