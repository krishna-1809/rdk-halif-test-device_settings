# CompositeIn Test Document

## Version History

| Date(DD/MM/YY) | Comment       | Version |
| -------------- | ------------- | ------- |
| 12/03/2024     | First Release | 1.0.0   |

## Table of Contents

- [Acronyms, Terms and Abbreviations](#acronyms-terms-and-abbreviations)
- [References](#references)
- [Introduction](#introduction)
- [Module Description](#module-description)
- [Testing Scope](#testing-scope)

## Acronyms, Terms and Abbreviations

- `HAL`   - Hardware Abstraction layer
- `SOC`   - System On a Chip
- `EDID`  - Extended Display Identification
- `API`   - Application programming interface
- `CPU`   - Central processing unit
- `RDK`   - Reference Design Kit
- `dsComposite` - Device Settings Composite

## References

## Introduction

This document provides an overview of the testing requirements for the `dsComposite` module. It outlines the scope of testing, objectives, testing levels and approaches, specific test requirements, emulator requirements, control plane requirements and expected deliverables.

Interface of the test is available in this link -  [https://github.com/rdkcentral/rdk-halif-device_settings/blob/main/include/dsCompositeIn.h](https://github.com/rdkcentral/rdk-halif-device_settings/blob/main/include/dsCompositeIn.h)

## Module Description

High level overview:

- `dsComposite` provides a variety of APIs for accessing information regarding the Composite Inputs.
- It facilitates interaction with Composite Input ports, aiding in their configuration and utilization within the system. This information is then relayed to the caller.
- For the source devices, to retrieve the available Composite Input information, an external device must be connected.

## Testing Scope

|#|Test Functionality|Test Description|
|-|------------------|----------------|
|1|Get Number of Inputs|The test aims to verify the availability of Composite Input ports by confirming the number present.|
|2|Get the Input Status|The test is to verify the status of all Composite Input Status|
|3|Set the Composite port|The test is to set the Composite Input port for Presentation|
|4|Scale the Composite Input Video|The test scales the COMPOSITE input video, ensuring that the width and height, determined by the x and y coordinates respectively, do not surpass the current resolution limits of the device.|
|5|Callback for connection Status|The test aims to verify the Callback function used for notifying applications of the COMPOSITE In hot plug status.|
|6|Callback for Signal Change|The test aims to verify the callback function used to inform applications about changes in the signal status of the Composite In.(NoSignal/UnstableSignal/NotSupportedSignal/StableSignal)|
|7|Callback for Status Change|The test validates the functionality of the callback function designed to notify applications of Composite Input status change events.(Port,IsPresented flag status)|
|8|Register Callback for connection event|The test aims to verify whether the registration of the COMPOSITE Input hot plug event is successful.|
|9|Register Callback for Signal Change event|The test aims to verify whether the registration of the Signal change event is successful.|
|10|Register Callback for Status Change event|The test aims to verify whether the registration of the Status change event is successful.|
-----------

## Get Number of Inputs

|Description|L2|L3|Control Plane Requirements|
|-----------|--|--|--------------------------|
|Verify that the function returns the correct number of COMPOSITE Input ports when there are no COMPOSITE Input ports available.|Y|N|The Control Plane boots with the number of input ports data|
|Validate that the function returns the correct number of COMPOSITE Input ports when there is only one COMPOSITE Input port available.|N|Y|The Control Plane boots with the number of input ports data|
|Ensure that the function correctly handles the maximum number of COMPOSITE Input ports.|N|Y|The Control Plane boots with the number of input ports data|


### Test Startup Requirement - Get Number of Inputs

The test begins with the configured composite input port details.

### Emulator Requirement - Get Number of Inputs

Emulator will boot with the port informations coming from the configuration file.

### Control Plane Requirement - Get Number of Inputs

The Control Plane boots with the number of input ports provided based on their availability.

## Get the Input Status

|Description|L2|L3|Control Plane Requirements|
|-----------|--|--|--------------------------|
|The scenarios where all Composite Input ports are disabled and reports the status accordingly.|Y|N|The Control Plane boots with the number of input ports data|
|Validate the status of each Composite Input port when some ports are disabled.|N|Y|The Control Plane boots with the number of input ports data |
|Validate the Composite Input port when all ports are in an enabled state.|N|Y|The Control Plane boots with the number of input ports data|

### Test Startup Requirement - Get the Input Status

The test begins with the configured composite input port numbers.

### Emulator Requirement - Get the Input Status

Emulator will boot with the port informations coming from the configuration file.

### Control Plane Requirement - Get the Input Status

The Control Plane boots with the number of input ports provided based on their availability/status.

## Set the Composite port

|Description|L2|L3|Control Plane Requirements|
|-----------|--|--|--------------------------|
|Verify that the function successfully sets the specified COMPOSITE Input port as active for presentation.|N|Y|The Control Plane boots with the number of input ports|
|Test the function's response when attempting to select a port that is not supported due to restrictions on source devices.|Y|N|The Control Plane boots with the number of input ports|
|Validate the function's behavior when called with a port ID that is connected but not active, ensuring it sets the port and updates the status accordingly.|N|Y|The Control Plane boots with the number of input ports|
|Assess the function's response when called with a port ID that is already selected as active, ensuring it does not introduce any unintended changes.|N|Y|The Control Plane boots with the number of input ports|

### Test Startup Requirement - Set the Composite port

The test begins with the configured composite input port numbers.

### Emulator Requirement - Set the Composite port

Emulator will boot with the port informations coming from the configuration file.

### Control Plane Requirement - Set the Composite port

The Control Plane boots with the number of input ports provided based on their availability.

## Scale the Composite Input Video

|Description|L2|L3|Control Plane Requirements|
|-----------|--|--|--------------------------|
|Verify that the function successfully scales the COMPOSITE input video when valid coordinates and dimensions are provided within the current resolution limits.|N|Y|N|

### Test Startup Requirement - Scale the Composite Input Video

The test begins with the configured composite input port numbers.

### Emulator Requirement - Scale the Composite Input Video

Emulator will boot with the port informations coming from the configuration file.

### Control Plane Requirement - Scale the Composite Input Video

The Control Plane boots with the number of input ports provided based on their availability.

## Callback for connection Status

|Description|L2|L3|Control Plane Requirements|
|-----------|--|--|--------------------------|
|Verify that the callback function properly notifies the application when a COMPOSITE Input port is connected or disconnected.|N|Y|Control Plane holds the true/false data to provide on Connection/Disconnection|
|Validate that the callback function updates the isPortConnected status correctly based on the connection state provided.|N|Y|Control Plane holds the true/false data to provide on Connection/Disconnection|
|Verify that the callback function properly updates the isPresented status in ::dsCompositeInStatus_t if the connected port is active and presents video after being connected.|N|Y|Control Plane holds the true/false data to provide on Connection/Disconnection|

### Test Startup Requirement - Callback for connection Status

The test begins with the configured composite input port numbers.

### Emulator Requirement - Callback for connection Status

Emulator will boot with the port information coming from the configuration file.

### Control Plane Requirement - Callback for connection Status

The Control Plane boots with the number of input ports provided based on their availability. Control Plane holds the true/false data to provide on Connection/Disconnection.

## Callback for Signal Change

|Description|L2|L3|Control Plane Requirements|
|-----------|--|--|--------------------------|
|Verify that the callback function properly handles different signal statuses (e.g., NoSignal, UnstableSignal, NotSupportedSignal, StableSignal) and updates the application accordingly.|N|Y|N|
|Validate that the callback function updates the sigStatus parameter correctly based on the signal status provided.|N|Y|N|

### Test Startup Requirement - Callback for Signal Change

The test begins with the configured composite input port numbers.

### Emulator Requirement - Callback for Signal Change

Emulator will boot with the port informations coming from the configuration file.

### Control Plane Requirement - Callback for Signal Change

None

## Callback for Status Change

|Description|L2|L3|Control Plane Requirements|
|-----------|--|--|--------------------------|
|Verify that the callback function properly notifies the application of the Composite Input status change event.|N|Y|N|
|Validate that the callback function updates the inputStatus parameter correctly based on the status change provided.|N|Y|N|
|Verify that the callback function properly triggers whenever the dsCompositeInStatus_t is updated|N|Y|N|

### Test Startup Requirement - Callback for Status Change

The test begins with the configured composite input port numbers.

### Emulator Requirement - Callback for Status Change

Emulator will boot with the port informations coming from the configuration file.

### Control Plane Requirement - Callback for Status Change

None

## Register Callback for connection event

|Description|L2|L3|Control Plane Requirements|
|-----------|--|--|--------------------------|
|Verify that the callback function for the COMPOSITE Input hot plug event is registered successfully|Y|Y|N|

### Test Startup Requirement - Register Callback for connection event

None

### Emulator Requirement - Register Callback for connection event

None

### Control Plane Requirement - Register Callback for connection event

None

## Register Callback for Signal Change event

|Description|L2|L3|Control Plane Requirements|
|-----------|--|--|--------------------------|
|Verify that the callback function for Composite Input Signal Change event is registered successfully|Y|Y|N|

### Test Startup Requirement - Register Callback for Signal Change event

None

### Emulator Requirement - Register Callback for Signal Change event

None

### Control Plane Requirement - Register Callback for Signal Change event

None

## Register Callback for Status Change event

|Description|L2|L3|Control Plane Requirements|
|-----------|--|--|--------------------------|
|Verify that the callback function for Composite Input Status Change event is registered successfully|Y|Y|N|

### Test Startup Requirement - Register Callback for Status Change event

None

### Emulator Requirement - Register Callback for Status Change event

None

### Control Plane Requirement - Register Callback for Status Change event

None

