<!-- loiodc70456eb75e49168fbd2d4eaac12cdf -->

# Examples for Directory API

This chapter collects examples for the APIs described in [Directory API](directory-api-07096c2.md).



<a name="loiodc70456eb75e49168fbd2d4eaac12cdf__section_rx1_nkd_lwb"/>

## Example for CommunicationChannelInService



### Request Example \(Read\)

```
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
	<SOAP-ENV:Header/>
	<SOAP-ENV:Body>
		<yq1:CommunicationChannelReadRequest xmlns:yq1="http://sap.com/xi/BASIS">
			<CommunicationChannelID>
				<PartyID></PartyID>
				<ComponentID>ComponentID</ComponentID> 
				<ChannelID>ChannelID</ChannelID> 
			</CommunicationChannelID> 
		</yq1:CommunicationChannelReadRequest> 
	</SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```



### Response Example \(Read\)

```
<SOAP-ENV:Envelope xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
	<SOAP-ENV:Body>
		<ns2:CommunicationChannelReadResponse xmlns:ns2='http://sap.com/xi/BASIS'>
			<CommunicationChannel>
				<MasterLanguage>EN</MasterLanguage> 
				<AdministrativeData> 
					<ResponsibleUserAccountID>User</ResponsibleUserAccountID>
					<LastChangeUserAccountID>User</LastChangeUserAccountID>
					<LastChangeDateTime>2022-12-16T08:46:11.560+01:00</LastChangeDateTime>
					<FolderPathID>/</FolderPathID>
				</AdministrativeData> 
				<Description languageCode='EN'></Description> 
				<CommunicationChannelID> 
					<PartyID></PartyID>
					<ComponentID>ComponentID</ComponentID> 
					<ChannelID>ChannelID</ChannelID> 
				</CommunicationChannelID>
				<AdapterMetadata>
					<Name>REST</Name> 
					<Namespace>http://sap.com/xi/XI/System</Namespace>
					<SoftwareComponentVersionID>SoftwareComponentVersionID</SoftwareComponentVersionID>
				</AdapterMetadata>
				<Direction>Receiver</Direction>
				<TransportProtocol>HTTP</TransportProtocol> 
				<TransportProtocolVersion></TransportProtocolVersion> 
				<MessageProtocol>REST</MessageProtocol> 
					<MessageProtocolVersion></MessageProtocolVersion> 
				<AdapterEngineName></AdapterEngineName> 
				<AdapterSpecificAttribute> 
					<Name>UseProxy</Name>
					<Namespace></Namespace> 
					<Value>0</Value> 
				</AdapterSpecificAttribute>
				<AdapterSpecificAttribute>
					<Name>ProxyHost</Name> 
					<Namespace></Namespace> 
					<Value>ProxyHost</Value> 
				</AdapterSpecificAttribute> 
				<AdapterSpecificAttribute>
					... 
				</AdapterSpecificAttribute> 
				<AdapterSpecificAttribute>
					... 
				</AdapterSpecificAttribute> 
					... 
				<ModuleProcess>
					<ProcessStep>
						<ModuleName>sap.com/com.sap.aii.adapter.rest.app/RESTAdapterBean</ModuleName>
						<ModuleType>Local Enterprise Bean</ModuleType> 
						<ParameterGroupID>rest</ParameterGroupID> 
					</ProcessStep>
				</ModuleProcess>
				<SenderIdentifier schemeAgencyID='' schemeID=''></SenderIdentifier> 
				<ReceiverIdentifier schemeAgencyID='' schemeID=''></ReceiverIdentifier> 
			</CommunicationChannel> 
			<LogMessageCollection></LogMessageCollection>
		</ns2:CommunicationChannelReadResponse> 
	</SOAP-ENV:Body>
</SOAP-ENV:Envelope> 
```



<a name="loiodc70456eb75e49168fbd2d4eaac12cdf__section_ddf_4kd_lwb"/>

