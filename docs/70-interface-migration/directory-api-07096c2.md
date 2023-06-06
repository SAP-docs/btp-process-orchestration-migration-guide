<!-- loio07096c2752c64dbd8bfdb23923087a23 -->

# Directory API

The SAP Process Orchestration Directory API is a set of SOAP APIs to read and change objects from the Integration Builder and Integration Directory.



<a name="loio07096c2752c64dbd8bfdb23923087a23__section_omv_pkp_kwb"/>

## Context

SAP Migration Assessment and the Migration Tooling use the Directory API to extract all necessary data for the migration from SAP Process Orchestration. See, for example, [Add an SAP Process Orchestration System](https://help.sap.com/docs/SAP_INTEGRATION_SUITE/51ab953548be4459bfe8539ecaeee98d/5f7672334ca74f90843d38375220d757.html?locale=en-US&version=CLOUD) in the Migration Assessment documentation.

There are several operations possible for different objects, for example, delete integrated configurations, or read detailed information from each communication channel. You can also make mass changes in the Integration Directory. Using the programming interface, you can carry out almost all those actions that you can also carry out using the user interface \(Integration Builder\).

> ### Note:  
> Make sure that the user used on the API has the assigned roles: `SAP_XI_API_DISPLAY_J2EE` and `SAP_XI_API_DEVELOP_J2EE`.



<a name="loio07096c2752c64dbd8bfdb23923087a23__section_mcb_qkp_kwb"/>

## Procedure



### Using the Web Services Navigator

1.  Open the Web Services Navigator using one of the following options:
    -   Open SAP NetWeaver Application Server and choose *Web Services Navigator*.

    -   Navigate directly to the URL `http(s)://<host>:<port>/wsnavigator`.

    -   Open the SAP NetWeaver Administrator \(`http(s)://<host>:<port>/nwa`\) and navigate to *Configuration* \> *Connectivity* \> *Single Service Administration*.


2.  Change the *Search Type* to *Provider System*.

3.  In *Search for*, enter an API and choose *Search*.

    For a list of the APIs used in Migration Assessment and Migration Tooling, see [APIs in the Directory API](directory-api-07096c2.md#loio07096c2752c64dbd8bfdb23923087a23__section_s4h_qkp_kwb).

4.  Select an API and choose *Next*.

5.  Select an operation and choose *Next*.

6.  Enter the input parameters according to the API selected in the previous step. Fill the user credentials at *Invocation Parameters*.

7.  The result is shown. You can check the execution result and download it at *Result* \> *XML Content* \> *Download as File*.

    You can use the request message while testing it on an HTTP client tool.




### Saving the WSDL

Save the WSDL from any directory API using the following format call:

-   **WSDL URL**: <code>http(s)://&lt;host&gt;:&lt;port&gt;/&lt;ServiceName&gt;InService/&lt;ServiceName&gt;ImplBean<b>?wsdl</b></code>

-   **Example**: `http(s)://<host>:<port>/IntegratedConfigurationInService/IntegratedConfigurationInImplBean?wsdl`




<a name="loio07096c2752c64dbd8bfdb23923087a23__section_s4h_qkp_kwb"/>

## APIs in the Directory API

The following APIs are used in Migration Assessment and Migration Tooling:

-   `CommunicationChannelInService`
-   `IntegratedConfigurationInService`
-   `IntegratedConfiguration750InService`
-   `SenderAgreementInService`
-   `ReceiverAgreementInService`
-   `ValueMappingInService`
-   `ConfigurationScenarioInService`
-   `AlertRuleInService`

Service / Base URL: `http(s)://<host>:<port>/<ServiceName>InService/<ServiceName>ImplBean`



### CommunicationChannelInService

With the **CommunicationChannelIn** API, you get detailed information about a communication channel.

An XML file is created with the administrative data, adapter metadata, transport / message protocol, all adapter-specific attributes, and some other information.

For the read request, `Component ID` and `Channel ID` are mandatory.

**Endpoint URL:** `http(s):// <host>:<port>/CommunicationChannelInService/CommunicationChannelInImplBean`

**Possible Operations:** Change, Check, Create, CreateFromTemplate, Delete, OpenForEdit, Query, Read, Revert

See [Example for CommunicationChannelInService](examples-for-directory-api-dc70456.md#loiodc70456eb75e49168fbd2d4eaac12cdf__section_rx1_nkd_lwb).



### IntegratedConfigurationInService

With the **IntegratedConfigurationIn** API, you get detailed information about an integrated configuration.

An XML file is created with the administrative data, inbound and outbound processing, communication channel with all adapter-specific attributes, the receiver, and some other information.

For the read request, the `Sender Component ID`, `Sender Interface Name`, and `Namespace` are mandatory.

**Endpoint URL:** `http(s):// <host>:<port>/IntegratedConfigurationInService/IntegratedConfigurationInImplBean`

**Possible Operations:** Change, Check, Create, Delete, OpenForEdit, Query, Read, Revert

See [Example for IntegratedConfigurationInService](examples-for-directory-api-dc70456.md#loiodc70456eb75e49168fbd2d4eaac12cdf__section_ddf_4kd_lwb).



### IntegratedConfiguration750InService

With the **IntegratedConfiguration750In** API, you get detailed information about an integrated configuration.

> ### Note:  
> This API is only available on SAP Process Orchestration, SAP NetWeaver 7.5.

> ### Note:  
> In contrast to **IntegratedConfigurationIn**, **IntegratedConfiguration750In** has `ReceiverWildcardIndicator` in the XML output.

An XML file is created with the administrative data, inbound and outbound processing, communication channel with all adapter-specific attributes, the receiver, and some other information.

For the read request, the `Sender Component ID`, `Sender Interface Name`, and `Namespace` are mandatory.

**Endpoint URL:** `http(s):// <host>:<port>/IntegratedConfiguration750InService/IntegratedConfiguration750InImplBean`

**Possible Operations:** Change, Check, Create, Delete, OpenForEdit, Query, Read, Revert

See [Example for IntegratedConfiguration750InService](examples-for-directory-api-dc70456.md#loiodc70456eb75e49168fbd2d4eaac12cdf__section_d14_4kd_lwb).



### SenderAgreementInService

With the **SenderAgreementIn** API, you get detailed information about the sender agreement.

An XML file is created with the administrative data, sender and receiver information, communication channel with all adapter-specific attributes, and some other information.

For the read request, the `Sender Component ID`, `Sender Interface Name`, and `Namespace` are mandatory.

**Endpoint URL:** `http(s):// <host>:<port>/SenderAgreementInService/SenderAgreementInImplBean`

**Possible Operations:** Change, Check, Create, Delete, OpenForEdit, Query, Read, Revert

See [Example for SenderAgreementInService](examples-for-directory-api-dc70456.md#loiodc70456eb75e49168fbd2d4eaac12cdf__section_ovw_4kd_lwb).



### ReceiverAgreementInService

With the **ReceiverAgreementIn**, API you get detailed information about the receiver agreement.

An XML file is created with the administrative data, sender and receiver information, communication channel, and some other information.

For the read request, the `Sender Component ID`, `Receiver Interface Name`, `Namespace`, and `Receiver Component ID` are mandatory.

**Endpoint URL:** `http(s):// <host>:<port>/ReceiverAgreementInService/ReceiverAgreementInImplBean`

**Possible Operations:** Change, Check, Create, Delete, OpenForEdit, Query, Read, Revert

See [Example for ReceiverAgreementInService](examples-for-directory-api-dc70456.md#loiodc70456eb75e49168fbd2d4eaac12cdf__section_e2j_pkd_lwb).



### ValueMappingInService

With the **ValueMappingIn** API, you get detailed information about the sender agreement.

An XML file is created with the administrative data, value mapping ID, and group name.

For the read request, the `Value Mapping ID` \(`Group ID`\) is mandatory.

**Endpoint URL:** `http(s):// <host>:<port>/ValueMappingInService/ValueMappingInImplBean`

**Possible Operations:** Change, Check, Create, Delete, OpenForEdit, Query, Read, Revert

See [Example for ValueMappingInService](examples-for-directory-api-dc70456.md#loiodc70456eb75e49168fbd2d4eaac12cdf__section_byn_pkd_lwb).



### ConfigurationScenarioInService

With the **ConfigurationScenarioIn** API, you get detailed information about the configuration scenario and all containing elements, for example, communication channel or integrated configuration.

An XML file is created with the administrative data, business components, communication channel, integrated configuration, and some other information.

For the read request, the `Configuration Scenario ID` is mandatory.

**Endpoint URL:** `http(s):// <host>:<port>/ConfigurationScenarioInService/ConfigurationScenarioInImplBean`

**Possible Operations:** Change, Check, Create, Delete, OpenForEdit, Query, Read, Revert

See [Example for ConfigurationScenarioInService](examples-for-directory-api-dc70456.md#loiodc70456eb75e49168fbd2d4eaac12cdf__section_iwp_skd_lwb).



### AlertRuleInService

With the **AlertRuleIn** API, you get a list of all alert rules with detailed information.

When `AlertRuleID` is empty in the query, a list of all rules is extracted.

No field is mandatory.

**Endpoint URL:** `http(s):// <host>:<port>/AlertRuleInService/AlertRuleInImplBeanHTTPS`

**Possible Operations:** DeregisterConsumer, Query, RegisterConsumer, RetrieveRuntimeComponents

See [Example for AlertRuleInService](examples-for-directory-api-dc70456.md#loiodc70456eb75e49168fbd2d4eaac12cdf__section_uq5_skd_lwb).

-   **[Examples for Directory API](examples-for-directory-api-dc70456.md "This chapter collects examples for the APIs described in Directory
		API.")**  
This chapter collects examples for the APIs described in [Directory API](directory-api-07096c2.md).

