<!-- loio02f233b97eec40bfbf5ef7ef23f101f0 -->

# Generating ABAP Proxies

With the introduction of the service interface object in SAP Integration Suite, you no longer have to migrate existing ESR proxies to the Metadata Repository \(MDR\). This new approach simplifies proxy lifecycle management, ensures consistency with Integration Suite artifacts, and removes the dependency on keeping the Enterprise Services Repository \(ESR\) used in SAP Process Orchestration.

ABAP proxy generation is fully supported on SAP Integration Suite through the service interface artifact, enabling seamless integration between cloud-defined interfaces and on-premise ABAP systems using XI message exchange.

The following high-level steps summarize how to generate ABAP proxies based on the new service interface import approach:

1.  **Import the required service interface from the ESR source system to the Design section of SAP Integration Suite**.

    Currently, you can't create or modify service interfaces directly in SAP Integration Suite.

2.  **Configure the connection with SAP Integration Suite**.

    This connection enables your ABAP system to access the service interface definition in SAP Integration Suite for the proxy generation.

    In your ABAP backend system, use transaction `SM59` \(type HTTP\) to create an HTTP destination. The HTTP destination must be named `SAP_PROXY_ESR` to ensure a successful connection and proxy generation.

3.  **Generate the ABAP proxy**.

    In the ABAP backend, open transaction `SPROXY`. Select SAP Integration Suite as the metadata source, choose the imported service interface, and generate the proxy objects.

4.  **Implement and reuse**.

    Once generated, you can implement the ABAP class methods corresponding to the service interface operations. If the service interface is updated in SAP Integration Suite, you can import and generate the proxy again.


See also [Generating ABAP Proxy](https://help.sap.com/docs/integration-suite/sap-integration-suite/generating-abap-proxy) and [ABAP Proxy Generation Support with SAP Integration Suite](https://community.sap.com/t5/technology-blog-posts-by-sap/abap-proxy-generation-support-with-sap-integration-suite/ba-p/14221791?emcs_t=S2h8ZW1haWx8ZGlnZXN0X25vdGlmaWNhdGlvbnxNSEsyTlE4V0dYWDhQUnwtMXxPVEhFUlN8aEs).



<a name="loio02f233b97eec40bfbf5ef7ef23f101f0__section_yfr_3sp_hhc"/>

## Comparison of Service Interface and ESR-to-MDR Approach

To learn about the advantages of using service interfaces for the ABAP proxy generation, see the following table. It highlights the key differences between the previous ESR-to-MDR migration approach and the new service interface import approach in SAP Integration Suite.

****


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Migrating ESR Proxies from ESR to MDR

</th>
<th valign="top">

Service Interface Import in SAP Integration Suite

</th>
</tr>
<tr>
<td valign="top">

Purpose

</td>
<td valign="top">

Enable reuse of ESR-based proxies in ABAP systems by migrating definitions to the Metadata Repository \(MDR\).

</td>
<td valign="top">

Enable direct generation of ABAP proxies based on service interfaces defined in SAP Integration Suite.

</td>
</tr>
<tr>
<td valign="top">

Maintainability

</td>
<td valign="top">

Requires migration and management of ESR proxies in SAP Process Integration and SAP Process Orchestration, and in the MDR. For compatibility, you require continuous updates.

</td>
<td valign="top">

You don't need to migrate or maintain ESR proxies. ABAP proxies are generated directly from SAP Integration Suite.

</td>
</tr>
<tr>
<td valign="top">

Design Principle

</td>
<td valign="top">

Process is based on ESR artifacts and on-premise architecture of SAP Process Integration and SAP Process Orchestration.

</td>
<td valign="top">

The cloud-native design is aligned with SAP Integration Suite metadata and structures.

</td>
</tr>
<tr>
<td valign="top">

Proxy Handling

</td>
<td valign="top">

ESR proxies are migrated to MDR using dedicated migration tools.

</td>
<td valign="top">

A service interface is imported into SAP Integration Suite from ESR. It's accessed from the ABAP backend using transaction `SPROXY` to generate ABAP proxies.

</td>
</tr>
<tr>
<td valign="top">

Required System Landscape

</td>
<td valign="top">

SAP Process Orchestration

</td>
<td valign="top">

SAP Integration Suite

</td>
</tr>
<tr>
<td valign="top">

Proxy Regeneration

</td>
<td valign="top">

Requires manual regeneration when the interface definitions change.

</td>
<td valign="top">

ABAP proxies can be regenerated in `SPROXY` if service interface definitions change in SAP Integration Suite.

</td>
</tr>
<tr>
<td valign="top">

Compatibility

</td>
<td valign="top">

Must be maintained for backward compatibility and legacy ESR scenarios.

</td>
<td valign="top">

Is fully compatible with SAP’s cloud-first integration strategy.

</td>
</tr>
<tr>
<td valign="top">

Migration Effort

</td>
<td valign="top">

High effort, as it involves technical adjustments and compatibility testing.

</td>
<td valign="top">

Low effort, as new proxies are generated directly from SAP Integration Suite.

</td>
</tr>
<tr>
<td valign="top">

Recommendation

</td>
<td valign="top">

Use only as interim solution during your transition to SAP Integration Suite.

</td>
<td valign="top">

Preferred and future-proof approach for all new implementations.

</td>
</tr>
</table>

