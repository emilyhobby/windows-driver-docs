---
title: Microsoft Bluetooth Test Platform Traduci board support
description: Bluetooth Test Platform (BTP) Traduci board support.
ms.date: 05/05/2022
---

# Traduci board support

## Overview

The Traduci makes use of specialized hardware to make Bluetooth testing easier. The Traduci board enables software on a host device (like a PC) to communicate with external devices over a sideband.

For example, an LE pairing test requires a peripheral device to be powered on, have certain IO capabilities, and be advertising as connectable/discoverable before it can be paired to. The peripheral device has well defined commands that can make this happen, so the BTP software on the host sends these commands over USB to the Traduci which in turn routes it to the appropriate device. After successful completion of the commands, the BTP software would then proceed with the test by requesting that the host pair to the peripheral device which is now ready to accept the pairing.
In the above scenario the Traduci makes several things simpler: It is able to provide and cut-off power with the correct voltage to the devices, it can route different commands to different devices, and it will mediate this communication through the correct protocols and baud rate.

It is important to note that BTP tests do not have a tight dependency on the Traduci. If other external hardware is needed for a test, the BTP is designed to allow easy extensibility to support that scenario.

The Traduci board is produced by [MCCI](https://mcci.com/usb/dev-tools/model-2411/)

:::image type="content" source="images/Traduci_Overhead.jpg" alt-text="Photo of a Traduci board.":::

- 4 12-pin ports to support 4 devices simultaneously
- Able to route data to and from multiple devices simultaneously
- 3 FPGAs connected to ports JA, JB, and JC respectively
- Supports audio testing via the integrated audio codec
- Unlabeled pins can easily be statically assigned to HIGH or LOW depending on the needs of the device plugged into the port
- The Traduci does not currently support hardware handshaking using CTS and RTS

These diagrams show how the Traduci-based BTP tests are executed

:::image type="content" source="images/btp-hwOverview.png" alt-text="Diagram of the hardware test.":::

:::image type="content" source="images/btp-swOverview.png" alt-text="Diagram of the software test.":::
