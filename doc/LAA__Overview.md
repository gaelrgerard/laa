LAA <-> SAM SM- Protocol Overview
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
In the following sequence diagrams, the process [1] executeGPSERAMScript is defined in [GPSERAM](LAA__References.md#GPSERAM) (Protocol Overview Diagram). 
See also "[End User](LAA__Terminology_And_Definitions.md#EU) interactions for user intent" section for process [0]

### Installation

#### Online installation
![install-samsm-script](uml/install-samsm.svg)
The GET DATA command is defined in [SAM Configuration](LAA__References.md#SAMCONF)  section�8.4

The [LAA](LAA__Terminology_And_Definitions.md#LAA)  SHALL be able to process [GPSERAM](LAA__References.md#GPSERAM) data containing SCP11a or SCP11c APDUs.

In this mode, the Device Application sends a null parameter as localScriptUri, and the initiateInstallation response contains the gpseramUri (for instance [https://sam-sm.server1.com/gp/seram/script1](https://sam-sm.server1.com/gp/seram/script1)).

Optionally at the end of this process, the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) MAY execute a GET STATUS command for a given ASP SD AID.

#### Local script
![install-local-script](uml/install-local.svg)

The [LAA](LAA__Terminology_And_Definitions.md#LAA)  SHALL also be able to process a local script containing SCP11c APDUs. This script is processed through a uri. The localScriptUri can be provided by the Device Application for local execution (for instance [file://data/local/euicc/sam/script1](file://data/local/euicc/sam/script1)).

In this mode, initiateInstallation is not sent to the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) and [LAA](LAA__Terminology_And_Definitions.md#LAA)  performs a local eligibility check and installation. The Device Application relies only on the [LAA](LAA__Terminology_And_Definitions.md#LAA)  checks. [LAA](LAA__Terminology_And_Definitions.md#LAA)  checks are out of scope of this specification. samSMFQDN parameter is only used for the notification.


### Personalization

This section describes how an SAM applet MAY be personalized by [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM). Notice that a SAM applet may be personalized through other means that are out of the scope of this specification.

![install-local-script](uml/perso.svg)

The same sessionId SHALL be used for the installation step and the personalization step.

### Deletion

#### Trigerred by LAA
![install-local-script](uml/delete-laa.svg)

A sessionId is generated by the Device Application itself in this scenario.

#### Trigerred by device application removal
![install-local-script](uml/delete-device-app.svg)

The [LAA](LAA__Terminology_And_Definitions.md#LAA)  SHALL also be able to process a delete script. This script retrieved from a URI. The URI can be a file uri or a [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) uri. Optionally at the end of this process, the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) MAY issue a GET STATUS command to the [SAM SD](LAA__Terminology_And_Definitions.md#SAMSD) (if SCP11a is supported) to check that the ASP SD has been deleted.

The sessionId is generated by the Device Application itself in this scenario.

### Memory reset
![install-local-script](uml/reset.svg)

This process allows an [End User](LAA__Terminology_And_Definitions.md#EU) to request the SAM SD memory reset. A strong confirmation SHOULD be required as defined in [SAMREQ](LAA__References.md#SAMREQ)
Notifications (to SAM SMs and to device applications) are send for each SAM services that are retrieved before the memory reset.

### List SAM services
![install-local-script](uml/servicelist.svg)

This process allows an [End User](LAA__Terminology_And_Definitions.md#EU) to request the list of all SAM Services. No user intent is required for this operation.


### End user interactions for user intent

[End User](LAA__Terminology_And_Definitions.md#EU) intent is acquired as defined in [SAMREQ](LAA__References.md#SAMREQ). This intent is acquired in advance or in real time. This process depends of the device and is implementation specific.

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

To be noticed that the /perso endpoint is out of scope of this specification. It is not necessarly implemented by the  [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM).

Errors
========

An object statusCodeData has been defined for the error management (like [SGP22](LAA__References.md#SGP22))
see [OpenAPI specification](spec/gpseram.yaml) ([Viewer](https://gaelrgerard.github.io/laa/)) for the details

Subject Code value are defined in this table below :
| **Subject Code**      | **Description**        | 
|-------------------|------------------------| 
| 1       | Generic   (as defined in [SGP22](LAA__References.md#SGP22))     | 
| 1.1        | Function Requester (as defined in [SGP22](LAA__References.md#SGP22))      |
| 1.2 | Function Provider (as defined in [SGP22](LAA__References.md#SGP22))|
| 2 | SAM SD |
| 2.1 | SAM SD Issuer certificate |
| 2.2 | SAM SD certificate |
| 3 | SAM SM |
| 3.1 | SAM SM certificate |
| 8 | SAM CA |


Reason Code value are defined in this table below :

| **Reason Code**      | **Description**        | 
|-------------------|------------------------| 
|1| Access Error (as defined in [SGP22](LAA__References.md#SGP22))|
|1.1| Unknown (Identification or Authentication) (as defined in [SGP22](LAA__References.md#SGP22))|
|1.2| Not Allowed (Authorisation) (as defined in [SGP22](LAA__References.md#SGP22))|
|2| Format Error (as defined in [SGP22](LAA__References.md#SGP22))|
|2.1| Invalid (as defined in [SGP22](LAA__References.md#SGP22))|
|2.2| Mandatory Element Missing (as defined in [SGP22](LAA__References.md#SGP22))|
|2.3| Conditional Element Missing (as defined in [SGP22](LAA__References.md#SGP22))|
|3| Conditions of Use Not Satisfied (as defined in [SGP22](LAA__References.md#SGP22))|
|3.1| Unsupported (as defined in [SGP22](LAA__References.md#SGP22))|
|3.3| Already in Use (Uniqueness) (as defined in [SGP22](LAA__References.md#SGP22))|
|3.7| Unavailable (as defined in [SGP22](LAA__References.md#SGP22))|
|3.8| Refused (as defined in [SGP22](LAA__References.md#SGP22))|
|3.9| Unknown (as defined in [SGP22](LAA__References.md#SGP22))|
|3.10| Invalid Association (as defined in [SGP22](LAA__References.md#SGP22))|
|3.11| Value has Changed (as defined in [SGP22](LAA__References.md#SGP22))|
|3.12| Invalid Match (as defined in [SGP22](LAA__References.md#SGP22))|
|4| Processing Error (as defined in [SGP22](LAA__References.md#SGP22))|
|4.2| Execution Error (as defined in [SGP22](LAA__References.md#SGP22))|
|4.3| Stopped on Warning (as defined in [SGP22](LAA__References.md#SGP22))|
|4.8| Insufficient Memory (as defined in [SGP22](LAA__References.md#SGP22))|
|4.10| Time to Live Expired (as defined in [SGP22](LAA__References.md#SGP22))|
|5| Transport Error (as defined in [SGP22](LAA__References.md#SGP22))|
|5.1| Inaccessible (as defined in [SGP22](LAA__References.md#SGP22))|
|6| Security Error (as defined in [SGP22](LAA__References.md#SGP22))|
|6.1| Verification Failed (as defined in [SGP22](LAA__References.md#SGP22))|
|6.3| Expired (as defined in [SGP22](LAA__References.md#SGP22))|
|6.4| Maximum number of attempts exceeded (as defined in [SGP22](LAA__References.md#SGP22))|





