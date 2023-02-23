## IN100 Host Controller API

The Host Controller API is used to control the IN100 in the context of using it with a microcontroller. The IN100 communicates with a host controller through the on chip UART. For the QFN18 packaging, this is GPIO 0 and GPIO 1. In the DFN8 packaging, this is MGPIO 4 and MGPIO 5. 

### File Description

#### IN100_Host Controller_Sample_c_Code.zip

This zip file contains a sample code written in C that shows how to setup the IN100 to advertise, change the parameters of the advertisement, and edit what is included on the payload. It is recommended to test this code using the IN100 Development Kit.

#### NanoBeacon Host Controller API Guide.pdf

This pdf file describes the UART communication protocol between the IN100 and its host controller. It also goes into details of the GPIO registers, gives an API description, and covers the software flow.

It is recommended to use this guide in conjunction with the IN100_Host Controller_Sample_C_Code.zip in order to understand and learn how to use this API in your applications.
