<!-- loioe402f4a382cb4088a16ef715edc7f956 -->

# Adapter Modules

Learn about the differences between adapter modules in SAP Process Orchestration and in Cloud Integration, and how you can redesign the adapter modules.



In SAP Process Orchestration, you can add a standard or custom adapter module while you're defining the properties of your communication channel. This allows you to perform different transformations like zip and encrypt the message, or change and remove the namespace in the XML. Although the same concept doesn't apply to adapter modules in Cloud Integration, you can transform the message using the standard integration flow steps or creating a JavaScript or Groovy script. The following table displays some strategies that can be used to redesign these adapter modules:


<table>
<tr>
<th valign="top">

SAP Process Orchestration



</th>
<th valign="top">

Description



</th>
<th valign="top">

Reimplementation strategy



</th>
</tr>
<tr>
<td valign="top">

AF\_Modules/PayloadSwapBean



</td>
<td valign="top">

You use this module to replace the application payload of the XI message that contains the business data with another payload that is appended to the XI message as an additional attachment.



</td>
<td valign="top">

This module is normally used while sending a single attachment as the application payload with Mail adapter.

Cloud Integration offers multiple options to handle this:

-   map properties as attachments directly in the Mail adapter by default

-   use Groovy script to create attachments in a step before Mail call

-   read attachments and set them as main payload after sender mail channel




</td>
</tr>
<tr>
<td valign="top">

AF\_Modules/StrictXml2PlainBean



</td>
<td valign="top">

You use this module to convert an XML document that is in the main payload of the XI message to text format.



</td>
<td valign="top">

In Cloud Integration, you have different ways to convert your XML document to text format. The most common way is to use the conversion steps available \(e.g., XML to CSV, XML to EDI, XML to JSON\). You can also use Groovy script to convert the XML message as you want in a step before the adapter call.



</td>
</tr>
<tr>
<td valign="top">

AF\_Modules/XMLAnonymizerBean



</td>
<td valign="top">

You use this module to anonymize XML elements and attributes by removing namespaces or namespace prefixes from the XML document of the main payload.



</td>
<td valign="top">

In Cloud Integration, you can use an XSLT in the step before the adapter call to change/remove the namespaces or prefixes.

You can also use Groovy script to achieve it.



</td>
</tr>
<tr>
<td valign="top">

SAP\_XI\_IDOC/IDOCXmlToFlatConvertor



</td>
<td valign="top">

You can use this module to convert IDoc XML to IDoc Flat format. If you add this module to the module chain, then it converts the data in the XI message payload from IDoc XML to IDoc Flat format. For example, you can add this module to the module chain of a receiver file adapter and create an IDoc Flat file.



</td>
<td valign="top">

In Cloud Integration, you can use the standard XML to CSV converter to achieve it.



</td>
</tr>
<tr>
<td valign="top">

SAP\_XI\_IDOC/IDOCFlatToXmlConvertor



</td>
<td valign="top">

You can use this module to convert the data in the XI message payload from IDoc Flat format to XML format. For example, you can add this module in the module chain of a sender file adapter and create IDoc XML from IDoc Flat format.



</td>
<td valign="top">

In Cloud Integration, you can use an external library or develop a custom Groovy/Javascript script to perform this conversion.



</td>
</tr>
<tr>
<td valign="top">

AF\_Modules/PayloadZipBean



</td>
<td valign="top">

You use this module to compress one or more payloads or extract payloads from a compressed file.



</td>
<td valign="top">

In Cloud Integration, you can use the standard Encoder and Decoder steps to compress or extract payloads in ZIP, GZIP, Base64, or MIME.



</td>
</tr>
<tr>
<td valign="top">

AF\_Modules/DynamicConfigurationBean



</td>
<td valign="top">

You use this module to edit the message header for adapter-specific message attributes. You can add attributes to the header or delete attributes from the header.



</td>
<td valign="top">

In Cloud Integration, you don’t have the same concept of adapter-specific attributes but you can use external parameters or runtime parameters \(e.g., $\{property.queryOptions\}\) while defining dynamic attributes in your adapter.

