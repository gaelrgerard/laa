Terminology and Definitions
===========================

The following meanings apply to SHALL, SHALL NOT, MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY in this document (refer to [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119)):
- **SHALL** indicates an absolute requirement, as does **MUST**.
- **SHALL NOT** indicates an absolute prohibition, as does **MUST NOT**.
- **SHOULD** and **SHOULD NOT** indicate recommendations.
- **MAY** indicates an option.


Selected terms used in this document are included in following table.

| Term                                                                    | Definition                                                                                                                                                                               |
|-------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <a name="SAMSM">SAM SM</a>           | An entity which, on behalf of the Application Service Provider, is in charge of managing SAM Applets through SAM Commands |
| <a name="SAMSMEndpoint">SAM SM Endpoint</a>                                    | Base URI used by the LAA to trigger some management                                                                                                                                |
| <a name="Command">Command</a>                                           | Message sends by the RA during the Remote Management Step                                                                                                                                |
| <a name="DataFormat">Data Format</a>                                    | How data exchanged between SAM SM and Local Applet Assistant are formatted. Defines as a MIME type.                                                                                           |
| <a name="Device">Device</a>                                             | User equipment used in conjunction with an eUICC to connect to a mobile network. E.g. a tablet, wearable, smartphone, or handset.                                                        |
| <a name="Handshake">Handshake</a>                                       | Protocol Step during which the Secure Element and the Protocol Binding to be used for the Remote Management Session is selected.                                                         |
| <a name="Initialisation">Initialization</a>                             | Protocol Step during which the sessionID is generated and shared                                                                                                                         |
| <a name="ManagementSession">Management Session</a>                      | The timing frame during which the management task associated with a sessionID is performed.                                                                                              |
| <a name="ProtocolBinding">Protocol Binding</a>                          | Rules associated with a Data Format and a Transport protocol to exchange Message                                                                                                         |
| <a name="SAMSM">SAM SM</a>                                  | A SAM SM intermediate between SAM SM and the Local Applet Assistant.                                                                                                 |
| <a name="RemoteManagementSession">Remote Management Session</a>         | A Protocol Step during which the Remote Platform perform the management of a Secure Element.                                                                                             |
| <a name="Response">Response</a>                                         | Message that provides a response to a Command Message                                                                                                                                    |
| <a name="RichExecutionEnvironment">Rich Execution Environment</a>       | As defined by GP TEE                                                                                                                                                                     |
| <a name="SecureElement">Secure Element</a>                              | Physical component attached with the Device manageable according with GP Card specification.                                                                                             |
| <a name="sessionID">sessionId</a>                                       | An identifier shared between the Device Application and the SAM SM and associated with a Management Session                                                                 |
| <a name="Transport">Transport</a>                                       | The transport protocol used between SAM SM and Local Applet Assistant.                                                                                                                        |
| <a name="LAA">Local Applet Assistant</a>                                    | A functional element in the Device that provides the capability to manage SAM  Services.                                                                                                                       |


