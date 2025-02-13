---
title: Microsoft Bluetooth Test Platform - Audio tests
description: Bluetooth Test Platform (BTP) audio tests.
ms.date: 04/11/2023
---

# BTP audio tests

The BTP audio tests verify the ability of the local system to pair with a remote device over BR/EDR and validate audio functionality including volume validation and audio glitch detection.

## Setting Up

Before using a Pmod device with the Traduci, check that the green power indicator, an optional yellow test LED, and 3 orange LEDs on the Traduci are on. Confirm that the SUT's Bluetooth radio is powered on and that the appropriate device(s) are correctly plugged in to the Traduci. Currently the RN52 device can **only** be plugged into JA. More detailed information on setting up can be found at [BTP overview](testing-btp-overview.md).

Two red LEDs on the BM-64-EVB should be on. One of the LEDs may eventually turn off. Confirm the switches, jumpers, and ports are configured for testing as described in the [BM-64-EVB board overview](testing-BTP-hw-bm64.md#getting-started).

Features and purchasing information for supported devices can be found at [Supported BTP Hardware](testing-BTP-hw.md).

## Supported devices

- [BM 64-EVB](testing-BTP-hw-bm64.md)
- [RN52](testing-BTP-hw-rn52.md) 

## Running the Audio Tests

Navigate to the folder where the BTP package was extracted. It's typically located under `C:\BTP`. In a folder named after the version of the package, you'll find the following scripts. Run either:

- `RunAudioTests.bat <device name>` from an elevated command prompt or
- `RunAudioTests.ps1 <device name>` from an elevated PowerShell console

Information on available device name parameters can be found at [Bluetooth Test Platform supported hardware](testing-BTP-hw.md)

You can also include the optional parameter `-VerboseLogs` at the end to get a more verbose output of inner operations of BTP.

As a test starts on the Traduci, the red LED next to the 12-pin adapter turns on once the command from the test to power the Pmod device has been sent. This LED is turned off at the end of every test. If it is on at the start of the next test due to the previous test failing, power it down and power it back on to return it to a known state. If the power cycle fails, the test fails due to the Pmod device being in an unknown state.

Red and blue LEDs on the BM-64-EVB flash in patterns, indicting steps of the process such as powering on, pairing, and playing audio.

## Capturing Logs

To capture the Bluetooth logs, follow the instructions for the [busiotools for Windows Repo on GitHub](https://github.com/microsoft/busiotools/blob/master/bluetooth/tracing/readme.md).

To parse the Bluetooth logs, follow the instructions for the [BTETLParse tool](testing-BTP-tools-btetlparse.md).

## Known issues

- BM64 EVB has the following eight known test failures:

  - `BluetoothTests::TaefAudioTests::MusicMediaReceiverMeasuredVolumeUpTest`
  - `BluetoothTests::TaefAudioTests::MusicMediaReceiverMeasuredVolumeDownTest`
  - `BluetoothTests::TaefAudioTests::MusicMediaSenderMeasuredVolumeUpTest`
  - `BluetoothTests::TaefAudioTests::MusicMediaSenderMeasuredVolumeDownTest`
  - `BluetoothTests::TaefAudioTests::VoiceMediaReceiverMeasuredVolumeUpTest`
  - `BluetoothTests::TaefAudioTests::VoiceMediaReceiverMeasuredVolumeDownTest`
  - `BluetoothTests::TaefAudioTests::VoiceMediaSenderMeasuredVolumeUpTest`
  - `BluetoothTests::TaefAudioTests::VoiceMediaSenderMeasuredVolumeDownTest`

- BTP may incorrectly identify support for the [Unified Audio Endpoint feature](https://blogs.windows.com/windows-insider/2021/04/29/announcing-windows-10-insider-preview-build-21370/) on some Windows builds, resulting in a test failure when identifying audio endpoints.

  ```console
    Error: [BluetoothTestHelpers::AudioDevice::WaitForAudioSourcesState]: Assertion failed: AudioSourceDeviceVoiceSourceModule->WaitForAudioSourceState( areReady, areReady ? c_audioSinkInterfaceBringupTimeout : c_audioSinkInterfaceRemovalTimeout)
    ```

  Upgrading to build 22000 or later should resolve the issue.

- The following mute tests fail on Windows builds 21275 and later:

  - `BluetoothTests::TaefAudioTests::VoiceInterruptMusicMeasuredMuteTest`
  - `BluetoothTests::TaefAudioTests::MeasuredMuteAndUnmuteFromMusicMediaSenderTest`
  - `BluetoothTests::TaefAudioTests::MeasuredMuteAndUnmuteFromVoiceMediaSenderTest`
