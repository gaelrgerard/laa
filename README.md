Local Applet Assistant (LAA)
========

Introduction
------------
LAA has been defined in [SAM Requirements](https://www.gsma.com/newsroom/wp-content/uploads//SAM.01-v1.0.pdf)
LAA is a module in the device that provides the capability to manage SAM applications (called also SAM applets).

Through the LAA, the End User is able to perform functions including, but not limited to, the following:
•	View the SAM Services information.
•	Manage (delete, upgrade, etc.) SAM applications on the SAM SD.
•	Select End User’s authentication and authorization methods (e.g. biometry, etc.).

The LAA is responsible for installing SAM applications on the SAM SD. 

To understand the protocol, please, refer to:

* [LAA Protocol Overview](doc/LAA__Overview.md)

The documentation also includes [Terminology and Definitions](doc/LAA__Terminology_And_Definitions.md) and
[References](doc/LAA__References.md).

Protocol binding
----------------

For **LAA - HTTP REST Binding** please refer to:

* [HTTP REST Binding - OpenAPI specification](spec/gpseram.yaml) ([Viewer](https://slegouix.github.io/SERAM/))
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