<!-- loio0efebfbaeeb2408e80a12aae083d400e -->

# Transition to SAP Integration Suite

There are two approaches in which you can plan to transition to SAP Integration Suite. In the first approach, which is the recommended one, all SAP Process Integration and SAP Process Orchestration interfaces are transitioned to SAP Integration Suite. In the second approach, SAP Process Integration and SAP Process Orchestration are used for a limited set of scenarios, predominantly for on-premise-to-on-premise integration scenarios. All cloud-to-cloud and hybrid integration scenarios are deployed and maintained on SAP Integration Suite.



<a name="loio0efebfbaeeb2408e80a12aae083d400e__section_gj3_nry_qqb"/>

## 1. Transition All Your Interfaces on SAP Process Integration or SAP Process Orchestration to SAP Integration Suite \(Recommended\)

In this approach, SAP Integration Suite is used as the primary integration platform and all the interfaces on SAP Process Integration and SAP Process Orchestration are transitioned to SAP Integration Suite. This transition is an opportunity to evaluate the integration scenarios and improve or adapt them to suit the cloud-first architecture. Modern integration approaches like event-based integration can be leveraged to build intelligent scenarios and improve the end-to-end efficiency of business processes.



<a name="loio0efebfbaeeb2408e80a12aae083d400e__section_sn4_nry_qqb"/>

## 2. Use SAP Integration Suite with SAP Process Integration or SAP Process Orchestration for Few Scenarios

In this approach, too, SAP Integration Suite is the primary integration platform. All the new scenarios including cloud-to-cloud and cloud-to-on-premise are deployed on SAP Integration Suite. Only on-premise-to-on-premise integration scenarios are deployed on the existing SAP Process Integration and SAP Process Orchestration landscape. If this approach is preferred, it's recommended to follow these steps as a high-level strategy for choosing the integration platform:

-   Transition existing cloud and hybrid scenarios to SAP Integration Suite

-   Upgrade to SAP NetWeaver 7.5

-   Build all new scenarios on SAP Integration Suite and deploy on-premise scenarios on the Cloud Integration runtime available in SAP NetWeaver 7.5

