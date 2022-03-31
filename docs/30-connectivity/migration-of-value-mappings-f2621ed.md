<!-- loiof2621edc148c4ecd9616144783801993 -->

# Migration of Value Mappings

Learn how you can import value mappings from SAP Process Orchestration to Cloud Integration.

In SAP Process Orchestration, the value mapping standard function is defined in ESR and is used to map different representations of an object to each other. At the same time, it's needed to define a value mapping group \(value-mapping tables\) in Integration Directory. The image below shows the representation of the value mapping defined in SAP Process Orchestration.

 ![](images/Value_mapping_ESR_ID_a7af7b2.png) 

This function can be used in different message mappings with the same key field, but the same value mapping group need to be referenced. Additionally, you can choose to use a rather static option called fixValues, which is a key-value list in which you can directly insert the value mapping in the message mapping while designing your interface in ESR. The fixValue mappings are automatically imported when importing the Message Mapping or Operation Mapping from SAP Process Orchestration.

For more information, see [Designing and Configuring Value Mappings](https://help.sap.com/viewer/bbd7c67c5eb14835843976b790024ec6/LATEST/en-US/d0acc9add2064ad59393669e13696961.html).

In Cloud Integration, the value mapping configuration is similar. It’s possible to import a CSV file containing the values. After the CSV file importation and deployment, on the message mapping, you need to add the value mapping function and fill in the identifier and agency. For more information, see [Creating Value Mapping](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/25eff9b4884d4f6e859e6ebf898dcb71.html).

It's possible to export a CSV file from SAP Process Orchestration and import it in Cloud Integration in a value mapping. If the value mapping already exists in Cloud Integration, the process only works if you import a CSV in an existing value mapping, too. The values are merged with existing Agency and Identifier entries.

Another way to import value mappings from SAP Process Orchestration to Cloud Integration using the SOAP API \(Directory APIs\) from of SAP Process Orchestration. This API exports the value mappings as a XML file. After this step, the XML file must be converted to CSV format and follow the process described in the previous paragraph.

