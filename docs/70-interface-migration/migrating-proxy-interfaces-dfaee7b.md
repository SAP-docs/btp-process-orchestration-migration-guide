<!-- loiodfaee7ba44aa4a63b62177d46d34c21d -->

# Migrating Proxy Interfaces

When working with ABAP proxies in the context of SAP Process Orchestration, you need to follow certain steps to ensure successful integration. The service interfaces are defined in the Enterprise Services Repository \(ESR\), which then generates the ABAP objects using the SPROXY transaction on the SAP side.

If you're migrating from SAP Process Orchestration to SAP Integration Suite, there are some key differences to be aware of when it comes to working with ABAP proxies. For example, the way that ABAP proxies are deployed and managed, and you need to adjust your existing processes and configurations accordingly. Additionally, there may be differences in the way that ABAP proxies interact with other systems and technologies within the SAP Integration Suite.

In order to successfully proceed with these changes, you need to have a solid understanding of the underlying principles and best practices as outlined in [Setting Up XI Proxy Runtime](setting-up-xi-proxy-runtime-6598c53.md), [Message Reprocessing](message-reprocessing-a98fbcf.md), and [Generating ABAP Proxies](generating-abap-proxies-02f233b.md).



<a name="loiodfaee7ba44aa4a63b62177d46d34c21d__section_bx4_pjf_mxb"/>

## Known Limitations

The following limitations apply when migrating proxy interfaces from SAP Process Orchestration to SAP Integration Suite:


<table>
<tr>
<th valign="top">

Limitations

</th>
<th valign="top">

Workaround

</th>
</tr>
<tr>
<td valign="top">

Acknowledgement is not supported.

</td>
<td valign="top">

There's currently no workaround for this limitation.

</td>
</tr>
<tr>
<td valign="top">

Native support for ExactlyOnceInOrder \(EOIO\) .

</td>
<td valign="top">

EOIO ensures that messages are delivered and processed by the receiver exactly once and in the same sequence they were sent. This is now supported using asynchronous decoupling with the JMS adapter \(exclusive access type\) or SAP Integration Suite, advanced event mesh \(exclusive or partitioned queues\). These configurations guarantee ordered processing by allowing only one consumer to read from a queue at a time. For more information, see [Quality of Service Exactly Once In Order](https://help.sap.com/docs/integration-suite/sap-integration-suite/quality-of-service-exactly-once-in-order?version=CLOUD).

</td>
</tr>
<tr>
<td valign="top">

There is a limit on the JMS resources.

</td>
<td valign="top">

Analyze your landscape and according to the expected usage of the resources and decide on the number of queues, consumers, etc. See [JMS Resource Limits and Optimizing their Usage](https://help.sap.com/docs/CLOUD_INTEGRATION/368c481cd6954bdfa5d0435479fd4eaf/4857054e3f194ae6a7ed93a52002d556.html).

</td>
</tr>
</table>

-   **[Setting Up XI Proxy Runtime](setting-up-xi-proxy-runtime-6598c53.md "Perform the following steps to set up the XI proxy runtime. ")**  
Perform the following steps to set up the XI proxy runtime.
-   **[Message Reprocessing](message-reprocessing-a98fbcf.md "To ensure a successful migration, you can use reprocessing functionalities to retry processing your ABAP proxies in case of errors. ")**  
To ensure a successful migration, you can use reprocessing functionalities to retry processing your ABAP proxies in case of errors.
-   **[Generating ABAP Proxies](generating-abap-proxies-02f233b.md "With the introduction of the service interface object in SAP Integration Suite, you no
		longer have to migrate existing ESR proxies to the Metadata Repository (MDR). This new
		approach simplifies proxy lifecycle management, ensures consistency with Integration Suite
		artifacts, and removes the dependency on keeping the Enterprise Services Repository (ESR)
		used in SAP Process Orchestration.")**  
With the introduction of the service interface object in SAP Integration Suite, you no longer have to migrate existing ESR proxies to the Metadata Repository \(MDR\). This new approach simplifies proxy lifecycle management, ensures consistency with Integration Suite artifacts, and removes the dependency on keeping the Enterprise Services Repository \(ESR\) used in SAP Process Orchestration.

