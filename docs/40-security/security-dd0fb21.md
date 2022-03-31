<!-- loiodd0fb21d47c54fff9ccab9667f3b4de7 -->

# Security

Discover the important aspects regarding security that must be evaluated before migrating from SAP Process Orchestration to Cloud Integration.

Using a cloud-based integration platform imposes dedicated security requirements on the software vendor \(SAP\) that hosts the platform, as well as on the customers who use the platform. Customers who use Cloud Integration agree that a significant part of their \(and their customers’\) sensitive data is processed by and stored within an infrastructure not owned by themselves. The core task of an integration platform is to serve as the transit place for messages that can contain sensitive customer data. First and foremost, these messages must be protected against eavesdropping and unauthorized access.

Therefore, the integration platform must fulfill the following main requirements:

-   The integration infrastructure is already designed and built in such a way that it meets the highest security standards. For more information on compliance, visit the [SAP Trust Center](https://www.sap.com/about/trust-center/certification-compliance.html).

    It must be guaranteed that the technical system landscape, the communication between the components of the integration platform, and the storage locations of messages are secure.

-   The processes related to the usage of Cloud Integration meet the highest security standards.

    These processes include processes at SAP related to the development and upgrade of the Cloud Integration software, the processes related to the provisioning and operation of the customers' virtual environment by the infrastructure provider, and the customer onboarding process during which customers set up secure connections between their infrastructure and SAP's integration platform.

-   Customers have several options to configure how messages are exchanged within an integration scenario so that the involved data is protected at the highest level.

    When designing integration flows, customers can choose between several options to protect messages by establishing secure communication channels \(transport-level security\) and by configuring digital encryption and digital signing of messages \(message-level security\).


For full help information on the security capabilities of Cloud Integration in the Cloud Foundry environment, see [Security, Cloud Foundry Environment](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/eb9923e8c533493997e233286cfa1bc7.html).

For access to the recommended Learning Journey to learn all about security from an SAP BTP perspective, go to [Security with SAP BTP](https://help.sap.com/doc/221f8f84afef43d29ad37ef2af0c4adf/HP_2.0/en-US/69aca66b45a74a73b4cc0efddd6ae63f.html).



<a name="loiodd0fb21d47c54fff9ccab9667f3b4de7__section_cpr_lxd_mqb"/>

## Securing User Access to Cloud Integration

A customer can decide to either use the identity provider [SAP ID service](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/LATEST/en-US/d6a8db70bdde459f92f2837349f95090.html) or add their own compatible identity provider such as Microsoft Azure Active Directory. The SAP ID service is initially used to authenticate that a particular user is who they claim to be by the user entering credentials \(such as a username and password\) to provide proof. Once authentication has been verified, the next stage \(authorization check\) takes place to determine what access to features and functions the user has for a particular application.

Cloud applications hosted on the SAP BTP typically use role-based access control. This means that authorizations to access specific applications \(such as Cloud Integration\) and execute specific tasks \(for example, Create and Edit Artifacts, Deploy Security Material, Monitor Integration Flows\) are provided to each user through the assignment of roles and role collections.

The provision of roles and role collections to users is a task typically performed by a Tenant Administrator using the security tools provided on the SAP BTP Cockpit. For detailed information on how to configure user access to the Cloud Integration application by assignment of roles and role collections, see [Configuring User Access to the Application](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/ed6033b2eabe4a64a20cce1e6076bacf.html).

The help documentation on [Tasks and Permissions](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/fda781c59e4b46a390ce5b409f60365e.html) provides a detailed table of the roles and roles collections available as standard to control access to each specific task and feature within Cloud Integration. The table provides the corresponding information for both the Cloud Foundry and the Neo environment.

-   **[Managing Security Material in Cloud Integration](managing-security-material-in-cloud-integration-09ec016.md "To securely transmit messages from a source system to a target system via middleware
		such as Cloud Integration, a number of key types of security components must be stored and
		managed securely on each Cloud Integration tenant.")**  
To securely transmit messages from a source system to a target system via middleware such as Cloud Integration, a number of key types of security components must be stored and managed securely on each Cloud Integration tenant.
-   **[Using Security Material in Integration Flows](using-security-material-in-integration-flows-626f672.md "")**  

-   **[Managing Destinations in SAP BTP Cockpit](managing-destinations-in-sap-btp-cockpit-4a8e98d.md "")**  


