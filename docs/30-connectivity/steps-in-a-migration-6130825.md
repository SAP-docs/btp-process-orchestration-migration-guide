<!-- loio6130825edd4045d29d403f0a93bbc0f8 -->

# Steps in a Migration

Follows these several structured steps to migrate your communication channels from an SAP Process Orchestration format to a Cloud Integration format.

-   [Assess and document the adapter configurations in use](steps-in-a-migration-6130825.md#loio6130825edd4045d29d403f0a93bbc0f8__section_iqr_v1f_mqb)

-   [Group and classify configurations according to key criteria](steps-in-a-migration-6130825.md#loio6130825edd4045d29d403f0a93bbc0f8__section_t3x_v1f_mqb)
-   [Map standard adapters from SAP Process Orchestration to Cloud Integration](steps-in-a-migration-6130825.md#loio6130825edd4045d29d403f0a93bbc0f8__section_gbz_v1f_mqb)
-   [Reimplement custom adapters or explore alternatives](steps-in-a-migration-6130825.md#loio6130825edd4045d29d403f0a93bbc0f8__section_i1b_w1f_mqb)
-   [Reimplement adapter modules or explore alternatives](steps-in-a-migration-6130825.md#loio6130825edd4045d29d403f0a93bbc0f8__section_udc_w1f_mqb)



<a name="loio6130825edd4045d29d403f0a93bbc0f8__section_iqr_v1f_mqb"/>

## Assess and Document the Adapter Configurations in Use

The integration artifacts in SAP Process Orchestration differ from those in Cloud Integration. In SAP Process Orchestration, there's a clear distinction between design time objects \(interfaces, mappings, …\) and configuration time objects \(channels, Integrated Configuration objects\). In Cloud Integration, there's no distinction between those objects as everything is encapsulated within one artifact called integration flow.

In SAP Process Orchestration, adapter configurations are maintained in communication channel objects. Each communication channel defines which transport protocol to use, specified as an adapter type, and several configuration parameters that define, for example, hostname, port, user, and password to the remote system.

Each communication channel in use in a particular SAP Process Orchestration system needs to be analyzed in order to map it to a corresponding communication channel definition in Cloud Integration.

Details on this topic are discussed in the sections [Connected Systems and Protocols](connected-systems-and-protocols-efce256.md) and [Standard Adapter Migration](standard-adapter-migration-2622c30.md).



<a name="loio6130825edd4045d29d403f0a93bbc0f8__section_t3x_v1f_mqb"/>

## Group and Classify Configurations According to Key Criteria

Once the adapter configurations have been extracted as communication channel definitions, group and classify them by several key criteria. These criteria can include, but aren’t limited to, the following considerations:

-   **Adapter direction** \(sender or receiver\) – some adapter types are only available in one direction in Cloud Integration \(for example the RFC adapter\)

-   **Adapter type** – standard SAP Process Orchestration adapter or custom adapter

-   **File Content Conversion usage** \(Yes/No\)

-   **Advanced filename selection usage** \(Yes/No\)

-   **Quality of Service \(QoS\) requirements** – Is Exactly Once in Order \(EOIO\) required, or Exactly Once \(EO\)

-   **Protocol** – For example, if it’s an HTTP, non-HTTP or File-based service, this can help while choosing a migration strategy for a similar adapter supported in .

-   **Retry strategy for asynchronous interfaces** \(if any\)

-   **Use of custom/special adapter modules** 




<a name="loio6130825edd4045d29d403f0a93bbc0f8__section_gbz_v1f_mqb"/>

## Map Standard Adapters from SAP Process Orchestration to Cloud Integration

In addition, some adapters in Cloud Integration may have feature restrictions in comparison to the SAP Process Orchestration equivalent. It's therefore critical to any migration to analyze all adapter types in use on SAP Process Orchestration and evaluate their availability on Cloud Integration or seek a replacement solution where an adapter type isn't available.

Details on this topic are discussed in the section [Standard Adapter Migration](standard-adapter-migration-2622c30.md).



<a name="loio6130825edd4045d29d403f0a93bbc0f8__section_i1b_w1f_mqb"/>

## Reimplementation Strategy for Custom Adapters

If you, or your implementation partner, have implemented fully bespoke adapters for SAP Process Orchestration, you may need to have these reimplemented using the [Adapter Development Kit \(ADK\)](https://tools.hana.ondemand.com/#cloudintegration) provided for Cloud Integration.

Alternatively, you can search for an OEM adapter equivalent, or use the [SAP Open Connectors service](https://help.openconnectors.ext.hana.ondemand.com/home) to connect to non-SAP solutions.

Details on this topic are discussed in the section [Custom Adapter Migration](custom-adapter-migration-32b9799.md).



<a name="loio6130825edd4045d29d403f0a93bbc0f8__section_udc_w1f_mqb"/>

## Reimplementation Strategy for Adapter Modules

SAP Process Orchestration supports the concept of adapter modules \(generally implemented as Enterprise JavaBeans, EJB, and deployed on the SAP Process Orchestration Java Server\). These provide the capability to further manipulate the incoming \(for sender communication channel\) or outgoing \(for receiver communication channel\) message payload before either processing the XML message within the SAP Process Orchestration messaging engine or sending the final message out to the target system.

Cloud doesn't support this concept, but instead supports the concept of introducing additional conversion steps into any integration flow to support any additional manipulation required before full processing, or transmission to the target system. This is arguably a much more transparent and flexible approach, but it also means that a conversion process needs to take place. Another option is to create a custom adapter providing the same features as the standard adapter and extend it with the additional functionality.

Details on this topic are discussed in the section [Adapter Modules](adapter-modules-e402f4a.md).