## Example for IntegratedConfigurationInService



### Request Example \(Read\)

```
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
	<SOAP-ENV:Body> 
		<yq1:IntegratedConfigurationReadRequest xmlns:yq1="http://sap.com/xi/BASIS"> 
			<ReadContext>User</ReadContext> 
			<IntegratedConfigurationID> 
				<SenderComponentID>ComponentID</SenderComponentID> 
				<InterfaceName>InterfaceName</InterfaceName> 
				<InterfaceNamespace>InterfaceNamespace</InterfaceNamespace> 
			</IntegratedConfigurationID> 
		</yq1:IntegratedConfigurationReadRequest> 
	</SOAP-ENV:Body> 
</SOAP-ENV:Envelope> 
```



### Response Example \(Read\)

```
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
	<SOAP-ENV:Body> 
		<ns2:IntegratedConfigurationReadResponse xmlns:ns2="http://sap.com/xi/BASIS"> 
			<IntegratedConfiguration> 
				<MasterLanguage>EN</MasterLanguage> 
				<AdministrativeData> 
					<ResponsibleUserAccountID>User</ResponsibleUserAccountID> 
					<LastChangeUserAccountID>User</LastChangeUserAccountID> 
					<LastChangeDateTime>2022-12-01T12:21:05.328+01:00</LastChangeDateTime> 
					<FolderPathID>/</FolderPathID> 
				</AdministrativeData> 
				<IntegratedConfigurationID> 
					<SenderPartyID/> 
					<SenderComponentID>SenderComponentID</SenderComponentID> 
					<InterfaceName>InterfaceName</InterfaceName> 
					<InterfaceNamespace>InterfaceNamespace</InterfaceNamespace> 
					<ReceiverPartyID/> 
					<ReceiverComponentID/> 
				</IntegratedConfigurationID> 
				<InboundProcessing> 
					<SenderInterfaceSoftwareComponentVersion>1234</SenderInterfaceSoftwareComponentVersion> 
					<CommunicationChannel> 
						<PartyID/> 
						<ComponentID>ComponentID</ComponentID> 
						<ChannelID>hannelID</ChannelID> 
					</CommunicationChannel> 
					<SchemaValidationIndicator>false</SchemaValidationIndicator> 
					<VirusScan>UseGlobal</VirusScan> 
					<AdapterSpecificAttribute> 
						<Name>wsse.namespace</Name> 
						<Namespace/> 
						<Value>http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd</Value> 
					</AdapterSpecificAttribute> 
					... 
				</InboundProcessing> 
				<Receivers> 
					<ReceiverRule> 
						<Receiver> 
							<PartyID/> 
							<ComponentID>ComponentID</ComponentID> 
						</Receiver> 
					</ReceiverRule> 
					<NoReceiverBehaviour>ErrorMessage</NoReceiverBehaviour> 
				</Receivers> 
				<ReceiverInterfaces> 
					<Receiver> 
						<PartyID/> 
						<ComponentID>ComponentID</ComponentID> 
					</Receiver> 
					<ReceiverInterfaceRule> 
						<Operation>Operation</Operation> 
						<Mapping> 
							<Name>Name</Name> 
							<Namespace>Namespace</Namespace> 
							<SoftwareComponentVersionID>1234</SoftwareComponentVersionID> 
						</Mapping> 
						<Interface> 
							<Name>Name</Name> 
							<Namespace>urn:Namespace</Namespace> 
							<SoftwareComponentVersionID>1234</SoftwareComponentVersionID> 
						</Interface> 
					</ReceiverInterfaceRule> 
					<QualityOfService>EO</QualityOfService> 
				</ReceiverInterfaces> 
				<OutboundProcessing> 
					<Receiver> 
						<PartyID/> 
						<ComponentID>ComponentID</ComponentID> 
					</Receiver> 
					<ReceiverInterface> 
						<Name>Name</Name> 
						<Namespace>urn:Namespace</Namespace> 
						<SoftwareComponentVersionID>1234</SoftwareComponentVersionID> 
					</ReceiverInterface> 
					<CommunicationChannel> 
						<PartyID/> 
						<ComponentID>ComponentID</ComponentID> 
						<ChannelID>ChannelID</ChannelID> 
					</CommunicationChannel> 
					<SchemaValidationIndicator>false</SchemaValidationIndicator> 
					<VirusScan>UseGlobal</VirusScan> 	
					<HeaderMapping> 
						<Sender/> 
						<Receiver/> 
					</HeaderMapping> 
				</OutboundProcessing> 
				<Logging> 
					<UseGlobal>true</UseGlobal> 
				</Logging> 
				<Staging> 
					<UseGlobal>true</UseGlobal> 
				</Staging> 
			</IntegratedConfiguration> 
			<LogMessageCollection/> 
		</ns2:IntegratedConfigurationReadResponse> 
	</SOAP-ENV:Body> 
</SOAP-ENV:Envelope> 
```



