<!-- loio75be745cbcfe42a58b0ff5c14168d4a7 -->

# Limitations & Workarounds for B2B Migration

Learn about the current limitations for B2B migration and their workarounds.

The following limitations and workarounds exist for the migration of B2B scenarios:

****


<table>
<tr>
<th valign="top">

Feature

</th>
<th valign="top">

Limitation and Workaround

</th>
</tr>
<tr>
<td valign="top">

Trading Partner Management Module

</td>
<td valign="top">

Currently, there's no direct support of Trading Partner Management objects like UDF and no direct import of master data like partner profiles.

For a comparison of the new framework of Trading Partner Management with SAP Process Integration and SAP Process Orchestration, see [Understanding Basic Concepts](https://help.sap.com/docs/integration-suite/sap-integration-suite/understanding-basic-concepts).

</td>
</tr>
<tr>
<td valign="top">

EDI XSD formats

</td>
<td valign="top">

The EDI XSD format differs in Cloud Integration and SAP Process Integration and SAP Process Orchestration, which means a direct migration without modification isn't possible. Therefore, you need to add a message transformation step before the migrated mapping to convert the XML structure in Cloud Integration to the XML structure in SAP Process Orchestration.

For more information, see the community package [B2B Interface Migration Accelerator - ASCX12](https://api.sap.com/package/BIMAB2BInterfaceMigrationAcceleratorASCX12/integrationflow) and the blogs [Migrate Inbound B2B ASCX12 Interfaces from SAP PI/PO to CI \(CPI\) Using BIMA Package](https://community.sap.com/t5/technology-blog-posts-by-sap/migrate-inbound-b2b-ascx12-interfaces-from-sap-pi-po-to-ci-cpi-using-bima/ba-p/14099425) and [Migrate Outbound B2B ASCX12 Interfaces from SAP PI/PO to CI \(CPI\) Using BIMA Package](https://community.sap.com/t5/technology-blog-posts-by-sap/migrate-outbound-b2b-ascx12-interfaces-from-sap-pi-po-to-ci-cpi-using-bima/ba-p/14099461).

For the latest features, review [What's New for Trading Partner Management](https://help.sap.com/whats-new/cf0cb2cb149647329b5d02aa96303f56?locale=en-US&version=Cloud&Component=Trading+Partner+Management) and the EDI flow step documentation at [Define EDI Splitter](https://help.sap.com/docs/integration-suite/sap-integration-suite/define-edi-splitter), [Define EDI to XML Converter](https://help.sap.com/docs/integration-suite/sap-integration-suite/define-edi-to-xml-converter), [Define XML to EDI Converter](https://help.sap.com/docs/integration-suite/sap-integration-suite/define-xml-to-edi-converter).

</td>
</tr>
<tr>
<td valign="top">

EDI Separator

</td>
<td valign="top">

Integration scenarios with sender or receiver channel adapter and EDI separator currently can't be migrated directly.

</td>
</tr>
<tr>
<td valign="top">

Communication Adapters

</td>
<td valign="top">

Currently OFTP2, RNIF, and the relevant message standards aren't supported in Cloud Integration, Integration Advisor, and Trading Partner Management.

For updates, follow the external road map in the [SAP Road Map Explorer](https://roadmaps.sap.com/board?BC=42F2E964F4E71EDA9FF9F6612D71E0E3&q=SAp%20integration%20Suite&range=CURRENT-LAST).

</td>
</tr>
</table>

