<!-- loioaeb106f049144c71a0b7814a2ffedc3f -->

# Customizing the Pipeline Concept

You can apply the pipeline concept as a template and fit it to your custom needs. For example, implement your own exception handling, or define a different global maximum number of retries.

The pipeline concept package provided on the SAP Business Accelerator Hub supports some extension points that allow you to customize the message processing behavior without having to change the standard generic integration flows. This way, you can ensure that the standard integration content still receives updates. See [Updates for SAP's Integration Packages](https://help.sap.com/docs/integration-suite/sap-integration-suite/updates-for-sap-s-integration-packages).

The following extensions and standard customizations are supported:

-   You can implement your own custom exception handling. See [Custom Exception Handling](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md#loioed9b82cb928049e6990a4d784aa6aac7__section_pm1_ggs_5bc).

-   You can configure the message end event type in case messages are stored in a dead letter queue. The default is *Escalated*. See [Standard Retry Handling](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md#loioed9b82cb928049e6990a4d784aa6aac7__section_l3k_qrn_j1c).

-   You can configure a pipeline JMS queue prefix, which simplifies configuring queue names if you create another set of generic integration flows.

-   As all adapter parameters of the generic integration flows have been externalized, you can configure their adapters.


Depending on your needs, you can modify the provided standard package. For example, you can customize the identification of scenarios, the status of the ProcessDirect flow, and the retry handling.

> ### Note:  
> If you modify the standard integration flows, you won't receive any updates SAP provides for the pipeline concept package.



<a name="loioaeb106f049144c71a0b7814a2ffedc3f__section_dfx_r1f_j1c"/>

## Identifying a Scenario

In SAP Process Orchestration, a scenario is uniquely defined via party, sender component, sender interface, namespace, and virtual receiver. In the pipeline concept, a scenario is identified using only sender component and sender interface. Depending on your specific requirements, you can extend the scenario definition. For example, change the partner ID to fetch the Partner Directory information accordingly.



<a name="loioaeb106f049144c71a0b7814a2ffedc3f__section_wzs_t1f_j1c"/>

## Status of ProcessDirect Integration Flows

If a scenario-specific integration flow that's called via the ProcessDirect adapter fails, the exception is fetched in an exception subprocess. In this exception subprocess, the custom status is set and the integration flow ends with an error end event. This ensures that the generic integration flow calling the scenario-specific integration flow keeps the message in the inbound queue until it's eventually retried. Furthermore, in the message monitor, the message processing log of the scenario-specific flow turns into status *Failed* with custom status *RetryViaParentFlow*.

If you prefer the scenario-specific integration flow \(or child flow\) to be set to *Completed* instead of *Failed* because the retry is handled by calling the generic integration flow \(or parent flow\) anyway, you can change the child flow's exception subprocess as follows:

1.  Switch the *error end event* with an *end event*.

2.  Set a header such as `error_occured` with value `true`. The header is then passed to the parent flow, showing that an error occurred in the child flow.

3.  In the parent flow, add a router after the request reply step that checks for the `error_occured` value, and, if `true`, raises an exception. Otherwise, the message in the parent flow isn't retried.


For a similar scenario, see [Handle Exceptions in Dependent Integration Flows](https://help.sap.com/docs/integration-suite/sap-integration-suite/handle-exceptions-in-dependent-integration-flows).



<a name="loioaeb106f049144c71a0b7814a2ffedc3f__section_sxr_51f_j1c"/>

## Retry Handling

For errors occurring in message processing, you can define a **scenario-specific maximum number of retries**. By default, if no such value is defined in the Partner Directory for the specific scenario, the number of retries is **5**.

You can change the global setting to any other value by adapting the Groovy script `readRetryHandlingFromPD`. In the following example, the default value is `10`.

> ### Note:  
> Since the header `SAPJMSRetries` is incremented after the retry, you must increment the `maxJMSRetries` by 1 to achieve 10 retries.

```
    // read retry handling from the Partner Directory
    def maxJMSRetries = service.getParameter("MaxJMSRetries", Pid , String.class);
    
    // if the value exists in the Partner Directory, create a new header holding the max number of retries incremented by 1
    // otherwise, set the header to default which is 10
    message.setHeader("maxJMSRetries", maxJMSRetries ? maxJMSRetries.toInteger() - 1 : '9');
```

