<!-- loioefce2565d2e04165a99bf6c607657217 -->

# Connected Systems and Protocols

When analyzing your SAP Process Orchestration system, extracting as many details as possible with regards to what systems it connects to and which transport and messaging protocols it uses is the first step.

This information about connected systems and protocols can then be further analyzed to identify any issues or challenges ahead, and to allow for an estimation of the effort required to migrate to a Cloud Integration tenant solution.

> ### Restriction:  
> Some features mentioned on this site are planned for the future and are subject to change. For more information on new features and future releases, access the [Road Map Explorer](http://help.sap.com/disclaimer?site=https://roadmaps.sap.com/board?CB=901B0ED1A0641ED8B4D1230C6387E0DB&range=CURRENT-LAST) and the [What's New section](https://help.sap.com/doc/7ac9748e20cf453a94efda779542d34e/sap.cp.integration.suite/en-US/c10c21cd7c684f0885fa8b5db2982284.html) of SAP Integration Suite.

To extract this information, the following techniques can be used:

1.  Utilize the standard Web Services that are available as part of the Integration Directory API. For details on this method, see the blog [SAP PI/PO Directory API: Extract detailed Communication Channel configurations into an Excel sheet without custom codes/macros](https://blogs.sap.com/2017/11/07/sap-pipo-directory-api-extract-detailed-communication-channel-configurations-into-an-excel-sheet-without-custom-codesmacros/).

2.  Utilize the upcoming SAP PI/PO Assessment Tool: Data Extraction Utility. This tool provides the capability to extract not only the communication channel data, but also details regarding each integrated configuration object, as well as the design time artifacts such as operation mappings and message mappings. It uses a Java Swing-based UI to provide a more user-friendly approach to extracting the data. Connectivity to your SAP Process Orchestration system is defined using the *Settings* dialog.


