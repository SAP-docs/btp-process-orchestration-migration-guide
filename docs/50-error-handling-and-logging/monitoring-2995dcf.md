<!-- loio2995dcfe97374c42a63f57f6f05be0fd -->

# Monitoring

Find out which monitors you can utilize when working with SAP Process Orchestration and Cloud Integration, and discover offerings for application lifecycle management.



<a name="loio2995dcfe97374c42a63f57f6f05be0fd__section_jn1_bgd_mqb"/>

## SAP Process Orchestration Monitoring

In SAP Process Orchestration, the following monitors support you in your daily operations and troubleshooting:



### Message Monitor

Using the message monitor in SAP NetWeaver Administrator, you can monitor the processing of messages on the Advanced Adapter Engine. You can use message monitoring in the following cases:

-   To create an overview of message processing. Message overview also provides two different modes for searching messages.

-   To track the status of messages.

-   To find errors that have occurred and to establish what caused them.


You can also search for messages that were persisted in the database, or for messages that have already been archived.



### Communication Channel Monitor

Use the communication channel monitor to obtain information about communication channels that are set up for the Advanced Adapter Engine. You can also perform some administrative activities.

If the Advanced Adapter Engine runs on a server cluster, the communication channels comprise multiple instances for the various cluster nodes.



### IDoc Adapter Monitor

Use the IDoc message monitor to search for IDoc messages processed in the adapter. Based on the various parameters of the IDoc message you provide as search criteria, the monitor retrieves the messages and displays information about them.

