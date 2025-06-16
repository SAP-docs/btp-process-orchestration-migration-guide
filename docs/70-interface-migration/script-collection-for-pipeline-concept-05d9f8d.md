<!-- loio05d9f8d85d7945af8d610dca81375b43 -->

# Script Collection for Pipeline Concept

Use the scripts collected in this section to read the Partner Directory.

You can access the full script collection `Pipeline Generic - Script Collection` in the integration package [Process Integration Pipeline - Generic Integration Flows & Templates](https://hub.sap.com/package/PIPipelineGenericIntegrationFlows/scriptcollection) on the SAP Business Accelerator Hub.

The following table describes the scripts included in the script collection:


<table>
<tr>
<th valign="top">

Script Name

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

`addCustomHeaderProperties` 

</td>
<td valign="top">

Use this script  to add custom header properties to the message processing log so you can search for message logs based on payload data.

</td>
</tr>
<tr>
<td valign="top">

`attachAdditionalInformation` 

</td>
<td valign="top">

Use this script to add information about the queue names to the message processing log if the message is parked in a dead letter queue. In addition, the log level is set to `DEBUG`.

</td>
</tr>
<tr>
<td valign="top">

`checkWellFormedXML` 

</td>
<td valign="top">

Use this script to check if the message body is in a well-formed XML format.

</td>
</tr>
<tr>
<td valign="top">

`customInterfaceDetermination` 

</td>
<td valign="top">

Use this script to check if a custom interface determination flow should be used by reading the corresponding ProcessDirect endpoint from the Partner Directory.

</td>
</tr>
<tr>
<td valign="top">

`customReceiverDetermination` 

</td>
<td valign="top">

Use this script to check if either a custom receiver determination flow or an extended receiver determination mapping should be used by reading the corresponding ProcessDirect endpoint from the Partner Directory.

</td>
</tr>
<tr>
<td valign="top">

`determinePartnerID` 

</td>
<td valign="top">

Use this script  to set the header partner ID either based on an alternative partner or as a combination of the sender component and the sender interface.

</td>
</tr>
<tr>
<td valign="top">

`determinePartnerIDForXIInbound`

</td>
<td valign="top">

Use this script for XI inbound scenarios to set the header partner ID, based on an alternative partner defined as a combination of the sender component, the sender interface and the sender interface namespace.

</td>
</tr>
<tr>
<td valign="top">

`displayBulkIDs` 

</td>
<td valign="top">

Use this script  to display all IDoc numbers of an IDoc bulk message in the message monitor.

</td>
</tr>
<tr>
<td valign="top">

`logOutboundProcessingEndpoint` 

</td>
<td valign="top">

Use this script to add outbound processing information to the pipeline processing log.

</td>
</tr>
<tr>
<td valign="top">

`mapMessageTypeToOperation` 

</td>
<td valign="top">

Use this script to determine the service interface operation based on the message type.

</td>
</tr>
<tr>
<td valign="top">

`mapReceiverAliasToBusinessSystemName`

</td>
<td valign="top">

Use this script to map the alias of the receiver system to the actual receiver business system name.

</td>
</tr>
<tr>
<td valign="top">

`PipelineLogger` 

</td>
<td valign="top">

Use this script to add pipeline processing information to a header passed to the attachAdditionalInformation script.

</td>
</tr>
<tr>
<td valign="top">

`readBypassOptionFromPD` 

</td>
<td valign="top">

Use this script  to check if the integration scenario follows the pattern Point-to-Point. If it does, the pipeline steps `receiver determination` and `interface determination` are skipped.

</td>
</tr>
<tr>
<td valign="top">

`readInboundConversionFromPD` 

</td>
<td valign="top">

Use this script to check if an inbound conversion is needed by reading the corresponding ProcessDirect endpoint from the Partner Directory.

</td>
</tr>
<tr>
<td valign="top">

`readInboundQueueFromPD`

</td>
<td valign="top">

Use this script to read the scenario-specific inbound processing queue from the Partner Directory.

</td>
</tr>
<tr>
<td valign="top">

`readReceiverNotDeterminedFromPD` 

</td>
<td valign="top">

Use this script to read the type of receiver-not-determined behavior from the Partner Directory if you're reusing an extended receiver determination mapping.

</td>
</tr>
<tr>
<td valign="top">

`readReceiverSpecificQueueFromPD` 

</td>
<td valign="top">

Use this script to read the outbound queue name from the Partner Directory if you need a receiver-specific queue.

</td>
</tr>
<tr>
<td valign="top">

`readRetryHandlingFromPD` 

</td>
<td valign="top">

Use this script to read the maximum number of retries from the Partner Directory.

</td>
</tr>
<tr>
<td valign="top">

`setIDocSenderInterface` 

</td>
<td valign="top">

Use this script  to concatenate the sender interface based on the IDoc control headers `MESTYP`, `IDOCTYP` and `CIMTYP`.

</td>
</tr>
<tr>
<td valign="top">

`throwException`

</td>
<td valign="top">

Use this script to throw an exception with the provided exception message.

</td>
</tr>
</table>

