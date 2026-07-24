<!-- loio7b226f5757d046ae9ea1d410a3513550 -->

# Partner ID

The partner ID clearly determines the configuration scenario. It’s based on the sender system name and the sender interface information.



> ### Note:  
> In SAP Process Orchestration, a configuration scenario is a container that groups all configuration artifacts such as Integrated Configuration Objects \(ICO\), communication components, or communication channels belonging to a specific business process. As such, one configuration scenario can hold multiple ICOs.
> 
> In Cloud Integration however, one configuration scenario would correspond to one ICO only.

The following partner ID approaches are supported:

-   **Recommended**: You define the partner ID as **configuration scenario name**, and you map **sender system name** and **sender interface name** to the partner ID using an **alternative partner**. See [Recommended: Using Alternative Partner](partner-id-7b226f5.md#loio7b226f5757d046ae9ea1d410a3513550__section_partnerid_recommended).
-   **Alternative**: You define the partner ID as a combination of the **sender system name** and the **sender interface name**. See [Alternative: Combining Sender System and Sender Interface](partner-id-7b226f5.md#loio7b226f5757d046ae9ea1d410a3513550__section_partnerid_alternative).

> ### Note:  
> The recommended option has been extended for higher flexibility during the setup of your configuration scenario. This means you define the partner ID as **configuration scenario name**, and map **sender system name**, **sender interface name**, and **sender interface namespace** to the partner ID using an **alternative partner**. Since the alternative partner is defined differently compared to the standard option, this option is only supported if the sender interface name doesn't exceed 120 characters.

During runtime, the generic inbound processing flow **first** checks if an alternative partner exists that matches the headers `SAP_Sender`, `SAP_SenderInterface`, and `SAP_SenderInterfaceNamespace`, which are passed from the scenario-specific inbound flows to the generic flows. If there's a match, the associated partner ID is used to read the Partner Directory parameters.

If such an alternative partner doesn’t exist in the Partner Directory, in a **second attempt**, the standard option is applied. The standard option checks for an alternative partner that matches only the **sender system name** and the **sender interface name**.

For the generic XI inbound processing flow, the same approach applies. However, in this case, the headers that define the sender key are passed from the XI sender adapter. In a first attempt, the partner ID is determined based on the headers `SapSenderService`, `SapInterfaceName` and `SapInterfaceNamespace`. If such an alternative partner doesn’t exist in the Partner Directory, in a second attempt, the standard option is applied, which checks for an alternative partner that matches the headers `SapSenderService` and `SapInterfaceName`.

For the generic IDoc inbound processing flow, the same approach applies: the first attempt considers the namespace , whereas the second attempt ignores the namespace. In this case, the headers defining the sender key are derived from the IDoc control header. Besides this general rule, the IDoc inbound case supports further options for determining the partner ID, depending on the sender partner type and the receiver partner and its type. These options are discussed in more details later on. See [Determine Partner ID for IDoc Inbound](partner-id-7b226f5.md#loio7b226f5757d046ae9ea1d410a3513550__section_partnerid_idoc_inbound).

If the partner ID still couldn't be determined in any of these cases, in a **third** attempt, the partner ID is constructed as a combination of the two header values **sender system name** and **sender interface name**, unless the option is switched off, as described in the following.

> ### Note:  
> You should only use the **recommended option** of using an alternative partner since the alternative option of using a combination of sender system and sender interface is only supported for compatibility reasons.
> 
> With the recommended option, not only are you less likely to run into any length restrictions of the partner ID, but it also supports sender wildcard scenarios, and allows you to group all your entries in the Partner Directory user interface using a scenario ID. Furthermore, only the recommended option supports the landscape stages feature.

> ### Note:  
> The alternative option of using a combination of sender system and sender interface is **switched off by default**. This way, if the partner ID can’t be determined based on an alternative partner, for example, due to inconsistencies or missing configuration in the Partner Directory, the processed message goes into an error instead of unintentionally constructing a wrong partner ID.
> 
> If you still want to use a combination of sender system and sender interface, you must configure the externalized parameter `CustomXPid_SwitchOffTilde` by changing from the default value `true` to `false` for the following integration flows:
> 
> -   `Pipeline v2 Generic Step01 - Inbound Processing for Idoc`
> -   `Pipeline v2 Generic Step01 - Inbound Processing for XI`
> -   `Pipeline v2 Generic Step02 - Inbound Processing`
> -   `Pipeline v2 Generic Step02 - Integrated Messaging Runtime Async`
> -   `Pipeline v2 Generic Step02 - Integrated Messaging Runtime Sync`



<a name="loio7b226f5757d046ae9ea1d410a3513550__section_partnerid_recommended"/>

## Recommended: Using Alternative Partner

The alternative partner allows you to be more flexible in defining the partner ID. Firstly, you're less likely to run into any length restrictions: Agency and scheme have a maximum length of 120, while the external ID can be up to 255 characters. Secondly, so-called sender wildcard scenarios are supported more easily, which means you can map multiple sender systems to the same partner ID, assuming that the configuration is the same.

To define an alternative partner, follow the following naming conventions:

-   **Agency** equals sender system name

-   **Scheme** is constant `SenderInterface`

-   **ID** holds the sender interface name

-   As **partner ID \(pid\)**, you can define a configuration scenario name


The following example shows an alternative partner:

```
### create alternative partner for Scenario 1 
POST https://{{apihost}}/api/v1/AlternativePartners 
content-type: application/json 
Authorization: Bearer {{accesstoken}} 
X-CSRF-Token: {{xsrftoken}} 
					
{ 
	"Agency": "Sender_1", 
	"Scheme": "SenderInterface", 					
	"Id": "Interface_1", 
	"Pid": "CS_Scenario_1"
} 
```

Taking the sender interface namespace into account, you can define an alternative partner as follows:

-   **Agency** equals the sender system name
-   **Scheme** holds the sender interface name
-   **ID** holds the sender interface namespace
-   As **partner ID \(pid\)**, define a configuration scenario name

The following example shows an alternative partner:

```
### create alternative partner for Scenario 2  
POST https://{{apihost}}/api/v1/AlternativePartners  
content-type: application/json  
Authorization: Bearer {{accesstoken}}  
X-CSRF-Token: {{xsrftoken}}  
					 
{
	"Agency": "Sender_2",  
	"Scheme": "Interface_2", 					 
	"Id": "http://namespace_2.com",  
	"Pid": "CS_Scenario_2" 
}
```

> ### Note:  
> If your business system name depends on a landscape stage, your business system name is first mapped to a system alias. The alias is then used as agency in the alternative partner of the partner ID that represents the configuration scenario. For this, create a partner ID in the Partner Directory equaling the system alias. For the system alias, create an alternative partner with **agency** equaling the landscape stage, **scheme** being the constant `BusinessSystemName`, and **ID** being the name of the business system. See [Landscape Stages](landscape-stages-05cace1.md).



<a name="loio7b226f5757d046ae9ea1d410a3513550__section_partnerid_alternative"/>

## Alternative: Combining Sender System and Sender Interface

The partner ID can be defined as the combination of the sender system name and the sender interface name, separated with "~".

The following is an example of a partner ID \(pid\):

```
@pid = Sender_1~Interface_1
```

> ### Note:  
> The partner ID is restricted to a maximum length of 60 characters. Depending on your naming conventions for the sender system and the sender interface, you may exceed the maximum length. In this case, use an **alternative partner**. For information on length restrictions, see [Partner Directory](https://help.sap.com/docs/integration-suite/sap-integration-suite/partner-directory).



<a name="loio7b226f5757d046ae9ea1d410a3513550__section_partnerid_idoc_inbound"/>

## Determine Partner ID for IDoc Inbound

To determine the partner ID for IDoc inbound scenarios, **agency**, **scheme**, and **ID** of the alternative partner are derived from the IDoc control record.

The **sender interface name** is defined as a combination of the message type `MESTYP`, the IDoc type `IDOCTYP`, and the extension type `CIMTYP`. The latter is only added if the IDoc control header field `CIMTYP` isn't empty.

If you take the sender interface namespace into account to determine the partner ID, the **sender interface namespace** is defined as the constant `urn:sap-com:document:sap:idoc:messages`.

> ### Note:  
> The scheme of the alternative partner doesn't support special characters, such as slash \(`/`\). Therefore, consider the following:
> 
> -   If any of the message type, IDoc type, or extension type contain any special characters and you choose the variant in which the scheme equals the derived sender interface name, you need to replace the special character with an underscore \(`_`\) when you define the alternative partner.
> 
> -   During message processing, the control record fields of the incoming IDoc message can contain special characters. However, to determine the partner ID, the special characters are automatically replaced with an underscore \(`_`\) and can therefore be matched with the alternative partner.
> 
> -   For the option in which the sender interface name is defined in the ID of the alternative partner, the ID supports the special characters, so you must keep them.

The definition of the agency depends on whether the sender partner type `SNDPRT` is of logical system **LS** for SAP systems, or a business partner such as customer **KU**, vendor **LI**, user **US**, bank **B**, or organizational unit **OR**.

Furthermore, you have the option to determine the partner ID based on a **virtual receiver**, that is, the receiver partner information provided in the IDoc control record. In this case, the combined sender and receiver information determine the partner ID.



### Sender Partner Type Equals LS

If the sender partner type `SNDPRT` of the incoming IDoc message equals **LS**, the sender partner number `SNDPRN` holds the logical system name of the sender. In this case, define the alternative partner as follows:

-   **Agency** equals the value of the sender partner number `SNDPRN`.
-   **Scheme** holds the sender interface name, as described before.
-   **ID** holds the sender interface namespace `urn:sap-com:document:sap:idoc:messages`.
-   As **partner ID \(pid\)**, define a configuration scenario name.

> ### Note:  
> Here, we've considered the sender interface namespace. Optionally, you can define the **scheme** as constant and set the **ID** to equal the sender interface name, as described before.

The following example shows an alternative partner for sender partner type equaling LS, with the logical system name **ABPCLNT100**:

```
### create alternative partner for configuration scenario 3  
POST https://{{apihost}}/api/v1/AlternativePartners  
content-type: application/json  
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{xsrftoken}}

{
	"Agency": "ABPCLNT100",
	"Scheme": "ORDERS.ORDERS05",
	"Id": "urn:sap-com:document:sap:idoc:messages",
	"Pid": "CS_Scenario_3"
}
```



### Sender Partner Type Equals LS with Landscape Stages

Usually, the business system name of an SAP system depends on the landscape stage. In this case, you can first map the logical system name to a system alias and then use the system alias when defining the alternative partner.

Create a partner in the Partner Directory with the partner ID equaling the business system alias. For each stage `stage ID`, create the following alternative partner to map the logical system name to the alias. See [Landscape Stages](landscape-stages-05cace1.md).

-   **Agency** equals the `stage ID`.
-   **Scheme** equals the fixed string `LogicalSystemName`.
-   **ID** equals the actual logical system name of the corresponding stage.

The following example shows an alternative partner for the sender system alias **BC\_AB\_100** with the logical system name **ABPCLNT100** within the landscape stage **PRD**:

```
### create alternative partner for sender system alias BC_AB_100
POST https://{{apihost}}/api/v1/AlternativePartners  
content-type: application/json  
Authorization: Bearer {{accesstoken}}  
X-CSRF-Token: {{xsrftoken}}  
					 
{
	"Agency": "PRD",
	"Scheme": "LogicalSystemName", 					 
	"Id": "ABPCLNT100",
	"Pid": "BC_AB_100" 
}
```

Use the alias to define the alternative partner for the configuration scenario as follows:

-   **Agency** equals the sender system alias.
-   **Scheme** holds the sender interface name, as described before.
-   **ID** holds the sender interface namespace `urn:sap-com:document:sap:idoc:messages`.
-   As **partner ID \(pid\)**, define a configuration scenario name.

The following example shows an alternative partner for the sender partner type equaling LS when using landscape stages:

```
### create alternative partner for configuration scenario 3  
POST https://{{apihost}}/api/v1/AlternativePartners  
content-type: application/json  
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{xsrftoken}}  

{
	"Agency": "BC_AB_100",
	"Scheme": "ORDERS.ORDERS05",
	"Id": "urn:sap-com:document:sap:idoc:messages",
	"Pid": "CS_Scenario_3" 
}
```



### Sender Partner Type not Equal LS

If the sender partner type `SNDPRT` doesn't equal **LS**, the agency is defined as a combination of the sender party and the logical system of the sender separated by a period, ".".

> ### Note:  
> This definition of the agency complies with the general rule about party support in the pipeline. See [Scenarios with Sender Party or Receiver Party](special-cases-1606af9.md#loio1606af9b55bf4391bea01d2f7ee112af__section_mxy_knp_chc).

The logical system name of the sender is derived from the values of the IDoc control record fields sender port `SNDPOR` and client `MANDT`. Here, we assume that the sender port is defined in the format `SAP<SID>` with the constant term `SAP` and the system ID `<SID>` of the SAP system. The logical system name is then defined as `<SID>CLNT<MANDT>`.

> ### Note:  
> For sender partner types not equaling LS, the generic IDoc inbound processing flow only supports sender ports that follow the format `SAP<SID>` with the constant term `SAP` and the system ID `<SID>` of the SAP system. Otherwise, an error is raised during message processing.

The sender party is derived from the IDoc control record fields sender partner type `SNDPRT`, sender partner function `SNDPFC`, and sender partner number `SNDPRN`, using the prefix **ALE** and separated by **\#**. The sender partner function `SNDPFC` is optional and can be empty. The sender party is defined as follows:

`ALE#<SNDPRT>[#<SNDPFC>]#<SNDPRN>`

In this case, define the alternative partner as follows:

-   **Agency** equals `ALE#<SNDPRT>[#<SNDPFC>]#<SNDPRN>.<SID>CLNT<MANDT>`.
-   **Scheme** holds the sender interface name, as described before.
-   **ID** holds the sender interface namespace `urn:sap-com:document:sap:idoc:messages`.
-   As **partner ID \(pid\)**, define a configuration scenario name.

The following example shows an alternative partner for sender partner types not equaling LS:

```
### create alternative partner for configuration scenario 4  
POST https://{{apihost}}/api/v1/AlternativePartners  
content-type: application/json  
Authorization: Bearer {{accesstoken}}  
X-CSRF-Token: {{xsrftoken}}  
					 
{
	"Agency": "ALE#LI#0000000123.ABPCLNT100",
	"Scheme": "ORDERS.ORDERS05", 					 
	"Id": "urn:sap-com:document:sap:idoc:messages",
	"Pid": "CS_Scenario_4" 
}
```



### Sender Partner Type not Equal LS Using Party Alias and Landscape Stages

You can map the IDoc control record fields that describe the sender partner to a party alias. Usually, you choose this option when using landscape stages. In this case, you first need to map the logical system name to a system alias, as described before. The combined party alias and system alias separated by a period, ".", is then used when defining the alternative partner.

Create a partner in the Partner Directory with the partner ID equaling the sender party alias and define the alternative partner as follows:

-   **Agency** equals the sender alias name.
-   **Scheme** equals `ALE#<SNDPRT>[#<SNDPFC>]`.
-   **ID** equals the value of the sender partner number `<SNDPRN>`.

> ### Note:  
> We assume that the IDoc partner number of a partner is the same for all business systems within a multi-tier landscape representing the same application system; for example, for the CRM systems in DEV, QA, and PRD that are mapped to the same system alias in the Partner Directory. Hence, we use the system alias name as agency.
> 
> However, the same partner can have a different partner number in another application represented by another system alias. Even the partner type or the partner function may differ. In this case, you can define another alternative partner mapped to the same party alias.

The following is an example of an alternative partner where the vendor number **0000000123** as defined in the system **BC\_AB\_100** is mapped to the sender party alias **Prty\_Party1**:

```
### create alternative partner for sender party alias Prty_Party1
POST https://{{apihost}}/api/v1/AlternativePartners  
content-type: application/json  
Authorization: Bearer {{accesstoken}}  
X-CSRF-Token: {{xsrftoken}}  
					 
{
	"Agency": "BC_AB_100",
	"Scheme": "ALE#LI", 					 
	"Id": "0000000123",
	"Pid": "Prty_Party1" 
}
```

The following example shows an alternative partner where the sold-to-party customer number **0000045678** as defined in the system **BC\_XY\_001** is mapped to the same sender party alias **Prty\_Party1**:

```
### create alternative partner for sender party alias Prty_Party1
POST https://{{apihost}}/api/v1/AlternativePartners  
content-type: application/json  
Authorization: Bearer {{accesstoken}}  
X-CSRF-Token: {{xsrftoken}}  
					 
{
	"Agency": "BC_XY_001",
	"Scheme": "ALE#KU#SP", 					 
	"Id": "0000045678",
	"Pid": "Prty_Party1" 
}
```

Use the sender party alias and sender system alias to define the alternative partner for the configuration scenario as follows:

-   **Agency** equals `<sender party alias>.<sender system alias>`.
-   **Scheme** holds the sender interface name, as described before.
-   **ID** holds the sender interface namespace `urn:sap-com:document:sap:idoc:messages`.
-   As **partner ID \(pid\)**, define a configuration scenario name.

The following example shows an alternative partner when using landscape stages and sender party alias. Here, the logical system name **ABPCLNT100** is mapped to the alias **BC\_AB\_100**. Furthermore, the alternative partner with agency equaling the system alias **BC\_AB\_100**, scheme equaling **ALE\#LI**, and ID equaling **0000000123** is mapped to the party alias **Prty\_Party1** as seen in the previous example.

```
### create alternative partner for configuration scenario 4  
POST https://{{apihost}}/api/v1/AlternativePartners  
content-type: application/json  
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{xsrftoken}}  

{
	"Agency": "Prty_Party1.BC_AB_100",
	"Scheme": "ORDERS.ORDERS05",
	"Id": "urn:sap-com:document:sap:idoc:messages",
	"Pid": "CS_Scenario_4" 
}
```



### Virtual Receiver

You can determine the partner ID based on a **virtual receiver**. This allows you to define a configuration scenario for a specific sender and already known receiver. The configuration scenario is then of the point-to-point pattern. In this case, both the sender partner information and the receiver partner information provided in the IDoc control record is considered to determine the partner ID of the configuration scenario.

> ### Note:  
> The option of using a virtual receiver is **switched off by default** to reduce the number of overall checks, assuming that the usage of a virtual receiver isn't used frequently. To enable the virtual receiver option, you must configure the externalized parameter `CustomXPid_ResolveVirtualReceiver` of the integration flow `Pipeline v2 Generic Step01 - Inbound Processing for Idoc` by changing from the default value `false` to `true`.

In the case of resolving a virtual receiver, the **agency** to map to the configuration scenario is defined as a combination of the sender and the receiver separated by a colon, ":". Technically, all combinations for the sender definition and the receiver definition in the alternative partner of the configuration scenario are supported:

-   The sender can be of partner type LS or not equal LS.
-   The receiver can be of partner type LS or not equal LS.
-   Either landscape stages can be used or not.
-   Either parties are mapped to party aliases or not.

In all cases, the receiver part within the **agency** follows the same rules as described before for the sender part. The only exception is that for the receiver part, the corresponding IDoc control record fields for the receiver are used, that is, receiver partner type `RCVPRT`, receiver partner function `RCVPFC`, and receiver partner number `RCVPRN`.

To keep it simple, we display only the options for sender partner type equals **LS**. The options for the sender partner type not equaling **LS** were described previously. Furthermore, we assume that the party alias is always used in combination with landscape stages.


<table>
<tr>
<th valign="top">

Receiver Partner Type

</th>
<th valign="top">

Staging and Party Alias Used

</th>
<th valign="top">

Agency

</th>
</tr>
<tr>
<td valign="top">

`LS`

</td>
<td valign="top">

No

</td>
<td valign="top">

`<SNDPRN>:<RCVPRN>`

</td>
</tr>
<tr>
<td valign="top">

`LS`

</td>
<td valign="top">

Yes

</td>
<td valign="top">

`<sender system alias>:<receiver system alias>`

</td>
</tr>
<tr>
<td valign="top">

`≠ LS`

</td>
<td valign="top">

No

</td>
<td valign="top">

`<SNDPRN>:ALE#<RCVPRT>[#<RCVPFC>]#<RCVPRN>`

</td>
</tr>
<tr>
<td valign="top">

`≠ LS`

</td>
<td valign="top">

Yes

</td>
<td valign="top">

`<sender system alias>:<receiver party alias>`

</td>
</tr>
</table>

The following example shows an alternative partner for sender partner type equaling LS and virtual receiver partner type not equaling LS:

```
### create alternative partner for configuration scenario 5
POST https://{{apihost}}/api/v1/AlternativePartners  
content-type: application/json  
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{xsrftoken}}  

{
	"Agency": "ABPCLNT100:ALE#LI#0000046162",
	"Scheme": "ORDERS.ORDERS05",
	"Id": "urn:sap-com:document:sap:idoc:messages",
	"Pid": "CS_Scenario_5" 
}
```

When you use landscape stages, the logical system name of the sender **ABPCLNT100** is mapped to the sender alias **BC\_AB\_100**. Furthermore, the vendor number of the receiver **0000046162** as defined in the sender system **BC\_AB\_100** is mapped to the receiver party alias **Prty\_Party2**:

```
### create alternative partner for sender party alias Prty_Party2
POST https://{{apihost}}/api/v1/AlternativePartners  
content-type: application/json  
Authorization: Bearer {{accesstoken}}  
X-CSRF-Token: {{xsrftoken}}  
					 
{
	"Agency": "BC_AB_100",
	"Scheme": "ALE#LI", 					 
	"Id": "0000046162",
	"Pid": "Prty_Party2" 
}
```

The corresponding alternative partner when using landscape stages and party alias is defined as follows:

```
### create alternative partner for configuration scenario 5
POST https://{{apihost}}/api/v1/AlternativePartners  
content-type: application/json  
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{xsrftoken}}  

{
	"Agency": "BC_AB_100:Prty_Party2",
	"Scheme": "ORDERS.ORDERS05",
	"Id": "urn:sap-com:document:sap:idoc:messages",
	"Pid": "CS_Scenario_5" 
}
```



### Order of Checks

To determine the configuration scenario partner ID, the following checks are carried out in the given order, whereas the checks are ordered from most specific to most generic:

1.  If the virtual receiver should be resolved, it's checked if the combined sender and receiver can be mapped to a partner ID. This applies to both, partner type equaling LS and not equaling LS.
2.  If there's no match, it's checked if the sender can only be mapped to a partner ID. This applies to both, partner type equaling LS and not equaling LS.
3.  If there's no match and if the partner type doesn't equal LS, it's checked if the logical sender system, which is derived from the sender partner port and the client, can be mapped to a partner ID. This is a sort of sender wildcard scenario, that is, the configuration scenario depends on the sender system only independent of the sender partner number.
4.  If there's no match and if the partner type doesn't equal LS, it's checked if the sender partner number can be directly mapped to a partner ID. This check has been implemented for reasons of backward compatibility, in case this option has been configured in the past when partner types not equaling LS wasn't supported in the pipeline.
5.  If there's no match and the "tilde" option is active, the partner ID is combined using the sender and the sender interface, as described previously.
6.  If the "tilde" option is inactive \(default\) and there's still no match, an error is raised.