<a name="loiodc70456eb75e49168fbd2d4eaac12cdf__section_d14_4kd_lwb"/>

## Example for IntegratedConfiguration750InService



### Request Example \(Read\)

```
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
	<SOAP-ENV:Body> 
		<yq1:IntegratedConfigurationReadRequest xmlns:yq1="http://sap.com/xi/BASIS"> 
			<ReadContext>User</ReadContext> 
			<IntegratedConfigurationID> 
				<SenderComponentID>BC_PIMAS_Sender</SenderComponentID> 
				<InterfaceName>SI_P2P_ASYNC_CSV_0002_Out</InterfaceName> 
				<InterfaceNamespace>urn:P2P_ASYNC_CSV:0002</InterfaceNamespace> 
			</IntegratedConfigurationID> 
		</yq1:IntegratedConfigurationReadRequest> 
	</SOAP-ENV:Body> 
</SOAP-ENV:Envelope> 
```



### Response Example \(Read\)

```
<?xml version="1.0" encoding="utf-8"?><SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<SOAP-ENV:Body>	
		<ns2:IntegratedConfiguration750ReadResponse xmlns:ns2="http://sap.com/xi/BASIS">	
			<IntegratedConfiguration>	
				<MasterLanguage>EN</MasterLanguage>	
				<AdministrativeData>	
					<ResponsibleUserAccountID>User</ResponsibleUserAccountID>	
					<LastChangeUserAccountID>User</LastChangeUserAccountID>	
					<LastChangeDateTime>2022-12-01T12:21:05.328+01:00</LastChangeDateTime>	
					<FolderPathID>/</FolderPathID>	
				</AdministrativeData>	
				<IntegratedConfigurationID>	
					<SenderPartyID/>	
					<SenderComponentID>SenderComponentID</SenderComponentID>	
					<InterfaceName>InterfaceName</InterfaceName>	
					<InterfaceNamespace>urn:InterfaceNamespace</InterfaceNamespace>	
					<ReceiverPartyID/>	
					<ReceiverComponentID/>	
				</IntegratedConfigurationID>	
				<InboundProcessing>	
					<SenderInterfaceSoftwareComponentVersion>1234</SenderInterfaceSoftwareComponentVersion>	
					<CommunicationChannel>	
						<PartyID/>	
						<ComponentID>ComponentID</ComponentID>	
						<ChannelID>ChannelID</ChannelID>	
					</CommunicationChannel>	
					<SchemaValidationIndicator>false</SchemaValidationIndicator>	
					<VirusScan>Use Global</VirusScan>	
					<AdapterSpecificAttribute>	
						<Name>wsse.namespace</Name>	
						<Namespace/>	
						<Value>http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd</Value>	
					</AdapterSpecificAttribute>	
					...	
				</InboundProcessing>	
				<Receivers>	
					<ReceiverWildcardIndicator>false</ReceiverWildcardIndicator>	
					<ReceiverRule>	
						<Condition/>	
						<Receiver>	
							<CommunicationParty>	
								<TypeID>Constant</TypeID>	
								<Value/>	
								<Datatype>xsd:string</Datatype>	
								<ContextObjectName/>	
								<ContextObjectNamespace/>	
							</CommunicationParty>	
							<CommunicationPartySchema>	
								<TypeID>Constant</TypeID>	
								<Value>XIParty</Value>	
								<Datatype>xsd:string</Datatype>	
								<ContextObjectName/>	
								<ContextObjectNamespace/>	
							</CommunicationPartySchema>	
							<CommunicationPartyAgency>	
								<TypeID>Constant</TypeID>	
								<Value>http://sap.com/xi/XI</Value>	
								<Datatype>xsd:string</Datatype>	
								<ContextObjectName/>	
								<ContextObjectNamespace/>	
							</CommunicationPartyAgency>	
							<CommunicationComponent>	
								<TypeID>Constant</TypeID>	
								<Value>Value</Value>	
								<Datatype>xsd:string</Datatype>	
								<ContextObjectName/>	
								<ContextObjectNamespace/>	
							</CommunicationComponent>	
						</Receiver>	
					</ReceiverRule>	
					<NoReceiverBehaviour>Error Message</NoReceiverBehaviour>	
				</Receivers>	
				<ReceiverInterfaces>	
					<Receiver>	
						<PartyID/>	
						<ComponentID>ComponentID</ComponentID>	
					</Receiver>	
					<ReceiverInterfaceRule>	
						<Operation>Operation</Operation>	
						<Mapping>	
							<Name>Name</Name>	
							<Namespace>urn:Namespace</Namespace>	
							<SoftwareComponentVersionID>1234</SoftwareComponentVersionID>	
						</Mapping>	
						<Interface>	
							<Name>Name</Name>	
							<Namespace>urn:Namespace</Namespace>	
							<SoftwareComponentVersionID>1234</SoftwareComponentVersionID>	
						</Interface>	
					</ReceiverInterfaceRule>	
					<QualityOfService>EO</QualityOfService>	
				</ReceiverInterfaces>	
				<OutboundProcessing>	
					<Receiver>	
						<PartyID/>	
						<ComponentID>ComponentID</ComponentID>	
					</Receiver>	
					<ReceiverInterface>	
						<Name>Name</Name>	
						<Namespace>urn:Namespace</Namespace>	
						<SoftwareComponentVersionID>1234</SoftwareComponentVersionID>	
					</ReceiverInterface>	
					<CommunicationChannel>	
						<PartyID/>	
						<ComponentID>ComponentID</ComponentID>	
						<ChannelID>ChannelID</ChannelID>	
					</CommunicationChannel>	
					<SchemaValidationIndicator>false</SchemaValidationIndicator>	
					<VirusScan>Use Global</VirusScan>	
					<HeaderMapping>	
						<Sender/>	
						<Receiver/>	
					</HeaderMapping>	
				</OutboundProcessing>
				<Logging>
					<UseGlobal>true</UseGlobal>
				</Logging>
				<Staging>
					<UseGlobal>true</UseGlobal>
				</Staging>
			</IntegratedConfiguration>
			<LogMessageCollection/>
		</ns2:IntegratedConfiguration750ReadResponse>
	</SOAP-ENV:Body>
</SOAP-ENV:Envelope>

```



