<!-- loio40a5d8e489d946f7a901403d4675bf12 -->

# What's New

Find out what's new in the migration guide for SAP Process Orchestration.




<table>
<tr>
<th valign="top">

Section

</th>
<th valign="top">

Description

</th>
<th valign="top">

Update

</th>
</tr>
<tr>
<td valign="top">

[Generating ABAP Proxies](70-interface-migration/generating-abap-proxies-02f233b.md)

</td>
<td valign="top">

You can now find information on generating ABAP proxies using the service interface object in SAP Integration Suite.

The service interface object in SAP Integration Suite streamlines ABAP proxy lifecycle management by eliminating the need to migrate ESR proxies to the Metadata Repository. This feature ensures seamless integration between cloud and on-premise systems, enhancing efficiency and consistency in managing SAP Integration Suite artifacts.

</td>
<td valign="top">

November 2025

</td>
</tr>
<tr>
<td valign="top">

[Pipeline Concept](70-interface-migration/pipeline-concept-6e527fb.md)

</td>
<td valign="top">

The pipeline concept has been extended by the chapter [Generic Inbound and Outbound](70-interface-migration/generic-inbound-and-outbound-5e2fdf8.md), in which you can find information on scenarios that use IDoc or XI protocol, both inbound and outbound.

</td>
<td valign="top">

November 2025

</td>
</tr>
<tr>
<td valign="top">

