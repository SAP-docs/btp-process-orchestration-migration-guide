<!-- loio524073ea3c9c46ba9a76fbae00b82a55 -->

# Special Cases: Bypass Options

In some cases, you can bypass one or more pipeline steps and improve your runtime behavior.

In the context of the pipeline concept, you have the following bypass options:

-   [Point-to-Point Scenarios](special-cases-bypass-options-524073e.md#loio524073ea3c9c46ba9a76fbae00b82a55__section_point-to-point)
-   [Combined Receiver and Interface Determination in a Single XSLT](special-cases-bypass-options-524073e.md#loio524073ea3c9c46ba9a76fbae00b82a55__section_single_xslt)
-   [Bypass Interface Determination](special-cases-bypass-options-524073e.md#loio524073ea3c9c46ba9a76fbae00b82a55__section_bypass_interface)
-   [Bypass Receiver Determination](special-cases-bypass-options-524073e.md#loio524073ea3c9c46ba9a76fbae00b82a55__section_bypass_receiver)

See also [Pipeline Bypass Options](special-cases-1606af9.md#loio1606af9b55bf4391bea01d2f7ee112af__section_bdm_kc3_hcc).



<a name="loio524073ea3c9c46ba9a76fbae00b82a55__section_point-to-point"/>

## Point-to-Point Scenarios

For Point-to-Point scenarios, you can bypass the two pipeline steps receiver determination and interface determination. In this case, you don't need to upload XSLT mappings to determine the list of receivers and receiver interfaces. Instead, create corresponding string parameters in the Partner Directory. See [Pipeline Bypass Options](special-cases-1606af9.md#loio1606af9b55bf4391bea01d2f7ee112af__section_bdm_kc3_hcc).

Define a Partner Directory string parameter with object ID `receiverDetermination` as follows:

```
POST https://{{apihost}}/api/v1/StringParameters 
content-type: application/json 
Authorization: Bearer {{accesstoken}} 
X-CSRF-Token: {{token}} 

{ 
    "Pid": "{{pid}}", 
    "Id": "receiverDetermination", 
    "Value": "Receiver_1" 
} 
```

Additionally, define a Partner Directory string parameter with the object ID as combination of the constant identifier `interfaceDetermination` and the receiver system name, separated with an underscore "\_". As value, enter the `ProcessDirect` endpoint of the scenario-specific integration flow for outbound processing. The following is an example for this definition:

```
POST https://{{apihost}}/api/v1/StringParameters 
content-type: application/json 
Authorization: Bearer {{accesstoken}} 
X-CSRF-Token: {{token}} 

{ 
    "Pid": "{{pid}}", 
    "Id": "interfaceDetermination_Receiver_1", 
    "Value": "/pip/07/scenario1" 
} 
```



<a name="loio524073ea3c9c46ba9a76fbae00b82a55__section_single_xslt"/>

## Combined Receiver and Interface Determination in a Single XSLT

In general, you can combine the receiver determination and the interface determination in one single XSLT instead of defining separate XSLTs for the receiver determination and an interface determination for each receiver. This allows you to only upload one single XSLT that carries out the XPath routing conditions to determine the list of receivers and the XPath conditions to determine the list of receiver interfaces. This way, you can bypass the interface determination step.

For the combined receiver and interface determination XSLT, the object ID is `receiverDetermination`, same as for the receiver determination XSLT. Assume that the encoded XSLT mapping is stored in the variable binary.

```
POST https://{{apihost}}/api/v1/BinaryParameters 
content-type: application/json 
Authorization: Bearer {{accesstoken}} 
X-CSRF-Token: {{token}} 

{ 
  "Pid": "{{pid}}", 
  "Id": "receiverDetermination", 
  "ContentType": "xsl", 
  "Value": "{{binary}}" 
} 
```



<a name="loio524073ea3c9c46ba9a76fbae00b82a55__section_bypass_interface"/>

## Bypass Interface Determination

This bypass option is a subset of the combined receiver and interface determination option. It applies to Recipient List scenarios without interface split, that is, scenarios in which each receiver has only a single receiver interface. This way, you can bypass the interface determination step.

The configuration is similar to the combined receiver and interface determination option. You only need to upload a single XSLT that carries out the XPath routing conditions to determine the list of receivers. However, you must define a fixed receiver interface in the XSLT for each receiver.



<a name="loio524073ea3c9c46ba9a76fbae00b82a55__section_bypass_receiver"/>

## Bypass Receiver Determination

For interface split scenarios with only a single receiver, you can bypass the receiver determination step. In this case, you don't need to upload an XSLT mapping to determine the list of receivers. Instead, create a corresponding string parameter in the Partner Directory. However, for the interface determination, you must create an XSLT in the Partner Directory that carries out the XPath routing conditions to determine the interfaces.

Define a Partner Directory string parameter with object ID `receiverDetermination` as follows:

```
POST https://{{apihost}}/api/v1/StringParameters  
content-type: application/json  
Authorization: Bearer {{accesstoken}}  
X-CSRF-Token: {{token}}  

{  
    "Pid": "{{pid}}",  
    "Id": "receiverDetermination",  
    "Value": "Receiver_1"  
}  
```

Additionally, define an interface determination XSLT. When you upload the XSLT, the object ID is a combination of a constant identifier `interfaceDetermination` and the receiver system name, separated by an underscore "\_". Assume that the encoded XSLT mapping is stored in the variable binary.

```
POST https://{{apihost}}/api/v1/BinaryParameters 
content-type: application/json 
Authorization: Bearer {{accesstoken}} 
X-CSRF-Token: {{token}} 

{ 
  "Pid": "{{pid}}", 
  "Id": "interfaceDetermination_Receiver_1", 
  "ContentType": "xsl", 
  "Value": "{{binary}}" 
} 
```

