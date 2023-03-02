LAA - Protocol Overview
============================

This documentation defines a protocol that allows a [LAA](LAA__Terminology_And_Definitions.md#LAA) to request the management of a [SAM SD](LAA__Terminology_And_Definitions.md#SAMSD) by a [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM).

The following figure presents the SAM architecture and its environment. All words in blue are defined in this documentation.

![Architecture Overview](images/LAA__SAM_Architecture_Overview.png)

This documentation is focusing on the SAM04 interface. [GPSERAM](LAA__References.md#GPSERAM) is also used on this SAM04 interface.
[SAM Configuration](LAA__References.md#SAMCONF) is focusing more on the [SAM SD](LAA__Terminology_And_Definitions.md#SAMSD) part.
A [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) and a [LAA](LAA__Terminology_And_Definitions.md#LAA) manage this protocol to allow the [LAA](LAA__Terminology_And_Definitions.md#LAA) to trigger a [Device Application](LAA__Terminology_And_Definitions.md#DeviceApplication) and the [Secure Element](LAA__Terminology_And_Definitions.md#SecureElement).


Protocol design
---------------

### Protocol Layers

LAA protocol is a message-oriented protocol which used the following protocol stack:

![Protocol layers](images/LAA__Protocol_layers.png)

[Messages](LAA__Terminology_And_Definitions.md#Message) are the data exchanged between the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) and the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA). The definition, the meaning and sequency of [Messages](LAA__Terminology_And_Definitions.md#Message) are states below in the [Messages section](#messages).

How [Messages](LAA__Terminology_And_Definitions.md#Message) are carried on the network relies on the [Protocol Binding](LAA__Terminology_And_Definitions.md#ProtocolBinding) used by the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) and the [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA). A [Protocol Binding](LAA__Terminology_And_Definitions.md#ProtocolBinding) defines the rules to map [Messages](LAA__Terminology_And_Definitions.md#Message) on the [Data Format](LAA__Terminology_And_Definitions.md#DataFormat) layer and the [Transport](LAA__Terminology_And_Definitions.md#Transport) layer.

This version of the specification defines the following [Data Format](LAA__Terminology_And_Definitions.md#DataFormat) and [Transport](LAA__Terminology_And_Definitions.md#Transport) protocol layers:

-   **HTTPS** as [Transport](LAA__Terminology_And_Definitions.md#Transport)

-   **JSON** as [Data Format](LAA__Terminology_And_Definitions.md#DataFormat)

This version of the specification defined the following [Protocol Binding](LAA__Terminology_And_Definitions.md#ProtocolBinding):

-   **HTTP REST**, which uses HTTPS as [Transport](LAA__Terminology_And_Definitions.md#Transport) protocol and JSON as [Data Format](LAA__Terminology_And_Definitions.md#DataFormat).


### Management Session

A [LAA](LAA__Terminology_And_Definitions.md#LAA) and a [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) relies on a session identifier, named [sessionId](LAA__Terminology_And_Definitions.md#sessionId). The [sessionId](LAA__Terminology_And_Definitions.md#sessionId) is shared and used for all communications between the [LAA](LAA__Terminology_And_Definitions.md#LAA) and the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM).

The session during which is performed some management tasks that are associated with one sessionId is called the [Management Session](LAA__Terminology_And_Definitions.md#ManagementSession).

The [Management Session](LAA__Terminology_And_Definitions.md#ManagementSession) is started by the [LAA](LAA__Terminology_And_Definitions.md#DeviceApplication) and is then controlled until its end by the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM).
Same [sessionId](LAA__Terminology_And_Definitions.md#sessionId) SHALL be used for the [GPSERAM](LAA__References.md#GPSERAM)  session.


Protocol details
----------------------
In the following sequence diagrams, the process executeGPSERAMScript is defined in [GPSERAM](LAA__References.md#GPSERAM) 

### Installation

#### Online installation
![install-samsm-script](doc/uml/install-samsm.svg)
The GET DATA command is defined in [SAM Configuration](LAA__References.md#SAMCONF)  section 8.4.

The [LAA](LAA__Terminology_And_Definitions.md#LAA)  SHALL be able to process [GPSERAM](LAA__References.md#GPSERAM) data containing SCP11a or SCP11c APDUs.

In this mode, the Device Application sends a null parameter as localScriptUri, and the initiateInstallation response contains the gpseramUri (for instance [https://sam-sm.server1.com/gp/seram/script1](https://sam-sm.server1.com/gp/seram/script1)).

Optionally at the end of this process, the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) MAY execute a GET STATUS command for a given ASP SD AID.

#### Local script
![install-local-script](doc/uml/install-local.svg)
The [LAA](LAA__Terminology_And_Definitions.md#LAA)  SHALL also be able to process a local script containing SCP11c APDUs. This script is processed through a uri. The localScriptUri can be provided by the Device Application for local execution (for instance [file://data/local/euicc/sam/script1](file://data/local/euicc/sam/script1)).

In this mode, initiateInstallation is not sent to the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) and [LAA](LAA__Terminology_And_Definitions.md#LAA)  performs a local eligibility check and installation. The Device Application relies only on the [LAA](LAA__Terminology_And_Definitions.md#LAA)  checks. [LAA](LAA__Terminology_And_Definitions.md#LAA)  checks are out of scope of this specification. samSMFQDN parameter is only used for the notification.


### Personalization

This section describes how an SAM applet MAY be personalized by [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM). Notice that a SAM applet may be personalized through other means that are out of the scope of this specification.

![install-local-script](doc/uml/perso.svg)
The same sessionId SHALL be used for the installation step and the personalization step.

### Deletion

#### Trigerred by LAA
![install-local-script](doc/uml/delete-laa.svg)
A sessionId is generated by the Device Application itself in this scenario.

#### Trigerred by device application removal
![install-local-script](doc/uml/delete-device-app.svg)
The [LAA](LAA__Terminology_And_Definitions.md#LAA)  SHALL also be able to process a delete script. This script retrieved from a URI. The URI can be a file uri or a [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) uri. Optionally at the end of this process, the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) MAY issue a GET STATUS command to the [SAM SD](LAA__Terminology_And_Definitions.md#SAMSD) (if SCP11a is supported) to check that the ASP SD has been deleted.

The sessionId is generated by the Device Application itself in this scenario.

Messages
========

The following type of [Messages](LAA__Terminology_And_Definitions.md#Message) are exchanged between [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) and [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM):

| Protocol Step    | Messages               | From         | To           |
|------------------|------------------------|--------------|--------------|
| /install        | **samInstallMsg**  | Local Applet Assistant  | SAM SM |
| /install        | **samManagementRespMsg** | SAM SM | Local Applet Assistant  |
| /delete        | **samDeleteMsg**  | Local Applet Assistant  | SAM SM |
| /delete        | **samManagementRespMsg** | SAM SM | Local Applet Assistant  |
| /notification | **notificationMsg**              | SAM SM | Local Applet Assistant  |


