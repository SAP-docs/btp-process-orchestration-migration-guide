<!-- loio1e83249a0b444a268f1df3dd3c806ce3 -->

# Scenario and Object Assessment

Get an overview of the scenarios and objects that are common scope of migration projects, and learn about the coverage aspects between the two solutions, SAP Process Orchestration and Cloud Integration.

> ### Note:  
> Before performing the necessary analyses of your migration project, access the [SAP Business Accelerator Hub](https://api.sap.com/) to find predelivered templates, packages, and blueprints for various market cloud solutions.
> 
> Since SAP regularly delivers updates and features to SAP Integration Suite, follow the previous and future releases in the [Road Map Explorer](https://roadmaps.sap.com/board?CB=901B0ED1A0641ED8B4D1230C6387E0DB&range=CURRENT-LAST) and [What's New in SAP Integration Suite](https://help.sap.com/whats-new/5793247a5d5741beb0decc5b7dee1160?locale=en-US&version=CLOUD).

You can use the SAP Integration Suite capability [Migration Assessment](https://help.sap.com/docs/SAP_INTEGRATION_SUITE/51ab953548be4459bfe8539ecaeee98d/5c5e50ee2d644cc59d864409d5b7871c.html?locale=en-US&version=CLOUD) to estimate the technical effort involved in the migration process and evaluate how your integration scenarios might be migrated.



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

See [Import Mapping Artifacts](scenario-and-object-assessment-1e83249.md#loio1e83249a0b444a268f1df3dd3c806ce3__section_glt_51j_qqb) for strategies on migrating each type of object.

</td>
</tr>
<tr>
<td valign="top">

Adapters

</td>
<td valign="top">

See [Connectivity](../30-connectivity/connectivity-94ab030.md).

</td>
</tr>
<tr>
<td valign="top">

B2B

</td>
<td valign="top">

There are some limitations compared to SAP Process Orchestration regarding adapters and features.

> ### Note:  
> For more information on new features and future releases, access the [Road Map Explorer](http://help.sap.com/disclaimer?site=https://roadmaps.sap.com/board?CB=901B0ED1A0641ED8B4D1230C6387E0DB&range=CURRENT-LAST) and [What's New in SAP Integration Suite](https://help.sap.com/whats-new/5793247a5d5741beb0decc5b7dee1160?locale=en-US&version=CLOUD).

Regarding B2B Scenarios, SAP recommends using the [Integration Content Advisor](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/6b9fe2d753534bebadcfa9080228bd94.html).

For more information, see the blog [Partner Directory - Step-by-Step example](https://blogs.sap.com/2017/07/25/cloud-integration-partner-directory-step-by-step-example/).

</td>
</tr>
<tr>
<td valign="top">

B2G

</td>
<td valign="top">

Standard content is available via [SAP Business Accelerator Hub](https://api.sap.com).

</td>
</tr>
<tr>
<td valign="top">

OP2OP

</td>
<td valign="top">

For ground-to-ground scenarios, SAP provides a hybrid deployment option, Edge Integration Cell, with which you can leverage all the capabilities of Cloud Integration, but in a local deployment. See [What Is Edge Integration Cell](https://help.sap.com/docs/integration-suite/sap-integration-suite/what-is-sap-integration-suite-edge-integration-cell).

You can also use the Integration Gateway Component to execute and operate cloud integration content from Cloud Integration in the Advanced Adapter Engine with all the deployment options \(PI-AEX, decentral Adapter Engine, SAP Process Orchestration and SAP PI dual usage type\).

See [Enable the Integration Gateway Component](https://help.sap.com/viewer/5cf7d2de571a45cc81f91261668b7361/7.5.21/en-US/a68695d0e6eb4552ace156cf5352a420.html) and SAP Note [2428801](https://me.sap.com/notes/2428801).

</td>
</tr>
<tr>
<td valign="top">

Message Monitoring

</td>
<td valign="top">

See [Monitoring](../50-error-handling-and-logging/monitoring-2995dcf.md) in [Error Handling and Logging Strategy](../50-error-handling-and-logging/error-handling-and-logging-strategy-8faa23e.md).

</td>
</tr>
<tr>
<td valign="top">

Deployment

</td>
<td valign="top">

See [Interface Governance](../60-interface-governance/interface-governance-e8819d7.md).

</td>
</tr>
<tr>
<td valign="top">

Security

</td>
<td valign="top">

See [Security](../40-security/security-dd0fb21.md).

</td>
</tr>
<tr>
<td valign="top">

User Governance

</td>
<td valign="top">

See [Interface Governance](../60-interface-governance/interface-governance-e8819d7.md).

</td>
</tr>
<tr>
<td valign="top">

Standard Content

</td>
<td valign="top">

See [SAP Business Accelerator Hub](https://api.sap.com/themes/INTEGRATIONCONTENT) for new standard content released for SAP Integration Suite.

</td>
</tr>
<tr>
<td valign="top">

Debug/Test

</td>
<td valign="top">

See [Error Handling and Logging Strategy](../50-error-handling-and-logging/error-handling-and-logging-strategy-8faa23e.md).

</td>
</tr>
<tr>
<td valign="top">

Alerting

</td>
<td valign="top">

See [Error Handling and Logging Strategy](../50-error-handling-and-logging/error-handling-and-logging-strategy-8faa23e.md).

</td>
</tr>
<tr>
<td valign="top">

Job Scheduler

</td>
<td valign="top">

When developing an integration flow to create a scheduled execution, you can use timer events. See [Add a Timer Start Event](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/LATEST/en-US/4ede1b465aff413c9f8e4c6306316e33.html).

</td>
</tr>
<tr>
<td valign="top">

SWCV

</td>
<td valign="top">

Cloud Integration doesn't have the concept of software component \(defined in SLD\) and namespace.

Instead, you can create a package into your tenant and create some design artifacts, such as integration flow and value mapping. The following artifacts can be created inside a package:

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

In Cloud Integration, there's no concept equivalent to Service Registry.

Instead, combine your interfaces created in Cloud Integration with the API Management capability. This way, you can create an omni-channel experience for customers and employees \(mobile, web, devices\) with benefits such as efficient API publishing, broad analytics, and new revenue streams \(Data-as-a-Service\). See [What is API Management](https://help.sap.com/viewer/66d066d903c2473f81ec33acfe2ccdb4/LATEST/en-US/0aef7634df25497896abf18faac8a1ce.html).

</td>
</tr>
</table>



<a name="loio1e83249a0b444a268f1df3dd3c806ce3__section_glt_51j_qqb"/>

## Import Mapping Artifacts

To import or migrate import mapping artifacts from SAP Process Orchestration to Cloud Integration, you can use two features included in the Cloud Integration capability:

-   Use the **Migration Tooling** feature to migrate your integration artifacts to SAP Integration Suite. For details about the feature, supported components and scenarios, and known limitations, see [Migration Tooling](https://help.sap.com/docs/SAP_INTEGRATION_SUITE/51ab953548be4459bfe8539ecaeee98d/60610163aec44849ac4783c92fb2e55c.html?locale=en-US&version=CLOUD).

-   You can also **import mappings from the Enterprise Services Repository**. This feature lets you connect your cloud instance to the Enterprise Services Repository using Cloud Connector and move these mapping artifacts to your integration flow. See [Importing Content from ES Repository](https://help.sap.com/docs/SAP_INTEGRATION_SUITE/51ab953548be4459bfe8539ecaeee98d/53db5fb382b54bba86abb413bd3711a7.html?version=CLOUD).

    ![Cloud Connector links Cloud Integration and the Enterprise Services Repository. The connection is bidirectional.](images/InterfaceMigration_CloudConnector_2c014b0.png)

    The following limitations and possible workarounds exist when importing content from the ES Repository:


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
    
    User-Defined Functions \(UDFs\) with function libraries, imported archives, or parameters are not supported when importing the message mapping.

    However, local Java UDFs are supported and can be viewed and edited.

    > ### Note:  
    > Lookups \(for example, RFC, JDBC\) are not supported. Use additional integration flow steps instead. For instructions, see the tutorials [Learn how to migrate JDBC Lookups from SAP Process Orchestration to Cloud Integration](https://developers.sap.com/tutorials/ci-jdbc-lookup.html) and [How to migrate RFC Lookups from SAP Process Orchestration to Cloud Integration](https://developers.sap.com/tutorials/ci-rfclookup.html).


    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    XSLT
    
    </td>
    <td valign="top">
    
    XSLT files are downloaded as .xsl under `src.main.resources.mapping`.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Value Mappings
    
    </td>
    <td valign="top">
    
    Message mapping containing reference to value mapping is not supported at runtime. Instead, redesign your message mapping and use the value mapping of Cloud Integration.

    See also [Migration of Value Mappings](../30-connectivity/migration-of-value-mappings-f2621ed.md).
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Fixed Values
    
    </td>
    <td valign="top">
    
    Although it’s supported in the automatic import feature, it’s highly recommended to change the Fixed Values reference to a Value Mapping in Cloud Integration. This way, you can reuse this artifact and maintain the values without changing the integration flow when necessary.

    For more information about how to import a CSV file as a Value Mapping, see [Formatting Guidelines for CSV Files used in Value Mapping](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/LATEST/en-US/8fa8203aff104e938bd7f51dd9daa3e1.html), or [Connectivity](../30-connectivity/connectivity-94ab030.md).
    
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
    
    Message mapping containing reference to function libraries is not supported. You need to redesign these mappings, using Javascript/Groovy script. The scripts can be created locally in the integration flow or you can create a script collection to make it available for different integration flows inside your package. See the blog [Script collection reusable artifact in SAP Cloud Integration](https://blogs.sap.com/2021/06/07/script-reusable-artifact-in-sap-cloud-integration/).

    > ### Note:  
    > Lookups \(for example, RFC, JDBC\) are not supported. Use additional integration flow steps instead. For instructions, see the tutorials [Learn how to migrate JDBC Lookups from SAP Process Orchestration to Cloud Integration](https://developers.sap.com/tutorials/ci-jdbc-lookup.html) and [How to migrate RFC Lookups from SAP Process Orchestration to Cloud Integration](https://developers.sap.com/tutorials/ci-rfclookup.html).


    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Java Mappings
    
    </td>
    <td valign="top">
    
    The JAR files can be imported and reused in Cloud Integration.

    You can also work with Javascript/Groovy scripts, which is the preferable approach when working in Cloud Integration. In this option, you can edit the script without having to reimport a compiled version.

    See [Migrating Java Mappings](migrating-java-mappings-468c179.md).
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    ABAP Mapping
    
    </td>
    <td valign="top">
    
    ABAP mapping is not supported. The logic must be reimplemented using any of other mapping methods in Cloud Integration: Graphical Mapping, XSLT, or Javascript/Groovy script.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Operation Mapping
    
    </td>
    <td valign="top">
    
    Due to limitations, it's not recommended to import operation mappings into Cloud Integration. Instead, import message mappings.

    See [Importing Mapping Content from ES Repository](https://help.sap.com/docs/cloud-integration/sap-cloud-integration/importing-mapping-content-from-es-repository).
    
    </td>
    </tr>
    </table>
    

For more information about how to set up the connection between SAP Process Orchestration and Cloud Integration, see [Configuring Connectivity to ES Repository](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/LATEST/en-US/8c36fd29df9a4e7bae8ce2699f6abbfd.html) or the blog [How to connect CPI and PI system to import mappings via SAP Cloud Connector](https://blogs.sap.com/2018/11/26/how-to-connect-cpi-and-pi-system-to-import-mappings-via-sap-cloud-connector/).

