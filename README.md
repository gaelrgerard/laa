Local Applet Assistant (LAA) <-> SAM SM 
========

Introduction
------------
[LAA](doc/LAA__Terminology_And_Definitions.md#LAA) has been defined in [SAM requirements](doc/LAA__References.md#SAMREQ).
[LAA](doc/LAA__Terminology_And_Definitions.md#LAA) is a module in the device that provides the capability to manage SAM applications (called also SAM applets).

Through the [LAA](doc/LAA__Terminology_And_Definitions.md#LAA), the End User is able to perform functions including, but not limited to, the following:
* View the SAM Services information.
* Manage (delete, upgrade, etc.) SAM applications on the [SAM SD](doc/LAA__Terminology_And_Definitions.md#SAMSD).
* Select End User’s authentication and authorization methods (e.g. biometry, etc.).

The [LAA](doc/LAA__Terminology_And_Definitions.md#LAA) is responsible for installing SAM applications on the [SAM SD](doc/LAA__Terminology_And_Definitions.md#SAMSD). 

To understand the protocol, please, refer to:

* [LAA Protocol Overview](doc/LAA__Overview.md)

The documentation also includes [Terminology and Definitions](doc/LAA__Terminology_And_Definitions.md) and
[References](doc/LAA__References.md).

Protocol binding
----------------

For **LAA - HTTP REST Binding** please refer to:

* [HTTP REST Binding - OpenAPI specification](spec/gpseram.yaml) ([Viewer](https://gaelrgerard.github.io/laa/))
* [HTTP REST Binding - explanation](doc/LAA__HTTP_REST_Binding.md)

Tools
----------------

There are different ways to generate the object from [HTTP REST Binding - OpenAPI specification](spec/laa.yaml).
This project is compliant with [maven](https://maven.apache.org/). The file [pom](pom.xml) has been designed to generate java objects. 
It can be modified to generate other language objects as described in [OpenAPI plugin documentation](https://openapi-generator.tech/docs/plugins/)
Simply launch the java object generation. The objects will be generated in target/generated directory.     
```batch
mvn clean install
```

Another way is to use the [OpenAPI CLI tool](https://openapi-generator.tech/docs/installation)