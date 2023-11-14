<!-- loiof9d762720b67409e9efc98eea0c31f8d -->

# Guidelines to Design Integration Flows

To start to develop an integration flow, the developer needs to make sure that the integration flows design is robust to avoid critical business processes for the project and for the company.

The integration flow designed should avoid errors and shouldn't break which could lead to errors in a critical business process. The integration flows must be kept readable and easy to understand, which is why the integration developer needs to know some characteristics to design an enterprise-grade integration flow. The following table lists some of the main aspects that need to be followed while developing integration flows:


<table>
<tr>
<th valign="top">

Guidelines

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

[High Availability](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/LATEST/en-US/3ea1e33606c24c27ad097d60b57b6e4e.html) 

</td>
<td valign="top">

Carefully build an integration flow considering certain patterns that never break the business process.

</td>
</tr>
<tr>
<td valign="top">

[Resource Management](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/LATEST/en-US/f8cf97498d2549daab65db34f11e119d.html) 

</td>
<td valign="top">

To correctly process messages in Cloud Integration, some resources are needed, like the capabilities used in the integration flow, on the computing system, database, and messaging service broker to process the messages.

</td>
</tr>
<tr>
<td valign="top">

[Readability](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/LATEST/en-US/578fa7780344468388f689455f38b3a4.html) 

</td>
<td valign="top">

When an integration developer is designing an integration flow, it’s important take the best practices and the readability of an integration flow into account. During the maintenance, it’s easier and simple to quickly check the message processing flow if the integration flow is well designed.

</td>
</tr>
<tr>
<td valign="top">

[Handling Failures Gracefully](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/LATEST/en-US/42c95f752c8d4b4cad98b7608223424f.html) 

</td>
<td valign="top">

Even well-designed integration flows can break during message processing, but this shouldn't disrupt the business process. To avoid this situation or increase the impact of the failure, it’s important to extend the integration flow with error handling. It’s convenient to have supervision during the integration flow execution to check the message flow, keep the data to test, and analyze the causes of the error.

</td>
</tr>
<tr>
<td valign="top">

[Prepackaged Integration Content](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/LATEST/en-US/95c68ce417e2476d994f082b9301a98d.html) 

</td>
<td valign="top">

Cloud Integration has prepackaged integration content available that contains integration flows, value mappings, documentation, and more. This is useful for the integration developer since these packages are a quick start into an integration project. Cloud Integration also allows to extend the capabilities of prepackaged integration content provided by SAP. In this case, the integration developer can design custom integration flows without changing the content.

</td>
</tr>
<tr>
<td valign="top">

[Highest Security Standards](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/LATEST/en-US/201fd43d4dab4bce9144ebfd9cdfbb20.html) 

</td>
<td valign="top">

The integration flow ultimately specifies how a message is processed and which options are applied to protect the content of the messages on the way between the sender and the receiver. Therefore, the integration developer has to make sure that the integration flows are designed in a way that ensures that the highest security standards are applied.

</td>
</tr>
<tr>
<td valign="top">

[Use Scripting Appropriately](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/LATEST/en-US/d4dc13c927b044b2a38e458f4cea9da5.html) 

</td>
<td valign="top">

You can use the Script step to apply script operations on the message content. The Script step type supports the following script languages:

-   Groovy

-   JavaScript


If you don't consider the proposed guidelines during integration design, there's the risk that your scenario is affected in the following way:

-   The scenario runs into an out-of-memory situation.

-   It's hard for the integration expert to understand the logic of the integration flow.

-   Your scenario runs into compatibility issues if there are Java upgrades or Cloud Integration updates.




</td>
</tr>
<tr>
<td valign="top">

[Use the Partner Directory Appropriately](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/LATEST/en-US/6e00412aebd549f8b5771c9397c08c5d.html) 

</td>
<td valign="top">

When designing business-to-business scenarios, you can use the Partner Directory to store information on business partners that are connected to the tenant in the context of a larger business network.

The Partner Directory contains information on partners that are connected to a tenant in the context of a larger business partner network. The information stored in the Partner Directory can be used to parameterize integration flows.

There's no dedicated user interface to access the Partner Directory. You can access its content only based on APIs.

</td>
</tr>
</table>