[Custom Preprocessing Exit](70-interface-migration/customizing-the-pipeline-concept-aeb106f.md#loioaeb106f049144c71a0b7814a2ffedc3f__section_uqy_gdd_kgc)

</td>
<td valign="top">

If you want to embed custom logic at the very beginning of the generic pipeline steps, you can now call a custom exit integration flow without having to edit the provided generic flows. To do so, you must implement a separate integration flow that can be called at the very beginning of each generic integration flow. You can configure the custom exit either globally or scenario-specifically.

</td>
<td valign="top">

August 2025

</td>
</tr>
<tr>
<td valign="top">

[Message Processing Behavior](70-interface-migration/using-the-partner-directory-in-the-pipeline-concept-9ec7d2d.md#loio9ec7d2dce72d423abff80543f11b2091__section_bxk_wty_31c)

</td>
<td valign="top">

With the `KeepBulk` feature, you can keep IDoc bulk messages intact without splitting them into single messages for specific scenarios. This feature is useful for maintaining the integrity of bulk data processing, ensuring efficient handling of large data sets in pipeline steps. By default, IDoc bulk messages are split into single IDoc messages, so you have to enable `KeepBulk` by setting it to `true`.

</td>
<td valign="top">

August 2025

</td>
</tr>
<tr>
<td valign="top">

[Pipeline Concept](70-interface-migration/pipeline-concept-6e527fb.md)

</td>
<td valign="top">

The Cloud Integration pipeline integration packages replace the [Process Integration Pipeline - Generic Integration Flows and Templates](https://help.sap.com/docs/link-disclaimer?site=https%3A%2F%2Fhub.sap.com%2Fpackage%2FPIPipelineGenericIntegrationFlows%2Foverview) package, which was split into four packages. This way, it allows you more flexibility in setting up your different pipelines, sender-specific IDoc and XI inbound flows, and receiver-specific outbound flows. For the same reason, the script collection was also replaced with local scripts.

The previous integration package will soon be deprecated. All new feature increments will only be shipped with the new integration packages.

For details on all ensuing changes, see [Pipeline Concept](70-interface-migration/pipeline-concept-6e527fb.md).

</td>
<td valign="top">

August 2025

</td>
</tr>
<tr>
<td valign="top">

[Migrating B2B Interfaces](70-interface-migration/migrating-b2b-interfaces-fc315dc.md)

</td>
<td valign="top">

Learn how to migrate your B2B scenarios to SAP Integration Suite. You can perform the migration using Cloud Integration or Trading Partner Management, with the optional addition of Integration Advisor.

</td>
<td valign="top">

June 2025

</td>
</tr>
<tr>
<td valign="top">

[Setting Up XI Proxy Runtime](70-interface-migration/setting-up-xi-proxy-runtime-6598c53.md) 

</td>
<td valign="top">

If you're working with proxies, consider the following update:

In [Setting Up XI Proxy Runtime](70-interface-migration/setting-up-xi-proxy-runtime-6598c53.md), step 9 has been corrected with a new table name and transaction. Also, pay attention to the note about deactivating the daily SLD access.

</td>
<td valign="top">

June 2025

</td>
</tr>
<tr>
<td valign="top">

[Monitoring and Error Handling in the Pipeline Concept](70-interface-migration/monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md)

</td>
<td valign="top">

In the pipeline concept, the section on custom header properties was updated with a new recommended approach.

</td>
<td valign="top">

June 2025

</td>
</tr>
<tr>
<td valign="top">

[Additional References for Interface Development](70-interface-migration/additional-references-for-interface-development-6daed01.md)

</td>
<td valign="top">

The topic now lists more references outlining how to migrate your B2B scenarios.

</td>
<td valign="top">

June 2025

</td>
</tr>
<tr>
<td valign="top">

[Conditional Routing Behavior](70-interface-migration/conditional-routing-behavior-010875d.md)

</td>
<td valign="top">

In this new topic about conditional routing, you learn the differences between SAP Process Orchestration and Cloud Integration, and how to align the routing logic during your migration.

</td>
<td valign="top">

June 2025

</td>
</tr>
<tr>
<td valign="top">

[Pipeline Concept](70-interface-migration/pipeline-concept-6e527fb.md)

</td>
<td valign="top">

The integration package for the pipeline concept has been updated.

You can now use two alternative pipelines: the integrated message runtime \(asynchronous\), which combines inbound conversion and receiver/interface determination in one pipeline step, and the integrated messaging runtime \(synchronous\), which handles synchronous content-based routing scenarios.

Furthermore, different tenant stages \(DEV, QA, PRD\) are now supported, and there are two new templates: `Pipeline Template Step01 - Inbound Processing Synchronous` and `Pipeline Template Step07 - Outbound Processing Synchronous`.

For more details, see the [change log](https://hub.sap.com/package/PIPipelineGenericIntegrationFlows/documents) in the pipeline integration package.

</td>
<td valign="top">

February 2025

</td>
</tr>
<tr>
<td valign="top">

[Pipeline Concept](70-interface-migration/pipeline-concept-6e527fb.md)

</td>
<td valign="top">

The integration package for the pipeline concept has been updated. You can now combine receiver and interface determination in one single XSLT mapping for an improved runtime behavior. Furthermore, you can now bypass the interface determination pipeline step in case of recipient list pattern without interface split, and also bypass the receiver determination pipeline step in case of interface split scenarios with only a single receiver.

</td>
<td valign="top">

December 2024

</td>
</tr>
<tr>
<td valign="top">

[Pipeline Concept](70-interface-migration/pipeline-concept-6e527fb.md)

</td>
<td valign="top">

The integration package for the pipeline concept has been updated and now includes the new script `addCustomHeaderProperties`. This script allows you to add custom header properties to the message processing log, which enables you to search for message logs based on payload data.

</td>
<td valign="top">

October 2024

</td>
</tr>
<tr>
<td valign="top">

[Adapter Modules](30-connectivity/adapter-modules-e402f4a.md)

</td>
<td valign="top">

A community package was released to address SAP Process Integration adapter modules and offers an alternative approach to their reimplementation. This initial version includes the modules `AF_Modules/XMLAnonymizerBean` and `AF_Modules/MessageTransformBean`.

</td>
<td valign="top">

September 2024

</td>
</tr>
<tr>
<td valign="top">

[Pipeline Concept](70-interface-migration/pipeline-concept-6e527fb.md)

</td>
<td valign="top">

There have been multiple changes for the pipeline concept. For example, the definition of a partner ID \(pid\) has changed, and alternative partners were introduced to support sender wildcard scenarios. Additionally, a new special case with Point-to-Point scenarios is now described that allows you to bypass some of the pipeline steps for an improved runtime behavior, and two new scripts have been added to the script collection, determinePartnerID and readBypassOptionfromPD.

For details, see [Pipeline Concept](70-interface-migration/pipeline-concept-6e527fb.md) and its subordinate topics.

</td>
<td valign="top">

August 2024

</td>
</tr>
<tr>
<td valign="top">

[Modernization Recommendations](70-interface-migration/modernization-recommendations-d337a6f.md)

</td>
<td valign="top">

Use the modernization recommendations to align your current integration practices with contemporary standards and the integration strategy of SAP. They're provided as part of the Migration Assessment capability of SAP Integration Suite.

</td>
<td valign="top">

June 2024

</td>
</tr>
<tr>
<td valign="top">

[Pipeline Concept](70-interface-migration/pipeline-concept-6e527fb.md)

</td>
<td valign="top">

Learn about the pipeline concept, which allows you to set up your asynchronous integration scenarios in Cloud Integration similarly to how messages are processed in SAP Process Orchestration, in pipelines.

</td>
<td valign="top">

March 2024

</td>
</tr>
<tr>
<td valign="top">

[Migrating Java Mappings](70-interface-migration/migrating-java-mappings-468c179.md)

</td>
<td valign="top">

Migrate your Java mappings in SAP Process Orchestration to the more efficient Groovy script in Cloud Integration using Groovy script templates.

</td>
<td valign="top">

February 2024

</td>
</tr>
<tr>
<td valign="top">

[Adapter Modules](30-connectivity/adapter-modules-e402f4a.md)

</td>
<td valign="top">

Learn how to migrate the archiver module `localejbs/ArchiverModuleBean` using the archiving feature provided by Cloud Integration.

</td>
<td valign="top">

September 2023

</td>
</tr>
<tr>
<td valign="top">

[Migrating Proxy Interfaces](70-interface-migration/migrating-proxy-interfaces-dfaee7b.md)

[Setting Up XI Proxy Runtime](70-interface-migration/setting-up-xi-proxy-runtime-6598c53.md)

[Message Reprocessing](70-interface-migration/message-reprocessing-a98fbcf.md)

</td>
<td valign="top">

There's now additional information available on the migration of proxy interfaces, such as known limitations, the procedure of setting up the XI proxy runtime, and general information on message reprocessing.

</td>
<td valign="top">

May 2023

</td>
</tr>
<tr>
<td valign="top">

[Interface Migration Strategy](70-interface-migration/interface-migration-strategy-46c8a36.md)

[Scenario and Object Assessment](70-interface-migration/scenario-and-object-assessment-1e83249.md)

[Interface Design and Implementation](70-interface-migration/interface-design-and-implementation-b763478.md)

</td>
<td valign="top">

The capability Migration Assessment and the migration tooling for Cloud Integration are now available in SAP Integration Suite. Both support you in your migration journey to the cloud. See [Assessing the Migration Strategy and Migrating Content](https://help.sap.com/docs/SAP_INTEGRATION_SUITE/51ab953548be4459bfe8539ecaeee98d/5ad08e16fe2645d291ea5e26a424619b.html?locale=en-US&version=CLOUD) in the documentation for SAP Integration Suite.

</td>
<td valign="top">

February 2023

</td>
</tr>
<tr>
<td valign="top">

[Directory API](70-interface-migration/directory-api-07096c2.md)

</td>
<td valign="top">

Learn about the APIs Migration Assessment and Migration Tooling use to extract all necessary data for the migration from SAP Process Orchestration.

</td>
<td valign="top">

February 2023

</td>
</tr>
</table>

