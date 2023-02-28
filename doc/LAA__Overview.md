LAA - Protocol Overview
============================

This documentation defines a protocol that allows a [LAA](LAA__Terminology_And_Definitions.md#LAA) to request the management of a [SAM SD](LAA__Terminology_And_Definitions.md#SAMSD) by a [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM).

The following figure presents the SAM architecture and its environment. All words in blue are defined in this documentation.

![Architecture Overview](images/LAA__SAM_Architecture_Overview.png)

This documentation is focusing on the SAM04 interface.
[GPSERAM](LAA__References.md#GPSERAM) is also used on this SAM04 interface.
[SAM Configuration](LAA__References.md#SAMCONF) is focusing more on the [SAM SD](LAA__Terminology_And_Definitions.md#SAMSD)
A [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) and a [LAA](LAA__Terminology_And_Definitions.md#LAA) manage this protocol to allow the [LAA](LAA__Terminology_And_Definitions.md#LAA) to trigger a a [Device Application](LAA__Terminology_And_Definitions.md#DeviceApplication) and the [Secure Element](LAA__Terminology_And_Definitions.md#SecureElement).

While [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM), [Device](LAA__Terminology_And_Definitions.md#Device) and [Secure Element](LAA__Terminology_And_Definitions.md#SecureElement) are physical entities, the [Device Application](LAA__Terminology_And_Definitions.md#DeviceApplication) and [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) are logical components, and the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) and the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) in this specification are to be considered as functions. These functions might be implemented as standalone applications or as libraries integrated inside larger business applications. In the LAA context, the terms [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) and [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) may be used interchangeably with *SAM SM function* and *Local Applet Assistant function*.

Note that if the [Device](LAA__Terminology_And_Definitions.md#Device) embeds a [Trusted Execution Environment](LAA__Terminology_And_Definitions.md#TrustedExecutionEnvironment), the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) may be implemented in this [Trusted Execution Environment](LAA__Terminology_And_Definitions.md#TrustedExecutionEnvironment).  Otherwise, the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) is implemented in the [Rich Execution Environment](LAA__Terminology_And_Definitions.md#RichExecutionEnvironment) of the [Device](LAA__Terminology_And_Definitions.md#Device). In these two cases, the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) will have to use an API providing access to the [Secure Element](LAA__Terminology_And_Definitions.md#SecureElement) and allowing it to forward commands to an application in this [Secure Element](LAA__Terminology_And_Definitions.md#SecureElement). This API is called an [SE Access API](LAA__Terminology_And_Definitions.md#SEAccessAPI) in this specification. The [SE Access API](LAA__Terminology_And_Definitions.md#SEAccessAPI) can be the [SIMalliance GlobalPlatform Open Mobile API](https://globalplatform.org/specs-library/open-mobile-api-specification-v3-3/) when the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) is implemented in the [Rich Execution Environment](LAA__Terminology_And_Definitions.md#RichExecutionEnvironment) (REE), and the [GlobalPlatform TEE Secure Element API](https://globalplatform.org/specs-library/tee-secure-element-api/) when the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) is implemented in the [Trusted Execution Environment](LAA__Terminology_And_Definitions.md#TrustedExecutionEnvironment) (TEE).

More precisely, an [SE Access API](LAA__Terminology_And_Definitions.md#SEAccessAPI) usually provides mechanisms for a device application to open a connection with the [Secure Element](LAA__Terminology_And_Definitions.md#SecureElement) and then to open a logical channel with a card application in order to send *APDUs* to this application.

Protocol design
---------------

### Protocol Layers

LAA is a message-oriented protocol which used the following protocol stack:

![Protocol layers](images/LAA__Protocol_layers.png)

[Messages](LAA__Terminology_And_Definitions.md#Message) are the data exchanged between the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) and the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA). The definition, the meaning and sequency of [Messages](LAA__Terminology_And_Definitions.md#Message) are states below in the [Messages section](#messages).

How [Messages](LAA__Terminology_And_Definitions.md#Message) are carried on the network relies on the [Protocol Binding](LAA__Terminology_And_Definitions.md#ProtocolBinding) used by the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) and the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA). A [Protocol Binding](LAA__Terminology_And_Definitions.md#ProtocolBinding) defines the rules to map [Messages](LAA__Terminology_And_Definitions.md#Message) on the [Data Format](LAA__Terminology_And_Definitions.md#DataFormat) layer and the [Transport](LAA__Terminology_And_Definitions.md#Transport) layer.

This version of the specification defines the following [Data Format](LAA__Terminology_And_Definitions.md#DataFormat) and [Transport](LAA__Terminology_And_Definitions.md#Transport) protocol layers:

-   **HTTPS** as [Transport](LAA__Terminology_And_Definitions.md#Transport)

-   **JSON** as [Data Format](LAA__Terminology_And_Definitions.md#DataFormat)

Others protocol layer elements may be defined in the future.

This version of the specification defined the following [Protocol Binding](LAA__Terminology_And_Definitions.md#ProtocolBinding):

-   **HTTP REST**, which uses HTTPS as [Transport](LAA__Terminology_And_Definitions.md#Transport) protocol and JSON as [Data Format](LAA__Terminology_And_Definitions.md#DataFormat).

Others [Protocol Binding](LAA__Terminology_And_Definitions.md#ProtocolBinding) may be defined in the future.

### Management Session

A [Device Application](LAA__Terminology_And_Definitions.md#DeviceApplication) and a [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) relies on a session identifier, named [sessionId](LAA__Terminology_And_Definitions.md#sessionId). The [sessionId](LAA__Terminology_And_Definitions.md#sessionId) is shared and used for all communications between the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) and the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM).

The session during which is performed some management tasks that are associated with one sessionId is called the [Management Session](LAA__Terminology_And_Definitions.md#ManagementSession).

![Management Session](images/GP_SERAM__Management_Session.png)

The [Management Session](LAA__Terminology_And_Definitions.md#ManagementSession) is started by the [Device Application](LAA__Terminology_And_Definitions.md#DeviceApplication) and is then controlled until its end by the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM).

### Protocol Steps

As shown by the next figure, this protocol has three steps. First the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) is triggered by the [Device Application](LAA__Terminology_And_Definitions.md#DeviceApplication) with the [sessionId](LAA__Terminology_And_Definitions.md#sessionId) and the [RA Endpoint](LAA__Terminology_And_Definitions.md#RAEndpoint). It then negotiates the [Data Format](LAA__Terminology_And_Definitions.md#DataFormat) and [Transport](LAA__Terminology_And_Definitions.md#Transport) protocol to use with the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM). Finally, the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) make the task required for the [Management Session](LAA__Terminology_And_Definitions.md#ManagementSession).

![Protocol Steps](images/GP_SERAM__Protocol_Steps.png)

Most of the [Initialization](LAA__Terminology_And_Definitions.md#Initialization) [Step](LAA__Terminology_And_Definitions.md#Step) is out of the scope of this document.

During the [Handshake](LAA__Terminology_And_Definitions.md#Handshake) [Step](LAA__Terminology_And_Definitions.md#Step), the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) performs a protocol negotiation with the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM), by sending its capabilities, the session identifier, and a list of manageable [Secure Element](LAA__Terminology_And_Definitions.md#SecureElement). A [Protocol Binding](LAA__Terminology_And_Definitions.md#ProtocolBinding) to be used for the next step is then selected.

Next, the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) starts a [Command Exchange](LAA__Terminology_And_Definitions.md#CommandExchange) [Step](LAA__Terminology_And_Definitions.md#Step) by sending a *Start* [Command](LAA__Terminology_And_Definitions.md#Command). During the [Command Exchange](LAA__Terminology_And_Definitions.md#CommandExchange), the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) may send *APDUs* to the [Secure Element](LAA__Terminology_And_Definitions.md#SecureElement), or send notifications to the [Device Application](LAA__Terminology_And_Definitions.md#DeviceApplication). The end of the [Management Session](LAA__Terminology_And_Definitions.md#ManagementSession) is announced by a *Stop* [Command](LAA__Terminology_And_Definitions.md#Command) form the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM).

Protocol details
----------------------

### Initialization Step

During this phase, a session identifier, named [sessionId](LAA__Terminology_And_Definitions.md#sessionId), SHALL be generated and shared between the [Device Application](LAA__Terminology_And_Definitions.md#DeviceApplication) and the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM). How this [sessionId](LAA__Terminology_And_Definitions.md#sessionId) is generated and shared is out of the scope of this specification.

The [sessionId](LAA__Terminology_And_Definitions.md#sessionId) SHALL be a unique identifier for the [Device Application](LAA__Terminology_And_Definitions.md#DeviceApplication) and the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM). How this uniqueness is handled is out of the scope of this specification.

Moreover, the [RA Endpoint](LAA__Terminology_And_Definitions.md#RAEndpoint) to communicate with the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) MUST also has been shared between entities. How this [RA Endpoint](LAA__Terminology_And_Definitions.md#RAEndpoint) is defined and shared is out of the scope of this specification.

LAA session starts after the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) is triggered with the [sessionId](LAA__Terminology_And_Definitions.md#sessionId) and the [RA Endpoint](LAA__Terminology_And_Definitions.md#RAEndpoint) of the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM). The [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) starts with the [Handshake](LAA__Terminology_And_Definitions.md#Handshake) [Step](LAA__Terminology_And_Definitions.md#Step).

### Handshake Step

As soon as it was triggered, the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) shall start the [Handshake](LAA__Terminology_And_Definitions.md#Handshake) [Step](LAA__Terminology_And_Definitions.md#Step).

Handshaking allows a [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) and [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) to negotiate the [Data Format](LAA__Terminology_And_Definitions.md#DataFormat) and the [Transport](LAA__Terminology_And_Definitions.md#Transport) protocol used to perform the remote management.

This method shall be used by the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) to tell which [Data Format](LAA__Terminology_And_Definitions.md#DataFormat) and which [Transport](LAA__Terminology_And_Definitions.md#Transport) protocols it supports. In response, the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) shall tell which ones it selects.

The attributes which are negotiated are:

-   The secure elements: the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) provides a list of [Secure Element](LAA__Terminology_And_Definitions.md#SecureElement) which may be targeted by the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM)

-   The [Data Format](LAA__Terminology_And_Definitions.md#DataFormat) (e.g. JSON)

-   The [Transport](LAA__Terminology_And_Definitions.md#Transport) protocols (e.g. HTTPS)

-   The version of the protocol

To allow the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) to track the [Command Exchange](LAA__Terminology_And_Definitions.md#CommandExchange) the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) provides a [sessionId](LAA__Terminology_And_Definitions.md#sessionId) that shall be reused in all subsequent exchanges as defined by the selected [Protocol Binding](LAA__Terminology_And_Definitions.md#ProtocolBinding).

The [Handshake](LAA__Terminology_And_Definitions.md#Handshake) [Step](LAA__Terminology_And_Definitions.md#Step) shall be performed using the *HTTP REST* [Protocol Binding](LAA__Terminology_And_Definitions.md#ProtocolBinding).

### Command Exchange Step

During the [Command Exchange](LAA__Terminology_And_Definitions.md#CommandExchange) [Step](LAA__Terminology_And_Definitions.md#Step), the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) performs a series of actions by sending [Commands](LAA__Terminology_And_Definitions.md#Command) to the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA). The [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) processed each [Command](LAA__Terminology_And_Definitions.md#Command) and if required send a [Response](LAA__Terminology_And_Definitions.md#Response) to the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM).

[Commands](LAA__Terminology_And_Definitions.md#Command) and [Responses](LAA__Terminology_And_Definitions.md#Response) are exchanged using, respectively, *Order* [Messages](LAA__Terminology_And_Definitions.md#Message) and *Report* [Messages](LAA__Terminology_And_Definitions.md#Message). An  *Order* [Message](LAA__Terminology_And_Definitions.md#Message) sent by the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) may carry one or more [Command](LAA__Terminology_And_Definitions.md#Command). Similary, a *Report* [Message](LAA__Terminology_And_Definitions.md#Message) from the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) may carry one or more [Response](LAA__Terminology_And_Definitions.md#Response). [Messages](LAA__Terminology_And_Definitions.md#Message) which are exchanges during the [Command Exchange](LAA__Terminology_And_Definitions.md#CommandExchange) [Step](LAA__Terminology_And_Definitions.md#Step) shall use the [Protocol Binding](LAA__Terminology_And_Definitions.md#ProtocolBinding) which has been selected during the [Handshake](LAA__Terminology_And_Definitions.md#Handshake) [Step](LAA__Terminology_And_Definitions.md#Step).

![SAM SM processing during Command Exchange](images/GP_SERAM__Remote_Agent_processing_during_Command_Exchange.png)

As shown by the diagram, the first and last [Command](LAA__Terminology_And_Definitions.md#Command) of the [Command Exchange](LAA__Terminology_And_Definitions.md#CommandExchange) [Step](LAA__Terminology_And_Definitions.md#Step) is respectively the *Start* [Command](LAA__Terminology_And_Definitions.md#Command) and *Stop* [Command](LAA__Terminology_And_Definitions.md#Command). Other *RAM* [Commands](LAA__Terminology_And_Definitions.md#Command) are used to send *APDUs* to the [Secure Element](LAA__Terminology_And_Definitions.md#SecureElement), or *Notifications* to the [Device Application](LAA__Terminology_And_Definitions.md#DeviceApplication). Only the *Start* and *Stop* [Commands](LAA__Terminology_And_Definitions.md#Command) are mandatory.

Protocol overview diagram
-------------------------

The following sequence diagram resumes the main exchanges during a [Management Session](LAA__Terminology_And_Definitions.md#ManagementSession). In the diagram the exchanges during the [Command Exchange](LAA__Terminology_And_Definitions.md#CommandExchange) [Step](LAA__Terminology_And_Definitions.md#Step) are illustrated with the two types of *RAM* [Command](LAA__Terminology_And_Definitions.md#Command) that can be sent by a [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) after the *Start* [Command](LAA__Terminology_And_Definitions.md#Command) and until the *Stop* [Command](LAA__Terminology_And_Definitions.md#Command).

![Protocol overview](images/GP_SERAM__Protocol_overview.png)

Messages
========

The following type of [Messages](LAA__Terminology_And_Definitions.md#Message) may be exchanged between [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) and [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM):

| Protocol Step    | Messages               | From         | To           |
|------------------|------------------------|--------------|--------------|
| Handshake        | **Handshake Command**  | Local Applet Assistant  | SAM SM |
| Handshake        | **Handshake Response** | SAM SM | Local Applet Assistant  |
| Command Exchange | **Order**              | SAM SM | Local Applet Assistant  |
| Command Exchange | **Report**             | Local Applet Assistant  | SAM SM |

Local Applet Assistant Behaviour
=====================

Upon end user request, the Local Applet Assistant initiates the installation by sending  to the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) a SAM Eligibility command.

On reception of the *Handshake Response* [Message](LAA__Terminology_And_Definitions.md#Message) from the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM), the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) goes to the next [Command Exchange](LAA__Terminology_And_Definitions.md#CommandExchange) [Step](LAA__Terminology_And_Definitions.md#Step) using the selected [Protocol Binding](LAA__Terminology_And_Definitions.md#ProtocolBinding). During this [Step](LAA__Terminology_And_Definitions.md#Step), the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) proceeds the [Command](LAA__Terminology_And_Definitions.md#Command) from *Order* [Messages](LAA__Terminology_And_Definitions.md#Message) one-by-one and, if required, it appends the associated [Response](LAA__Terminology_And_Definitions.md#Response) into *Report* [Messages](LAA__Terminology_And_Definitions.md#Message). As the first [Command](LAA__Terminology_And_Definitions.md#Command) shall be a *Start* and the last one a *Stop*, the internal state machine of the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) is detailed in the next figure:

![Messages State Machine](images/GP_SERAM__Messages_State_Machine.png)

On *Notification* [Command](LAA__Terminology_And_Definitions.md#Command) the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) shall sent a notification to the [Device Application](LAA__Terminology_And_Definitions.md#DeviceApplication). How the [Device](LAA__Terminology_And_Definitions.md#Device) notify the [Device Application](LAA__Terminology_And_Definitions.md#DeviceApplication) and its reliability is implementation dependent. *Notification* [Command](LAA__Terminology_And_Definitions.md#Command) do not require [Response](LAA__Terminology_And_Definitions.md#Response), nor a state change.

On *SE RAM* [Command](LAA__Terminology_And_Definitions.md#Command) the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) shall send each *C-APDU* to the selected [Secure Element](LAA__Terminology_And_Definitions.md#SecureElement) according with the [SE Access API](LAA__Terminology_And_Definitions.md#SEAccessAPI) and add the *R-APDU* to the *SE RAM* [Response](LAA__Terminology_And_Definitions.md#Response). If the *C-APDU* is a *SELECT Command* as defined by [GP Card Specification](https://globalplatform.org/specs-library/card-specification-v2-3-1/), the [SE Access API](LAA__Terminology_And_Definitions.md#SEAccessAPI), may required the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) to use a dedicated function to open a *logicial channel* with the [Secure Element](LAA__Terminology_And_Definitions.md#SecureElement). This *logicial channel* shall be used for the subsequent *C-APDU* and closed if another *SELECT Command* is received or at the end of the *Management Session*. On any error to transmit the *C-APDU*, the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) shall discard all the remaining *C-APDU* and shall not include any *R-APDU* in the response for the faulty transmission. The [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) do not need to parse and handle *R-APDU*. Any warning or error *R-ADPDU* (i.e. those with a 69xx or 68xx status word) are valid *R-APDU* that shall be added to the *SE RAM* [Response](LAA__Terminology_And_Definitions.md#Response).

