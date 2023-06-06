<!-- loio0c666a74404e49a897d36f12e814a412 -->

# Operation

Learn more about the ways both SAP Process Orchestration and Cloud Integration operate, for example when deploying interfaces, performing connectivity tests, logging files, or working with APIs to automate operations.



<a name="loio0c666a74404e49a897d36f12e814a412__section_fdq_tlx_lqb"/>

## Deploying Interface

In SAP Process Orchestration, once you activate your [Integrated Configuration](https://help.sap.com/viewer/d0a0a7cb51dc40529bfcac724dd05796/7.5.latest/en-US/48cfac399bf23e49e10000000a421937.html) object, your interface is up and running.

In Cloud Integration, once you finish the design of your integration flow, you must deploy the artifact. After deployment, you can perform some tasks such as restarting the artifact, undeploying the artifact, and downloading the deployed artifact to your PC. The last option is useful when you need to recover the deployed version of your integration flow.



<a name="loio0c666a74404e49a897d36f12e814a412__section_wqy_h2d_mqb"/>

## Connectivity Tests

A feature introduced in Cloud Integration is the connectivity tests, which allow you to perform some simple test connections in different protocols to assure the connectivity with the target system. In TLS protocol, for example, you can download the full certificate chain that should be imported in Cloud Integration keystore most of the times. For more information, see [Performing Connectivity Tests](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/d5b2faebc03b4c27b664a35c65ad5a2d.html).

In SAP Process Orchestration, after activating your communication channel in Integration Directory, for some of them \(see SAP Note [1890633](https://launchpad.support.sap.com/#/notes/1890633)\) you can also navigate to the Communication Channel Monitor and try the ping channel, which provides the result of a basic connectivity test. Another option, especially for TLS protocol, is to use [XPI Inspector tool](https://wiki.scn.sap.com/wiki/display/XI/Tracing+PI+issues+with+XPI+Inspector+tool) to have access to the certificate chain that should be imported to the keystore. XPI Inspector offers a full trace and dump during a connectivity test, which helps to analyze and solve connectivity issues. The only exception concerns the RFC adapter, for which you need to maintain an HTTP destination in the SAP BTP tenant as described in [Creating an RFC Destination](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/3b55fa7b83874b5ca3b6b6b5998a73f6.html).



<a name="loio0c666a74404e49a897d36f12e814a412__section_wfd_32d_mqb"/>

## Log Files

Both SAP Process Orchestration and Cloud Integration provide logging mechanisms to support the monitoring and troubleshooting of interfaces that are executed on the middleware systems. As Cloud Integration is a cloud-based service, the persistence of logs and any attachments to logs differs from SAP Process Orchestration in that the duration of persistence is much shorter and the deletion of logs lies outside of the control of the customer.

SAP Process Orchestration stores activities of system, integration, and database events. In the Log Viewer, you can see the technical detail system status. Based on information in system logs, you can check, monitor, and investigate any issues and possible root causes.

The following system logs are stored with multiseverity:

-   Fatal error messages

-   Error messages

-   Warning messages

-   Information messages

-   Path messages

-   Debug messages


You can access the Log Viewer by going to *SAP NetWeaver Administrator* \> *Troubleshooting* \> *Logs and Traces* \> *Log Viewer*.

For Cloud Integration, you must use the SAP Audit Log service to monitor the security-relevant chronological records such as events, activity logs, and application logs. For more information, see [Audit Logging in the Cloud Foundry Environment](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/f92c86ab11f6474ea5579d839051c334.html). You can also use the Audit Log Retrieval API to extract possessed by the tenant. For more information, access the [SAP Business Accelerator Hub](https://api.sap.com/api/CFAuditLogRetrievalAPI/overview).



<a name="loio0c666a74404e49a897d36f12e814a412__section_ly4_h2d_mqb"/>

## Automate Operations Using APIs

Most of these administrative tasks described for Cloud Integration and SAP Process Orchestration, such as read integration messages, security artifacts, log files, and communication channels, are available in APIs to be used externally. This way, you can automate some procedures using custom script or even build your own toolset. In Cloud Integration, the most common usage is to build your own alert notification mechanism, but you can even create a procedure to automatically maintain some objects in the tenant keystore \(e.g. key pair, certificate chain\).

To access the most updated list of APIs for Cloud Integration, visit the [SAP Business Accelerator Hub](https://api.sap.com/package/CloudIntegrationAPI/odata). The capabilities include:

-   Manage and query integration artifacts at design time and runtime.

-   Access and query HTTP and trace log files on a tenant.

-   Get an overview of the messages processed on a tenant and get the details for individual messages.

-   Access message store entries, JMS resources, and data store entries.

-   Access the [Partner Directory](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/6e00412aebd549f8b5771c9397c08c5d.html) to maintain and manage data.

-   Access and manage security content to configure secure connections with remote systems.


For SAP Process Orchestration, there's official documentation for some available APIs, for example for [Integration Directory](https://help.sap.com/viewer/d0a0a7cb51dc40529bfcac724dd05796/7.5.latest/en-US/48d127e1e1c60783e10000000a42189d.html) and [SAPControl Web Service](https://www.sap.com/documents/2016/09/0a40e60d-8b7c-0010-82c7-eda71af511fa.html), and also some blogs that explore other types of automation, for example [An overview on SAP PI/PO APIs](https://blogs.sap.com/2020/10/14/automate-it-an-overview-on-sap-pi-po-apis/).

