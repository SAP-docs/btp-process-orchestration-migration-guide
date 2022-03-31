<!-- loio32b979958c8e4ed79fa1061801ca1746 -->

# Custom Adapter Migration

If you, or your implementation partner, have implemented fully bespoke adapters for SAP Process Orchestration, you may need to have these reimplemented using the Adapter Development Kit \(ADK\) provided for Cloud Integration.

It may be of value to assess the marketplace to determine whether an OEM partner has already implemented an adapter that provides the connectivity you require. Some of the adapters provided by SAP partners are fully SAP-certified and fully supported for several non-SAP systems. There are many adapters like Salesforce, ServiceNow, Workday, etc. available out-of-the-box in SAP Integration Suite. For a full list of available adapters, see [Configure Adapter in Communication Channels](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/1f066330e8314324bf3ebe3b6adc21b2.html).

You can search on [API Business Hub](https://api.sap.com/) and the internet for different OEM partners and their adapters.

If an OEM adapter isn't available, an additional alternative is to use the SAP Open Connectors service, which is one of the key complimentary components of the SAP Integration Suite. Open Connectors provides out-of-the-box connectivity to more than 170 non-SAP applications or services. It provides harmonized RESTful APIs with built-in interactive API documentation using OpenAPI Specification and normalized authentication, which provides built in security capabilities for secure robust connectivity to third-party applications. It also drastically reduces the time needed to connect to top non-SAP SaaS applications.

Once a connection instance to a particular non-SAP system has been configured, the built-in Open Connectors adapter in Cloud Integration can seamlessly connect to it using configurable authentication credentials to perform the usual CRUD \(Create, Read, Update, Delete\) operations.

The following blogs provide details on the topic:

-   [Google Calendar’s Info with API Management and Open Connectors Services](https://blogs.sap.com/2020/02/20/google-calendars-info-with-api-management-and-open-connectors-services/)

-   [How to create a sample integration scenario using Open Connectors Adapter](https://blogs.sap.com/2019/03/13/cloud-integration-how-to-create-a-sample-integration-scenario-using-open-connectors-adapter/)

-   [The SAP Open Connectors service by Cloud Elements](https://www.youtube.com/watch?v=W0qGNqucNaw&ab_channel=SAPTechnology) \(video\)


If neither of these options provides a solution, the final option is the reimplementation of your custom adapter using the ADK. As both Process Orchestration and Cloud Integration are based on Java, and the adapters are, too, a significant proportion of coding can be ported easily.

The ADK is available for download from [SAP Development Tools - Cloud Integration](https://tools.hana.ondemand.com/#cloudintegration). The deployment of adapters can be done via the Web UI of Cloud Integration.

The blog [Cloud Integration Adapter development using Maven Project perspective](https://blogs.sap.com/2017/07/27/sap-cloud-integration-adapter-development-using-maven-project-perspective/) walks you through the process of adapter development by illustrating the creation of a simple sample adapter. Additionally, the blog [Cloud Integration - Developing Custom Adapters to access On-Premise systems](https://blogs.sap.com/2019/10/31/cloud-integration-developing-custom-adapters-to-access-on-premise-systems/) illustrates the creation of a custom adapter that is able to communicate with on-premise systems via Cloud Connector.

