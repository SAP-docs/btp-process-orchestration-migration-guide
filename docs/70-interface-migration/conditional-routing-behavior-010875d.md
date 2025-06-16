<!-- loio010875d30fa1448ca8491304b78f9e40 -->

# Conditional Routing Behavior

Learn about the different behaviors regarding conditional routing in SAP Process Orchestration and Cloud Integration.



<a name="loio010875d30fa1448ca8491304b78f9e40__section_nxn_lm3_4fc"/>

## Current Behavior

In SAP Process Orchestration, the following conditions are configured:

-   **Condition A**: `/ZINVOIC02/IDOC/EDI_DC40/MESTYP = 'RE'`
-   **Condition B**: `/ZINVOIC02/IDOC/EDI_DC40/MESTYP != 'RE'`

In **SAP Process Orchestration**, if the field `/ZINVOIC02/IDOC/EDI_DC40/MESTYP` doesn't exist in the incoming payload, the system evaluates condition B \(`/ZINVOIC02/IDOC/EDI_DC40/MESTYP != 'RE'`\) as true. This leads the message to follow the second route, "`!= 'RE'`".

In **Cloud Integration**, the behavior differs. If the field `/ZINVOIC02/IDOC/EDI_DC40/MESTYP` doesn't exist in the payload, Cloud Integration doesn't evaluate the `!=` condition. Instead, it defaults to the fallback route. This results in a different outcome as compared to SAP Process Orchestration.

This difference in runtime behavior can lead to unexpected results after migrating your interfaces, especially if your routing logic relies on the non-existence of a field.



<a name="loio010875d30fa1448ca8491304b78f9e40__section_uld_4m3_4fc"/>

## Solution in Cloud Integration

To align the routing logic with the behavior of SAP Process Orchestration, the conditions in Cloud Integration must explicitly account for the non-existence of the field.

You can adapt one of the following recommendations:

1.  `not(/ZINVOIC02/IDOC/EDI_DC40/MESTYP)` or `/ZINVOIC02/IDOC/EDI_DC40/MESTYP != 'RE'`

    This condition evaluates as true if the field doesn't exist or if its value isn't `RE`.

2.  `not(/ZINVOIC02/IDOC/EDI_DC40/MESTYP = 'RE')`

    This condition achieves the same result by negating the equality condition, through which it accounts for both the absence and the mismatched value of the field.


> ### Note:  
> Always test the integration flows with a variety of payloads **on both platforms** to confirm that the routing behavior aligns with your business requirements.