<a name="loiodc70456eb75e49168fbd2d4eaac12cdf__section_ovw_4kd_lwb"/>

## Example for SenderAgreementInService



### Request Example \(Read\)

```
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
	<SOAP-ENV:Body>
		<yq1:SenderAgreementReadRequest xmlns:yq1="http://sap.com/xi/BASIS">
			<ReadContext>User</ReadContext>
			<SenderAgreementID>
				<SenderComponentID>SenderComponentID</SenderComponentID>
				<InterfaceName>InterfaceName</InterfaceName>
				<InterfaceNamespace>InterfaceNamespace</InterfaceNamespace> 
			</SenderAgreementID>
		</yq1:SenderAgreementReadRequest> 
	</SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```



### Response Example \(Read\)

```
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
	<SOAP-ENV:Body>
		<ns2:SenderAgreementReadResponse xmlns:ns2="http://sap.com/xi/BASIS">
			<SenderAgreement>
				<MasterLanguage>EN</MasterLanguage>
				<AdministrativeData>
					<ResponsibleUserAccountID>User</ResponsibleUserAccountID>
					<LastChangeUserAccountID>User</LastChangeUserAccountID>
					<LastChangeDateTime>2016-04-29T11:58:35.034+02:00</LastChangeDateTime>
					<FolderPathID>/</FolderPathID>
				</AdministrativeData>
				<Description languageCode="EN"/>
				<SenderAgreementID>
					<SenderPartyID/> 
					<SenderComponentID>SenderComponentID</SenderComponentID>
					<InterfaceName>InterfaceName</InterfaceName>
					<InterfaceNamespace>InterfaceNamespace</InterfaceNamespace>
					<ReceiverPartyID/>
					<ReceiverComponentID/> 
				</SenderAgreementID>
				<CommunicationChannel> 
					<PartyID/>
					<ComponentID>ComponentID</ComponentID>
					<ChannelID>ChannelID</ChannelID>
				</CommunicationChannel> 
				<SoftwareComponentVersion>2171ef81-4319-11db-ae76-c6090a4240fd</SoftwareComponentVersion>
				<ForIntegratedConfiguration>true</ForIntegratedConfiguration>
				<SchemaValidation>No Validation</SchemaValidation>
				<VirusScan>Use Global</VirusScan>
				<AdapterSpecificAttribute>
					<Name>propagatePrincipal</Name>
					<Namespace/>
					<Value>0</Value>
				</AdapterSpecificAttribute>
			</SenderAgreement>
			<LogMessageCollection/>
		</ns2:SenderAgreementReadResponse>
	</SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```



