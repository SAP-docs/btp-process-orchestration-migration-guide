<!-- loio2622c30ed8374702937d74a5f576032e -->

# Standard Adapter Migration

SAP Process Orchestration provides many adapter types as standard. Depending on the adapter type, an equivalent may be available in Cloud Integration, or an alternative may need to be used.

For detailed documentation of the adapters in Cloud Integration, see [Configure Adapter in Communication Channels](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/1f066330e8314324bf3ebe3b6adc21b2.html).

> ### Restriction:  
> Some adapters mentioned on this site are planned for the future and are subject to change. For more information on new features and future releases, access the [Road Map Explorer](http://help.sap.com/disclaimer?site=https://roadmaps.sap.com/board?CB=901B0ED1A0641ED8B4D1230C6387E0DB&range=CURRENT-LAST) and the [What's New section](https://help.sap.com/doc/7ac9748e20cf453a94efda779542d34e/sap.cp.integration.suite/en-US/c10c21cd7c684f0885fa8b5db2982284.html) of SAP Integration Suite.



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

Cloud Integration supports IDoc in HTTP protocol, which means that the traditional IDoc with packing \(via RFC\) can't be used.

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

Alternative – Use timer event along with JDBC receiver adapter to achieve the same JDBC polling mechanism.

</td>
</tr>
<tr>
<td valign="top">

JMS

</td>
<td valign="top">

AMQP

</td>
<td valign="top">

Although Cloud Integration supports the JMS adapter, it can only be used internally and not to external JMS servers. For this scenario, the AMQP adapter should be used instead.

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

SAP is working on supporting multiple cloud and on-premise database vendors.

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

Planned for Cloud Integration

Currently implemented through HTTP adapter

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

Available through Web service

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

File Content Conversion can be performed in standard step CSV to XML or using a script step.

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

Cloud Integration supports IDoc in HTTP protocol, which means that the traditional IDoc with packing \(via RFC\) can't be used.

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

AMQP

</td>
<td valign="top">

Although Cloud Integration supports the JMS adapter, it can only be used internally and not to external JMS servers. For this scenario, the AMQP adapter should be used instead.

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

SAP is working on supporting multiple cloud and on-premise database vendors.

</td>
</tr>
<tr>
<td valign="top">

REST

</td>
<td valign="top">

Planned for Cloud Integration

Currently implemented through HTTP adapter

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