-   Transition to the [Hybrid Deployment Option](https://roadmaps.sap.com/board?PRODUCT=000D3A47875C1EDB98A8A910864AC24B&range=CURRENT-LAST#;INNO=901B0ED1A0641EDABE80AF561BFAC0F8) when it's released


A detailed explanation of this strategy is available in the article [Technical Guide: Transitioning to SAP Cloud Platform Integration Suite](https://sapinsider.org/articles/technical-guide-transitioning-to-sap-cloud-platform-integration-suite/).



<a name="loio0efebfbaeeb2408e80a12aae083d400e__section_adr_nry_qqb"/>

## Transition to the Cloud in Three Easy Steps



### Assess

The assessment of the integration landscape, both existing and the envisioned target landscape, is an important step in the overall transition to the cloud. The transition is an opportunity to assess various aspects of the existing landscape and identify areas of improvement and innovation. This exercise will provide a lot of value and amplify the benefit of transitioning to the cloud.

The following tools and assets can help with this assessment exercise:

-   **[Integration Value Calculator](https://www.sap.com/dmc/exp/2021-05-76145-integration-value-calculator/index.html)**: This tool provides a subjective view of the cost savings that can be achieved with SAP Integration Suite. It offers a wizard-like experience where certain parameters like the type of integrations, average price per hour for integration consultants, duration, etc. are considered to provide an estimate of how much cost can be saved by transitioning to SAP Integration Suite.

-   **[SAP Integration Solution Advisory Methodology](https://www.sap.com/dmc/exp/2020-05-68434/en-us/index.html)**: The SAP Integration Solution Advisory Methodology tool analyses the integration maturity of an organization and provides possible ways to improve it and take it to the next level. The result of this tool provides an evaluation of the current integration maturity level and actionable suggestions to improve this.

-   **[Integration Flow Design Guidelines](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/6803389050a0487ca16d534583414d2b.html)**: Enterprise-grade integration scenarios must be scalable, robust, and secure. The design guidelines provide best practices that can be used to build such high-quality integration scenarios. They contain certain patterns, tips and tricks, and development best practices that can act as guiding principles for development.

-   **[Future-proof Integration Strategy](https://www.sap.com/documents/2020/07/b00a39ed-a07d-0010-87a3-c30de2ffd8ff.html)**: A future-proof integration strategy ensures that organizations are prepared for the next steps in their digital transformation journeys. It's critical for organizations to factor this into the overall strategy to control costs and encourage innovation at the same time.




### Transform

One of the primary objectives of moving to the cloud and to SAP Integration Suite is to digitally transform your organization. The key component in this transformation journey is to upgrade, refactor, and build modern business process and customer experiences that leverage the latest integration patterns like API-first approach, event-sensing capability, and machine learning based interface development. It's important to understand that while a lift and shift sounds like the path of least resistance, a transformation with a KPI to improve business process efficiency and user experience results in maximum return on investment.

The following pointers can guide you in the transformation journey:

-   **[Accelerate Using Prebuilt Integrations from SAP API Business Hub](https://api.sap.com/)**: One of the key differentiators of SAP Integration Suite is the business content that is provided on SAP API Business Hub. This not only accelerates your development project but also saves you time and effort on maintenance. The content is managed by the content owners who provide upgrades and patches that can be consumed with a few clicks and no impact to running processes. If standard unedited content is used for SAP-to-SAP integration, the messages processed by this are free of cost. Customization of this standard content can be done through extensions that don't disrupt the lifecycle of the prepackaged content.

-   **[Leverage APIs and Events](https://www.youtube.com/watch?v=98FNX-HFdGg)**: A modern-day integration landscape takes advantage of APIs and events to build an intelligent enterprise. The scenarios can be configured to sense and respond to business events in real time. Communication is simplified with APIs that not only provide a greater degree of control over the way data is exposed, but also protect the mission backend systems. An API-first approach is recommended to build a landscape that is open to innovation and helps deliver world-class customer experience.

-   **[Secure the Cloud](https://api.sap.com/package/SecurityBestPractices/policytemplate)**: Cloud-first strategy should be coupled with enterprise-grade security to ensure data confidentiality and protection. There are various approaches to securing cloud-based business processes, in addition to the security features provided by the SaaS service providers. SAP Integration Suite offers security policy templates that offer enterprise-grade security and ensure that APIs are protected at the highest possible standards.




### Move

The Move step is designed to provide the most efficient way to transition to SAP Integration Suite from SAP Process Integration and SAP Process Orchestration. The steps involved ensure that existing integration assets are reused as much as possible to reduce costs and time, while also ensuring that the transformation goals are achieved.

-   **[Assess the Landscape](../20-landscape/landscape-ca24a08.md)**: A detailed assessment of the existing integration landscape and the involved artifacts with reference to the target landscape provides an overview of the artifacts that can be reused, refactored, and developed from scratch. This exercise ensures optimum reuse while accelerating your move and saving costs at the same time.

-   **[Connectivity Migration](../30-connectivity/connectivity-94ab030.md)**: The connectivity in the on-premise SAP Process Integration and SAP Process Orchestration systems must be migrated to the respective adapters and connectors on SAP Integration Suite. In this step, the protocols used in these communication channels are evaluated and equivalent connectivity option should be chosen on SAP Integration Suite.

-   **[Security](../40-security/security-dd0fb21.md)**: The security aspects of a cloud-based integration platform depend on two main factors: security features provided by the platform, which in this case is SAP, and the security configurations that are developed to protect the integration scenarios using the features provided by the platform. This security guide provides an overview of the security aspects that should be considered when moving to SAP Integration Suite from SAP Process Integration and SAP Process Orchestration.

-   **[Error Handling and Logging](../50-error-handling-and-logging/error-handling-and-logging-strategy-8faa23e.md)**: Transitioning to a cloud-based integration platform necessitates the requirement for a cloud-based error handling and logging strategy. The objective of this exercise is to understand the different approaches and adapt to the error handling and logging features provided by SAP Integration Suite.

-   **[Interface Governance](../60-interface-governance/interface-governance-e8819d7.md)**: Understand how interfaces are governed in the cloud and how to manage them across multiple landscapes. Learn about how transport service on the SAP Business Technology Platform can be used to implement an interface governance model.

-   **[Interface Migration](../70-interface-migration/interface-migration-0cab9f4.md)**: Understand the different aspects involved in moving interfaces from SAP Process Integration and SAP Process Orchestration to SAP Integration Suite. Learn about scenario and object assessment and how parts of testing can be automated with the available tools.


