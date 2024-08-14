<!-- loio6e527fb074834af2be2546c6e7e2fa5f -->

# Pipeline Concept

The **pipeline concept** allows you to set up your asynchronous integration scenarios in Cloud Integration similarly to how messages are processed in SAP Process Integration and SAP Process Orchestration, in pipelines.





### Pipelines in SAP Process Orchestration

In SAP Process Integration and SAP Process Orchestration, messages are processed in **pipelines**. A pipeline is the sum of all steps of processing a message. It consists of a set of pipeline elements that call pipeline services, for example, for carrying out the mapping or routing the messages to different receivers.

While you’re flexible in orchestrating the message flows in Cloud Integration, pipelines in SAP Process Integration and SAP Process Orchestration are static. Each pipeline consists of a fixed number of pipeline steps in a fixed order. For example, when a message is processed within the SAP Process Orchestration runtime, first the receiver is determined, then the interface, and then the mapping is carried out.



### Who Can Use the Pipeline Concept?

Use the pipeline concept either as an alternative approach or as an addition to the individual migration of single integration scenarios supported by the [migration tooling](https://help.sap.com/docs/integration-suite/sap-integration-suite/migration-tooling) within SAP Integration Suite or other migration tools by partners.

The applicability of the pipeline concept depends on the number and types of your integration scenarios. If you only want to migrate a few integration scenarios to Cloud Integration, it can be easier to create individual integration flows for each of your original integration scenarios. If you have a **large number of integration scenarios**, the pipeline concept can speed up the migration project and reduce effort and cost, for example, for operating and monitoring your integration scenarios in the Cloud Integration.



### Handling JMS Queues

The pipeline concept improves the JMS queue handling for asynchronous integration scenarios in Cloud Integration. As resources on an SAP Integration Suite tenant are limited, you must model your integration flows to suit the resource limits of your tenants. See [Run an Integration Flow Under Well-Defined Boundary Conditions](https://help.sap.com/docs/integration-suite/sap-integration-suite/run-integration-flow-under-well-defined-boundary-conditions). If you migrate your asynchronous integrated configuration scenarios in SAP Process Orchestration to integration flows in Cloud Integration one by one and use an own JMS queue for each integration flow to ensure exactly once delivery, you end up with a high number of JMS queues. Depending on your use case, you may need thousands of JMS queues.

With the pipeline concept, you can reduce the number of JMS queues you need to run your integration scenarios on Cloud Integration. With proper usage of JMS queues and ProcessDirect adapters and relying on the Partner Directory to be able to dynamically configure your integration flows, you can reduce the number of required JMS queues to four. With four more JMS queues for the retry and dead letter handling, you arrive at eight required JMS queues. Even if you duplicate the set of integration flows to build up multiple pipelines, for example, to handle low, medium, and high priority scenarios, you only need a low number of JMS queues. These few JMS queues are easier to handle than the thousands of JMS queues of a typical migration use case.



<a name="loio6e527fb074834af2be2546c6e7e2fa5f__section_onh_jnk_31c"/>

## Key Elements



### Integration Flows

In the pipeline concept, each step corresponds to an integration flow. There are two types of integration flows: **Generic integration flows** and **scenario-specific integration flows**. The generic integration flows are used across all integration scenarios and must only be deployed once. Scenario-specific integration flows handle the scenario-specific message conversions and mappings. They're either created manually or generated using a migration tool. In both cases, integration artifacts such as message types and mappings can be reused.

In general, the integration flows are decoupled using JMS queues. This ensures that messages can be restarted and is a prerequisite for guaranteed delivery. Using pipelines, you can drastically reduce the number of required JMS queues.

See [Pipeline Steps](pipeline-steps-f8e69f4.md).



### ProcessDirect Adapter

Use the ProcessDirect adapter to call the scenario-specific integration flows. The adapter establishes fast and direct communication between integration flows by reducing latency and network overhead. A disadvantage of using the ProcessDirect adapter is that the connection between the integration flows is synchronous: If the integration flow called by ProcessDirect fails, it remains in the status `Failed` even if the calling integration flow can handle the retry of the message. Replacing the ProcessDirect connection with a JMS connection isn't an option as it would again result in a large number of JMS queues.

You can overcome the ProcessDirect disadvantage in a way that balances handling resource limitations and operation costs. Monitoring and operation is improved by maintaining SAP headers and custom status. Furthermore, you can implement a retry handling of failed messages including dead letter queues in which the messages that have exceeded the maximum number of retries can be parked. See [Monitoring and Error Handling in the Pipeline Concept](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md).



### Partner Directory

The Partner Directory helps to define the message processing behavior. For example, you can define a scenario-specific maximum number of retries or receiver-specific outbound queues. You can also use the Partner Directory to dynamically configure the generic integration flows, which helps to reduce the number of required JMS queues.

See [Using the Partner Directory in the Pipeline Concept](using-the-partner-directory-in-the-pipeline-concept-9ec7d2d.md).



### XSLT Mappings

XSLT mappings are used to carry out the receiver determination and interface split pipeline steps. The idea comes from the extended receiver determination capability in SAP Process Orchestration, which allows you to run an operation mapping to determine your receivers in a content-based router or recipient list pattern. XSLT mappings simplify the integration flow models of the receiver determination and interface split: Instead of a combination of multicast branches and multiple routers for all your content-based router xpath expressions, which complicates your integration flow model, simply run the xpath expressions within an XSLT mapping. This makes the model more neat and easier to read. Additionally, the concept uses XSLT instead of graphical message mapping because the Partner Directory supports XSLT mappings. This way, the usage of XSLT in combination with the Partner Directory contributes to the reduction of the number of required JMS queues.

See [XSLT Mappings](using-the-partner-directory-in-the-pipeline-concept-9ec7d2d.md#loio9ec7d2dce72d423abff80543f11b2091__section_thd_scz_31c).



<a name="loio6e527fb074834af2be2546c6e7e2fa5f__section_n2d_t2f_l1c"/>

## Special Cases

Besides the generic cases, the pipeline concept also considers the following special scenarios:

-   For scenarios in which **sender systems connect to Cloud Integration via the XI message protocol**, you can use a generic inbound integration flow that acts as one single entry point for XI proxy inbound scenarios. See [XI Sender Adapter](special-cases-1606af9.md#loio1606af9b55bf4391bea01d2f7ee112af__section_vcg_m1f_j1c).

-   For scenarios in which **sender systems connect to Cloud Integration via the IDoc sender adapter**, you can use a generic inbound integration flow that acts as one single entry point for IDoc inbound scenarios. See [IDoc Sender Adapter](special-cases-1606af9.md#loio1606af9b55bf4391bea01d2f7ee112af__section_tjw_z3f_j1c).

-   If your integration scenario on SAP Process Orchestration uses the **extended receiver determination**, you can reuse the receiver determination mapping instead of the XSLT mapping. See [Reuse Extended Receiver Determination](special-cases-1606af9.md#loio1606af9b55bf4391bea01d2f7ee112af__section_kjy_1jf_j1c).

-   By default, each scenario uses the same set of generic JMS queues. For scenarios in which you want to **control the outbound delivery**, you can define receiver-specific JMS queues. See [Receiver-Specific Outbound Queues](special-cases-1606af9.md#loio1606af9b55bf4391bea01d2f7ee112af__section_n2d_cjf_j1c).

-   For Point-to-Point scenarios, you can skip the two pipeline steps `receiver determination` and `interface determination`. See [Point-to-Point Scenarios](special-cases-1606af9.md#loio1606af9b55bf4391bea01d2f7ee112af__section_bdm_kc3_hcc).

See [Special Cases](special-cases-1606af9.md).

-   **[Pipeline Steps](pipeline-steps-f8e69f4.md "The pipeline concept works with a fixed sequence of integration flows, the pipeline
		steps. ")**  
The pipeline concept works with a fixed sequence of integration flows, the pipeline steps.
-   **[Using the Partner Directory in the Pipeline Concept](using-the-partner-directory-in-the-pipeline-concept-9ec7d2d.md "In the pipeline concept, most generic integration flows rely on the Partner Directory.
		This topic discusses parameters in the Partner Directory that help to define the message
		processing behavior and the XSLTs that are stored in the Partner Directory as binaries and
		used to dynamically determine receivers and interfaces. ")**  
In the pipeline concept, most generic integration flows rely on the Partner Directory. This topic discusses parameters in the Partner Directory that help to define the message processing behavior and the XSLTs that are stored in the Partner Directory as binaries and used to dynamically determine receivers and interfaces.
-   **[Script Collection for Pipeline Concept](script-collection-for-pipeline-concept-05d9f8d.md "Use the scripts collected in this section to read the Partner Directory.")**  
Use the scripts collected in this section to read the Partner Directory.
-   **[Special Cases](special-cases-1606af9.md "Before you get started with the pipeline concept, consider a few special cases, like the
		XI sender adapter, the IDoc sender adapter, reusing extended receiver determination,
		receiver-specific outbound queues, and the bypass option for Point-to-Point
		scenarios.")**  
Before you get started with the pipeline concept, consider a few special cases, like the XI sender adapter, the IDoc sender adapter, reusing extended receiver determination, receiver-specific outbound queues, and the bypass option for Point-to-Point scenarios.
-   **[Monitoring and Error Handling in the Pipeline Concept](monitoring-and-error-handling-in-the-pipeline-concept-ed9b82c.md "Perform monitoring and error handling in the pipeline concept, for example by using
		retry handling, message monitoring, and using the dead letter queue.")**  
Perform monitoring and error handling in the pipeline concept, for example by using retry handling, message monitoring, and using the dead letter queue.
-   **[Customizing the Pipeline Concept](customizing-the-pipeline-concept-aeb106f.md "You can apply the pipeline concept as a template and fit it to your custom needs. For example, implement your own exception handling, or
		define a different global maximum number of retries.")**  
You can apply the pipeline concept as a template and fit it to your custom needs. For example, implement your own exception handling, or define a different global maximum number of retries.
-   **[Testing the Pipeline](testing-the-pipeline-e373569.md "SAP's partners provide regression test tools that you can use to test your integration scenarios and apply the pipeline
		concept.")**  
SAP's partners provide regression test tools that you can use to test your integration scenarios and apply the pipeline concept.

