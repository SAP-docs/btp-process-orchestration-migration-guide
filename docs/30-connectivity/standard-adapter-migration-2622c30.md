<!-- loio2622c30ed8374702937d74a5f576032e -->

# Standard Adapter Migration

SAP Process Orchestration provides many adapter types as standard. Depending on the adapter type, an equivalent may be available in Cloud Integration, or an alternative may need to be used.

For detailed documentation of the adapters in Cloud Integration, see [Configure Adapter in Communication Channels](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/1f066330e8314324bf3ebe3b6adc21b2.html).

> ### Restriction:  
> Some adapters mentioned on this site are planned for the future and are subject to change. For more information on new features and future releases, access the [Road Map Explorer](https://roadmaps.sap.com/board?PRODUCT=73554900100800003241&range=CURRENT-LAST#Q2%202026) and the [What's New section](https://help.sap.com/whats-new/5793247a5d5741beb0decc5b7dee1160) of SAP Integration Suite.



<a name="loio2622c30ed8374702937d74a5f576032e__section_mkf_j3k_mqb"/>

## Standard Sender Adapter Types


<table>
<tr>
<th valign="top">

SAP Process Orchestration

</th>
<th valign="top">

Cloud Integration

</th>
<th valign="top">

Restrictions/Alternatives

</th>
</tr>
<tr>
<td valign="top">

AS2

</td>
<td valign="top">

AS2, AS4

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

EDISeparator

</td>
<td valign="top">

Available through AS2, AS4, or SFTP adapter

</td>
<td valign="top">

Alternative – Possible use of AS2/AS4/SFTP adapters with EDI Splitter step or EDI Validator step in integration flow.

</td>
</tr>
<tr>
<td valign="top">

File

</td>
<td valign="top">

Available through FTP or SFTP adapter

</td>
<td valign="top">

Alternative – Possible use of FTP or SFTP adapters.

File Content Conversion can be performed in standard step CSV to XML or using a script step.

Alternatively, message conversion can be implemented using a script step. For more advanced or reusable transformations \(for example, CSV ↔ XML, plain text, JSON\), consider using the [Message Transformation Utilities](https://api.sap.com/package/com.sap.integration.cloud.utilities.MessageTransformations/integrationflow) package available on the SAP Business Accelerator Hub.

</td>
</tr>
<tr>
<td valign="top">

HTTP\_AAE

</td>
<td valign="top">

HTTPS

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

IDoc\_AAE

</td>
<td valign="top">

IDoc

</td>
<td valign="top">

Cloud Integration supports IDoc in HTTP protocol, which means that the traditional IDoc with packing \(using RFC\) can't be used.

</td>
</tr>
<tr>
<td valign="top">

JDBC

</td>
<td valign="top">

Planned for future

</td>
<td valign="top">

Alternative – Use timer event along with JDBC receiver adapter to achieve the same JDBC polling mechanism. Note that transaction handling is limited. For more information, see [Known Limitations of Migration Tooling](https://help.sap.com/docs/integration-suite/sap-integration-suite/known-limitations?version=CLOUD).

</td>
</tr>
<tr>
<td valign="top">

JMS

</td>
<td valign="top">

AMQP or IBM MQ

</td>
<td valign="top">

Although Cloud Integration supports the JMS adapter, it can only be used internally and not to external JMS servers. For this scenario, the AMQP adapter should be used instead.

IBM MQ - The IBM MQ adapter enables seamless and efficient integration with IBM MQ systems. It is available for Standard service plans and above of SAP Integration Suite

For more information on mapping and configuring JMS \(IBM MQ\) adapters, see [Mapping SAP Process Orchestration JMS \(IBM MQ\) Adapter to SAP Integration Suite IBM MQ Adapter](https://community.sap.com/t5/integration-blog-posts/mapping-sap-process-orchestration-jms-ibm-mq-adapter-to-sap-integration/ba-p/14347177)

</td>
</tr>
<tr>
<td valign="top">

Mail

</td>
<td valign="top">

Mail

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

Marketplace

</td>
<td valign="top">

Available through HTTP adapter

</td>
<td valign="top">

Alternative – Possible use of the HTTP adapter with implementation of XSLT to convert from MML and XML or JSON.

</td>
</tr>
<tr>
<td valign="top">

OData

</td>
<td valign="top">

OData

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

OFTP \(Odette FTP\)

</td>
<td valign="top">

Available through external application

</td>
<td valign="top">

Alternative – Possible use of an external application to make a bridge between HTTP requests and OFTP.

</td>
</tr>
<tr>
<td valign="top">

REST

</td>
<td valign="top">

RESTful communication is currently handled using the HTTP adapter

</td>
<td valign="top">

Alternative – Use integration flow steps to handle HTTP verbs and decomposition of URIs.

</td>
</tr>
<tr>
<td valign="top">

RFC

</td>
<td valign="top">

Available for Edge Integration Cell

</td>
<td valign="top">

Alternative – Implement as a Web service in Cloud Integration and build an outbound SOAP proxy in your ABAP system to replace the RFC call.

</td>
</tr>
<tr>
<td valign="top">

SFSF

</td>
<td valign="top">

SuccessFactors

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

SFTP

</td>
<td valign="top">

SFTP

</td>
<td valign="top">

Limited support for advanced file selection.

</td>
</tr>
<tr>
<td valign="top">

SOAP

</td>
<td valign="top">

SOAP

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

SOAP-XI

</td>
<td valign="top">

XI

</td>
<td valign="top">

The runtime and generation of XI proxies in SAP S/4HANA differ from those in Cloud Integration. See [Migrating Proxy Interfaces](../70-interface-migration/migrating-proxy-interfaces-dfaee7b.md).

</td>
</tr>
<tr>
<td valign="top">

WS\_AAE

</td>
<td valign="top">

Implemented through SOAP adapter

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

X400

</td>
<td valign="top">

Planned for future

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

Other adapters:

BC, CIDX, Ebics, RNIF \(RosettaNet Implementation Framework\), RNIF11

</td>
<td valign="top">

Planned for future

</td>
<td valign="top">

 

</td>
</tr>
</table>



<a name="loio2622c30ed8374702937d74a5f576032e__section_f43_j3k_mqb"/>

## Standard Receiver Adapter Types


<table>
<tr>
<th valign="top">

SAP Process Orchestration

</th>
<th valign="top">

Cloud Integration

</th>
<th valign="top">

Restrictions/Alternatives

</th>
</tr>
<tr>
<td valign="top">

AS2

</td>
<td valign="top">

AS2, AS4

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

EDISeparator

</td>
<td valign="top">

Available through AS2, AS4, or SFTP adapter

</td>
<td valign="top">

Alternative – Possible use of AS2/AS4/SFTP adapters with EDI Splitter step or EDI Validator step in integration flow.

</td>
</tr>
<tr>
<td valign="top">

File

</td>
<td valign="top">

Available through FTP or SFTP adapter

</td>
<td valign="top">

Alternative – Possible use of FTP or SFTP adapters.

File Content Conversion can be configured in the adapter \(for example, FTP/SFTP sender\) for CSV to XML transformation.

Alternatively, message conversion can be implemented using a script step.

For more advanced or reusable transformations \(for example, CSV ↔ XML, plain text, JSON\), consider using the [Message Transformation Utilities](https://api.sap.com/package/com.sap.integration.cloud.utilities.MessageTransformations/integrationflow) package available on the SAP Business Accelerator Hub.

</td>
</tr>
<tr>
<td valign="top">

HTTP\_AAE

</td>
<td valign="top">

HTTP

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

IDoc\_AAE

</td>
<td valign="top">

IDoc

</td>
<td valign="top">

Cloud Integration supports IDoc in HTTP protocol, which means that the traditional IDoc with packing \(using RFC\) can't be used.

</td>
</tr>
<tr>
<td valign="top">

JDBC

</td>
<td valign="top">

JDBC

</td>
<td valign="top">

Some limitations to which database vendors are currently supported.

</td>
</tr>
<tr>
<td valign="top">

JMS

</td>
<td valign="top">

AMQP or IBM MQ

</td>
<td valign="top">

Although Cloud Integration supports the JMS adapter, it can only be used internally and not to external JMS servers. For this scenario, the AMQP adapter should be used instead.

The IBM MQ adapter enables seamless and efficient integration with IBM MQ systems. It's available for standard service plans and above of SAP Integration Suite

</td>
</tr>
<tr>
<td valign="top">

Mail

</td>
<td valign="top">

Mail

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

Marketplace

</td>
<td valign="top">

Available through HTTP adapter

</td>
<td valign="top">

Alternative – Possible use of the HTTP adapter with implementation of XSLT to convert from MML and XML or JSON.

</td>
</tr>
<tr>
<td valign="top">

OData

</td>
<td valign="top">

OData

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

REST

</td>
<td valign="top">

RESTful communication is currently handled using the HTTP adapter

</td>
<td valign="top">

Alternative – Use integration flow steps to handle HTTP verbs and decomposition of URIs.

</td>
</tr>
<tr>
<td valign="top">

RFC

</td>
<td valign="top">

RFC

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

SFSF

</td>
<td valign="top">

SuccessFactors

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

SFTP

</td>
<td valign="top">

SFTP

</td>
<td valign="top">

Limited support for advanced file selection

</td>
</tr>
<tr>
<td valign="top">

SOAP

</td>
<td valign="top">

SOAP

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

SOAP-XI

</td>
<td valign="top">

XI

</td>
<td valign="top">

The runtime and generation of XI proxies in SAP S/4HANA differ from those in Cloud Integration. See [Migrating Proxy Interfaces](../70-interface-migration/migrating-proxy-interfaces-dfaee7b.md).

</td>
</tr>
<tr>
<td valign="top">

WS\_AAE

</td>
<td valign="top">

Implemented through SOAP adapter

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

X400

</td>
<td valign="top">

Planned for future

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

Other adapters:

BC, CIDX, Ebics, OFTP \(Odette FTP\), RNIF \(RosettaNet Implementation Framework\), RNIF11

</td>
<td valign="top">

Planned for future

</td>
<td valign="top">

 

</td>
</tr>
</table>