<a name="loiodc70456eb75e49168fbd2d4eaac12cdf__section_e2j_pkd_lwb"/>

## Example for ReceiverAgreementInService



### Request Example \(Read\)

```
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
		<SOAP-ENV:Header/> 
	<SOAP-ENV:Body>
		<yq1:ReceiverAgreementReadRequest xmlns:yq1="http://sap.com/xi/BASIS">
			<ReceiverAgreementID>
				<SenderPartyID></SenderPartyID>
				<SenderComponentID>SenderComponentID</SenderComponentID>
				<InterfaceName>InterfaceName</InterfaceName>
				<InterfaceNamespace>InterfaceNamespace</InterfaceNamespace> 
				<ReceiverPartyID></ReceiverPartyID>
				<ReceiverComponentID>ReceiverComponentID</ReceiverComponentID>
			</ReceiverAgreementID>
	</yq1:ReceiverAgreementReadRequest>
		</SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```



### Response Example \(Read\)

```
<?xml version="1.0" encoding="UTF-8"?> 
<SOAP-ENV:Envelope xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
	<SOAP-ENV:Body>
		<ns2:ReceiverAgreementReadResponse xmlns:ns2='http://sap.com/xi/BASIS'> 
			<ReceiverAgreement>
				<MasterLanguage>EN</MasterLanguage> 
				<AdministrativeData>
					<ResponsibleUserAccountID>User</ResponsibleUserAccountID> 
					<LastChangeUserAccountID>User</LastChangeUserAccountID>
					<LastChangeDateTime>2022-03-18T14:42:17.353Z</LastChangeDateTime> 
					<FolderPathID>/</FolderPathID>
				</AdministrativeData> 
				<ReceiverAgreementID> 
					<SenderPartyID></SenderPartyID>
					<SenderComponentID>SenderComponentID</SenderComponentID> 
					<InterfaceName>InterfaceName</InterfaceName> 
					<InterfaceNamespace>InterfaceNamespace</InterfaceNamespace> 
					<ReceiverPartyID></ReceiverPartyID>
					<ReceiverComponentID>ReceiverComponentID</ReceiverComponentID> 
				</ReceiverAgreementID>
				<CommunicationChannel>
					<PartyID></PartyID>
					<ComponentID>ComponentID</ComponentID>
					<ChannelID>ChannelID</ChannelID>
				</CommunicationChannel>
				<SoftwareComponentVersion>0050568f-0aac-1ee8-94ef-d636a5cec849</SoftwareComponentVersion>
				<SchemaValidationIndicator>false</SchemaValidationIndicator>
				<VirusScan>Use Global</VirusScan>
				<HeaderMapping>
					<Sender></Sender>
					<Receiver></Receiver>
				</HeaderMapping>
			</ReceiverAgreement> 
			<LogMessageCollection></LogMessageCollection> 
		</ns2:ReceiverAgreementReadResponse> 
	</SOAP-ENV:Body> 
</SOAP-ENV:Envelope>
```



