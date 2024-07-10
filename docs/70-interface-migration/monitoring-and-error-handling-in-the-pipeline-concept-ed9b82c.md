<!-- loioed9b82cb928049e6990a4d784aa6aac7 -->

# Monitoring and Error Handling in the Pipeline Concept

Perform monitoring and error handling in the pipeline concept, for example by using retry handling, message monitoring, and using the dead letter queue.



The following measures improve monitoring and error handling in the pipeline concept:

-   Use **SAP headers** to search for messages based on sender system, interface/message type, and receiver system.

-   Set a **custom status** for more information on the error root cause.
-   Use **retry handling** to limit the number of overall retries. See [Standard Retry Handling](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md#loioed9b82cb928049e6990a4d784aa6aac7__section_l3k_qrn_j1c).

-   User **custom exception handling** as an alternative to the standard retry handling and implement your own logic. See [Custom Exception Handling](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md#loioed9b82cb928049e6990a4d784aa6aac7__section_pm1_ggs_5bc).
-   With a **dead letter queue**, you can park messages for which the maximum number of retries has been exceeded. See [Dead Letter Queue](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md#loioed9b82cb928049e6990a4d784aa6aac7__section_lq1_2sn_j1c).

-   Attach **additional information to the message processing log** if errors occur.




<a name="loioed9b82cb928049e6990a4d784aa6aac7__section_l3k_qrn_j1c"/>

## Standard Retry Handling

If you want to define a scenario-specific retry behavior, you need to create a string parameter with ID `MaxJMSRetries`. Otherwise, the maximum number of retries is set to unlimited. In the generic inbound processing integration flow, this parameter is read from the Partner Directory and written in the message header `maxJMSRetries`. The header is passed to all other integration flows in the sequence of flows.

In all integration flows that read from a JMS queue, the following standard retry handling is implemented. For custom retry handling, see [Custom Exception Handling](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md#loioed9b82cb928049e6990a4d784aa6aac7__section_pm1_ggs_5bc).

If a message processing error occurs, the error is fetched in an exception subprocess. Within the exception subprocess, a local integration process is called. Then, the local integration process checks if the maximum number of retries has already been exceeded using the following condition expression:

```
${header.SAPJMSRetries} > ${header.maxJMSRetries} and ${header.maxJMSRetries} != 'unlimited'
```

The default route, that is, if the maximum number of retries hasn't been exceeded, sets the custom status to *AutomaticRetry* and then ends with an **error end event**. This means that the message remains in the status *Failed* and is retried from the inbound JMS queue.

Otherwise, if the maximum number of retries has been exceeded, the custom status is set to `MaxRetriesExceeded`. In a Groovy script, additional information about the inbound queue name and the dead letter queue name is attached to the message processing log. The name of the dead letter queue follows the following pattern:

`<name of the inbound queue>_DLQ`

The message is then written to the dead letter queue and ends with an end event, which then sets the message status to *Successful*.

The following is an example of retry handling:

![The screenshot shows the integration flow editor with an example of retry handling using an exception subprocess and a dead letter queue.](images/PipelineConcept_RetryHandling_99dcda0.png)



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

You can either create your custom exception handling flow from scratch or use the provided integration flow `Pipeline Template – Custom Error Handling` as template. The `Pipeline Template - Custom Error Handling` has implemented a similar logic like the standard retry handling. If you define your own integration flow from scratch, ensure that the allowed headers are set as described in the previous steps. You also need to pass back the headers *customXError\_Status* and *customXError\_EndEvent*.



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
> Currently, you can't move a **single message** from one queue to another. The move feature in the queue monitor only enables you to move **all messages within a queue**.

The following is an example of how to reprocess messages in dead letter queues:

![The screenshot shows the monitoring section in SAP Integration Suite with an example of how to reprocess messages in dead letter queues.](images/PipelineConcept_Reprocess_messages_in_dead_letter_queues_13eee24.png) 

