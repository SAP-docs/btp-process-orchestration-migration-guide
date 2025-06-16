<!-- loio05c719fe4b3545c7bf804a8440ec9e6a -->

# Migration Strategy for B2B Interfaces

Plan, prepare, and implement a migration strategy for B2B integration scenarios using SAP Integration Suite. You can evaluate, analyze, and migrate content with the option of using migration tooling and prepackaged integration content.

1.  **Evaluate** your current state

    -   Evaluate the number and complexity of your integration scenarios for migration using [Migration Assessment](https://help.sap.com/docs/SAP_INTEGRATION_SUITE/51ab953548be4459bfe8539ecaeee98d/5c5e50ee2d644cc59d864409d5b7871c.html?locale=en-US&version=CLOUD) or optional advisory services .

    -   Analyze the current and the target landscape, for example, using the [SAP Integration Solution Advisory Methodology](https://help.sap.com/docs/link-disclaimer?site=https%3A%2F%2Fblogs.sap.com%2F2019%2F02%2F24%2Fintegration-solution-advisory-methodology-isa-m-define-integration-guidelines-for-your-organization%2F) . as well p Plan the number of systems \(2 or 3-tier\) foreseen you want to use for the B2B content lifecycle.

    -   Create a high-level architecture for the connected systems and list these systems with the B2B related communication protocols, adapters, needed certificates and authentication methods \(for example, AS2 with/without authentication\) used.

    -   Check if there are other Verify the different options offered available to for integrating the scenarios based on the published integration packages on the [SAP Business Accelerator Hub](http://hub.sap.com), such as Cloud Trading Partner Management or Integration Advisor.


2.  **Plan** your migration by creating a strategy

    -   Review the options for migrating B2B integration scenarios:

        -   Migrate semi-automatically \([Migration Tooling](https://help.sap.com/docs/SAP_INTEGRATION_SUITE/51ab953548be4459bfe8539ecaeee98d/60610163aec44849ac4783c92fb2e55c.html?locale=en-US&version=CLOUD), [Import Mapping Artifacts](https://help.sap.com/docs/help/90c8ad90cb684ee5979856093efe7462/1e83249a0b444a268f1df3dd3c806ce3.html?locale=en-US#import-mapping-artifacts)\)

        -   Redesign scenarios \(use standard integration packages from [SAP Business Accelerator Hub](http://hub.sap.com), learn what interfaces aren't covered by the migration tooling\)


    -   Consider business and functional requirements while having the highest possible reuse and scalability to adapt and onboard new businesses. Also, consider the availability of features of B2B capabilities of Trading Partner Management, Integration Advisor, and Cloud Integration.


3.  **Prepare and Implement**

    -   Set up and activate the capabilities within SAP Integration Suite:

        -   Configure authorizations and roles SAP Integration Suite

        -   Activate Trading Partner Management, including Integration Advisor


    -   Import or configure artifacts \(certificates and user credentials, for example, adapter-specific user accounts like AS2 own IDs\)

    -   Setup Cloud Connector \(if required\)

    -   Test the connectivity to the connected applications \(optional\)

    -   Setup implementation guidelines and architecture if you plan to redesign integration scenarios

    -   Migrate content

        -   Configure standard content \(see the pre-packaged integration content for [Trading Partner Management](https://api.sap.com/package/CloudIntegrationTradingPartnerManagement/integrationflow) or [Integration Advisor](https://api.sap.com/package/ICAPrepackagedContent/integrationflow)\)

        -   Import content of [Message Mapping](https://help.sap.com/docs/help/90c8ad90cb684ee5979856093efe7462/1e83249a0b444a268f1df3dd3c806ce3.html?locale=en-US#loio1e83249a0b444a268f1df3dd3c806ce3__section_glt_51j_qqb) , [Function Library](https://blogs.sap.com/2023/05/30/sap-integration-suite-import-pi-po-function-library-into-cloud-integration/), [Message Type / Data Type](https://blogs.sap.com/2023/06/08/sap-integration-suite-import-pi-po-datatype-and-messagetype-objects-into-sap-cloud-integration/) 

        -   Reimplement redesigned interfaces and objects not supported by the migration tooling



4.  **Test**

    Run test phases to test the migrated content \(see the blog [Int4 Suite for SAP BTP Integration Suite testing fully integrated with SAP Cloud ALM](https://blogs.sap.com/2023/07/06/int4-suite-for-sap-btp-integration-suite-testing-fully-integrated-with-sap-cloud-alm/)\).


