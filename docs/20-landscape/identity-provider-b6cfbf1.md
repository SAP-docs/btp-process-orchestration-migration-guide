<!-- loiob6cfbf1fc9434f66a3bd2b4a3f815308 -->

# Identity Provider

Learn more about identity providers and user governance in SAP BTP.



The users of SAP BTP are provided by identity providers. Customers can either use the default SAP identity provider \(accounts.sap.com\) with their email ID or can configure their own corporate identity provider \(e.g. SAP Identity and Authentication Service \(IAS\) or Azure AD\). If customers use an external Identity provider, they must configure a trust relationship between SAP BTP and the identity provider.

For more information on how to connect with different Active Directories, see the tutorial [Integrate Microsoft Azure AD with SAP BTP, Cloud Foundry environment](https://developers.sap.com/tutorials/cp-azure-ad-saml.html) and the blog [How to integrate Azure AD with SAP BTP, Cloud Foundry environment](https://blogs.sap.com/2019/03/07/how-to-integrate-azure-ad-with-sap-cloud-platform-cloud-foundry/).

Additionally, you can enable single sign-on using the Identity Authentication service and an external Active Directory as described in the following tutorials:

-   [Connect Azure Active Directory to Identity Authentication Service](https://developers.sap.com/tutorials/cp-ias-azure-ad.html)
-   [Register SAP BTP, Cloud Foundry Subaccount in Identity Authentication Service](https://developers.sap.com/tutorials/cp-ias-azure-ad-cf.html)

> ### Note:  
> Once the custom IDP configuration is complete, it's necessary to grant permissions to users for SAP BTP applications through the SAP BTP Cockpit before they try to access them. For more information, see [Configuring User Access to the Application](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/ed6033b2eabe4a64a20cce1e6076bacf.html).
> 
> You can find the different personas for administering the roles in [Persona](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/2937e5ca6ef448cfb21451a2461cc2a6.html) in the Cloud Integration documentation and in SAP Note [2872526](https://launchpad.support.sap.com/#/notes/2872526) on Roles in API Management.



<a name="loiob6cfbf1fc9434f66a3bd2b4a3f815308__section_gw3_jmd_mqb"/>

## User Governance

The global account and subaccounts get their users from identity providers. Administrators make sure that users can only access their dedicated subaccount by making sure that there's a dedicated trust relationship only between the identity providers and the respective subaccounts. Developers configure and deploy application-based security artifacts containing authorizations, and administrators assign these authorizations using the SAP BTP Cockpit.

The SAP Integration Suite is a bundle of services running on SAP BTP. The authorization groups, roles, and their assignments of the SAP Integration Suite are managed through the SAP BTP Cockpit and can be managed via web browser. There's also the option to perform Authorization Management using SAP BTP APIs.

Using [SAP BTP Authorization Management REST APIs](https://api.sap.com/api/AuthorizationAPI/overview) provides functionality to manage roles and their assignments to users. It’s not limited to SAP Integration Suite and can be extended to other subscriptions and services under SAP BTP subaccounts. These APIs can be used in cases where user assignment needs to happen in a controlled manner to enforce security policies, audit, and compliance from SAP GRC or other user management and governance solutions.

Authorization Management API – Operations:

-   Groups – Manage groups and their assignments to users and roles within the specified account.

-   Roles – Manage roles and their assignments to users and groups in the specified account and application.

-   Users – Manage role and group assignments to the specified user.


