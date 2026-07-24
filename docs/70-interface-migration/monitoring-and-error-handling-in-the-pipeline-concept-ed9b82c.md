<!-- loioed9b82cb928049e6990a4d784aa6aac7 -->

# Monitoring and Error Handling in the Pipeline Concept

Perform monitoring and error handling in the pipeline concept, for example by using retry handling, message monitoring, and using the dead letter queue.



The following measures improve monitoring and error handling in the pipeline concept:

-   Use **SAP headers** to search for messages based on sender system, interface/message type, and receiver system.

-   Set a **custom status** for more information on the error root cause.
-   Use **retry handling** to limit the number of overall retries. See [Standard Retry Handling](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md#loioed9b82cb928049e6990a4d784aa6aac7__section_l3k_qrn_j1c).

-   Customize the retry handling by configuring the **skip retry handling** for errors where an automatic retry does not make sense. See [Skip Retry Handling](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md#loioed9b82cb928049e6990a4d784aa6aac7__section_skip_retry_handling).
-   User **custom exception handling** as an alternative to the standard retry handling and implement your own logic. See [Custom Exception Handling](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md#loioed9b82cb928049e6990a4d784aa6aac7__section_pm1_ggs_5bc).
-   With a **dead letter queue**, you can park messages for which the maximum number of retries has been exceeded. See [Dead Letter Queue Handling](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md#loioed9b82cb928049e6990a4d784aa6aac7__section_lq1_2sn_j1c).

-   Attach **additional information to the message processing log** if errors occur.

-   Add **custom header properties** to the message processing log so you can search logs based on payload data. See [Custom Header Properties](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md#loioed9b82cb928049e6990a4d784aa6aac7__section_c4h_dkz_zcc).




<a name="loioed9b82cb928049e6990a4d784aa6aac7__section_l3k_qrn_j1c"/>

## Standard Retry Handling

If you want to define a scenario-specific retry behavior, you need to create a string parameter with ID `MaxJMSRetries`. Otherwise, the maximum number of retries is set to 5, which is the global default value. In the generic inbound processing integration flow, this parameter is read from the Partner Directory and written in the message header `maxJMSRetries`. The header is passed to all other integration flows in the sequence of flows.

In all generic integration flows that read from a JMS queue, the following standard retry handling is implemented. For custom retry handling, see [Custom Exception Handling](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md#loioed9b82cb928049e6990a4d784aa6aac7__section_pm1_ggs_5bc).

Depending on whether a splitter is used within the generic integration flow, the implementation of the standard retry handling differs slightly. For the integrated messaging runtime, the generic receiver determination and the interface determination integration flows where the message is split, transaction handling ensures that split messages are rolled back in case of an error. However, if the message is forwarded to the dead letter queue, the message processing ends with either a message end event or an escalation end event so that already split messages are committed. If the message is moved from the dead letter queue to the actual queue for reprocessing, this may lead to duplicates. To avoid duplicates, an additional restart is required after the maximum number of retries have been actually exceeded. Its check needs to be done at the beginning of the integration flows, before splitting the message.

> ### Note:  
> Because of the additional retry, the original error message is lost. To retrieve the original error message, you can configure the integrated messaging runtime, the generic receiver determination and the interface determination integration flows as follows. As prerequisite, in the SAP BTP Cockpit, you've created a service key of service `SAP Process Integration Runtime` and plan `api`.
> 
> -   Set the externalized parameter `CI_ODataAPI_TokenURL` to equal the tenant-specific OAuth token URL from your service key.
> -   Set the externalized parameter `CI_ODataAPI_URL` to equal the tenant-specific OData API URL from your service key.
> -   Create a new user credential and set the externalized parameter `CI_ODataAPI_UserCredentials` to equal the alias of the user credential containing the service key’s client ID and client secret from your service key.
> 
> Before the message is stored in the dead letter queue, the original error message is retrieved from the last failed message processing log of the corresponding correlation ID using the OData API, and is added to the log.

In general, if a message processing error occurs, the error is fetched in an exception subprocess. Within the exception subprocess, a local integration process is called.

For the generic inbound processing and the generic outbound processing flows, the local integration process checks if the maximum number of retries has already been exceeded using the following condition expression:

```
${header.SAPJMSRetries} = ${header.maxJMSRetries} or ${header.maxJMSRetries} = '0'
```

As mentioned before, for the generic receiver determination and the generic interface determination integration flows, the check must be done in the beginning, and one additional retry is needed. Hence, the condition expression looks as follows:

```
${header.SAPJMSRetries} > ${header.maxJMSRetries} and ${property.CustomXError_Enabled} != 'true'
```

If the condition is met, the custom status is set to `MaxRetriesExceeded` and an error is raised. In this case, the condition expression in the exception subprocess reads as follows:

```
${property.SAP_MessageProcessingLogCustomStatus} = 'MaxRetriesExceeded'
```

In both cases, the default route, that is, if the maximum number of retries hasn't been exceeded, sets the custom status to *AutomaticRetry* and then ends with an **error end event**. This means that the message remains in the status *Failed* and is retried from the inbound JMS queue.

Otherwise, if the maximum number of retries has been exceeded, the custom status is set to `MaxRetriesExceeded`. In a Groovy script, additional information about the inbound queue name and the dead letter queue name is attached to the message processing log. The name of the dead letter queue follows the following pattern:

`<name of the inbound queue>_DLQ`

The message is then written to the dead letter queue. By default, the message ends with an escalation end event, which then sets the message status to *Escalated*. You can change this behavior by configuring the externalized parameter `DLQ_EndEvent` of the generic integration flows. By default, the value of the parameter is `Escalated`, but you can change the value to `Completed` to end the message with the message status `Completed`.

For failed test messages, that is, failed messages for which the header `testMode` is set to `true`, the retry handling is skipped and the message is instantly completed with the custom status *ErrorInTestMode*.

The following is an example of retry handling:

![The screenshot shows the integration flow editor with an example of retry handling using an exception subprocess and a dead letter queue.](images/PipelineConcept_RetryHandling_99dcda0.png)



<a name="loioed9b82cb928049e6990a4d784aa6aac7__section_skip_retry_handling"/>

## Skip Retry Handling

In error cases in which automatic retries don't make sense, you can deviate from the standard retry handling to reduce unnecessary load on the tenant runtime. The failed messages are then directly stored in the dead letter queue.

For the integrated messaging runtime, the generic receiver determination, and the interface determination integration flows, the retry is skipped in the following cases:

-   Partner ID couldn't be determined.
-   Configuration option isn't supported.
-   Receiver couldn't be determined if Receiver Not Found option equals Error.
-   Receiver interface couldn't be determined.

For all other error cases, the standard retry handling applies.

For the generic outbound processing flow, you can configure skip retry handling. We distinguish between global and scenario-specific settings. By default, the global skip retry handling is enabled, that is, the externalized parameter `SkipRetriesGlobal_Enabled` of the generic outbound processing flow equals `true`. If you want to disable the skip retry handling, change the parameter to `false`. The following options are supported:

-   **Hard coded**: Retry is skipped for mapping errors only. For all other error cases, the standard retry handling applies. This is the default setting.
-   Lookup the skip retry handling from a predefined value mapping. Here, you can customize the skip retry option for particular error classes by configuring a value mapping provided as part of the standard packages. Since you can't deploy a copy of the provided value mapping with the same combination of agency and scheme, choose this option if you want to customize the skip retry handling globally across all scenarios.
-   Lookup the skip retry handling from a global partner ID. Here, for each copied generic outbound processing flow, you can maintain an own skip retry profile as partner ID in the Partner Directory. This gives you a bit more flexibility compared to the previous value mapping option. For example, if you share your tenant across multiple units within your organization where each unit has its own set of pipelines, you can setup skip retry profiles for each unit.
-   Define the skip retry handling scenario-specific by configuring a corresponding parameter in the partner ID representing your configuration scenario. If maintained, this overrules the global settings for the particular configuration scenario.



### Global Default Option

To use the default, option, keep the externalized parameter `SkipRetriesGlobal_Source` of the generic outbound processing flow equaling `Default`. Retry is then skipped for mapping errors only \(exception class `com.sap.xi.mapping.camel.XiMappingException`\). For all other error cases, the standard retry handling applies.



### Global Value Mapping Option

To configure the skip retry handling in a value mapping, change the externalized parameter `SkipRetriesGlobal_Source` of the generic outbound processing flow to `ValueMapping`.

The prerequisite is that you've deployed the value mapping **Pipeline V2 - Value Mapping - Skip Retry Configuration** from the integration package **Cloud Integration Pipeline - Templates**.

By default, the skip retry handling of the value mapping behaves like the hard-coded default option. The retry is only skipped for mapping errors, that is, the exception class `com.sap.xi.mapping.camel.XiMappingException` is mapped to `true`. In the standard delivery of the value mapping, all other exception classes are mapped to `false`. If you want to change the behavior for a particular exception class, configure the mapped value to `true` and redeploy the value mapping.



### Global Partner ID Profile

If you like want configure the skip retry handling using the Partner Directory, create a new partner ID that acts as a skip retry handling profile. You can use the profile for a particular generic outbound processing flow or across multiple copied generic outbound processing flows. For each exception class for which message retry should be skipped, add a string parameter with ID equaling the exception class and value `true`.

> ### Note:  
> To create the profile from scratch, look up the names of the exception classes from the provided value mapping table **Pipeline V2 - Value Mapping - Skip Retry Configuration**. Alternatively, you can have the profile be generated automatically using the helper integration flow **Pipeline v2 - Partner Directory Upload Helper - Skip Retry Configuration** from the integration package **Cloud Integration Pipeline - Templates**. The helper integration flow runs only once upon deployment. Before deploying the helper flow, make sure to configure it properly. You can reconfigure and redeploy to get multiple profiles created. As prerequisite, in the SAP BTP cockpit, you've created a service key of service `SAP Process Integration Runtime` and plan `api`. Furthermore, you've created a credential of type `OAuth2 Client Credentials`. Configure the helper flow as follows, then deploy:
> 
> -   Set the externalized parameter `API_URL` to equal the tenant-specific OData API URL from your service key.
> -   Set the externalized parameter `API_Credential_Alias` to equal the alias of the previously created user credential of type `OAuth2 Client Credentials`.
> -   Maintain the target profile name in the externalized parameter `PartnerDirectory_PID`. By default, the value equals `SAP_Integration_Suite_SkipRetryGlobalProfile` \(see the following\). Change the name to your own preferences.
> -   Maintain the technical ID of the source value mapping in the externalized parameter `ValueMapping_TechnicalID`. By default, the value equals `com.sap.integration.cloud.pipeline.v2.value.mapping.skipretry`. Unless you've copied the original value mapping, keep the value unchanged.
> -   Maintain the source value mapping version in the externalized parameter `ValueMapping_Version`. By default, the value equals `1.0.1`.
> 
> Once you've deployed the helper flow, a new profile with the partner ID as configured in the helper flow is created, the value mappings are read from the value mapping table, and the corresponding exception classes are added as string parameters with the mapped values from the value mapping. You may have to change your profile to your needs.

Next, configure the generic outbound processing flow as follows:

-   Change the externalized parameter `SkipRetriesGlobal_Source` to `PartnerDirectory`.
-   Furthermore, maintain the externalized parameter `SkipRetriesGlobal_SourcePidProfile` to hold the name of the partner ID created previously. By default, the name equals `SAP_Integration_Suite_SkipRetryGlobalProfile`. Change the value to the name you chose previously.



### Scenario-Specific Profile

To configure the skip retry handling for a particular configuration scenario, first create and maintain a new skip retry handling profile in the Partner Directory as described in the previous section.

Then, for your partner ID representing your configuration scenario, create a string parameter `SkipRetriesProfile` with the value equaling the partner ID of the skip retry handling profile. In this case, the global settings are overridden by the scenario-specific profile.



<a name="loioed9b82cb928049e6990a4d784aa6aac7__section_pm1_ggs_5bc"/>

## Custom Exception Handling

As an alternative to the standard retry handling, you can implement your own custom exception handling. The generic integration flows support a kind of custom exit that you can use to run your own custom exception logic without changing the delivered generic integration flows. To do so, you must implement a separate integration flow that's called instead of the standard retry handling if an exception occurs.

To enable the custom exception handling, configure the generic integration flows as follows:

1.  In the integration flow configuration, switch to the tab *More* and set the parameter *CustomXError\_Enabled* to `true` \(the default value is `false`\).

2.  Next, in the tab *Receiver*, select the receiver *CustomErrorFlow* of adapter type *ProcessDirect*. Maintain the end point of the integration flow that should be called in an exception occurs. By default, the value is set to `/pip/custom/errorHandling`. You can keep that value or change it to your preference.

    Instead of the standard retry handling, the local integration process `Call custom error handling` is now called.

3.  You can exchange message headers and the message body between the generic integration flows and the custom exception handling integration flow.

    In a content modifier step, the following headers are passed to the custom exception handling integration flow:


    <table>
    <tr>
    <th valign="top">

    Name
    
    </th>
    <th valign="top">

    Source Type
    
    </th>
    <th valign="top">

    Source Value
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    `exceptionTimestamp`
    
    </td>
    <td valign="top">
    
    Expression
    
    </td>
    <td valign="top">
    
    `${date:now:dd-MM-yyyy HH:mm z}`
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `exceptionStacktrace`
    
    </td>
    <td valign="top">
    
    Expression
    
    </td>
    <td valign="top">
    
    `${exception.stacktrace`
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `exceptionMessage`
    
    </td>
    <td valign="top">
    
    Expression
    
    </td>
    <td valign="top">
    
    `${exception.message}`
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `pipelineStepID`
    
    </td>
    <td valign="top">
    
    Expression
    
    </td>
    <td valign="top">
    
    `${camelId}`
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `partnerID`
    
    </td>
    <td valign="top">
    
    Expression
    
    </td>
    <td valign="top">
    
    `${property.partnerID}`
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    `incomingQueue`
    
    </td>
    <td valign="top">
    
    Expression
    
    </td>
    <td valign="top">
    
    `{{JMS_Incoming}}`
    
    </td>
    </tr>
    </table>
    
    Additionally, the following further headers of the Camel runtime or headers that have already been defined in the generic integration flow before are also passed to the custom exception handling integration flow:

    -   `SAP_Sender`

    -   `SAP_SenderInterface`

    -   `SAP_MessageType`

    -   `SAP_Receiver`

    -   `maxJMSRetries`

    -   `SAPJMSRetries`

    -   `testMode`


    You can use these headers within the custom exception handling integration flow to implement your custom exception logic. If you do so, remember to enter the headers in the *Allowed Header\(s\)* runtime configuration in the custom exception handling integration flow.

4.  In a request reply step, the custom exception handling integration flow is then called via a ProcessDirect adapter.

5.  As response, the headers *customXError\_Status* and *customXError\_EndEvent* are excepted. The headers must be set in the custom exception handling integration flow.

6.  In a content modifier, the custom status is set to the value of the header *customXError\_Status*.

7.  Depending on the value of the *customXError\_EndEvent*, the local integration process ends as follows:

    -   If the value equals *Complete*, it ends with an end event.

    -   If the value equals *Escalated*, it ends with an escalation end event.

    -   In all other cases, it ends with an error end event.



The following screenshot shows the local integration flow as it calls the custom exception handling integration flow:

![](images/Call_custom_error_handling_a64762d.png)

You can either create your custom exception handling flow from scratch or use the provided integration flow `Pipeline v2 Template – Custom Error Handling` from the integration package **Cloud Integration Pipeline - Templates** as template. The `Pipeline v2 Template - Custom Error Handling` has implemented a similar logic like the standard retry handling. If you define your own integration flow from scratch, ensure that the allowed headers are set as described in the previous steps. You also need to pass back the headers *customXError\_Status* and *customXError\_EndEvent*.



<a name="loioed9b82cb928049e6990a4d784aa6aac7__section_xfy_1sn_j1c"/>

## Message Monitoring

To showcase the monitoring handling, the following section discusses the monitoring of a message that fails in the inbound conversion.

In the SAP Integration Suite, go to *Monitor* \> *Integration and APIs* \> *Monitor Message Processing*. Here, you can filter for the **correlation ID**, which shows the logs of the different pipeline steps that have been carried out so far for a particular message. You can also see that Sender and Application Message Type are set as well, so you can also filter for the sender system and the sender interface name.

If the inbound conversion failed, the logs of the scenario-specific conversion integration flow are in status *Failed*. In this example, you see two failed logs because one restart has already been carried out. The custom status is set to *RetryViaParentFlow*, which indicates that the retry is handled by the calling integration flow.

The following is an example of a failed inbound conversion integration flow:

![The screenshot shows the monitoring section in SAP Integration Suite with an example of a failed inbound conversion integration flow.](images/PipelineConcept_Example_of_a_failed_inbound_conversion_flow_55f131c.png)

In the Monitoring section, you can also filter for a **Custom Status**, for example, for *MaxRetriesExceeded*.

The following is an example in which the maximum number of retries has been exceeded:

![The screenshot shows the monitoring section in SAP Integration Suite with an example in which the maximum number of retries has been exceeded.](images/PipelineConcept_Example_where_maximum_number_of_retries_have_been_exceeded_94a1c33.png)



<a name="loioed9b82cb928049e6990a4d784aa6aac7__section_lq1_2sn_j1c"/>

## Dead Letter Queue Handling

If the maximum number of retries has been exceeded, the message is sent to a **dead letter queue**. The name of the queue is provided in the additional information attached to the message processing log.

The following is an example of additional information:

![The screenshot shows the monitoring section in SAP Integration Suite with an example of a dead letter queue mentioned in the message processing log attachments.](images/PipelineConcept_Example_of_additional_information_0b9e0cc.png)

Once you've fixed the root cause of the error, you can reprocess the messages in the dead letter queue: simply move the message from the dead letter queue to the corresponding inbound queue.

> ### Note:  
> In the past, the move feature in the queue monitor only enabled you to move **all messages within a queue**. With the latest software update, you can move a **single message** or **selected messages** from one queue to another.

The following is an example of how to reprocess messages in dead letter queues:

![The screenshot shows the monitoring section in SAP Integration Suite with an example of how to reprocess messages in dead letter queues.](images/PipelineConcept_Reprocess_messages_in_dead_letter_queues_13eee24.png) 



<a name="loioed9b82cb928049e6990a4d784aa6aac7__section_c4h_dkz_zcc"/>

## Custom Header Properties

By default, the generic integration flows automatically add information to the message processing log that help you to better monitor, search, and filter your messages. This information is added as custom header properties. The following custom header properties have been added:

> ### Note:  
> The following list is not complete and can vary depending on the flow and use case.

-   `partnerID`: Partner ID of the configuration scenario.
-   `QualityOfService`: Either `ExactlyOnce` for asynchronous message processing or `BestEffort` for synchronous message processing.
-   `SenderJMSQueue`: JMS queue from which the generic flows reads the message.
-   `ReceiverJMSQueue`: JMS queue to which the generic flows stores the message.
-   `tenantStage`: The virtual landscape stage if landscape staging is used, for example, DEV, DQ, PRD.
-   `SenderAlias`: Sender alias name of landscape staging is used. Otherwise, the alias is displayed as Sender in the Properties section of the message processing log.
-   `ReceiverAlias`: Receiver alias name if landscape staging is used. Otherwise, the alias is displayed as Receiver in the Properties section of the message processing log.
-   `SenderParty`: Sender party name if applicable.
-   `ReceiverParty`: Receiver party name if applicable.
-   `SAP_SenderOperation`: Service interface operation if applicable.
-   `originalPayloadSizeBytes`: Size of the payload at integration flow inbound.

For IDoc inbound and outbound processing, the following custom header properties have been added:

-   `IDocSenderPartner`: Combination of sender partner type, partner number, and port.
-   `IDocReceiverPartner`: Combination of receiver partner type, partner number, and port.
-   `SapIDocTransferId` and `SapIDocDbId`.
-   `overrideControlRecordParameters`: List of IDoc control headers which got overridden.
-   `overrideResultValues`: Corresponding values to parameter before.
-   `AlternativePartner`: Alternative partner of the partner ID to get full transparency about which rule led to the partner ID determination.
-   `SenderLogicalSystem`: Logical system of sender.

If you want to search the message processing logs based on any payload data, you can create custom header properties in the generic integration flows. To do so, you must configure and pass the header `customHeaderProperties` to the generic integration flows.

Depending on your integration scenario, you can configure the header in either the scenario-specific inbound processing flow or the scenario-specific inbound conversion flow.

The following approaches are supported:

-   **Recommended option**: Define exchange properties with prefix `customHeader_` and call the Groovy script `addCustomHeaderProperties` to set the header `customHeaderProperties` as JSON pairs in base64 encoded. In this case, any special characters inside the custom header values are supported.
-   **Alternative option**: Define the header `customHeaderProperties` as a list of name and value pairs.

    > ### Note:  
    > This option uses the characters colon \("`:`"\) and pipe \("`|`"\) to separate name and value and their pairs. Therefore, you can't use this option if the value of the custom header properties contains any of those special characters.

-   **Combination**: For compatibility reasons, you can combine both options.



### Recommended Option: Using Exchange Properties

For each custom header property, you can create an exchange property with prefix `customHeader_` in a content modifier step. The name of the exchange property without the prefix becomes the name of the custom header property.

After the content modifier step, call the Groovy script `addCustomHeaderProperties` from the script collection `Pipeline Generic - Script Collection` of the provided integration package. The script creates the header `customHeaderProperties`, adding the name and value pairs of the previously defined exchange properties with prefix `customHeader_` as JSON format and base64 encodes it. Furthermore, it adds the custom header properties to your scenario-specific integration flow. The header `customHeaderProperties` is then passed to the generic integration flows.

In the generic integration flows, the same Groovy script `addCustomHeaderProperties` encodes the value of the header `customHeaderProperties`, splits up the list of name and value pairs, and adds the custom header properties accordingly.

In the message monitor, you can find the custom headers in the *Properties* tab of the message processing logs of the generic integration flows. In the filter section, you can search for specific custom header values.



### Alternative Option: Directly Maintaining Header CustomHeaderProperties

In a content modifier step, you can create a new header `customHeaderProperties`. Its source value must follow the following pattern:

-   Name and value are separated by colon \(“`:`”\)

-   Name and value pairs are separated by pipe \(“`|`”\)


Optionally, you can call the script `addCustomHeaderProperties` to add the custom header properties to your scenario-specific flow.

In the generic integration flows, the Groovy script `addCustomHeaderProperties` splits up the list of name and value pairs and adds the custom header properties accordingly.

In the message monitor, the custom headers are displayed in the Properties tab of the message processing logs of the generic integration flows. In the filter section, you can search for specific custom header values.



### Provided Templates

The templates `Pipeline v2 Template Step01 - Inbound Processing At Least Once`, `Pipeline v2 Template Step01 - Inbound Processing Exactly Once`, and `Pipeline v2 Template Step01 - Inbound Processing Synchronous` from the integration package **Cloud Integration Pipeline - Templates** contain content modifier flow steps and a Groovy script flow step that support the custom header properties.

If you go for the recommended option, you only need one content modifier in which you define the exchange properties with prefix `customHeader_` and source type `XPath` parsing the incoming XML message. For example, `customHeader_prop_1` and `customHeader_prop_2`.

If you decide to apply the alternative option, in the first content modifier step, you can define exchange properties, for example, prop\_1, prop\_2, by parsing the incoming XML message. In the second content modifier step, you then maintain the name and value pairs in the source value of source type *Expression* of the header `customHeaderProperties` following the following pattern:

`name_1:${property.prop_1}|name_2:${property.prop_2}`

If your incoming payload isn't in XML format, create a script to parse the body of your message. Alternatively, you can define the custom header properties in the scenario-specific inbound conversion flow, if applicable. In this case, refer to the template `Pipeline v2 Template Step03 - Inbound Conversion` from the integration package **Cloud Integration Pipeline - Templates**.

Depending on the option you choose, delete the unnecessary message header or exchange property from the template copy. If you don’t need custom header properties, delete the unnecessary flow steps from the template copy.