For more information, see [Displaying IDoc Messages](https://help.sap.com/viewer/5cf7d2de571a45cc81f91261668b7361/7.5.latest/en-US/de82c727b3d94714a04a4a579663fcf5.html).

It's also possible to use the IDoc metadata monitor to display IDoc metadata information and clear the metadata for the selected IDoc type from the cache.



### Adapter Engine Status

Use the adapter engine status to get information about the adapter engine, queues, message traffic \(e.g. number of asynchronous or synchronous messages\), database locks, overview of messages \(being\) processed per sender, and receiver components.



### Channel-Independent Logs

Use the channel-independent logs to display execution steps of adapters that can't be assigned to a particular communication channel.



### Cache Monitor

Use the cache monitor to display objects that are currently in the runtime cache of the Advanced Adapter Engine and the Mapping Runtime. You can enter selection criteria to search for current objects in the runtime cache and review the details of a selected object.



### Performance Monitor

Use the performance monitor to inspect the processed data by intervals of time and their processing time for individual adapters.



### CPA Cache History

Use the CPA cache history to display an overview of cache refresh actions and their statuses.



### Background Job Monitor

Displays an overview of background jobs \(adapter engine, adapter framework scheduler jobs, etc.\) and offers the ability to manage them.



### More Information

-   You can also [centralize the Process Integration monitoring with SAP Solution Manager](https://wiki.scn.sap.com/wiki/display/TechOps/Central+PI+Monitoring+with+SAP+Solution+Manager+7.2).

-   SAP Process Orchestration has a standard functionality called [Component-Based Message Alerting](https://help.sap.com/viewer/bdfc9b7d99b544d8bbda40546b70967a/7.5.latest/en-US/2cf0a3d4540c4c9a9af65139801ef826.html) which allows you to create alert rules to your interfaces.

-   For more information, see [Monitoring the Advanced Adapter Engine](https://help.sap.com/viewer/5cf7d2de571a45cc81f91261668b7361/7.5.latest/en-US/afd36bc882e846f29ddef9dc1741527b.html).




<a name="loio2995dcfe97374c42a63f57f6f05be0fd__section_jt2_bgd_mqb"/>

## Cloud Integration Monitoring

In Cloud Integration, a message monitor allows you to display the processed messages and their statuses, logs, and traces. Compared to SAP Process Orchestration, there are less monitors because you don’t have such components like Adapter Engine, or you don’t perform as many administrative tasks since some of these are part of SAP’s platform support service. You also don’t have monitors such as Cache Monitor, Metadata Monitor, Adapter Engine Monitor, and Communication Channel Monitor. For more details about the message monitor and its capabilities, see [Guidelines and Best Practices for Message Monitoring](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/6f598b4d4e0e44c3bd8445b5d58b832c.html).

Cloud Integration isn't delivered with pre-built out-of-the-box alert capabilities, but you can use a predelivered package that uses the SAP Alert Notification service for SAP BTP to send alerts of failure of integration flows. You can also create your own integration using the available APIs to read the Cloud Integration tenant content.

For more information, see the following blogs:

-   [Creating Custom Alert Notifications in SAP Integration Suite](https://blogs.sap.com/2020/07/31/creating-custom-alert-notifications-in-sap-cloud-platform-integration-suite/)

-   [Receive Notifications for Failed SAP Cloud Integration Flows via Any Channel with Alert Notification](https://blogs.sap.com/2019/10/14/receive-notifications-for-failed-sap-cloud-platform-integration-flows-via-any-channel-with-alert-notification/)


For a comprehensive walkthrough of the capabilities of the SAP Alert Notification service, review this [blog series about SAP Alert Notification](https://blogs.sap.com/2019/06/05/sap-cloud-platform-alert-notification-is-now-generally-available/).

If the standard capabilities of the SAP Alert Notification service aren't sufficient to meet customer requirements, or there's no external system or service like SAP Solution Manager to generate alert notifications, integration flows that invoke calls to the standard APIs published by the SAP Alert Notification service can be built within Cloud Integration. Full documentation of these APIs can be found on the [API Business Hub](https://api.sap.com/package/AlertNotification/rest). Another option is to combine the exception subprocesses while developing your integration flow with some procedure to collect the error/success message and send it via email. For details, see the blog [How to send a mail from SAP Cloud Platform Integration](https://blogs.sap.com/2018/01/17/how-to-send-a-mail-from-sap-cloud-platform-integration/).



<a name="loio2995dcfe97374c42a63f57f6f05be0fd__section_fnm_xhx_lqb"/>

## Application Lifecycle Management \(ALM\)



### SAP Cloud ALM

SAP Cloud ALM is an offering for application lifecycle management. It's intended for customers who use cloud solutions provided by SAP, and who don't want to use their own ALM on-premise platform for managing those solutions. SAP Cloud ALM runs on SAP Business Technology Platform and is optimized for SAP HANA. It provides extensive implementation and operation capabilities for cloud solutions with the following key features:

-   Implement cloud-centric solutions with a preconfigured, content-driven guided workspace based on SAP Activate methodology and SAP Best Practices.

-   Run fit-to-standard workshops and manage all implementation, testing, and deployment activities.

-   Accelerate team member onboarding, define business process scope according to project milestones, manage requirements, and track project progress.

-   Ensure smooth business operations without disruptions with proactive end-to-end monitoring and alerting.

-   Increase business-process execution quality and performance by finding and analyzing issues on business process, integration, user, and application level.

-   Understand solution health and efficiency with advanced analytics and intelligence.


For more information, access the openSAP courses [SAP Cloud ALM in a Nutshell](https://open.sap.com/courses/calm1) and [Accelerate Cloud Implementations with SAP Cloud ALM](https://open.sap.com/courses/calm2).

You can also access the SAP Support pages [SAP Cloud ALM for Implementation](https://support.sap.com/en/alm/sap-cloud-alm/implementation.html) and [SAP Cloud ALM for Operations](https://support.sap.com/en/alm/sap-cloud-alm/operations.html).



### SAP Solution Manager

SAP Solution Manager is an application lifecycle management platform used to implement, maintain, and integrate SAP systems, troubleshoot issues, and keep operations running securely, cleanly, and smoothly. This tool was originally designed to support on-premise systems only \(including SAP Process Orchestration\), but the scope of capability has been increased to include cloud-based services, including Cloud Integration.

For detailed information on the capabilities and setup procedures to connect SAP Solution Manager to Cloud Integration, see the [SAP Support page for Cloud Integration](https://support.sap.com/en/alm/solution-manager/expert-portal/public-cloud-operations/sap-cloud-platform-integration.html).



### SAP Cloud ALM vs SAP Solution Manager

> ### Restriction:  
> Some features mentioned on this site are planned for the future and are subject to change. For more information on new features and future releases, access the [Road Map Explorer](http://help.sap.com/disclaimer?site=https://roadmaps.sap.com/board?CB=901B0ED1A0641ED8B4D1230C6387E0DB&range=CURRENT-LAST) and the [What's New section](https://help.sap.com/doc/7ac9748e20cf453a94efda779542d34e/sap.cp.integration.suite/en-US/c10c21cd7c684f0885fa8b5db2982284.html) of SAP Integration Suite.

Though SAP Solution Manager can currently be used for cloud products and SAP Cloud ALM can also be used for hybrid scenarios as part of future roadmap, it's important to understand the positioning of these two different products. SAP Solution Manager is recommended for on-premise products and SAP Cloud ALM is engineered keeping the cloud applications in mind. Both of these products have different use cases, and both serve a different market.

For more information, see the blog [SAP Cloud ALM vs SAP Solution Manager](https://blogs.sap.com/2020/08/12/sap-cloud-alm-vs-sap-solution-manager/).