<a name="loiodc70456eb75e49168fbd2d4eaac12cdf__section_byn_pkd_lwb"/>

## Example for ValueMappingInService



### Request Example \(Read\)

```
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
	<SOAP-ENV:Body>
		<yq1:ValueMappingReadRequest xmlns:yq1="http://sap.com/xi/BASIS">
			<ReadContext>User</ReadContext>
			<ValueMappingID>GroupID</ValueMappingID>
		</yq1:ValueMappingReadRequest> 
	</SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```



### Response Example \(Read\)

```
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
	<SOAP-ENV:Body>
		<ns2:ValueMappingReadResponse xmlns:ns2="http://sap.com/xi/BASIS"> 
			<ValueMapping>
				<MasterLanguage>EN</MasterLanguage>
				<AdministrativeData> 
					<ResponsibleUserAccountID>User</ResponsibleUserAccountID> 
					<LastChangeUserAccountID>User</LastChangeUserAccountID> 
					<LastChangeDateTime>2018-11-27T06:18:24.949+01:00</LastChangeDateTime> 
					<FolderPathID>/</FolderPathID> 
				</AdministrativeData>
				<Description languageCode="EN"/>
				<ValueMappingID>ValueMappingID</ValueMappingID> 
				<GroupName>GroupName</GroupName>
			</ValueMapping>
			<LogMessageCollection/> 
		</ns2:ValueMappingReadResponse>
	</SOAP-ENV:Body>
</SOAP-ENV:Envelope> 
```



<a name="loiodc70456eb75e49168fbd2d4eaac12cdf__section_iwp_skd_lwb"/>

## Example for ConfigurationScenarioInService



### Request Example \(Read\)

```
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
	<SOAP-ENV:Body>
		<yq1:ConfigurationScenarioReadRequest xmlns:yq1="http://sap.com/xi/BASIS"> 
			<ReadContext>User</ReadContext>
			<ConfigurationScenarioID>PI_Elevation_PIMAS_PIMG</ConfigurationScenarioID> 
		</yq1:ConfigurationScenarioReadRequest>
	</SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```



### Response Example \(Read\)

