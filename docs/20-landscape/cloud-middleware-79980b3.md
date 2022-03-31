<!-- loio79980b3118184318a3aefcb133713eb5 -->

# Cloud Middleware

Learn more about possible communications between Cloud Integration and an on-premise system.

> ### Restriction:  
> Some features mentioned on this site are planned for the future and are subject to change. For more information on new features and future releases, access the [Road Map Explorer](http://help.sap.com/disclaimer?site=https://roadmaps.sap.com/board?CB=901B0ED1A0641ED8B4D1230C6387E0DB&range=CURRENT-LAST) and the [What's New section](https://help.sap.com/doc/7ac9748e20cf453a94efda779542d34e/sap.cp.integration.suite/en-US/c10c21cd7c684f0885fa8b5db2982284.html) of SAP Integration Suite.

A migration from SAP Process Orchestration to SAP Integration Suite means moving to the cloud, which requires that all on-premise systems must be able to communicate with the Internet. With the planned release of the on-premise runtime of SAP Integration Suite \(hybrid deployment option\), this may no longer be applicable. In that case, it means developing and operating in the cloud, and executing on-premise. Since the hybrid deployment option isn't available yet, we'll focus on the cloud-only version. The guide will be updated when the hybrid deployment option is available.

**[On-premise system to Cloud Integration](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/0f92842bee8a46a9890c8b02b6bec05a.html)**

-   The on-premise system must be able to establish an HTTPS connection to Cloud Integration \(SSL Handshake, Authorization, and Authentication\).

-   If any proxies or firewall changes are required, this should be considered and recorded as an infrastructure change requirement.


Since Cloud Integration is a cloud solution, security is a key aspect and therefore SSL protocol is a must.

**[Cloud Integration to on-premise system](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/92dd2a6fdb6045f98d23c828d1567fef.html)**

The on-premise system must be able to receive a message from the Internet, using one of several options:

-   [Cloud Connector](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/e6c7616abb5710148cfcf3e75d96d596.html)

-   [Reverse Proxy](https://help.sap.com/viewer/683d6a1797a34730a6e005d1e8de6f22/7.5.latest/en-US/488fe37933114e6fe10000000a421937.html) which requires allowlisting of IP range at customer DC


There might also be some challenges regarding security that have to be evaluated for on-premise systems and are described in [Security](../40-security/security-dd0fb21.md).

