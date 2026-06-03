<!-- loio91623a6fe2204f6a99dc132db998f8d0 -->

# Accessing the Partner Directory Using API

> ### Note:  
> The REST client used in the tests for the pipeline concept is **Visual Studio Code**, so the example requests follow the syntax of this extension for Visual Studio Code.

In Visual Studio Code, you can define a settings file in which you maintain the environment variables holding the required URLs and credentials. As a prerequisite, you have setup the service instance and service key. See [Setting Up Inbound HTTP Connections \(for API Clients\)](https://help.sap.com/docs/integration-suite/sap-integration-suite/setting-up-inbound-http-connections-for-api-clients).

You need the following environment variables, which you can retrieve from your service key:

-   `apitokenurl`

-   `api_clientid` and `api_clientsecret`

-   `apihost`


For a request towards the Partner Directory API, authenticate yourself towards the token service to fetch an access token:

```
### fetch access token
# @name getAccessToken
GET {{apitokenurl}}?grant_type=client_credentials HTTP/1.1
Authorization: Basic {{api_clientid}}:{{api_clientsecret}}
```

Store the returned token in a variable:

```
###
@accesstoken = {{getAccessToken.response.body.access_token}}
```

For POST requests, fetch an XSRF token. Authentication is done using the bearer token that you fetched before:

```
### fetch XSRF token
# @name getXSRFToken
GET https://{{apihost}}/api/v1 HTTP/1.1
X-CSRF-Token: fetch
Authorization: Bearer {{accesstoken}}
```

Again, store the returned XSRF token in a variable:

```
###
@xsrftoken = {{getXSRFToken.response.headers.x-csrf-token}}
```

Use both tokens for writing data into the Partner Directory. The following is an example for a string parameter:

```
### create string parameter
POST https://{{apihost}}/api/v1/StringParameters
content-type: application/json
Authorization: Bearer {{accesstoken}}
X-CSRF-Token: {{xsrftoken}}

{
    "Pid": "your partner ID",
    "Id": "ID of the object",
    "Value": "Value of the object"
}
```

The following example shows how to **read** a string parameter:

```
### read string parameter
GET https://{{apihost}}/api/v1/StringParameters(Pid='your partner ID',Id='ID of the object')
Authorization: Bearer {{accesstoken}}
```

The following example shows how to **delete** a string parameter:

```
### delete string parameter
DELETE https://{{apihost}}/api/v1/StringParameters(Pid='your partner ID',Id='ID of the object')
Authorization: Bearer {{accesstoken}}
```

To map an authorized user to a partner ID, set up a service instance and service key with the service plan `integration-flow` that enable a sender system to send messages to Cloud Integration over the HTTP protocol. See [Setting Up Inbound HTTP Connections \(Integration Flow Processing\)](https://help.sap.com/docs/integration-suite/sap-integration-suite/setting-up-inbound-http-connections-integration-flow-processing). The following example shows how to **create an authorized user**:

```
### create authorized user 
POST https://{{apihost}}/api/v1/AuthorizedUsers 
content-type: application/json 
Authorization: Bearer {{accesstoken}} 
X-CSRF-Token: {{xsrftoken}} 

{ 
    "User": "client ID of service key", 
    "Pid": "your partner ID" 
} 
```

The following example shows how to **create an alternative partner**:

```
### create alternative partner 
POST https://{{apihost}}/api/v1/AlternativePartners 
content-type: application/json 
Authorization: Bearer {{accesstoken}} 
X-CSRF-Token: {{xsrftoken}} 

{ 
    "Agency": "your agency", 
    "Scheme": "your identification scheme", 
    "Id": "identifier for the partner issued by the agency", 
    "Pid": "your internal ID of the partner" 
} 
```

The following example shows how to **create a binary parameter**:

```
### create string parameter 
POST https://{{apihost}}/api/v1/BinaryParameters 
content-type: application/json 
Authorization: Bearer {{accesstoken}} 
X-CSRF-Token: {{xsrftoken}} 

{ 
    "Pid": "your partner ID", 
    "Id": "ID of the object", 
    "ContentType": "content type such as xml, xsl, xsd, etc.", 
    "Value": "Base64 encoded value of your binary" 
} 
```

