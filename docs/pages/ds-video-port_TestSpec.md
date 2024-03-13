# Device Settings Video Port Test Specification Documentation

## Table of Contents

- [Acronyms, Terms and Abbreviations](#acronyms-terms-and-abbreviations)
- [Introduction](#introduction)
- [Module Description](#module-description)
- [Testing Scope](#testing-scope)
  - [Check the Video port status](#check-the-video-port-status)
  - [Emulator Requirements](#emulator-requirements)
  - [Check Video Format and HDR Capability](#check-video-format-and-hdr-capability)
  - [Check Video Resolution and HDMI Status](#check-video-resolution-and-hdmi-status)
  - [HDCP and DTCP Management](#hdcp-and-dtcp-management)
  - [Color Capabilities](#color-capabilities)

## Acronyms, Terms and Abbreviations

- `HAL`    - Hardware Abstraction Layer
- `API`    - Caller Programming Interface
- `DS`     - Device Settings
- `HDMI`   - High-Definition Multimedia Interface
- `DTCP`   - Digital Transmission Content Protection
- `HDCP`   - High-bandwidth Digital Content Protection
- `HDR`    - High Dynamic Range
- `SDR`    - Standard Dynamic Range
- `EDID` - Extended Display Identification Data
- `EOTF` - Electro-Optical Transfer Function

## Introduction

This document provides an overview of the testing requirements for the Device Settings Video Port module. It outlines the scope of testing, objectives, testing levels and approaches, specific test requirements, and expected deliverables.

Interface of the test is available here: [dsVideoPort HAL header](https://github.com/rdkcentral/rdk-halif-device_settings/blob/main/include/dsVideoPort.h)

## Module Description

`DS` Video Port `HAL` provides a set of `APIs` to initialize, query and set information about the Video ports like getting  video port handle, fetching connected display information such as color depth, color space, matrix coefficients, quantization range, supported video resolutions using the video port handle. It also provides `APIs` to enable or disable content protection like `HDCP` and `DTCP`, to set the background color and preferred color depth of the video port.

## Testing Scope

|#|Test Functionality|Description|
|-|------------------|-----------|
|1|[Check the Video port status](#check-the-video-port-status)|Check the Video Port Access and Status |
|2|[Check Video Format and HDR Capability](#check-video-format-and-hdr-capability)|Check Video Format and `HDR` Capability|
|3|[Check Video Resolution and HDMI Status](#check-video-resolution-and-hdmi-status)|Check Video resolution and `HDMI` status|
|4|[HDCP and DTCP Management](#hdcp-and-dtcp-management)|Check `HDCP` and `DTCP` Status|
|5|[Color Capabilities](#color-capabilities)|Check the color capabilities|

### Emulator Requirements

Boot configuration: Check video ports, formats, frame rates, and device-supported resolutions, along with the number of ports supported by each device.

Supported Video Port [dsVideoPortType_t link](https://github.com/rdkcentral/rdk-halif-device_settings/blob/main/include/dsAVDTypes.h#L132)

Supported Video resolutions [dsTVResolution_t link](https://github.com/rdkcentral/rdk-halif-device_settings/blob/main/include/dsAVDTypes.h#L489)

Supported Frame rates [dsVideoFrameRate_t link](https://github.com/rdkcentral/rdk-halif-device_settings/blob/main/include/dsAVDTypes.h#L508)

Supported Video formats [dsHDRStandard_t link](https://github.com/rdkcentral/rdk-halif-device_settings/blob/main/include/dsAVDTypes.h#L625)

### Check the video port status

|Test Functionality|Description|L2|L3|
|------------------|-----------|--|--|
|Check the video port status|Get the video port handle,check the Video Port enable|Y|`NA`|
||Check the display connected/disconnected for valid port|Y|`NA`|
||Check the surround mode status and Capability|Y|`NA`|
||Check the Video port status(i.e. active or not) |Y|`NA`|

#### Test Startup Requirement-Check the video port status

`NA`

#### Emulator Requirements-Check the video port status

`NA`

#### Control Plane Requirements-Check the video port status

`NA`

### Check Video Format and HDR Capability

|Test Functionality|Description|L2|L3|
|------------------|-----------|--|--|
|Check Video Format and HDR Capability|Notify an event when the list of video Format changes|`NA`|Y|
||Get the HDR capabilities and status|Y|`NA`|
||Set/Get Force Disable 4KSupport|Y|`NA`|
||Reset the video output to SDR|`NA`|Y|

#### Test Startup Requirement-Check Video Format and HDR Capability

`NA`

#### Emulator Requirements-Check Video Format and HDR Capability

[Emulator Requirements](#emulator-requirements)

#### Control Plane Requirements-Check Video Format and HDR Capability

Trigger an event for list of video format change.

### Check Video Resolution and HDMI Status

|Test Functionality|Description|L2|L3|
|------------------|-----------|--|--|
|Check Resolution and HDMI Status|set/get pixel resolution|`NA`|Y|
||set/get AspectRatio|`NA`|Y|
||set/get video Stereo Scopic modes|`NA`|Y|
||set/get video Frame rates|`NA`|Y|
||set/get interlaced/progressive|`NA`|Y|
||Check EDID status|`NA`|Y|
||set/get HDMI Protocol version|Y|`NA`|

#### Test Startup Requirement-Check Video Resolution and HDMI Status

`NA`

#### Emulator Requirements-Check Video Resolution and HDMI Status

[Emulator Requirements](#emulator-requirements)

#### Control Plane Requirements-Check Video Resolution and HDMI Status

Set list of supported HDMI Protocol version.

### HDCP and DTCP Management

|Test Functionality|Description|L2|L3|
|------------------|-----------|--|--|
|Check HDCP and DTCP Management|Check enable/disable the DTCP/HDCP for the specified video port|Y|`NA`|
||Check DTCP/HDCP status for valid port|Y|`NA`|
||Check HDCP protocol status|Y|`NA`|
||Notify event if the HDCP status change|`NA`|Y|

#### Test Startup Requirement-HDCP and DTCP Management

`NA`

#### Emulator Requirements-HDCP and DTCP Management

[Emulator Requirements](#emulator-requirements)

#### Control Plane Requirements-HDCP and DTCP Management

Trigger an event HDCP status change.

### Color Capabilities

|Test Functionality|Description|L2|L3|
|------------------|-----------|--|--|
|Check Color Capabilities|Set/Get Color Space|Y|`NA`|
||Set/Get Color Depth Capabilities |Y|`NA`|
||Check QuantizationRange status|Y|`NA`|
||Check MatrixCoefficients status|Y|`NA`|
||Check Video`EOTF` status|Y|`NA`|
||Set Background Color|Y|`NA`|
||Get Current OutputSettings|Y|`NA`|

#### Test Startup Requirement-Color Capabilities

`NA`

#### Emulator Requirements-Color Capabilities

`NA`

#### Control Plane Requirements-Color Capabilities

`NA`
