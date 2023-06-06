<!-- loioa98fbcf24dda43298612a0fc91d26fb2 -->

# Message Reprocessing

To ensure a successful migration, you can use reprocessing functionalities to retry processing your ABAP proxies in case of errors.

SAP Process Orchestration provides a message monitoring feature that enables users to monitor messages passing through the system. This feature allows you to view and manage messages that have failed to process, messages that are currently being processed, and messages that have been successfully processed. SAP Process Orchestration also supports a retry mechanism that allows you to define the number of times a message should be retried if it fails to process. You can also define the time interval between each retry attempt.

In Cloud Integration, the reprocessing of messages is done by using either the temporary storage data store or a JMS queue. When a data store is used, the message is stored temporarily in the tenant's database and can be monitored in the data store monitor. When a JMS queue is used, the message is stored in a JMS queue on the connected JMS broker. It's recommended to use a JMS queue because it's more performant.

For more information, see [Cloud Integration - Configuring Scenario Using the XI Sender Adapter](https://blogs.sap.com/2018/06/04/cloud-integration-configuring-scenario-using-the-xi-sender-adapter/).