For more information about external parameters, see the blog [Externalizing parameters using SAP Cloud Platform Integration's Web Application](https://blogs.sap.com/2017/06/20/externalizing-parameters-using-sap-cloud-platform-integrations-web-application/).



</td>
</tr>
<tr>
<td valign="top">

localejbs/ArchiverModuleBean



</td>
<td valign="top">

You use this module for archiving messages from the sender and receiver channels.



</td>
<td valign="top">

In Cloud Integration, you can either use the standard archiving feature \(see [Configuring the Communication Channel with Archiver Module](https://help.sap.com/docs/SAP_PROCESS_INTEGRATION,_BUSINESS-TO-BUSINESS_ADD-ON/22e34f550ba84f20b35b7652ba94ef9c/ce5c9a811c25452681888ddb139b2702.html)\) or external logging \(see [Archiver Module](adapter-modules-e402f4a.md#loioe402f4a382cb4088a16ef715edc7f956__section_pzy_yfv_ryb)\).



</td>
</tr>
</table>

For more information on the standard adapter modules, see [Adding Modules to the Module Processor](https://help.sap.com/docs/SAP_NETWEAVER_750/2462a9a468b1491b91fda1923d23f667/cd5af7c0c994e24fb0d0088443513de2.html).



<a name="loioe402f4a382cb4088a16ef715edc7f956__section_pzy_yfv_ryb"/>

## Archiver Module

The archiver module `localejbs/ArchiverModuleBean` of SAP Process Orchestration contains the parameters `archiveBaseDir`, `archiveFile`, and `removeErroneous`. The following table describes the parameters further:


<table>
<tr>
<th valign="top">

Parameter Name



</th>
<th valign="top">

Description



</th>
</tr>
<tr>
<td valign="top">

`archiveBaseDir` 



</td>
<td valign="top">

The parameter archives messages to a base directory on the SAP Process Integration server.



</td>
</tr>
<tr>
<td valign="top">

`archiveFile` 



</td>
<td valign="top">

The parameter archives messages to a directory on the SAP Process Integration server and describes the file name of the archived files.



</td>
</tr>
<tr>
<td valign="top">

`removeErroneous` 



</td>
<td valign="top">

When set to true, the parameter removes the archived files created by a faulty archiver module or archive mapping. If the `remove erroneous` flag is set to false, the faulty combinations are ignored, and the files are archived for all combinations.



</td>
</tr>
</table>



### Migration of Archiver Module to Cloud Integration

To migrate archiving functionality provided by the archiver module on SAP Process Orchestration to Cloud Integration and archive message processing logs \(MPLs\) of integration flows running on Cloud Integration, SAP recommends using the data archiving feature provided out-of-the box on Cloud Integration instances running in Cloud Foundry environment.

This solution requires you to use an external Content Management System \(CMS\). The archiving system can be from any third party if it supports the CMIS API standard version 1.1. To configure this feature, see [Archiving Data, Cloud Foundry Environment](https://help.sap.com/docs/cloud-integration/sap-cloud-integration/archiving-data-cloud-foundry-environment).



### External Logging Using Splunk Cloud

The external logging feature enables you to send message processing logs to an external system, independent of available database storage. Major use cases for the external logging feature include integration into existing monitoring solutions \(such as Splunk\) or the consolidation of logs from multiple tenants. In this case, you must take care of archiving log entries in the external logging system. For example, Splunk provides an integrated archiving feature where log entries are stored on Amazon S3.

To configure external logging for Cloud Integration with Splunk, see [External Logging](https://help.sap.com/docs/cloud-integration/sap-cloud-integration/external-logging) or the blog post [SAP Integration Suite – External logging to Splunk](https://blogs.sap.com/2023/06/23/sap-integration-suite-external-logging-to-splunk/).

> ### Note:  
> SAP strongly discourages from using log attachments when transitioning from the `ArchiverModuleBean` in SAP Process Orchestration to Cloud Integration \(see [Create a Script Step to Log the Payload](https://help.sap.com/docs/cloud-integration/sap-cloud-integration/create-script-step-to-log-payload)\).
> 
> Log attachments don’t qualify as a comprehensive archiving solution as the data is stored on Cloud Integration's internal database for 30 days, after which it's deleted permanently. Incorporating log attachments in this context can also cause a performance issue by burdening the allocated database storage within your Cloud Integration instance with an excessive influx of MPL entries.

