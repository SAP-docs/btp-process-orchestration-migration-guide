<!-- loio37605e970ad645c08cc6d6d8f9a8ae36 -->

# Landscape Architecture Use Cases

Learn what landscape requirements are met with the integration architecture approaches of SAP Process Orchestration.

In the section [SAP Process Orchestration Architecture](sap-process-orchestration-architecture-a13372e.md), the different integration architecture approaches of SAP Process Orchestration are categorized as central, distributed \(model 1\), and distributed \(model 2\) domains. These approaches can be used to meet different landscape requirements. Some important aspects of these requirements are the following:


<table>
<tr>
<th valign="top">

Assessment Criteria



</th>
<th valign="top">

Description



</th>
</tr>
<tr>
<td valign="top">

Administration



</td>
<td valign="top">

Administration defines how difficult the overall landscape is to operate and maintain with respect to downtime, planned upgrades etc. The application of support packages, notes, and hot fixes are included in this criterion.



</td>
</tr>
<tr>
<td valign="top">

Availability



</td>
<td valign="top">

Availability relates to how available the SAP Process Integration system is for message processing. In distributed \(model 1\) and distributed \(model 2\) domain models, availability is improved through the decentralized message processing capability and technical abstraction.



</td>
</tr>
<tr>
<td valign="top">

Monitoring



</td>
<td valign="top">

With SAP Process Integration, IT professionals can configure and monitor service-enabled applications across the landscape. Using the integrated capabilities of SAP Solution Manager and SAP NetWeaver, IT administrators can monitor the availability and performance of applications, processes, and services, as well as analyze the root cause of problems, and undertake optimization measures. This criterion defines the complexity and coverage of the monitoring solution in each deployment model.



</td>
</tr>
<tr>
<td valign="top">

TCO



</td>
<td valign="top">

Total Cost of Ownership defines how much it costs to implement, operate, and support a given IT solution. This includes areas such as the technical infrastructure, software licensing, implementation costs, support costs, upgrade, and downtime costs etc.



</td>
</tr>
<tr>
<td valign="top">

Internal Performance



</td>
<td valign="top">

This criterion covers the internal performance of the SAP application software, database, and operating system when processing a message in SAP Process Integration. Other variables such as message packaging and size of messages are assumed to be constant, which is an indicate measurement showing the relationship between each architectural model.



</td>
</tr>
<tr>
<td valign="top">

Network Utilization



</td>
<td valign="top">

This criterion looks at the impact on or utilization of the physical communication network. The geographical location of business systems, integration servers, and adapter engines are considered, as well as latency and reliability.



</td>
</tr>
<tr>
<td valign="top">

Common Business Process Delivery



</td>
<td valign="top">

The ability to enforce common business processes across the SAP Process Integration landscape, including design-time object reuse and redundancy avoidance.



</td>
</tr>
<tr>
<td valign="top">

Globalization & Localization



</td>
<td valign="top">

The ability to meet local and global requirements both technically and on a business level. For example, a distributed \(model 2\)-domain solution with local governance can add flexibility and abstraction while a centralized governance model might not meet local requirements.



</td>
</tr>
</table>

However, with the migration to SAP Integration Suite, aspects should be reviewed, and their eligibility discussed. In the next chapters, uses cases of the above-mentioned architecture are highlighted.

