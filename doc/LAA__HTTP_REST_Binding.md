LAA - HTTP REST Binding
============================

This file details the *HTTP REST Binding* which uses HTTPS as [Transport](LAA__Terminology_And_Definitions.md#Transport) protocol layer and JSON as [Data Format](LAA__Terminology_And_Definitions.md#DataFormat) protocol layer.

The [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) acts as a HTTP client and the [SAM SM](LAA__Terminology_And_Definitions.md#SAMSM) as a HTTP server. Each GP SERAM [Message](LAA__Terminology_And_Definitions.md#Message) may be transmitted in exactly one HTTP message.

The formal API specification of the *HTTP REST Binding* is provided in [OpenAPI format](/spec/laa.yaml). This specification file may be used to generate code skeleton as shown in maven project file (pom.xml).

The *HTTP REST Binding* SHALL comply with:
- [RFC2818 – HTTP Over TLS](https://www.rfc-editor.org/rfc/rfc2818)
- [RFC6265 – HTTP State Management Mechanism](https://www.rfc-editor.org/rfc/rfc6265)
- [RFC7230 – Hypertext Transfer Protocol (HTTP/1.1): Message Syntax and Routing](https://www.rfc-editor.org/rfc/rfc7230)
- [RFC7231 – Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content](https://www.rfc-editor.org/rfc/rfc7231)
- [RFC7232 – Hypertext Transfer Protocol (HTTP/1.1): Conditional Requests](https://www.rfc-editor.org/rfc/rfc7232)
- [RFC7234 – Hypertext Transfer Protocol (HTTP/1.1): Caching](https://www.rfc-editor.org/rfc/rfc7234)


Management Session and HTTP messages
------------------------------------

HTTP messages are linked with a [Management Session](LAA__Terminology_And_Definitions.md#ManagementSession) based on the [sessionId](LAA__Terminology_And_Definitions.md#sessionId). The [sessionId](LAA__Terminology_And_Definitions.md#sessionId) is explicitly inserted in each HTTP request and implicitly determined for HTTP response based on the client-server paradigm of the HTTP protocol.

Implementors MAY uses another HTTP mechanism to reinforce the HTTP session (e.g. HTTP cookies). A [Local Applet Assistant](LAA__Terminology_And_Definitions.md#LAA) SHOULD support HTTP cookies as defined in [RFC6265](https://www.rfc-editor.org/rfc/rfc6265).

HTTP REST Endpoints
-------------------

3 endpoints are defined: 

| **Endpoint**      | **Description**        |
|-------------------|------------------------|
| /install        | Trigger a SAM Service installation         |
| /delete        | Trigger a SAM Service deletion         |
| /notification | Notify a SAM Service management event |




