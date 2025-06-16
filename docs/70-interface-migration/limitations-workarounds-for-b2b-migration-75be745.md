<!-- loio75be745cbcfe42a58b0ff5c14168d4a7 -->

# Limitations & Workarounds for B2B Migration

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

Currently, there's no direct support of Trading Partner Management objects like UDF, and during the migration, master data can't be imported.

For the new framework of Trading Partner Management in comparison to SAP Process Integration and SAP Process Orchestration, see [Understanding Basic Concepts](https://help.sap.com/docs/integration-suite/sap-integration-suite/understanding-basic-concepts).

</td>
</tr>
<tr>
<td valign="top">

EDI XSD formats

</td>
<td valign="top">

The EDI XSD format differs in Cloud Integration and SAP Process Integration and SAP Process Orchestration, which means a direct migration without modification isn't possible. Therefore, you need to add a message transformation step before the migrated mapping to convert the XML structure in Cloud Integration to the XML structure in SAP Process Orchestration.

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
</table>

