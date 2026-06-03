<!-- loiof7fb3cac0a94498885fa75f60dbfb4c8 -->

# XSLT Mappings

This section discusses the different XSLTs that are used to execute the XPath conditions for either determining the receivers or the interfaces.



<a name="loiof7fb3cac0a94498885fa75f60dbfb4c8__section_thd_scz_31c"/>

## XSLT Mapping for Determining Receivers

Unless you reuse the extended receiver determination mapping, you must create an XSLT in the Partner Directory for each scenario. The XSLT mapping carries out the XPath routing conditions to determine the list of receivers. For an example, see [Receiver Determination \(Generic\)](fully-decoupled-pipeline-f8e69f4.md#loiof8e69f43059a44cdb891892f4ff083d8__section_qbb_wyk_31c).

> ### Note:  
> The XSLT mapping is stored as binary. When using the API, you need to encode the XSLT before uploading to the Partner Directory. When you upload the XSLT using the Partner Directory user interface, selecting the content type `xsl` and the encoding `UTF-8` automatically encodes the XSLT.

For the receiver determination XSLT, the object ID is `receiverDetermination`. Let's assume that the encoded XSLT mapping is stored in the variable binary.

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



<a name="loiof7fb3cac0a94498885fa75f60dbfb4c8__section_xslt_mapping_interfaces"/>

## XSLT Mapping for Determining Interfaces

For each receiver of your scenario, you need to create an XSLT in the Partner Directory that carries out the XPath routing conditions to determine the interfaces. For an example, see [Interface Determination \(Generic\)](fully-decoupled-pipeline-f8e69f4.md#loiof8e69f43059a44cdb891892f4ff083d8__section_drs_wyk_31c).

> ### Note:  
> The XSLT mapping is stored as binary. When using the API, you need to encode the XSLT before uploading to the Partner Directory. When you upload the XSLT using the Partner Directory user interface, selecting the content type `xsl` and the encoding `UTF-8` automatically encodes the XSLT.

For the interface determination XSLT, the object ID is a combination of a constant identifier `interfaceDetermination` and the receiver system name, separated with an underscore "\_". Let's assume that the encoded XSLT mapping is stored in the variable binary.

> ### Note:  
> From version 1.0.6 of the provided standard integration package onwards, the partner ID \(pid\) and the identifier \(Id\) used to upload the interface determination XSLT to the Partner Directory have been changed to overcome the partner ID restrictions. This change is an incompatible change. Hence, you must change your code and update the Partner Directory entries accordingly.

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

