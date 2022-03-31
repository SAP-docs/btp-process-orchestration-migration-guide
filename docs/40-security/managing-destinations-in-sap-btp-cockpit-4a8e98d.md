<!-- loio4a8e98d93a954187b4d705926a670b08 -->

# Managing Destinations in SAP BTP Cockpit

Destinations are key building blocks in SAP BTP and are used to define connections for outbound communication from your application to remote systems. These remote systems can be on-premise or in the cloud. Typically, Cloud Integration can directly access the virtual systems exposed by the Cloud Connector, except for the RFC channel. In Cloud Integration, for the RFC channel it’s necessary to configure a destination in SAP BTP Cockpit.

Similar to destinations in SAP BTP, in SAP Process Orchestration, for some communication channels you can maintain RFC/HTTP destinations to reuse them as much as necessary, for example, when you want to connect SAP Process Orchestration to your ECC receiver.

A destination has a name, a URL, authentication details, and other configuration details specific to the requirement and type of destination.

For full help documentation regarding the use of the Destinations Editor \(and other methods to maintain destinations\), as well as the setup of the different destination types, see [SAP BTP Connectivity - Initial Setup](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/78198e8b58f949af977e579b5de42299.html).

