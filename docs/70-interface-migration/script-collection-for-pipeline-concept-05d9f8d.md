<!-- loio05d9f8d85d7945af8d610dca81375b43 -->

# Script Collection for Pipeline Concept

Use the scripts collected in this section to read the Partner Directory.

The following scripts are part of the script collection `Pipeline Generic - Script Collection`:

-   [`attachAdditionalInformation`](script-collection-for-pipeline-concept-05d9f8d.md#loio05d9f8d85d7945af8d610dca81375b43__section_qdh_px2_j1c)

-   [`readInboundConversionFromPD`](script-collection-for-pipeline-concept-05d9f8d.md#loio05d9f8d85d7945af8d610dca81375b43__section_tf2_zx2_j1c)

-   [`readReceiverSpecificQueueFromPD`](script-collection-for-pipeline-concept-05d9f8d.md#loio05d9f8d85d7945af8d610dca81375b43__section_xzr_cy2_j1c)

-   [`readRetryHandlingFromPD`](script-collection-for-pipeline-concept-05d9f8d.md#loio05d9f8d85d7945af8d610dca81375b43__section_jjn_gy2_j1c)

-   [`reuseExtendedReceiverDetermination`](script-collection-for-pipeline-concept-05d9f8d.md#loio05d9f8d85d7945af8d610dca81375b43__section_ism_jy2_j1c)

-   [`readReceiverNotDeterminedFromPD`](script-collection-for-pipeline-concept-05d9f8d.md#loio05d9f8d85d7945af8d610dca81375b43__section_pmr_my2_j1c)

-   <code><a href="script-collection-for-pipeline-concept-05d9f8d.md#loio05d9f8d85d7945af8d610dca81375b43__section_yjh_bh4_vbc">displayBulkIDs</a></code>
-   <code><a href="script-collection-for-pipeline-concept-05d9f8d.md#loio05d9f8d85d7945af8d610dca81375b43__section_dp4_xj4_vbc">setIDocSenderInterface</a></code>



<a name="loio05d9f8d85d7945af8d610dca81375b43__section_qdh_px2_j1c"/>

## attachAdditionalInformation

Use the following Groovy script `attachAdditionalInformation` to add information about the queue names to the message processing log if the message is parked in a dead letter queue. In addition, the log level is set to `DEBUG`.

```
import com.sap.gateway.ip.core.customdev.util.Message 
import java.util.HashMap 

def Message processData(Message message) { 

    // get queue names 
    def propertyMap = message.getProperties() 
    def incomingQueue = propertyMap.get("incomingQueue"); 
    def deadLetterQueue = incomingQueue + '_DLQ'; 

    def messageLog = messageLogFactory.getMessageLog(message); 
    if (messageLog != null) { 
        def body = 'Maximum number of retries exceeded' 
        body = body + '\nMessage removed from queue ' + incomingQueue + ' and sent to dead letter queue ' + deadLetterQueue; 
    // add attachment to message processing log 
        messageLog.addAttachmentAsString('Additional Information', body, 'text/plain'); 
    // set log level to DEBUG at message level 
        message.setHeader('SAP_MessageProcessingLogLevel', 'DEBUG'); 
    } 
    return message; 
} 
```



<a name="loio05d9f8d85d7945af8d610dca81375b43__section_tf2_zx2_j1c"/>

## readInboundConversionFromPD

Use the following Groovy script `readInboundConversionFromPD` to check if an inbound conversion is needed by reading the corresponding ProcessDirect endpoint from the Partner Directory.

```
import com.sap.gateway.ip.core.customdev.util.Message;
import java.util.HashMap;
import com.sap.it.api.pd.PartnerDirectoryService;
import com.sap.it.api.ITApiFactory;

def Message processData(Message message) {
    
    def service = ITApiFactory.getApi(PartnerDirectoryService.class, null); 
    if (service == null){
        throw new IllegalStateException("Partner Directory Service not found");
    }
    
    // get pid
    def properties = message.getProperties(); 
    def Pid = properties.get("partnerID");
    if (Pid == null){
        throw new IllegalStateException("Partner ID not found in sent message");   
    }

    // read the inbound conversion end point from the Partner Directory
    def inbConvEndpoint = service.getParameter("InboundConversionEndpoint", Pid , String.class);
    
    // if the inbound conversion end point exists, create a new exchange property containing the end point
    // otherwise, the exchange property is not created
    message.setProperty("inbConvEndpoint", inbConvEndpoint ?: null);
    
    // create a new exchange property with value true or false depending on whether the end point exists
    message.setProperty("inbConvBoolean", inbConvEndpoint ? 'true' : 'false');

    return message;
}
```



<a name="loio05d9f8d85d7945af8d610dca81375b43__section_xzr_cy2_j1c"/>

## readReceiverSpecificQueueFromPD

Use the following Groovy script `readReceiverSpecificQueueFromPD` to read the outbound queue name from the Partner Directory if you need a receiver-specific queue.

```
import com.sap.gateway.ip.core.customdev.util.Message;
import java.util.HashMap;
import com.sap.it.api.pd.PartnerDirectoryService;
import com.sap.it.api.ITApiFactory;

def Message processData(Message message) {
    
    def service = ITApiFactory.getApi(PartnerDirectoryService.class, null); 
    if (service == null){
        throw new IllegalStateException("Partner Directory Service not found");
    }
    
    // get pid (pid equals SAP_Receiver)
    def headers = message.getHeaders();
    def Pid = headers.get("SAP_Receiver");
    // throw exception if pid is missing
    if (Pid == null){
        throw new IllegalStateException("Partner ID not found in sent message");   
    }
    
    // read the receiver-specific JMS queue from the Partner Directory
    def receiverSpecificQueue = service.getParameter("ReceiverSpecificQueue", Pid , String.class);
    
    // if the receiver-specific queue exists, create a new exchange property containing the queue name
    // otherwise, the exchange property is not created
    message.setProperty("receiverSpecificQueueName", receiverSpecificQueue ?: null);
    
    // create a new exchange property with value true or false depending on whether the queue exists
    message.setProperty("receiverSpecificQueueBoolean", receiverSpecificQueue ? 'true' : 'false');

    return message;
}
```



<a name="loio05d9f8d85d7945af8d610dca81375b43__section_jjn_gy2_j1c"/>

## readRetryHandlingFromPD

Use the following Groovy script `readRetryHandlingFromPD` to read the maximum number of retries from the Partner Directory.

```
import com.sap.gateway.ip.core.customdev.util.Message;
import java.util.HashMap;
import com.sap.it.api.pd.PartnerDirectoryService;
import com.sap.it.api.ITApiFactory;

def Message processData(Message message) {
    
    def service = ITApiFactory.getApi(PartnerDirectoryService.class, null); 
    if (service == null){
        throw new IllegalStateException("Partner Directory Service not found");
    }
    
    // get pid
    def properties = message.getProperties(); 
    def Pid = properties.get("partnerID");
    if (Pid == null){
        throw new IllegalStateException("Partner ID not found in sent message");   
    }

    // read retry handling from the Partner Directory
    def maxJMSRetries = service.getParameter("MaxJMSRetries", Pid , String.class);
    
    // if the value exists in the Partner Directory, create a new header holding the max number of retries incremented by 1
    // otherwise, set the header to default which is unlimited
    message.setHeader("maxJMSRetries", maxJMSRetries ? maxJMSRetries.toInteger() - 1 : 'unlimited');
    
    return message;
}
```



<a name="loio05d9f8d85d7945af8d610dca81375b43__section_ism_jy2_j1c"/>

## reuseExtendedReceiverDetermination

Use the following Groovy script `reuseExtendedReceiverDetermination` to check if an extended receiver determination mapping can be reused by reading the corresponding ProcessDirect endpoint from the Partner Directory.

```
import com.sap.gateway.ip.core.customdev.util.Message;
import java.util.HashMap;
import com.sap.it.api.pd.PartnerDirectoryService;
import com.sap.it.api.ITApiFactory;

def Message processData(Message message) {
    
    def service = ITApiFactory.getApi(PartnerDirectoryService.class, null); 
    if (service == null){
        throw new IllegalStateException("Partner Directory Service not found");
    }
    
    // get pid
    def properties = message.getProperties(); 
    def Pid = properties.get("partnerID");
    if (Pid == null){
        throw new IllegalStateException("Partner ID not found in sent message");   
    }

    // read the extended receiver determination end point from the Partner Directory
    def reuseXRDEndpoint = service.getParameter("ReuseXRDEndpoint", Pid , String.class);
    
    // if the extended receiver determination end point exists, create a new exchange property containing the end point
    // otherwise, the exchange property is not created
    message.setProperty("reuseXRDEndpoint", reuseXRDEndpoint ?: null);
    
    // create a new exchange property with value true or false depending on whether the end point exists
    message.setProperty("reuseXRDBoolean", reuseXRDEndpoint ? 'true' : 'false');
    
    return message;
}
```



<a name="loio05d9f8d85d7945af8d610dca81375b43__section_pmr_my2_j1c"/>

## readReceiverNotDeterminedFromPD

Use the following Groovy script `readReceiverNotDeterminedFromPD` to read the type of receiver-not-determined behavior from the Partner Directory if you're reusing an extended receiver determination mapping.

```
import com.sap.gateway.ip.core.customdev.util.Message;
import java.util.HashMap;
import com.sap.it.api.pd.PartnerDirectoryService;
import com.sap.it.api.ITApiFactory;

def Message processData(Message message) {
    
    def service = ITApiFactory.getApi(PartnerDirectoryService.class, null); 
    if (service == null){
        throw new IllegalStateException("Partner Directory Service not found");
    }
    
    // get pid
    def properties = message.getProperties(); 
    def Pid = properties.get("partnerID");
    if (Pid == null){
        throw new IllegalStateException("Partner ID not found in sent message");   
    }

    // read receiver not determined type from the Partner Directory
    def receiverNotDeterminedType = service.getParameter("ReceiverNotDeterminedType", Pid , String.class);
    
    // if the value exists in the Partner Directory, assign the value to a new exchange property
    // otherwise, set the property to default which is Error
    message.setProperty("receiverNotDeterminedType", receiverNotDeterminedType ? receiverNotDeterminedType : 'Error');
    
    // depending on the type, read default receiver from the Partner Directory
    if (receiverNotDeterminedType == 'Default') {
        def receiverNotDeterminedDefault = service.getParameter("ReceiverNotDeterminedDefault", Pid , String.class);
        if (receiverNotDeterminedDefault == null){
            throw new IllegalStateException("Partner ID " + Pid + " not found or ReceiverNotDeterminedDefault parameter not found in the Partner Directory for the partner ID " + Pid);      
        }
        message.setProperty("receiverNotDeterminedDefault", receiverNotDeterminedDefault);
    }
    
    return message;
}
```



<a name="loio05d9f8d85d7945af8d610dca81375b43__section_yjh_bh4_vbc"/>

## displayBulkIDs

Use the following Groovy script `displayBulkIDs` to display all IDoc numbers of an IDoc bulk message in the message monitor.

```
import com.sap.gateway.ip.core.customdev.util.Message 
import org.w3c.dom.NodeList 

def Message processData(Message message) { 
    def nodes = message.getProperty('nodelistToHeader') as NodeList 
    def headerName = message.getProperty('nodelistName') as String 
    def messageLog = messageLogFactory.getMessageLog(message) 

    for (i = 0; i < nodes.getLength(); i++) { 
        messageLog?.addCustomHeaderProperty(headerName, nodes.item(i).getTextContent()) 
    } 

    return message 
}
```



<a name="loio05d9f8d85d7945af8d610dca81375b43__section_dp4_xj4_vbc"/>

## setIDocSenderInterface

Use the following Groovy script `setIDocSenderInterface` to concatenate the sender interface based on the IDoc control headers `MESTYP`, `IDOCTYP` and `CIMTYP`.

```
import com.sap.gateway.ip.core.customdev.util.Message; 
import java.util.HashMap; 

def Message processData(Message message) { 
    // headers 
    def map = message.getHeaders() 

    // set sender interface name 
    message.setHeader("SAP_SenderInterface", map.get("SAP_IDoc_EDIDC_MESTYP") + "." + map.get("SAP_IDoc_EDIDC_IDOCTYP") + (map.get("SAP_IDoc_EDIDC_CIMTYP") ? "." +map.get("SAP_IDoc_EDIDC_CIMTYP") : "")) 

    return message; 
} 
```

