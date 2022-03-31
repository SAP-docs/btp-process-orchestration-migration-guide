<!-- loio1e83249a0b444a268f1df3dd3c806ce3 -->

# Scenario and Object Assessment

Get an overview of the scenarios and objects that are common scope of migration projects, and learn about the coverage aspects between the two solutions, SAP Process Orchestration and Cloud Integration.

It’s important to highlight some of the additional sources of information while you're assessing a migration project. SAP delivers updates and features to SAP Integration Suite on a regular basis, so before performing the necessary analyses of the migration project, access the [SAP API Business Hub](https://api.sap.com/) to find predelivered templates, packages, and blueprints for various market cloud solutions.

To follow the previous and future releases, you can access the [Road Map Explorer](https://roadmaps.sap.com/board?CB=901B0ED1A0641ED8B4D1230C6387E0DB&range=CURRENT-LAST) and the [What's New section](https://help.sap.com/doc/7ac9748e20cf453a94efda779542d34e/sap.cp.integration.suite/en-US/c10c21cd7c684f0885fa8b5db2982284.html) of SAP Integration Suite .



<a name="loio1e83249a0b444a268f1df3dd3c806ce3__section_nc3_s1j_qqb"/>

## Scenario and Object Overview

This table highlights some scenarios and objects with the scope of migrating from SAP Process Orchestration:


<table>
<tr>
<th valign="top">

Scenarios / Objects



</th>
<th valign="top">

Cloud Integration



</th>
</tr>
<tr>
<td valign="top">

Message Mapping



</td>
<td valign="top">

Cloud Integration supports various types of mapping methods, such as Operation Mapping \(from SAP Process Orchestration\), Message Mapping \(XML and JSON\), XSLT, and Groovy Script.

The section [Import Mapping Artifacts](scenario-and-object-assessment-1e83249.md#loio1e83249a0b444a268f1df3dd3c806ce3__section_glt_51j_qqb) details the strategy to migrate each type of object.



</td>
</tr>
<tr>
<td valign="top">

Adapters



</td>
<td valign="top">

For more information, see [Connectivity](../30-connectivity/connectivity-94ab030.md).



</td>
</tr>
<tr>
<td valign="top">

B2B



</td>
<td valign="top">

There are some limitations compared to SAP Process Orchestration regarding adapters and features.

> ### Note:  
> For more information on new features and future releases, access the [Road Map Explorer](http://help.sap.com/disclaimer?site=https://roadmaps.sap.com/board?CB=901B0ED1A0641ED8B4D1230C6387E0DB&range=CURRENT-LAST) and the [What's New section](https://help.sap.com/doc/7ac9748e20cf453a94efda779542d34e/sap.cp.integration.suite/en-US/c10c21cd7c684f0885fa8b5db2982284.html) of SAP Integration Suite.

Regarding B2B Scenarios, SAP recommends using the [Integration Content Advisor](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/6b9fe2d753534bebadcfa9080228bd94.html).

For more information, see the blog [Partner Directory - Step-by-Step example](https://blogs.sap.com/2017/07/25/cloud-integration-partner-directory-step-by-step-example/).



</td>
</tr>
<tr>
<td valign="top">

B2G



</td>
<td valign="top">

Standard Content available via [SAP API Business Hub](https://api.sap.com) 



</td>
</tr>
<tr>
<td valign="top">

OP2OP



</td>
<td valign="top">

For ground-to-ground scenarios, SAP plans to provide a [hybrid deployment option](https://roadmaps.sap.com/board?CB=901B0ED1A0641ED8B4D1230C6387E0DB&range=CURRENT-LAST#;INNO=901B0ED1A0641EDABE80AF561BFAC0F8) with which you can leverage all the capabilities of the Cloud Integration, but in a local deployment.

You can also use the Integration Gateway Component to execute and operate cloud integration content from the Cloud Integration in the Advanced Adapter Engine with all the deployment options \(PI-AEX, decentral Adapter Engine, SAP Process Orchestration and SAP PI dual usage type\).

For more information, see [Enable the Integration Gateway Component](https://help.sap.com/viewer/5cf7d2de571a45cc81f91261668b7361/7.5.21/en-US/a68695d0e6eb4552ace156cf5352a420.html) and SAP Note [2428801](https://launchpad.support.sap.com/#/notes/2428801).



</td>
</tr>
<tr>
<td valign="top">

Message Monitoring



</td>
<td valign="top">

For more information, see [Monitoring](../50-error-handling-and-logging/monitoring-2995dcf.md) in [Error Handling and Logging Strategy](../50-error-handling-and-logging/error-handling-and-logging-strategy-8faa23e.md).



</td>
</tr>
<tr>
<td valign="top">

Deployment



</td>
<td valign="top">

For more information, see [Interface Governance](../60-interface-governance/interface-governance-e8819d7.md).



</td>
</tr>
<tr>
<td valign="top">

Security



</td>
<td valign="top">

For more information, see [Security](../40-security/security-dd0fb21.md).



</td>
</tr>
<tr>
<td valign="top">

User Governance



</td>
<td valign="top">

For more information, see [Interface Governance](../60-interface-governance/interface-governance-e8819d7.md).



</td>
</tr>
<tr>
<td valign="top">

Standard Content



</td>
<td valign="top">

New standard content will be released for SAP Integration Suite \(see [API Business Hub](https://api.sap.com/themes/INTEGRATIONCONTENT)\)



</td>
</tr>
<tr>
<td valign="top">

Debug/Test



</td>
<td valign="top">

For more information, see [Error Handling and Logging Strategy](../50-error-handling-and-logging/error-handling-and-logging-strategy-8faa23e.md).



</td>
</tr>
<tr>
<td valign="top">

Alerting



</td>
<td valign="top">

For more information, see [Error Handling and Logging Strategy](../50-error-handling-and-logging/error-handling-and-logging-strategy-8faa23e.md).



</td>
</tr>
<tr>
<td valign="top">

Job Scheduler



</td>
<td valign="top">

It's possible to use timer events when developing an integration flow to create a scheduled execution.

For more information, see [Add a Timer Start Event](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/LATEST/en-US/4ede1b465aff413c9f8e4c6306316e33.html).



</td>
</tr>
<tr>
<td valign="top">

SWCV



</td>
<td valign="top">

Different from SAP Process Orchestration, in Cloud Integration you don’t have the concept of software component \(defined in SLD\) and namespace.

In Cloud Integration, you can create a package into your tenant and create some design artifacts such as integration flow and value mapping. So far, the following artifacts can be created inside a package:

-   Integration Flow

-   REST API

-   Message Mapping

-   SOAP API

-   Value Mapping

-   OData API

-   Script Collection

-   Integration Adapter




</td>
</tr>
<tr>
<td valign="top">

Service Registry



</td>
<td valign="top">

There is not an equivalent concept in Cloud Integration, however, you can combine your interfaces created in Cloud Integration with the API Management capability to create an omni-channel experience for customers and employees \(mobile, web, devices\). It can bring other benefits such as:

-   Efficient API publishing

-   Broad analytics

-   New revenue streams \(Data-as-a-Service\)


For more information, see [What is API Management](https://help.sap.com/viewer/66d066d903c2473f81ec33acfe2ccdb4/LATEST/en-US/0aef7634df25497896abf18faac8a1ce.html).



</td>
</tr>
</table>



<a name="loio1e83249a0b444a268f1df3dd3c806ce3__section_glt_51j_qqb"/>

## Import Mapping Artifacts

When migrating an operation mapping or message mapping from SAP Process Orchestration to Cloud Integration, you may adopt as your first option the automatic import feature, which is already available as part of the standard features of Cloud Integration.

With that, you can connect your cloud instance to the Enterprise Services Repository using Cloud Connector and move any of these mapping artifacts to your integration flow.

![](images/InterfaceMigration_CloudConnector_2c014b0.png)

However, there are some limitations when using this method. The following table describes these limitations and possible workarounds:


<table>
<tr>
<th valign="top">

Mappings



</th>
<th valign="top">

Limitations and Workaround



</th>
</tr>
<tr>
<td valign="top">

Graphical Mapping \(UDF\)



</td>
<td valign="top">

User-Defined Functions \(UDFs\) with function libraries, imported archives or parameters are not supported when importing the message mapping.

A local Java UDF is supported but viewing or editing it is not. If you need to change it, you must rewrite the logic using Javascript/Groovy or reimport a new version of the message mapping from the Enterprise Services Repository.

> ### Note:  
> Lookups \(e.g., RFC, JDBC\) are not supported. You can use additional integration flow steps instead.



</td>
</tr>
<tr>
<td valign="top">

XSLT



</td>
<td valign="top">

XSLT files are downloaded as .xsl under src.main.resources.mapping.



</td>
</tr>
<tr>
<td valign="top">

Value Mappings



</td>
<td valign="top">

Message Mapping containing reference to Value Mapping is not supported at runtime. In this case, you must redesign your message mapping and use the value mapping of Cloud Integration.

Access the Connectivity Migration document for more information about how to migrate value mappings from SAP Process Orchestration to Cloud Integration.



</td>
</tr>
<tr>
<td valign="top">

Fixed Values



</td>
<td valign="top">

Although it’s supported in automatic import feature, it’s highly recommended to change the Fixed Values reference to a Value Mapping in Cloud Integration. This way, you can reuse this artifact and maintain the values without changing the integration flow when necessary.

For more information about how to import a CSV file as a Value Mapping, see [Formatting Guidelines for CSV Files used in Value Mapping](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/LATEST/en-US/8fa8203aff104e938bd7f51dd9daa3e1.html), or see [Connectivity](../30-connectivity/connectivity-94ab030.md).



</td>
</tr>
<tr>
<td valign="top">

Libraries



</td>
<td valign="top">

The JAR files that contain the external Java libraries can be imported manually in Cloud Integration.



</td>
</tr>
<tr>
<td valign="top">

Function Libraries



</td>
<td valign="top">

Message Mapping containing reference to Function Libraries is not supported. In this case, it’s necessary to redesign these mappings. You can use Javascript/Groovy script in this case. The scripts can be created locally in the integration flow or you can create a [Script Collection](https://blogs.sap.com/2021/06/07/script-reusable-artifact-in-sap-cloud-integration/) to make it available for different integration flows inside your package.

> ### Note:  
> Lookups \(e.g., RFC, JDBC\) are not supported. You can use additional integration flow steps instead.



</td>
</tr>
<tr>
<td valign="top">

Java Mappings



</td>
<td valign="top">

The JAR files can be imported and reused in Cloud Integration.

You can also work with Javascript/Groovy scripts, which is the preferable approach when working in Cloud Integration. In this option, you can edit the script without having to reimport a compiled version.

For more information about the Java Mappings, see the blog [Using Java Mappings in SAP Cloud Platform Integration](https://blogs.sap.com/2018/03/19/using-java-mappings-in-sap-cloud-platform-integration-cpi/).



</td>
</tr>
<tr>
<td valign="top">

ABAP Mapping



</td>
<td valign="top">

ABAP Mapping is not supported, which means that the logic must be reimplemented using any of other mapping methods in Cloud Integration: Graphical Mapping, XSLT, or Javascript/Groovy script.



</td>
</tr>
</table>

For more information about how to set up the connection between SAP Process Orchestration and Cloud Integration, see [Configuring Connectivity to ES Repository](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/LATEST/en-US/8c36fd29df9a4e7bae8ce2699f6abbfd.html) or the blog [How to connect CPI and PI system to import mappings via SAP Cloud Connector](https://blogs.sap.com/2018/11/26/how-to-connect-cpi-and-pi-system-to-import-mappings-via-sap-cloud-connector/).

