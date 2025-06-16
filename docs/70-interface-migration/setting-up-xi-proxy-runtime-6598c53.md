<!-- loio6598c5349d59417b97b2200a07b38e12 -->

# Setting Up XI Proxy Runtime

Perform the following steps to set up the XI proxy runtime.



<a name="loio6598c5349d59417b97b2200a07b38e12__prereq_oxg_t4f_mxb"/>

## Prerequisites

If it's your first time setting up the outbound connectivity from SAP ERP to Cloud Integration, import the server certificates as described in SAP Note [3193513](https://me.sap.com/notes/3193513).



<a name="loio6598c5349d59417b97b2200a07b38e12__context_znv_b4f_mxb"/>

## Context

While SAP Process Orchestration uses a single RFC destination for all outbound communication from the SAP system to the SAP Process Orchestration system, Cloud Integration requires the creation of a unique destination for each interface. The destination must be configured with the target endpoint of the integration flow once it's been deployed on the Cloud Integration tenant.

You can also implement a router integration flow to receive multiples messages in a single-entry point. See [Cloud Integration - Configuring Scenario with XI Sender handling Multiple Interfaces](https://blogs.sap.com/2018/12/04/cloud-integration-configuring-scenario-with-xi-sender-handling-multiple-interfaces/).



<a name="loio6598c5349d59417b97b2200a07b38e12__steps_sjs_c4f_mxb"/>

## Procedure

1.  To create an RFC destination, in your SAP system, run transaction *SM59* and choose *Create*.

2.  In the dialog, enter following details:


    <table>
    <tr>
    <th valign="top">

    Field
    
    </th>
    <th valign="top">

    Value
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    *RFC Destination*
    
    </td>
    <td valign="top">
    
    Enter an RFC destination name, for example, `CI_XI_<Interface Identification>`.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Connection Type*
    
    </td>
    <td valign="top">
    
    `G HTTP connection to external server`
    
    </td>
    </tr>
    </table>
    
3.  In the tab *Logon & Security*, enter the required security settings.

    If you're connecting to Cloud Integration using basic authentication, see [Creating Service Instance and Service Key for Inbound Authentication](https://help.sap.com/docs/CLOUD_INTEGRATION/368c481cd6954bdfa5d0435479fd4eaf/19af5e205fe14af6a4f8a9fd80d4dc92.html).

4.  Next, you need to create a sender/receiver definition in the sender backend system. It determines which interfaces are sent through the RFC destination you created previously.

    Run transaction *SXMSIF* and choose *New Entries*.

5.  Enter the following details for your new sender/receiver definition:


    <table>
    <tr>
    <th valign="top">

    Field
    
    </th>
    <th valign="top">

    Description
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    *Sender/Receiver ID*
    
    </td>
    <td valign="top">
    
    Identification of your interface, for example `BP_BULK`
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Description*
    
    </td>
    <td valign="top">
    
    Description of your settings
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Agency*
    
    </td>
    <td valign="top">
    
    Sender agency identification, if applicable.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Schema*
    
    </td>
    <td valign="top">
    
    Sender schema identification, if applicable.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Party*
    
    </td>
    <td valign="top">
    
    Sender party identification, if applicable
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Component*
    
    </td>
    <td valign="top">
    
    Sender business system/component name
    
    </td>
    </tr>
    </table>
    
6.  In section *Message Category*, select *Request* and enter the following details:


    <table>
    <tr>
    <th valign="top">

    Field
    
    </th>
    <th valign="top">

    Description
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    *Interface Name*
    
    </td>
    <td valign="top">
    
    Identification of the sender service interface, for example `BusinessPartnerSUITEBulkReplicateRequest_Out`
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Interface Namespace*
    
    </td>
    <td valign="top">
    
    Identification of the service interface namespace, for example, `http://sap.com/xi/SAP_BS_FND/MDG/Global2`
    
    </td>
    </tr>
    </table>
    
    > ### Note:  
    > You can use wildcard characters, like **\***, to indicate multiple possible characters when filling out the fields.

7.  Next, you can continue with configuring the interface-specific runtime.

    Run transaction *SXMB\_ADMIN* and, in section *Configuration*, choose *Integration Engine Configuration*.

8.  To view the list of parameters for the integration engine, choose *Configuration*.

    Choose *New Entries* and enter the following details:


    <table>
    <tr>
    <th valign="top">

    Field
    
    </th>
    <th valign="top">

    Value
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    *Category*
    
    </td>
    <td valign="top">
    
    `RUNTIME`
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Parameters*
    
    </td>
    <td valign="top">
    
    `IS_URL` 
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Subparameter*
    
    </td>
    <td valign="top">
    
    Enter the sender/receiver ID
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    *Current Value*
    
    </td>
    <td valign="top">
    
    `dest://<Destination ID>`
    
    </td>
    </tr>
    </table>
    
9.  Finally, if you use the Cloud Integration runtime and no SLD business system is connected to your SAP system, verify that an entry in table `LCRT_CLNTCACHE` represents the business system of your SAP system.

    If the business system name isn't represented correctly, use the report `SXMS_BS_CACHE` to create or update entries in `LCRT_CLNTCACHE`.

    Execute the report by running transaction *SE38* and maintain an entry like the following:


    <table>
    <tr>
    <th valign="top">

    ID
    
    </th>
    <th valign="top">

    Creation Date
    
    </th>
    <th valign="top">

    Business System
    
    </th>
    <th valign="top">

    Role
    
    </th>
    <th valign="top">

    Caption
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    `<SID><CLIENT>`, for example `PRD100`
    
    </td>
    <td valign="top">
    
    Date of creation
    
    </td>
    <td valign="top">
    
    Identification of your choice, for example, `PRDCLNT100`
    
    </td>
    <td valign="top">
    
    `LOC`
    
    </td>
    <td valign="top">
    
    Caption of your choice, for example, `PRDCLNT100`
    
    </td>
    </tr>
    </table>
    
    You only have to perform this action once.

    > ### Note:  
    > During the lifetime of the current client, the business system name of the technical system doesn't change. If the SLD can't be reached the first time it's called on a given day, problems in the application can lead to a system standstill.
    > 
    > To prevent this, **deactivate the daily SLD access** using report **SXMS\_BS\_CACHE**. This way, the business system name is always read from the table `LCRT_CLNTCACHE`. See SAP Note [3547972](https://me.sap.com/notes/3547972).


