<!-- loio2ecd2a83362742e9baa278cd889bbf0a -->

# Linking Communication Channels to Interfaces

In Cloud Integration, there’s no separation between the communication channels and the other artifacts \(such as Message Mapping Schema definitions\) that make up an interface. It’s therefore key to understand which communication channels are used by which interfaces as the same channel can be used by more than one interface.

To achieve this understanding, a list of Integrated Configuration objects needs to be extracted and analyzed to provide the linkage between the Integrated Configuration objects and the communication channels the interface uses.

Several techniques can be employed to extract this information, for example the one described in the following:

Like the communication channel extraction, utilize the standard Web services that are available as part of the Integration Directory API. The blog [SAP PI/PO Directory API: Extract detailed Communication Channel configurations into an Excel sheet without custom codes/macros](https://blogs.sap.com/2017/11/07/sap-pipo-directory-api-extract-detailed-communication-channel-configurations-into-an-excel-sheet-without-custom-codesmacros/) provides details on how to extract the information for the communication channels. A similar approach can be employed, but in this case using an alternative Web service. Go to *SAP NetWeaver Administrator* \> *Configuration* \> *Connectivity* \> *Single Service Administration*, and in *Service Definitions*, search for *IntegratedConfiguration750In* instead of *CommunicationChannelIn*:

![](images/Connectivity_Service_Definitions_f420701.png)

Some of the columns that can be found in the extraction after converting to MS Excel are:

-   Sender Party ID \(Interface Configuration Object key\)

-   Sender Component ID \(Interface Configuration Object key\)

-   Interface Name \(Interface Configuration Object key\)

-   Interface Namespace \(Interface Configuration Object key\)

-   Party ID \(Communication Channel key\)

-   Component ID \(Communication Channel key\)

-   Channel ID \(Communication Channel key\)


With that, you can apply pivot tables and formulas to improve the visualization of key data.