```
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<SOAP-ENV:Body> 
		<ns2:ConfigurationScenarioReadResponse xmlns:ns2="http://sap.com/xi/BASIS">
			<ConfigurationScenario>
				<MasterLanguage>EN</MasterLanguage>
				<AdministrativeData> 
					<ResponsibleUserAccountID>User</ResponsibleUserAccountID>
					<LastChangeUserAccountID>User</LastChangeUserAccountID>
					<LastChangeDateTime>2023-01-13T14:34:01.971+01:00</LastChangeDateTime>
					<FolderPathID>/</FolderPathID>
				</AdministrativeData>
				<ConfigurationScenarioID>PI_Elevation_PIMAS_PIMG</ConfigurationScenarioID>
				<BusinessComponent>
					<PartyID/>
					<ComponentID>ComponentID</ComponentID>
				</BusinessComponent>
				<CommunicationChannel> 
					<PartyID/>
					<ComponentID>ComponentID</ComponentID>
					<ChannelID>ChannelID</ChannelID>
				</CommunicationChannel> 
				<CommunicationChannel> 
					... 
				</CommunicationChannel> 
				<IntegratedConfiguration> 
					<SenderPartyID/> 
					<SenderComponentID>SenderComponentID</SenderComponentID> 
					<InterfaceName>InterfaceName</InterfaceName>
					<InterfaceNamespace>urn:InterfaceNamespace</InterfaceNamespace> 
					<ReceiverPartyID/> 
					<ReceiverComponentID/> 
				</IntegratedConfiguration> 
				<IntegratedConfiguration> 
					... 
				</IntegratedConfiguration> 
			</ConfigurationScenario>
			<LogMessageCollection/>
		</ns2:ConfigurationScenarioReadResponse>
	</SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```



<a name="loiodc70456eb75e49168fbd2d4eaac12cdf__section_uq5_skd_lwb"/>

## Example for AlertRuleInService



### Request Example \(Query\)

```
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:bas="http://sap.com/xi/BASIS"> 
	<soapenv:Header/>
	<soapenv:Body>
		<bas:AlertRuleQueryRequest>
			<AlertRuleID></AlertRuleID>
			<Description languageCode=""></Description>
			<AdministrativeData>
				<ResponsibleUserAccountID></ResponsibleUserAccountID> 
				<LastChangeUserAccountID></LastChangeUserAccountID>
				<LastChangeDateTime></LastChangeDateTime>
				<FolderPathID></FolderPathID>
			</AdministrativeData>
		</bas:AlertRuleQueryRequest>
	</soapenv:Body>
</soapenv:Envelope>
```



### Response Example \(Query\)

```
<SOAP-ENV:Envelope xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
	<SOAP-ENV:Body>
		<ns2:AlertRuleQueryResponse xmlns:ns2='http://sap.com/xi/BASIS'>
			<AlertRule>
				<AlertRuleID>AlertRuleID</AlertRuleID>
				<AlertRuleTechnicalID>dff69b116cba3bee900f564757a3c339</AlertRuleTechnicalID>
				<Description languageCode=''></Description>
				<AdministrativeData>
					<ResponsibleUserAccountID>User</ResponsibleUserAccountID>
					<LastChangeUserAccountID>User</LastChangeUserAccountID>
					<LastChangeDateTime>2022-07-12T07:52:04.603Z</LastChangeDateTime> 
				</AdministrativeData> 
				<Severity>LOW</Severity> 
				<State>ENABLED</State> 
				<PayloadInAlert>DISABLED</PayloadInAlert> 
				<AlertConsumers></AlertConsumers> 
			</AlertRule>
			<AlertRule>
				<AlertRuleID>AlertRuleID</AlertRuleID> 
				<AlertRuleTechnicalID>cc6dae12dc7d363b8d351651a46804a3</AlertRuleTechnicalID>
				<Description languageCode=''></Description> 
				<AdministrativeData>
					<ResponsibleUserAccountID>User</ResponsibleUserAccountID>
					<LastChangeUserAccountID>User</LastChangeUserAccountID>
					<LastChangeDateTime>2021-11-10T16:22:27.602Z</LastChangeDateTime>
				</AdministrativeData> 
				<Severity>LOW</Severity> 
				<State>ENABLED</State> 
				<PayloadInAlert>ENABLED</PayloadInAlert> 
				<AlertConsumers>RS-ALERT</AlertConsumers> 
			</AlertRule>
		</ns2:AlertRuleQueryResponse>
	</SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

