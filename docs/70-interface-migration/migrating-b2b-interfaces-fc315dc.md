<!-- loiofc315dcd716d4a48bb7bb2db6eb1e0e6 -->

# Migrating B2B Interfaces

Learn how to migrate B2B interfaces from SAP Process Integration and SAP Process Orchestration to SAP Integration Suite.



<a name="loiofc315dcd716d4a48bb7bb2db6eb1e0e6__section_fxp_fnq_m2c"/>

## B2B Add-On for SAP Process Integration

In SAP Process Integration, the **B2B \(business-to-business\) add-on** runs on the SAP Process Integration Adapter Framework, which is based on the Java Connector Architecture \(JCA\). Accordingly, its capabilities are being used for enabling the common message delivery options \(best-effort, exactly-once, exactly-once-in-order\), an automatic retry mechanism and information logging. The configuration of B2B adapters, monitoring and operations is done in the same way as for other adapters of SAP Process Integration.

The B2B add-on comes with the **AS2 adapter**, **OFTP adapter**, and **X.400 adapter**, which all support specific B2B messaging protocols.

The B2B add-on also contains a set of adapter modules allowing the conversion of native Electronic Data Interchange \(EDI\) messages into EDI-XML messages and the other way around. In addition to that, a plain text module is being provided for handling custom B2B message formats in the same way. This content conversion is beneficial as SAP Process Integration is optimized for processing XML messages. They support all common message types and versions of the following B2B/EDI standards:

-   ANSI X.12
-   EDIFACT
-   EANCOM
-   TRADACOM
-   Odette
-   VDA
-   Custom Format

At the chain of business process between business or trading partners, data is exchanged by leveraging standard B2B protocols. For example, you can exchange purchase orders using ASC X12 or UN/EDIFACT files in a design-to-operate process that integrates a manufacturer with suppliers.

The end-to-end flow of a B2B integration project includes defining and implementing interfaces for different partners, creating mappings between those interfaces, and setting up the integration scenarios.

For more information, see the [SAP Process Integration, business-to-business add-on master guide](https://help.sap.com/doc/6fdd13c4265444adbc71a8aa08c1f2d1/2.0.2/en-US/loioe048f53dffe343ef9d42aebd1292fc16.pdf) and [Trading Partner Management](https://help.sap.com/docs/SAP_PROCESS_INTEGRATION,_BUSINESS-TO-BUSINESS_ADD-ON/22e34f550ba84f20b35b7652ba94ef9c/e86a1c520f309a33e10000000a44538d.html) in the B2B add-on configuration guide.



<a name="loiofc315dcd716d4a48bb7bb2db6eb1e0e6__section_vvw_jk2_p2c"/>

## Trading Partner Management in SAP Integration Suite

Business-to-business \(B2B\) scenarios describe the collaborative process of business transactions between your company and a trading partner. Clearly defined accountability and explicit, transparent arrangements ensure that this collaboration runs well.

With the Trading Partner Management capability within SAP Integration Suite, you can define and maintain individually agreed B2B scenarios between yourself and your trading partners. Individually means that there should be an efficient way to define the individual trading partner’s communication parameters, the kind of business transactions \(business documents\) should be exchanged in a 2-way \(request-response\) or 1-way \(notifications\) as well as how these business transactions must be mapped so that these fulfill your and your trading partner's requirements.

To learn more about Trading Partner Management, check out the following resources:

-   For an overview of the **terms and components** used within Trading Partner Management, like company, trading partner, and trading partner agreement, see [Understanding the Basic Concepts](https://help.sap.com/docs/integration-suite/sap-integration-suite/understanding-basic-concepts).
-   To learn how to **create a trading partner agreement template** and a **trading partner agreement**, see [Trading Partner Agreement](https://help.sap.com/docs/integration-suite/sap-integration-suite/creating-trading-partner-agreement). Pay attention to the mapping step choice using Process Direct for alternative mappings other than from Integration Advisor.


-   **[Migration Strategy for B2B Interfaces](migration-strategy-for-b2b-interfaces-05c719f.md "Plan, prepare, and implement a migration strategy for B2B integration scenarios using
		SAP Integration Suite. You can evaluate, analyze, and migrate content with the option of
		using migration tooling and prepackaged integration content.")**  
Plan, prepare, and implement a migration strategy for B2B integration scenarios using SAP Integration Suite. You can evaluate, analyze, and migrate content with the option of using migration tooling and prepackaged integration content.
-   **[B2B Migration Approaches](b2b-migration-approaches-6d6c139.md "Learn about the different options that you have for migrating your B2B
		interfaces.")**  
Learn about the different options that you have for migrating your B2B interfaces.
-   **[Limitations & Workarounds for B2B Migration](limitations-workarounds-for-b2b-migration-75be745.md "")**  


**Related Information**  


[Migration Tooling](https://help.sap.com/docs/integration-suite/sap-integration-suite/migration-tooling)

[Trading Partner Management](https://help.sap.com/docs/integration-suite/sap-integration-suite/trading-partner-management)

[Manage B2B Scenarios Effectively with SAP Integration Suite](https://learning.sap.com/courses/manage-b2b-scenarios-effectively-with-sap-integration-suite)

