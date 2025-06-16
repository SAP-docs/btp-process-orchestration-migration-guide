<!-- loio6d6c139c67f24c7e90f1ddd78c88bdb1 -->

# B2B Migration Approaches

Learn about the different options that you have for migrating your B2B interfaces.



<a name="loio6d6c139c67f24c7e90f1ddd78c88bdb1__section_vlq_wf2_p2c"/>

## B2B Interface Migration Categorizations

Scenarios can be categorized the based on their direction:

-   **Inbound scenarios**: Trading Partner \> Sender Adapter \> Module Processor \> Messaging System \> Mapping Runtime \> Messaging System \> Module Processor \> Receiver Adapter \> Own System
-   **Outbound scenarios**: Own System \> Sender Adapter \> Module Processor \> Messaging System \> Mapping Runtime \> Messaging System \> Module Processor \> Receiver Adapter \> Trading Partner



<a name="loio6d6c139c67f24c7e90f1ddd78c88bdb1__section_nvz_xf2_p2c"/>

## B2B Interface Migration Approaches

The following migration approaches give you an overview of a potential combination of different capabilities fit best for the majority of the B2B use cases. Hybrid approaches are possible given the flexible options of the underlying feature set of SAP Integration Suite and its capabilities of the B2B domain.



### B2B Migration to Cloud Integration

Scenarios with messages without frequent changes can be migrated using a 1:1 migration path. In this case, the recommended migration is directly to Cloud Integration without Trading Partner Management or Integration Advisor.

In a phased approach, first you can shift your legacy content to SAP Integration Suite, then lift the scenarios to Trading Partner Management and Integration Advisor.



### B2B Migration to Trading Partner Management with Integration Advisor

Scenarios with messages with frequent changes, new messages, and scenarios that must be incorporated with additional B2B libraries and trading partner onboardings planned can be migrated to Trading Partner Management and Integration Advisor.



### B2B Migration to Trading Partner Management without Integration Advisor

Scenarios with messages foreseen for frequent changes and the module Trading Partner Management is used \(not mandatory\) can be migrated to Trading Partner Management and Cloud Integration with partial use of Integration Advisor.

-   **[Migration to Cloud Integration](migration-to-cloud-integration-8e2cbe0.md "Learn how to migrate your B2B scenarios to Cloud Integration use cases that are based on
		sample scenarios.")**  
Learn how to migrate your B2B scenarios to Cloud Integration use cases that are based on sample scenarios.
-   **[Migration to Trading Partner Management, using Integration Advisor](migration-to-trading-partner-management-using-integration-advisor-0c7c320.md "Learn how to migrate your B2B scenarios to Trading Partner Management, with partial use
		of Integration Advisor.")**  
Learn how to migrate your B2B scenarios to Trading Partner Management, with partial use of Integration Advisor.

**Related Information**  


[Migration to Cloud Integration](migration-to-cloud-integration-8e2cbe0.md "Learn how to migrate your B2B scenarios to Cloud Integration use cases that are based on sample scenarios.")

[Migration to Trading Partner Management, using Integration Advisor](migration-to-trading-partner-management-using-integration-advisor-0c7c320.md "Learn how to migrate your B2B scenarios to Trading Partner Management, with partial use of Integration Advisor.")

