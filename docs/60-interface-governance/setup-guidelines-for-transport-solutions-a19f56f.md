<!-- loioa19f56fb4695459ca472877cd58581aa -->

# Setup Guidelines for Transport Solutions

Discover information and guidance on different transport solutions.

For detailed guidance on the options available to transport integration artifacts, and how to set up the transport service, it's recommended to read the sections on [Content Transport](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/f4bf46bd9dbe4d08b7ee3c66b55b15a3.html) in the Cloud Integration documentation.



<a name="loioa19f56fb4695459ca472877cd58581aa__section_r4r_g5z_mqb"/>

## Decision Help

We provide a [decision help](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/19e0e73a57f142299f20ed16fc3e8ed1.html) that looks at cloud-based transport options and describes the advantages and disadvantages of each:


<table>
<tr>
<th valign="top">

Transport Option

</th>
<th valign="top">

Recommendations

</th>
</tr>
<tr>
<td valign="top">

Manual export/import

</td>
<td valign="top">

-   Use only in exceptional cases, for example for urgent fixes in case the transport system is down.

-   This option is easy-to-use \(no configuration required\).

-   No control and logging of the transport events and the involved users.

-   Risk of losing control of who is transporting what and when. Using this option, you don't have any advantage of the tool support provided by a transport system, like, for example, logging. For this reason, manual exports and imports should be avoided in an integration project or while operating Cloud Integration.




</td>
</tr>
<tr>
<td valign="top">

CTS+

</td>
<td valign="top">

-   CTS+ is a recommended option.

-   This option provides a fully automated transport mechanism \(allows the assignment of roles, definition of transport routes, approvals, and comes with additional useful features like logging\).

-   If an on-premise CTS+ is already installed and used for other systems or objects, it's an option to use CTS+ also for integration content transport.


> ### Note:  
> CTS+ has been available for many years to transport on-premise non-ABAP content. This concept has been extended some time ago to support SAP BTP. However, only cloud content that can be packaged in MTAR files can be transported. For integration content transport, this constraint is fulfilled. Therefore, if you use MTAR-based content only in SAP BTP, CTS+ is a valid choice.



</td>
</tr>
<tr>
<td valign="top">

SAP Cloud Transport Management service

</td>
<td valign="top">

-   SAP Cloud Transport Management is a recommended option.

-   It provides a fully automated transport mechanism \(allows the assignment of roles, definition of transport routes, approvals, and comes with additional useful features like logging\).

-   If there's no on-premise CTS+ available in your landscape, a good option is to go for SAP Cloud Transport Management. SAP Cloud Transport Management is the solution for transporting content in SAP BTP. Compared to using CTS+, this option initially implies a smaller investment in implementation and operation. Note that SAP Cloud Transport Management is a cloud service \(subscription-based with maintenance and updates by SAP\). It's therefore the way to go for customers planning to implement projects using SAP BTP services.




</td>
</tr>
<tr>
<td valign="top">

MTAR Download

</td>
<td valign="top">

-   MTAR Download is a semiautomated option \(in between manual export/import on the one hand and using CTS+ or SAP Cloud Transport Management on the other hand\).

-   It allows you to download an integration package manually from a source tenant as an .mtar file. In a subsequent step, you can upload this file to the transport system and, finally, transport it to the target tenant.

-   Using this option, you benefit of having certain advantages of a transport system. However, there's still a manual step. As manual steps should be avoided as far as possible, it's recommended to use this option only in exceptional cases, for example for urgent fixes in case the connection between source tenant and transport system is down.




</td>
</tr>
</table>

> ### Note:  
> The manual export/import and the MTAR download options are not discussed any further in this document due to their lack of full automation and inherent lack of ability to support any governance model.



<a name="loioa19f56fb4695459ca472877cd58581aa__section_pn5_g5z_mqb"/>

## Prerequisites

For the two automated approaches specified above, there are prerequisites that need to be performed depending on the environment your SAP BTP is deployed in.

For more information, see [Enabling Content Transport, Cloud Foundry Environment](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/452c677debfc4fda904310560ab03743.html).



<a name="loioa19f56fb4695459ca472877cd58581aa__section_cjw_g5z_mqb"/>

## CTS+

For more information on enabling the use of CTS+, see [Content Transport Using CTS+](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/3cdfb512a75941d187b6f5a86e418983.html).



<a name="loioa19f56fb4695459ca472877cd58581aa__section_tcy_g5z_mqb"/>

## SAP Cloud Transport Management Service

For setup instructions for using SAP Cloud Transport Management, see [Content Transport Using Transport Management Service](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/d458b172b98d4112a08499541fddfc54.html).

For more information on using the SAP Cloud Transport Management solution, see also the blog [Introducing SAP Content Agent service: Enhanced Transport Capabilities for Cloud Integration Content](https://blogs.sap.com/2020/08/30/introducing-sap-cloud-platform-content-agent-enhanced-transport-capabilities-for-sap-cloud-platform-integration-suite-content/)



<a name="loioa19f56fb4695459ca472877cd58581aa__section_bj1_h5z_mqb"/>

## SAP Solution Manager

For initial information on connecting your SAP Solution Manager system to various cloud services \(including Cloud Integration\), see [Integrating Cloud Services in SAP Solution Manager](https://help.sap.com/viewer/82f6dd44db4e4518aad4dfce00116fcf/7.2.12/en-US/c99b729e-ee22-4a19-a403-198f4870bc27.html).

