<!-- loiod337a6f0d324405f9ef0c410fd0d3739 -->

# Modernization Recommendations

Learn about a set of recommendations aimed at aligning your integration practices with contemporary standards and the integration strategy of SAP.

Modernization recommendations are suggestions by SAP aimed at improving your integration practices, for example, regarding scalability, maintenance, flexibility, and responsiveness. The recommendations often include transitioning from custom legacy content to predelivered packages or modern integration styles, as well as open and standardized protocols like SOAP, REST, and OData.

The modernization recommendations are used in the Migration Assessment capability of SAP Integration Suite. Once you've extracted your integration scenarios and executed a scenario evaluation, you can find the modernization recommendations in the downloadable reports and the dashboard. Depending on your data and the current ruleset the application works with, you might not receive any recommendations. See [Create a Scenario Evaluation Request](https://help.sap.com/docs/integration-suite/sap-integration-suite/create-scenario-evaluation-request).

The following modernization recommendations are covered, sorted by area:

-   [Clean Core](modernization-recommendations-d337a6f.md#loiod337a6f0d324405f9ef0c410fd0d3739__section_kfp_nmx_fbc):

    -   Replace RFCs \(BAPIs\) with SOAP/OData APIs

    -   Replace custom interfaces with predelivered packages

    -   Replace IDOCs with SOAP/OData APIs or Business Events


-   [Integration Style](modernization-recommendations-d337a6f.md#loiod337a6f0d324405f9ef0c410fd0d3739__section_xqx_v5v_hbc):

    -   Multiple Receivers Async to Business Event

    -   IDoc to Business Event

    -   Polling to Push


-   [Mapping](modernization-recommendations-d337a6f.md#loiod337a6f0d324405f9ef0c410fd0d3739__section_uyj_kxv_hbc):

    -   Java/ABAP Mapping to Graphical/XSLT/Groovy Script Mapping


-   [Monitoring and Operations](modernization-recommendations-d337a6f.md#loiod337a6f0d324405f9ef0c410fd0d3739__section_nsd_vzv_hbc):

    -   Alert Rules to SAP Cloud ALM


-   [Protocol](modernization-recommendations-d337a6f.md#loiod337a6f0d324405f9ef0c410fd0d3739__section_brd_31w_hbc):

    -   File-based protocols \(NFS, FTP, SFTP\) to API-based protocols \(SOAP, OData, REST\)

    -   IDoc to API-based protocols \(SOAP, OData, REST\)

    -   RFC protocol to API-based protocols \(SOAP, OData, REST\)

    -   Mail-based protocols \(SMTP, POP3, IMAP\) to API-based protocols \(SOAP, OData, REST\)

    -   JDBC to API-based protocols \(SOAP, OData, REST\)


-   [Security](modernization-recommendations-d337a6f.md#loiod337a6f0d324405f9ef0c410fd0d3739__section_q4w_hcw_hbc):

    -   HTTP to HTTPS

    -   Basic Authentication to Client Certificate Authentication or OAuth 2.0 Authentication

    -   FTP to SFTP

    -   SFTP-Weak Algorithms to Strong Algorithms





<a name="loiod337a6f0d324405f9ef0c410fd0d3739__section_kfp_nmx_fbc"/>

## Clean Core



### Replace RFCs \(BAPIs\) with SOAP/OData APIs


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Possible Modernization

</td>
<td valign="top">

RFCs \(BAPIs\)

</td>
</tr>
<tr>
<td valign="top">

Recommendation

</td>
<td valign="top">

SOAP/OData APIs

</td>
</tr>
<tr>
<td valign="top">

Benefits

</td>
<td valign="top">

-   SOAP and OData APIs allow linking with different apps and systems

-   You can find documentation, support, and implementation guidelines for public APIs on the SAP Business Accelerator Hub.

-   Modern APIs are more flexible for future changes in the integration strategy




</td>
</tr>
<tr>
<td valign="top">

Checks

</td>
<td valign="top">

Check if an API for the relevant functionality is available in [SAP Business Accelerator Hub](https://api.sap.com).

</td>
</tr>
<tr>
<td valign="top">

Applicable Scenarios

</td>
<td valign="top">

All scenarios are applicable.

</td>
</tr>
<tr>
<td valign="top">

Not Applicable Scenarios

</td>
<td valign="top">

None

</td>
</tr>
</table>

Do you need hands-on instructions for the modernization of your RFC communication? Check out the tutorials [Learn How to Modernize RFC Sender Communications into API-Based protocols in Cloud Integration](https://developers.sap.com/tutorials/modernize-rfc.html) and [Learn How to Modernize RFC Receiver Communications into API-Based Protocols in Cloud Integration](https://developers.sap.com/tutorials/modernize-rfc-receiver.html).



### Replace custom interfaces with predelivered packages

In Cloud Integration, a custom interface is an integration solution that’s developed from scratch to address your specific and unique business requirements. With the prepackaged integration content delivered by SAP, you can get started quickly with minimal integration developer effort.


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

**Possible Modernization Item**

</td>
<td valign="top">

Custom Interface

</td>
</tr>
<tr>
<td valign="top">

**Recommendation**

</td>
<td valign="top">

Predelivered Package

</td>
</tr>
<tr>
<td valign="top">

**Benefits**

</td>
<td valign="top">

-   The preconfigured integration flows, mappings, and settings included in predelivered packages save time and effort for developers.

-   Predelivered packages are based on best practices and industry standards, which leads to more robust and reliable implementations.

-   Using predelivered packages and prebuilt components helps in maintaining consistency across different integration projects within your organization.

-   Predelivered packages are designed to be scalable and can therefore cater for growth.

-   If you’re new to SAP Cloud Integration or integration development, predelivered packages provide a starting point and give guidance on how to structure integration flows and configure components.

-   SAP regularly updates predelivered content to include improvements, new features, and bug fixes.




</td>
</tr>
<tr>
<td valign="top">

**Checks**

</td>
<td valign="top">

-   Check for compatibility or version requirements in predelivered content, for example, regarding the version of Cloud Integration you’re using.

-   Before getting started, review the documentation and release notes for the predelivered package to understand if it can fulfill your existing business requirements. The documentation provides details on configuration and deployment that help your understand and customize prepackaged content.

-   Check how the predelivered content can be customized to meet your specific integration requirements. Determine whether it provides flexibility for adaptation and if there are any recommended or supported customization approaches to avoid issues during updates.

-   Verify that the predelivered package aligns with your organization's security policies and standards.

-   Review the authentication and authorization mechanisms used in the integration flows to ensure they comply with your security requirements.

-   Identify and review the dependencies on external systems, such as APIs, applications, or data sources. Ensure that these systems are compatible and accessible.

-   Verify the licensing requirements associated with the predelivered content and ensure compliance with SAP licensing policies. Check for any third-party components or services included in the predelivered package and ensure compliance with their respective licenses.




</td>
</tr>
<tr>
<td valign="top">

**Applicable Scenarios**

</td>
<td valign="top">

All scenarios are applicable.

</td>
</tr>
<tr>
<td valign="top">

**Not Applicable Scenarios**

</td>
<td valign="top">

None

</td>
</tr>
</table>



<a name="loiod337a6f0d324405f9ef0c410fd0d3739__section_xqx_v5v_hbc"/>

## Integration Style



### Multiple Receivers Async to Business Event

You can replace integrations that must deliver a message to multiple receivers with a publish/subscribe approach. This approach uses decoupling to allow publishers and subscribers to operate independently, which means that publishers don’t have to cater for a specific number of subscribers. They can also flexibly add or remove subscribers. Additionally, the publish/subscribe approach fosters asynchronous communication, which is crucial for distributed systems as it enables efficient handling of high message rates and reduces latency.


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

**Possible Modernization**

</td>
<td valign="top">

Multiple Receivers Async

</td>
</tr>
<tr>
<td valign="top">

**Recommendation**

</td>
<td valign="top">

Business Event

</td>
</tr>
<tr>
<td valign="top">

**Benefits**

</td>
<td valign="top">

-   Loose coupling of receivers allows to quickly add or remove receivers.

-   Independent scalability of sender and receivers.

-   Asynchronous communication increases the resilience of your integration solution since a failure in a subscribed system might not impact the delivery of others.




</td>
</tr>
<tr>
<td valign="top">

**Checks**

</td>
<td valign="top">

-   Check if event-based integration is supported on the sender and receiver side.

-   Optionally, in S/4HANA, check if standard business events are available.

-   Check the [SAP Business Accelerator Hub](https://api.sap.com) for event objects that support your scenario.




</td>
</tr>
<tr>
<td valign="top">

**Applicable Scenarios**

</td>
<td valign="top">

You have asynchronous scenarios with multiple receivers.

</td>
</tr>
<tr>
<td valign="top">

**Not Applicable Scenarios**

</td>
<td valign="top">

-   Synchronous communication

-   You require delivery message in order

-   You expect point-to-point to a single receiver




</td>
</tr>
</table>



### IDoc to Business Event

Instead of IDoc, use open and standardized protocols such as SOAP, REST, and OData for event communication. These protocols enable you for interoperability, wider adoption, and easier integration with non-SAP systems.


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

**Possible Modernization**

</td>
<td valign="top">

IDocs

</td>
</tr>
<tr>
<td valign="top">

**Recommendation**

</td>
<td valign="top">

Business Events

</td>
</tr>
<tr>
<td valign="top">

**Benefits**

</td>
<td valign="top">

Reduce complexity and overhead on your integration solution using a modern and lightweight messaging format.

</td>
</tr>
<tr>
<td valign="top">

**Checks**

</td>
<td valign="top">

-   Check if event-based integration is supported on the sender and receiver side.

-   In S/4HANA, check if standard business events are available \(optional\).

-   Check the [SAP Business Accelerator Hub](https://api.sap.com) for event objects that support your scenario.




</td>
</tr>
<tr>
<td valign="top">

**Applicable Scenarios**

</td>
<td valign="top">

-   You want to keep the message size to a minimum.

-   You want to reduce the overall complexity of your interface.




</td>
</tr>
<tr>
<td valign="top">

**Not Applicable Scenarios**

</td>
<td valign="top">

-   You want to replicate master data.

-   Sender and/or receiver don’t support business events.




</td>
</tr>
</table>



### Polling to Push

Push can provide real-time updates with reduced latency and increased efficiency. In push systems, servers proactively send information to clients when updates occur, which minimizes unnecessary requests and optimizes resource usage.


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

**Possible Modernization**

</td>
<td valign="top">

Polling

</td>
</tr>
<tr>
<td valign="top">

**Recommendation**

</td>
<td valign="top">

Push

</td>
</tr>
<tr>
<td valign="top">

**Benefits**

</td>
<td valign="top">

-   Only produce relevant messages, which reduces additional messages consumption.

-   Provide immediate updates between systems.




</td>
</tr>
<tr>
<td valign="top">

**Checks**

</td>
<td valign="top">

-   Check if you sender system can push data via an API call.

-   Check the [SAP Business Accelerator Hub](https://api.sap.com) for event objects that support your scenario.




</td>
</tr>
<tr>
<td valign="top">

**Applicable Scenarios**

</td>
<td valign="top">

-   \(Near\) real-time applications

-   Alert Notification applications




</td>
</tr>
<tr>
<td valign="top">

**Not Applicable Scenarios**

</td>
<td valign="top">

Integrations that must be executed at a specific time.

</td>
</tr>
</table>



<a name="loiod337a6f0d324405f9ef0c410fd0d3739__section_uyj_kxv_hbc"/>

## Mapping



### Java/ABAP Mapping to Graphical/XSLT/Groovy Script Mapping

Graphical mapping can help you keep your mapping clean and maintainable by leveraging built-in capabilities from Cloud Integration. You can also convert your mappings to Groovy script, which provides a more concise and expressive syntax and therefore reduces the amount of code needed for common tasks. Additionally, you can replacing your mapping with XSLT, which simplifies code, separates transformation logic from Java, and improves maintainability, which allows you to make changes in the transformation rules without modifying the application code.


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

**Possible Modernization**

</td>
<td valign="top">

Java/ABAP Mapping

</td>
</tr>
<tr>
<td valign="top">

**Recommendation**

</td>
<td valign="top">

Graphical/XSLT/Groovy Script Mapping

</td>
</tr>
<tr>
<td valign="top">

**Benefits**

</td>
<td valign="top">

-   Concise and expressive syntax

-   Quick development cycles and easy maintenance

-   Developers familiar with Java can smoothly transition to Groovy script




</td>
</tr>
<tr>
<td valign="top">

**Checks**

</td>
<td valign="top">

Check that the operations executed on the Java/ABAP mapping are supported on Cloud Integration. See [Migrating Java Mappings](migrating-java-mappings-468c179.md).

</td>
</tr>
<tr>
<td valign="top">

**Applicable Scenarios**

</td>
<td valign="top">

All scenarios are applicable.

</td>
</tr>
<tr>
<td valign="top">

**Not Applicable Scenarios**

</td>
<td valign="top">

None

</td>
</tr>
</table>



<a name="loiod337a6f0d324405f9ef0c410fd0d3739__section_nsd_vzv_hbc"/>

## Monitoring and Operations



### Alert Rules to SAP Cloud ALM

Alert Rules are objects maintained in the Integration Directory in SAP Process Orchestration that you can use to trigger alerts in certain conditions for defined interfaces, but only in the SAP Process Orchestration system. To use alert rules in Cloud Integration, migrate them to the alert notifications service on SAP Cloud ALM. For more information on SAP Cloud ALM, see [Integration & Exception Monitoring](https://support.sap.com/en/alm/sap-cloud-alm/operations/expert-portal/integration-monitoring/int-mon-setup-support.html).


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

**Possible Modernization**

</td>
<td valign="top">

Alert Rules

</td>
</tr>
<tr>
<td valign="top">

**Recommendation**

</td>
<td valign="top">

Alert Notification service on SAP Cloud ALM

</td>
</tr>
<tr>
<td valign="top">

**Benefits**

</td>
<td valign="top">

-   Receive immediate notifications for potential issues in your integration landscape.
-   Identify problems early with advanced analytics and machine learning.
-   Ensure business continuity through proactive monitoring and alerting.
-   Facilitate quick response and collaboration among teams with centralized alert management.
-   Customize alerts to the needs of your organization for more effective monitoring.
-   Optimize resource usage by proactively addressing potential disruptions.

Use the centralized platform for managing and responding to alert notifications.

</td>
</tr>
<tr>
<td valign="top">

**Checks**

</td>
<td valign="top">

Check the currently implemented alert rules and find out which alerts you must move to SAP Cloud ALM.

</td>
</tr>
<tr>
<td valign="top">

**Applicable Scenarios**

</td>
<td valign="top">

Any interface that has an alert rule can be a candidate you can move to SAP Cloud ALM.

</td>
</tr>
<tr>
<td valign="top">

**Not Applicable Scenarios**

</td>
<td valign="top">

None

</td>
</tr>
</table>



<a name="loiod337a6f0d324405f9ef0c410fd0d3739__section_brd_31w_hbc"/>

## Protocol



### File-based protocols \(NFS, FTP, SFTP\) to API-based protocols \(SOAP, OData, REST\)

Replace file-based approaches like NFS, FTP, or SFTP with protocols that supports end-to-end monitoring to increase security, provide fine-grained access control, transaction support, structured communication, platform independence, versioning flexibility, robust monitoring and logging, scalability, and standardized error handling. You can use Web services, which are suitable for scenarios in which you require data integrity, security, and structured communication.


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

**Possible Modernization**

</td>
<td valign="top">

File-based protocols \(NFS, FTP, SFTP\)

</td>
</tr>
<tr>
<td valign="top">

**Recommendation**

</td>
<td valign="top">

API-based protocols \(SOAP, OData, REST\)

</td>
</tr>
<tr>
<td valign="top">

**Benefits**

</td>
<td valign="top">

-   End-to-end monitoring
-   More secure message exchange
-   Enhanced error handling capabilities



</td>
</tr>
<tr>
<td valign="top">

**Checks**

</td>
<td valign="top">

Check which protocols are supported.

</td>
</tr>
<tr>
<td valign="top">

**Applicable Scenarios**

</td>
<td valign="top">

-   Consider SOAP for bulk load, complex objects handling, asynchronous delivery, and scenarios in which you need WS-Security.
-   Consider OData/REST for single objects handling, bulk loads, and operations using resource IDs.



</td>
</tr>
<tr>
<td valign="top">

**Not Applicable Scenarios**

</td>
<td valign="top">

Messages with a considerable size \(for example, bigger than 100 MB\) that can't be split during the processing.

</td>
</tr>
</table>



### IDoc to API-based protocols \(SOAP, OData, REST\)

IDoc, while commonly used for data exchange, is an SAP-proprietary protocol, which poses challenges for the seamless communication with other systems. To leverage interoperability, protocols must be grounded in open standards. Newly developed APIs therefore leverage SOAP, REST, and OData protocols to facilitate smooth and inclusive data exchanges across heterogeneous environments in a lightweight format.


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

**Possible Modernization**

</td>
<td valign="top">

IDocs

</td>
</tr>
<tr>
<td valign="top">

**Recommendation**

</td>
<td valign="top">

API-based protocols \(SOAP, OData, REST\)

</td>
</tr>
<tr>
<td valign="top">

**Benefits**

</td>
<td valign="top">

-   Open standard that can easily be used by non-SAP applications.
-   Standard SAP APIs are frequently updated and enhanced.



</td>
</tr>
<tr>
<td valign="top">

**Checks**

</td>
<td valign="top">

-   Check if the sender and/or receiver support the protocols.
-   If you use asynchronous integrations, confirm the availability of standard API.
-   Check if you require bulk operation.



</td>
</tr>
<tr>
<td valign="top">

**Applicable Scenarios**

</td>
<td valign="top">

-   Consider SOAP for bulk load, complex objects handling, asynchronous delivery, and scenarios in which you need WS-Security.
-   Consider OData/REST for single objects handling, bulk loads, and operations using resource IDs.



</td>
</tr>
<tr>
<td valign="top">

**Not Applicable Scenarios**

</td>
<td valign="top">

External third-party systems that only support IDoc.

</td>
</tr>
</table>



### RFC protocol to API-based protocols \(SOAP, OData, REST\)

RFC, while commonly used for data exchange, is an SAP-proprietary protocol, which poses challenges for the seamless communication with other systems. To leverage interoperability, protocols must be grounded in open standards. Newly developed APIs therefore leverage SOAP, REST, and OData protocols to facilitate smooth and inclusive data exchanges across heterogeneous environments in a lightweight format.

If RFC is enabled, you can generate a SOAP webservice out of your function module.


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

**Possible Modernization**

</td>
<td valign="top">

RFC protocol

</td>
</tr>
<tr>
<td valign="top">

**Recommendation**

</td>
<td valign="top">

API-based protocols \(SOAP, OData, REST\)

</td>
</tr>
<tr>
<td valign="top">

**Benefits**

</td>
<td valign="top">

-   HTTP-based protocol means better compatibility with external systems
-   Can use asynchronous calls.
-   Standard SAP APIs are frequently updated and enhanced.



</td>
</tr>
<tr>
<td valign="top">

**Checks**

</td>
<td valign="top">

-   Check if the RFC check is enabled in the function module.
-   Check if service ICF */sap/bc/soap/rfc* and */sap/bc/soap/wsdl11* are enabled in SICF.
-   For SOAP webservices, consume your RFC as SOAP webservice using an out-of-the-box functionality as described, for example, in the blog [How Easy It Is To Consume Function Module as Web service and Connect it Using SAP Cloud Platform Integration](https://community.sap.com/t5/technology-blogs-by-sap/how-easy-it-is-to-consume-function-module-as-web-service-and-connect-it/ba-p/13317991).



</td>
</tr>
<tr>
<td valign="top">

**Applicable Scenarios**

</td>
<td valign="top">

-   Consider SOAP for bulk load, complex objects handling, asynchronous delivery, and scenario in which you need WS-Security.
-   Consider OData/REST for single objects handling, bulk loads and operations using resource IDs



</td>
</tr>
<tr>
<td valign="top">

**Not Applicable Scenarios**

</td>
<td valign="top">

External third-party systems that only support RFC.

</td>
</tr>
</table>



### Mail-based protocols \(SMTP, POP3, IMAP\) to API-based protocols \(SOAP, OData, REST\)

If you migrate the protocol you use for alert notifications, like SMTP, POP3, and IMAP to protocols like SOAP, OData, and REST, you gain end-to-end monitoring for enhanced visibility, improved security options, streamlined interface descriptions, testing, and validation, simplified consumer/provider implementation, and the shift from polling to push for real-time message consumption.

Apply this approach when you rely on monitoring insights, for example when using SAP Alert Notification service for SAP BTP or similar services, or when using an external logging tool. However, it may not be suitable if you rely on email-based alerting or when you require message-agnostic behavior.


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

**Possible Modernization**

</td>
<td valign="top">

Mail-based protocols \(SMTP, POP3, IMAP\)

</td>
</tr>
<tr>
<td valign="top">

**Recommendation**

</td>
<td valign="top">

API-based protocols \(SOAP, OData, REST\)

</td>
</tr>
<tr>
<td valign="top">

**Benefits**

</td>
<td valign="top">

-   End-to-end monitoring
-   More security possibilities.
-   Changing the integration style from polling to push.



</td>
</tr>
<tr>
<td valign="top">

**Checks**

</td>
<td valign="top">

-   Check if the protocol is supported by the sender and/or receiver.
-   Get informed about the [SAP Alert Notification service on SAP BTP](https://help.sap.com/docs/alert-notification?locale=en-US).



</td>
</tr>
<tr>
<td valign="top">

**Applicable Scenarios**

</td>
<td valign="top">

When sender and/or receiver can receive a success/error response from the integration process.

</td>
</tr>
<tr>
<td valign="top">

**Not Applicable Scenarios**

</td>
<td valign="top">

-   Messages must be received via email – CALM isn’t possible/feasible.
-   You need message-agnostic behavior.



</td>
</tr>
</table>



### JDBC to API-based protocols \(SOAP, OData, REST\)

If you migrate JDBC communication to modern protocols like SOAP, REST, or OData, you gain scalability, simplicity in client development, efficiency, enhanced security, data presentation flexibility, and alignment with current integration practices.


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

**Possible Modernization**

</td>
<td valign="top">

JDBC

</td>
</tr>
<tr>
<td valign="top">

**Recommendation**

</td>
<td valign="top">

API-based protocols \(SOAP, OData, REST\)

</td>
</tr>
<tr>
<td valign="top">

**Benefits**

</td>
<td valign="top">

-   End-to-end monitoring
-   Enhanced security on message exchange.
-   Improved interoperability with various platforms and technologies.



</td>
</tr>
<tr>
<td valign="top">

**Checks**

</td>
<td valign="top">

Check if the protocol is supported by the sender and/or receiver.

</td>
</tr>
<tr>
<td valign="top">

**Applicable Scenarios**

</td>
<td valign="top">

-   Consider SOAP for bulk load, complex objects handling, asynchronous delivery, and scenarios in which you need WS-Security.
-   Consider OData/REST for single objects handling, bulk loads, and operations using resource IDs.



</td>
</tr>
<tr>
<td valign="top">

**Not Applicable Scenarios**

</td>
<td valign="top">

-   External third-party systems that only support JDBC.
-   If you must use specific, complex query combinations or procedure calls.



</td>
</tr>
</table>



<a name="loiod337a6f0d324405f9ef0c410fd0d3739__section_q4w_hcw_hbc"/>

## Security



### HTTP to HTTPs

Transition to using HTTPS in your interface to bolster security by encrypting the data exchanged between integrated applications. This encryption fortifies sensitive transmissions, such as user credentials and confidential information, and shields against unauthorized access and tampering. By adopting HTTPS, you establish a secure communication channel, minimize interception threats, and enhance the integrity of your application integration, which ensures data confidentiality.


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

**Possible Modernization**

</td>
<td valign="top">

HTTP

</td>
</tr>
<tr>
<td valign="top">

**Recommendation**

</td>
<td valign="top">

HTTPS

</td>
</tr>
<tr>
<td valign="top">

**Benefits**

</td>
<td valign="top">

-   Data encryption
-   Secure communication
-   Data integrity
-   Compliance with security standards
-   Credential protection



</td>
</tr>
<tr>
<td valign="top">

**Checks**

</td>
<td valign="top">

The target system must own a valid server certificate and support TLS/SSL communication.

</td>
</tr>
<tr>
<td valign="top">

**Applicable Scenarios**

</td>
<td valign="top">

All scenarios are applicable.

</td>
</tr>
<tr>
<td valign="top">

**Not Applicable Scenarios**

</td>
<td valign="top">

None

</td>
</tr>
</table>



### Basic Authentication to Client Certificate Authentication or OAuth 2.0 Authentication

Basic authentication requires a valid username and password as the mechanism relies on the standard base64 encoded username and password HTTP header. Because the username and password can be decoded from the request, basic authentication should only be used over HTTPS.

By moving to certificate-based authentication, you ensure strong mutual authentication and secure communication channels. Meanwhile, OAuth authentication streamlines secure authorization, which offers granular access control. OAuth provides a more secure and adaptable authorization mechanism by employing tokens instead of transmitting credentials with each request. This approach reduces the risks associated with prolonged credentials exposure and facilitates third-party access to resources without directly exposing user login credentials, thereby enhancing user privacy and security.


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

**Possible Modernization**

</td>
<td valign="top">

Basic Authentication

</td>
</tr>
<tr>
<td valign="top">

**Recommendation**

</td>
<td valign="top">

Client Certificate Authentication or OAuth 2.0 Authentication

</td>
</tr>
<tr>
<td valign="top">

**Benefits**

</td>
<td valign="top">

For Client Certificate authentication:

-   Strong mutual authentication
-   Secure communication
-   Reduced dependency on user credentials

For OAuth authentication:

-   Granular access control
-   Token-based security



</td>
</tr>
<tr>
<td valign="top">

**Checks**

</td>
<td valign="top">

-   The target system must support more types of authentications other than basic authentications.
-   You must be using a valid certificate to leverage client certificate authentication.
-   Deploy OAuth2 client credentials.



</td>
</tr>
<tr>
<td valign="top">

**Applicable Scenarios**

</td>
<td valign="top">

All scenarios are applicable.

</td>
</tr>
<tr>
<td valign="top">

**Not Applicable Scenarios**

</td>
<td valign="top">

None

</td>
</tr>
</table>



### FTP to SFTP

Secure File Transfer Protocol \(SFTP\) has enhanced security features as it encrypts both commands and data during transmission, providing a secure channel for file transfers. In contrast, FTP sends data in plaintext, making it vulnerable to eavesdropping and unauthorized access. SFTP also utilizes Secure Shell \(SSH\) for authentication, adding an extra layer of security compared to FTP's basic username and password authentication. With its built-in encryption and secure authentication methods, SFTP ensures the confidentiality and integrity of data transfers, making it a more secure choice for file exchange over untrusted networks compared to the less secure FTP protocol.

By moving from FTP to SFTP, you enhance security by encrypting both commands and data, preventing interception of sensitive information. SFTP's use of SSH for authentication adds another layer of security, requiring cryptographic authentication, unlike FTP's vulnerable username/password system. Moreover, SFTP's single, secure connection reduces the attack surface by eliminating the need for multiple open ports, while supporting key-based authentication for stronger access control. These features increase the file transfer security, safeguarding sensitive data from unauthorized access and interception.


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

**Possible Modernization**

</td>
<td valign="top">

FTP

</td>
</tr>
<tr>
<td valign="top">

**Recommendation**

</td>
<td valign="top">

SFTP

</td>
</tr>
<tr>
<td valign="top">

**Benefits**

</td>
<td valign="top">

-   Robust encryption algorithms to safeguard transmitted data, mitigating the risk of unauthorized access and ensuring confidentiality.
-   Relies on the Secure Shell \(SSH\) protocol for user authentication, enhancing the verification process and bolstering access control measures.
-   Singular port \(typically port 22\) facilitates firewall management, streamlining network security configurations while maintaining the efficiency of file transfers.
-   Facilitates the resumption of interrupted file transfers and supports partial transfers, contributing to resilience in the face of network disruptions.



</td>
</tr>
<tr>
<td valign="top">

**Checks**

</td>
<td valign="top">

-   The target system must support and/or has enabled the port 22 for SFTP communication.
-   The SSH key exchanged and properly imported in Cloud Integration known the host’s file.



</td>
</tr>
<tr>
<td valign="top">

**Applicable Scenarios**

</td>
<td valign="top">

All scenarios are applicable.

</td>
</tr>
<tr>
<td valign="top">

**Not Applicable Scenarios**

</td>
<td valign="top">

None

</td>
</tr>
</table>



### SFTP-Weak Algorithms to Strong Algorithms

SFTP uses a variety of encryption algorithms such as 3DES, Blowfish, and AES. It also supports powerful key exchange algorithms like Diffie Hellman, ensuring a secure pathway for data transfer.

> ### Note:  
> Some deprecated algorithms are not supported on JSch library anymore. See SAP Note [3079510](https://me.sap.com/notes/3079510).


<table>
<tr>
<th valign="top">

Category

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

**Possible Modernization**

</td>
<td valign="top">

SFTP-Weak Algorithms

</td>
</tr>
<tr>
<td valign="top">

**Recommendation**

</td>
<td valign="top">

Strong Algorithms

</td>
</tr>
<tr>
<td valign="top">

**Benefits**

</td>
<td valign="top">

-   Stronger encryption keeps your files more secret during transfers.
-   Tougher encryption makes it harder for bad actors to “break” the secret key.
-   Strong algorithms resist advanced attacks, which ensures the safety of your data over time.



</td>
</tr>
<tr>
<td valign="top">

**Checks**

</td>
<td valign="top">

-   Check the server-side configuration of your SFTP server. The configuration file \(often located at /etc/ssh/sshd\_config on Unix-based systems\) specifies the encryption algorithms in use.
-   When initiating an SFTP connection from the command line, you can use the -v \(verbose\) option to display detailed information about the connection, including the algorithms in use.
-   SFTP often relies on the SSH \(Secure Shell\) protocol. Check the SSH client configuration file \(for example, ~/.ssh/config or /etc/ssh/ssh\_config\) for settings related to the preferred algorithms.



</td>
</tr>
<tr>
<td valign="top">

**Applicable Scenarios**

</td>
<td valign="top">

All scenarios are applicable.

</td>
</tr>
<tr>
<td valign="top">

**Not Applicable Scenarios**

</td>
<td valign="top">

None

</td>
</tr>
</table>

