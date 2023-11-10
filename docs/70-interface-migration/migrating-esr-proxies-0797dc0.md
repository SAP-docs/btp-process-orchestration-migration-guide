<!-- loio0797dc0e8ee64589803fd2194e59eb64 -->

# Migrating ESR Proxies

Migrate existing ESR proxies from the Enterprise Services Repository \(ESR\) to the Metadata Repository \(MDR\).

Use transaction *SPXNMIG* and report *SPROX\_MDR\_MIGRATION* to migrate existing ESR proxies to the MDR. The web services are then available locally in the backend system where they can be changed and extended.

> ### Note:  
> You don't have to migrate all your existing proxies from ESR to MDR. You only need to migration the proxies that you need to maintain the structure later.



<a name="loio0797dc0e8ee64589803fd2194e59eb64__section_dkt_2sf_ttb"/>

## Prerequisites

Before the migration, define which namespaces should be considered by assigning them to the MDR. Since MDR proxies and ESR proxies share the same namespaces, the system checks which namespaces should be assigned whenever a proxy object is to be generated.

1.  Open transaction *SPXNGENAPPL* to customize the default settings for namespace assignment.

    By default, ESR is considered for Business Suite systems and MDR for Business By Design.

2.  Maintain the list of namespaces by selecting *Backend Metadata Repository* as the *Generation Source*.

    Since wildcards are allowed, you can create a generic entry `*` that considers all valid namespaces.

3.  Save your changes.



<a name="loio0797dc0e8ee64589803fd2194e59eb64__section_owh_2sf_ttb"/>

## Steps

1.  In transaction *SPXNMIG*, define a namespace range and select *Execute*. If no namespace range is provided, all entries previously maintained in *SPXNGENAPPL* are used as selection.

2.  The system displays a list of all proxy objects that can be migrated, with information if additional steps are needed. It cross-checks the ESR object/namespace and MDR namespace assignment.

    Some object types cannot be migrated and are therefore not included in the list. See [Restrictions](migrating-esr-proxies-0797dc0.md#loio0797dc0e8ee64589803fd2194e59eb64__section_x55_dsf_ttb).

3.  Select *Migrate* to trigger the migration for the complete list, or a previously selected subset. Once the migration is finished, the results are displayed.




<a name="loio0797dc0e8ee64589803fd2194e59eb64__section_x55_dsf_ttb"/>

## Restrictions

The following objects cannot be migrated and are therefore not displayed in the list of proxies to be migrated:

-   **External definitions**

    Migrating ESR interfaces based on external definitions is not supported. They can be replaced by an external consumer/provider generated from WSDL directly in backend. A new ABAP name for the class is then generated so the previous usage should be reviewed.

-   **SAP namespace \(\*.sap.com\)**

    Objects from SAP namespace cannot be migrated.

-   **Inactive proxy objects**

Additionally, **inline types** cannot be migrated to the MDR automatically. You can migrate them manually by using one of the following options:

-   Change inline types to global types in the ESR and regenerating them to become global types. Instead of defining dependent elements inline, you need to create these elements separately and refer to them within the parent element. The following examples show the difference between an inline type and a global type:

    -   For the **inline type**, all XSD elements are contained within one sequence:

        ```
        <xsd:complexType name="dt_inline"> 
        	<xsd:sequence> 
        		<xsd:element name="tier_1">
        			<xsd:complexType>
        				<xsd:sequence> 
        					<xsd:element name="tier_2"> 
        						<xsd:complexType>
        							<xsd:sequence>
        								<xsd:element name="integer" type="xsd:integer"/>
        							</xsd:sequence>
        						</xsd:complexType>
        					</xsd:element>
        				</xsd:sequence>
        			</xsd:complexType>
        		</xsd:element>
        	</xsd:sequence> 
        </xsd:complexType> 
        ```

    -   However, the **global type** consists of three different XSD parts:

        ```
        <xsd:complexType name="dt_global"> 
        	<xsd:sequence> 
        		<xsd:element name="tier_1" type="dt_tier1"/> 
        	</xsd:sequence> 
        </xsd:complexType> 
        <xsd:complexType name="dt_tier1"> 
        	<xsd:sequence> 
        		<xsd:element name="tier_2" type="dt_tier2"/> 
        	</xsd:sequence> 
        </xsd:complexType> 
        <xsd:complexType name="dt_tier2"> 
        	<xsd:sequence> 
        		<xsd:element name="integer" type="xsd:integer"/> 
        	</xsd:sequence> 
        </xsd:complexType> 
        ```


-   **For systems classified as `SAP` only:** 

    Using the migration tool, you can convert inline types semiautomatically with the button *Convert Inlines*. This means that inline types can be converted into global types by specifying a global name for each inline type the tool needs to generate a global type for. See SAP Note [3313582](https://me.sap.com/notes/3313582).

    > ### Note:  
    > If this option is used, a migration back to ESR is not possible.




<a name="loio0797dc0e8ee64589803fd2194e59eb64__section_qd1_dsf_ttb"/>

## New Interfaces

For new interfaces, the creation of objects should be done directly in the backend. You can use wizards for this task.

For more information, see:

-   [Modeling Web Service Objects in the Backend](https://help.sap.com/docs/ABAP_PLATFORM_2021/684cffda9cbc4187ad7dad790b03b983/ef66cfa6ff2445d3ae51f137d924277a.html)

-   [Enterprise Services Wizard](https://help.sap.com/docs/ABAP_PLATFORM_2021/684cffda9cbc4187ad7dad790b03b983/33a3eb8c7ece4fb4b4cb6ac3f4f84c15.html)

-   [MDR: Defining web services from ABAP without requiring PI](https://blogs.sap.com/2012/05/14/mdr-defining-web-services-from-abap-without-requiring-pi/)

