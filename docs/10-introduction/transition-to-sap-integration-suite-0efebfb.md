<!-- loio0efebfbaeeb2408e80a12aae083d400e -->

# Transition to SAP Integration Suite

Review the process for transitioning to SAP Integration Suite.

SAP Integration Suite is used as the primary integration platform and all the interfaces on SAP Process Integration and SAP Process Orchestration are transitioned to SAP Integration Suite. This transition is an opportunity to evaluate the integration scenarios and improve or adapt them to suit the cloud-first architecture. Modern integration approaches like event-based integration can be leveraged to build intelligent scenarios and improve the end-to-end efficiency of business processes.

Adopt [Edge Integration Cell](https://help.sap.com/docs/integration-suite/sap-integration-suite/what-is-sap-integration-suite-edge-integration-cell) for securely running cloud-designed integration content in on-premise environments, enabling a modern and flexible hybrid integration landscape. For more information, see [Hybrid Deployment Using Edge Integration Cell](https://help.sap.com/docs/integration-suite/sap-integration-suite/hybrid-deployment-using-edge-integration-cell).

For in-depth guidance on migrating integration scenarios to SAP Integration Suite, see the learning journey [Migrating to SAP Integration Suite](https://learning.sap.com/learning-journeys/migrating-to-sap-integration-suite).



<a name="loio0efebfbaeeb2408e80a12aae083d400e__section_adr_nry_qqb"/>

## Transitioning to the Cloud

The following three steps build your process of transitioning to the cloud: assess, transform, and move.



### Assess

Assess your existing landscape and identify areas of improvement and innovation for you envisioned target landscape, which can amplify the benefit of transitioning to the cloud.

The following tools and assets can help with the assessment:

-   **[Assess the Landscape](../20-landscape/landscape-ca24a08.md)**: A detailed assessment of the existing integration landscape and the involved artifacts provides an overview of the artifacts that can be reused, refactored, and developed from scratch. This ensures optimum reuse while accelerating your move and saving costs at the same time

-   The **[SAP Integration Solution Advisory Methodology](https://help.sap.com/docs/integration-suite/sap-integration-suite/sap-integration-solution-advisory-methodology)** tool evaluates the current integration maturity level of an organization and provides possible improvements.

-   As enterprise-grade integration scenarios must be scalable, robust, and secure, the **[Integration Flow Design Guidelines](https://help.sap.com/docs/cloud-integration/sap-cloud-integration/integration-flow-design-guidelines?version=Cloud)** provide best practices that can be used to build such high-quality integration scenarios. They contain patterns, tips and tricks, and development best practices that can act as guiding principles for development.

-   A **future-proof integration strategy** ensures that you're prepared for the next steps in your digital transformation journeys. It's critical to factor this into your overall strategy to control costs and encourage innovation.

-   The **[Migration Assessment](https://help.sap.com/docs/SAP_INTEGRATION_SUITE/51ab953548be4459bfe8539ecaeee98d/5c5e50ee2d644cc59d864409d5b7871c.html)** tool in SAP Integration Suite helps to estimate the technical effort involved in the migration process and evaluate how your integration scenarios might be migrated from SAP Process Orchestration to SAP Integration Suite. In addition to evaluating migration feasibility, it also provides Modernization Recommendations, which highlight ways to adapt integration scenarios in line with current SAP strategy and modern integration practices.




### Transform

One of the primary objectives of moving to the cloud and to SAP Integration Suite is to digitally transform your organization. The key component in this transformation journey is to upgrade, refactor, and build modern business process and customer experiences that leverage the latest integration patterns, like API-first approach, event-sensing capability, and machine learning-based interface development. While a lift and shift may sound like the path of least resistance, a transformation with a KPI to improve business process efficiency and user experience results in maximum return on investment.

The following pointers can guide you in the transformation journey:

-   **[Accelerate Using Prebuilt Integrations from SAP Business Accelerator Hub](https://api.sap.com/)**: One of the key differentiators of SAP Integration Suite is the business content provided on SAP Business Accelerator Hub, which accelerates your development project and saves you maintenance effort. The content is managed by the content owners who provide upgrades and patches that can be consumed with a few clicks and no impact to running processes. If standard unedited content is used for SAP-to-SAP integration, the messages processed by this are free of cost. Customization of this standard content can be done through extensions that don't disrupt the lifecycle of the prepackaged content.

-   **[Leverage Events](https://learning.sap.com/learning-journeys/discovering-event-driven-integration-with-sap-integration-suite-advanced-event-mesh)**: A modern-day integration landscape takes advantage of APIs and events to build an intelligent enterprise. The scenarios can be configured to sense and respond to business events in real time. Communication is simplified with APIs that not only provide a greater degree of control over the way data is exposed, but also protect the mission backend systems. An API-first approach is recommended to build a landscape that is open to innovation and helps deliver world-class customer experience.

-   **[Secure the Cloud](https://learning.sap.com/courses/architecting-security-for-sap-business-technology-platform)**: Cloud-first strategy should be coupled with enterprise-grade security to ensure data confidentiality and protection. There are various approaches to securing cloud-based business processes, in addition to the security features provided by the SaaS service providers. SAP Integration Suite offers security policy templates that offer enterprise-grade security and ensure that APIs are protected at the highest possible standards.




### Move

To make your transition to SAP Integration Suite efficient, the steps involved ensure that existing integration assets are reused as much as possible to reduce costs and time, while also supporting that transformation goals are achieved.

-   **[Connectivity Migration](../30-connectivity/connectivity-94ab030.md)**: The connectivity in the on-premise SAP Process Integration and SAP Process Orchestration systems must be migrated to the respective adapters and connectors on SAP Integration Suite. In this step, the protocols used in these communication channels are evaluated and equivalent connectivity options should be chosen on SAP Integration Suite.

-   **[Security](../40-security/security-dd0fb21.md)**: The security aspects of a cloud-based integration platform depend on two main factors: security features provided by the platform \(in this case SAP\), and the security configurations that are developed to protect the integration scenarios using the features provided by the platform. This security guide provides an overview of the security aspects that should be considered when moving to SAP Integration Suite from SAP Process Integration and SAP Process Orchestration.

-   **[Error Handling and Logging](../50-error-handling-and-logging/error-handling-and-logging-strategy-8faa23e.md)**: When transitioning to a cloud-based integration platform, you also require a cloud-based error handling and logging strategy. Learn about the different approaches and adapt to the error handling and logging features provided by SAP Integration Suite.

-   **[Interface Governance](../60-interface-governance/interface-governance-e8819d7.md)**: Understand how interfaces are governed in the cloud and how to manage them across multiple landscapes. Learn about how transport service on the SAP Business Technology Platform can be used to implement an interface governance model.

-   **[Interface Migration](../70-interface-migration/interface-migration-0cab9f4.md)**: Understand the different aspects involved in moving interfaces from SAP Process Integration and SAP Process Orchestration to SAP Integration Suite. Learn about scenario and object assessment and how parts of testing can be automated with the available tools.


