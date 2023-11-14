<!-- loio626f672f799d45a3ab98d4b8c3095ad1 -->

# Using Security Material in Integration Flows

To ensure the security and protection of the message exchange, multiple solutions are possible. It’s possible to use methods to encrypt and decrypt the message content, and to digitally sign and verify the message. Another option to secure the communication on transport level is by selecting the HTTPS or SFTP protocol and using specific authentication methods.

The security material deployed and managed in a Cloud Integration tenant is accessed at runtime by integration flows and APIs to implement two forms of security:

-   **Transport-Level Security \(TLS\)**, which involves the encryption of traffic communication between two systems across a network.

-   **Message-Level Security \(MLS\)**, which involves the encryption of actual message payload being transmitted, and they remain encrypted until the payload is explicitly decrypted using a valid key.


Cloud Integration uses the security material discussed in [Managing Security Material in Cloud Integration](managing-security-material-in-cloud-integration-09ec016.md) to implement TLS and MLS.



<a name="loio626f672f799d45a3ab98d4b8c3095ad1__section_mvg_mb2_mqb"/>

## Transport-Level Security

Transport-level security provides communication security and protection of data integrity and privacy between two communicating applications. It's used for web browsers and other applications that require data to be securely exchanged on a network.

The following table lists some security elements:


<table>
<tr>
<th valign="top">

Security Elements

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Certificate-based authentication

</td>
<td valign="top">

The authentication of a sender is done based on a client certificate. The system checks if a service key is available that contains the client certificate \(provided by the sender\). Afterwards, the system checks if the associated service instance has a role specified which has permissions to call the integration flow endpoint.

For more information, see the blog [How to Set Up Secure HTTP Inbound Connection with Client Certificates](https://blogs.sap.com/2019/08/14/cloud-integration-on-cf-how-to-setup-secure-http-inbound-connection-with-client-certificates/).

</td>
</tr>
<tr>
<td valign="top">

Securely connecting to on-premise via Cloud Connector

</td>
<td valign="top">

For more information, see the section [Connecting to On-Premise Systems Using Cloud Connector](../30-connectivity/connecting-to-on-premise-systems-using-cloud-connector-de83ef5.md).

</td>
</tr>
<tr>
<td valign="top">

SSH

</td>
<td valign="top">

Used to read files from the system \(sender adapter\) or to write files to the system \(receiver adapter\).

See SAP Note [2700759](https://me.sap.com/notes/2700759) for information on how to obtain a Host Key to establish an SSH connection between Cloud Integration and an SFTP server.

</td>
</tr>
<tr>
<td valign="top">

OAuth2 Authentication

</td>
<td valign="top">

The following receiver adapter types support the option *OAuth2 Client Credentials*:

-   AMQP/WebSocket, OData V2, OData V4, HTTP


The following receiver adapter types support the option *OAuth2 SAML*:

-   *Bearer Assertion*: OData V2, HTTP, SAP SuccessFactors OData V2


For more information, see the blog [SAP Cloud Integration - OAuth2 Client Credentials Support in OData V2 Adapter](https://blogs.sap.com/2018/07/31/sap-cloud-platform-integration-oauth2-client-credentials-support-in-odata-v2-adapter/).

</td>
</tr>
<tr>
<td valign="top">

Principal Propagation

</td>
<td valign="top">

The Connectivity and Destination services on SAP BTP allow the use of principal propagation to forward the identity of a Cloud user to the remote system. This assists in the use of Single Sign-On \(SSO\).

For more information, see the help documentation on [Principal Propagation](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/e2cbb48def4342048362039cc157b12e.html), [Scenario for Cloud to On-Premise](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/70b8ef33812e486d8b745a0b47fd093e.html), and [Scenario for Cloud to Cloud](https://help.sap.com/viewer/cca91383641e40ffbe03bdc78f00f681/Cloud/en-US/65b11d4ed333450ebebb8a2e25e805b7.html).

</td>
</tr>
</table>

For more information about transport-level security, see [Security Elements \(Transport-Level Security\)](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/1f7676849a564961872cc45999608a7e.html).



<a name="loio626f672f799d45a3ab98d4b8c3095ad1__section_klj_mb2_mqb"/>

## Message-Level Security

Message-level security allows you to digitally encrypt or decrypt, and sign or verify a message \(or both\). It can be used when the transport-level security can't be implemented, which happens if a legacy communication endpoint doesn't support this option.

The following table presents some message-level security options:


<table>
<tr>
<th valign="top">

Message-Level Security Options

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

PGP Encryption and Decryption

</td>
<td valign="top">

Used to encrypt/decrypt the message content and signing/verification a message.

For more information, see the blog on using a [HCI Encrypt with PGP](https://blogs.sap.com/2018/10/11/hci-encrypt-with-pgp/) on how to use a PGP public key to encrypt data, and the help documentation on [using a PGP encryption step](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/7a07766899c84ed2bb38897e3a332032.html) and on using a [PGP decryption step](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/d0dc511970b04f9bb4a844bcc3d5b89e.html).

</td>
</tr>
<tr>
<td valign="top">

PKCS\#7 Encryption

</td>
<td valign="top">

Used to encrypt the content of the message while it’s being sent to the cloud.

For more information, see the help documentation on [encrypting and signing with PKCS\#7](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/21fd21135941432fbade76e67b9e7194.html), and on [verifying PKCS\#7 signatures](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/f095dc6b9bb04530bbdaf037b250dd7f.html).

</td>
</tr>
<tr>
<td valign="top">

XML Signatures

</td>
<td valign="top">

Used for signing and verifying a payload, which ensures the authenticity of a message and guarantees the identity of the signer and the message was not changed after signing. It’s possible to digitally sign and validate a message based on the XML signature standard. In this case, the digital signature of a document is stored as an XML element.

For more information, see the help documentation on [signing message content with an XML digital signature](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/9a013dba51dc45429b0103a866b0e484.html) and on [verifying XML digital signatures](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/090b932b15d6492aaf5e953803d181bb.html).

</td>
</tr>
<tr>
<td valign="top">

WS Security

</td>
<td valign="top">

Used for signing and verifying a SOAP body and encrypt/decrypt message content \(and the other way round to verify a message and to decrypt the message content\).

For more information, see the help documentation on [Sender SOAP Adapter](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/e53bb5cd1e1745afa7f785e0aff735a1.html) and [Receiver SOAP Adapter](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/e9f42bfe466b4c979dc0860841c05752.html).

</td>
</tr>
</table>

For more information about message-level security options, see [Message-Level Security](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/463a9085156d4672bc4ee9095277e453.html).

