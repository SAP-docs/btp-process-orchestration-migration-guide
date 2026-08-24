<!-- loiob6cfbf1fc9434f66a3bd2b4a3f815308 -->

# Identity Provider

Learn more about identity providers and user governance in SAP BTP.



The users of SAP BTP are provided by identity providers. You can either use the default SAP identity provider \(SAP ID service\) with your email ID or configure your own corporate identity provider \(for example, SAP Cloud Identity Services - Identity and Authentication service or Azure Active Directory\). If you use an external identity provider, you must configure a trust relationship between SAP BTP and the identity provider.

For more information on how to connect with different Active Directory services, see the blog [How to integration Azure AD with SAP BTP, Cloud Foundry environment](https://help.sap.com/docs/link-disclaimer?site=https%3A%2F%2Fblogs.sap.com%2F2019%2F03%2F07%2Fhow-to-integrate-azure-ad-with-sap-cloud-platform-cloud-foundry%2F).

Additionally, you can enable single sign-on using the Identity Authentication service and an external Active Directory as described in the tutorial [Connect Azure Active Directory to Identity Authentication Service](https://developers.sap.com/tutorials/cp-ias-azure-ad.html).

> ### Note:  
> Once the custom IDP configuration is complete, it's necessary to grant permissions to users for SAP BTP applications through the SAP BTP cockpit before they try to access them. See [Configuring User Access to the Application](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/ed6033b2eabe4a64a20cce1e6076bacf.html).
> 
> You can find the different personas for administering the roles in [Users and Roles in SAP BTP](https://help.sap.com/docs/btp/sap-business-technology-platform/users-and-roles) or in [SAP API Management Standalone Service-Tasks and Corresponding Roles](https://help.sap.com/docs/sap-api-management/sap-api-management-iat/assign-user-roles)



<a name="loiob6cfbf1fc9434f66a3bd2b4a3f815308__section_gw3_jmd_mqb"/>

## User Governance

The global account and subaccounts get their users from identity providers. Administrators make sure that users can only access their dedicated subaccount by ensuring that there's a dedicated trust relationship only between the identity providers and the respective subaccounts. Developers configure and deploy application-based security artifacts containing authorizations, and administrators assign these authorizations using the SAP BTP cockpit.

The SAP Integration Suite is a bundle of services running on SAP BTP. The authorization groups, roles, and their assignments of the SAP Integration Suite are managed through the SAP BTP cockpit and can be managed via web browser. There's also the option to perform Authorization Management using SAP BTP APIs.

Using [SAP BTP Authorization Management REST APIs](https://api.sap.com/api/AuthorizationAPI/overview) provides functionality to manage roles and their assignments to users. It’s not limited to SAP Integration Suite and can be extended to other subscriptions and services under SAP BTP subaccounts. These APIs can be used in cases where user assignment needs to happen in a controlled manner to enforce security policies, audit, and compliance from SAP GRC or other user management and governance solutions.

Authorization Management API – Operations:

-   Groups – Manage groups and their assignments to users and roles within the specified account.

-   Roles – Manage roles and their assignments to users and groups in the specified account and application.

-   Users – Manage role and group assignments to the specified user.


