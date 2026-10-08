---
title: "BLE packet sizes: link layer and ATT MTU"
description: "Why a 2000-byte notification works when people say BLE packets are 27 to 251 bytes."
date: 2026-10-08
tags: ["BLE", "Zephyr", "nRF52840", "L2CAP", "GATT"]
showToc: true
TocOpen: true
---

BLE has more than one packet size limit. Each limit applies to a different layer of the stack, so people often mix them up.

```mermaid
flowchart TD
    A["<b>GATT</b><br/>App sends a notification<br/>Value: max 512 B"] --> B["<b>ATT</b><br/>Adds 3 B header<br/>Packet: max ATT MTU"]
    B --> E["<b>L2CAP</b><br/>Adds 4 B header"]
    E --> C{"Packet<br/>above 251 B?"}
    C -- No --> D["<b>Link layer</b><br/>Sends 1 packet"]
    C -- Yes --> F["<b>Link layer</b><br/>Sends n fragments<br/>Each: max 251 B"]
    D --> G["<b>Radio</b><br/>ACK per packet<br/>Resends failed ones"]
    F --> G
    G --> H["<b>Receiver L2CAP</b><br/>Joins fragments<br/>Gives full packet to ATT"]
```

## The three limits at a glance

| Layer | Limit | Set by |
|---|---|---|
| Link layer payload | 27 B, or 251 B with DLE | Bluetooth Core Spec, same for every device |
| ATT packet | ATT MTU, 23 B default | MTU exchange at connection time |
| Attribute value | 512 B | Core Spec Vol 3, Part F, 3.2.9 |

## Other names for the same things

Datasheets, SDKs and forum posts use different words for these limits. Use this table to map a term to its layer.

| Layer | Other names you will see |
|---|---|
| Link layer payload | LL PDU payload, LL data length, maxTxOctets / maxRxOctets, Data Length Extension (DLE), "BLE packet size" |
| ATT packet | ATT_MTU, GATT MTU, "MTU", MaxPduSize (Windows), maximumWriteValueLength + 3 (Apple) |
| L2CAP | L2CAP SDU, segmentation and reassembly, fragmentation, ACL buffer size |
| Attribute value | Characteristic value length, GATT_MAX_ATTR_LEN, max attribute length |

When someone says "MTU" without a layer, they almost always mean the ATT MTU.

## Link layer

The link layer sends small packets. Each link-layer packet carries at most **27 bytes** of payload. With Data Length Extension (DLE), the limit increases to **251 bytes**.

This is the limit that people usually mean by "BLE packets are 27 to 251 bytes." It is the same for every device. No phone, laptop or chip sends a link-layer packet with more than 251 bytes of payload.

## ATT layer and MTU

The ATT layer sends larger packets. GATT notifications and writes travel as ATT packets. The **ATT MTU** sets the largest ATT packet that the two devices accept, and they agree on it at connection time. Each side states its maximum, and the connection uses the smaller value. The MTU is independent of the 251-byte link-layer limit.

## L2CAP connects the two layers

If an ATT packet is larger than 251 bytes, L2CAP splits it into several link-layer packets. The receiver joins the fragments into the full ATT packet again.

L2CAP uses two terms for its data:

- **SDU (Service Data Unit):** the block that an upper layer gives to L2CAP. For GATT, one full ATT packet is one SDU.
- **PDU (Protocol Data Unit):** the SDU plus the 4-byte L2CAP header (2-byte length, 2-byte channel ID). ATT uses fixed channel 0x0004.

```
 ATT        [ ATT header (3 B) | value ]           <- L2CAP SDU
 L2CAP      [ L2CAP header (4 B) | SDU ]           <- L2CAP PDU
 Link layer [ frag 1 ][ frag 2 ] ... [ frag n ]    <- each <= 251 B
```

The L2CAP length field is 16 bits, so the format allows an SDU of up to 65535 bytes. The radio never sees the full SDU, only the fragments.

A 2000-byte notification therefore goes over the air as about **eight** link-layer packets, usually in one connection event.

## Fragmentation does not lose data

The link layer acknowledges each packet and retransmits failed ones. A failed fragment adds latency but does not corrupt the message.

## Cost of large packets

- The radio stays on longer in each connection event, which uses more power.
- Both devices need more ACL buffer memory to hold the fragments.

## The spec ceiling: 512 bytes

The Bluetooth Core Specification, Vol 3, Part F, Section 3.2.9, limits an attribute value to **512 bytes**. A notification carries one attribute value, so a spec-compliant notification is at most 512 bytes.

This is why most stacks stop at an ATT MTU of **517 bytes**: 512 bytes of value plus the largest ATT header (5 bytes, for a Prepare Write). An MTU above 517 gives no benefit to a spec-compliant peer.

## Limits on phones and laptops

These are ATT MTU limits. The link-layer limit is 251 bytes on all of them.

| Platform | ATT MTU | Notes |
|---|---|---|
| Android 14 and later | 517 | The stack requests 517 on the first `requestMtu()` call and ignores later requests. Result is `min(517, peer MTU)`. |
| Android 13 and earlier | Up to 517 | The app requests a value with `requestMtu()`. |
| iPhone / iPad (iOS) | 185 on many devices, 527 seen on newer ones | iOS starts the exchange. The app cannot set it. Read it with `maximumWriteValueLength(for:)`. Values change with model and iOS version. |
| Mac (macOS) | Set by the OS | Same CoreBluetooth API as iOS. The app cannot set it. |
| Windows 10 / 11 | Set by the OS | Negotiated before the app gets the connection. Read it with `GattSession.MaxPduSize`. |
| Linux (BlueZ) | Up to 517 | `BT_ATT_MAX_LE_MTU` is 517 in BlueZ. |

Do not hard-code these numbers in an app. Read the negotiated value after the connection and size each write to `MTU - 3` bytes.

## Setting a large ATT MTU in Zephyr

A large MTU is an **ATT** change. You also make the **L2CAP host buffer** large enough to hold it. The **link layer** stays at 251 bytes.

For a target ATT MTU of **N** bytes, set:

| Setting | Value | Direction | What it controls |
|---|---|---|---|
| `CONFIG_BT_L2CAP_TX_MTU` | N | Send | Largest ATT packet this device sends |
| `CONFIG_BT_BUF_ACL_RX_SIZE` | N + 4 | Receive | Host buffer for one reassembled L2CAP PDU. RX MTU = this − 4 (L2CAP header). |
| `CONFIG_BT_BUF_ACL_TX_SIZE` | 251 | Host to controller | Size of one HCI ACL packet. Not the MTU. |
| `CONFIG_BT_CTLR_DATA_LENGTH_MAX` | 251 | Over the air | Link-layer payload (DLE). Cannot go above 251. |

Zephyr sends one value in the MTU exchange: the smaller of its TX MTU and RX MTU (`BT_LOCAL_ATT_MTU_UATT` in `att_internal.h`). The connection then uses the smaller of the two devices' values.

### Example: TX 1024, RX buffer 1027

| Step | Value |
|---|---|
| TX MTU | 1024 |
| RX MTU | 1027 − 4 = 1023 |
| Local ATT MTU | min(1024, 1023) = **1023** |
| Largest notification value | 1023 − 3 = **1020 bytes** |

The 4-byte L2CAP header makes the RX side one byte smaller than expected. To get a symmetric 1024, set `CONFIG_BT_BUF_ACL_RX_SIZE=1028`.

### Pitfall: DLE can silently stay at 27 bytes

`CONFIG_BT_CTLR_DATA_LENGTH_MAX` defaults to `CONFIG_BT_BUF_ACL_RX_SIZE` only when that value is 251 or less. Above 251, the default is **27**. With a large RX buffer, set `CONFIG_BT_CTLR_DATA_LENGTH_MAX=251` explicitly. If you do not, the large MTU still works, but each link-layer packet carries 27 bytes, and throughput drops.

### Limits

- `CONFIG_BT_L2CAP_TX_MTU` has a Kconfig range of 23 to 2000.
- Both devices must use the same large values. The connection uses the smaller one.

## Why large notifications work between two Zephyr devices

- Both ends set a large MTU with the settings above.
- On the **send** side, Zephyr does not check the 512-byte attribute limit.
- On the **receive** side, Zephyr **4.4.x and earlier** accept values above 512 bytes. Zephyr **4.5 (from v4.5.0-rc1)** drops a received notification above 512 bytes and logs "Ignoring value with invalid length" (`gatt.c`).
- A phone or PC central caps the MTU at about 517 bytes. For those centrals, keep notifications at 512 bytes or less.

For large transfers that stay compliant and work on Zephyr 4.5, phones and PCs, use an **L2CAP connection-oriented channel (CoC)**. Its SDU can be up to 65535 bytes, and it has credit-based flow control.

## Summary

> **"BLE is limited to 251 bytes."**
>
> 251 bytes is the link-layer packet size. A large MTU is at the ATT layer, and L2CAP splits each ATT packet across link-layer packets.

## References

- [Android 14 behavior changes: ATT MTU 517](https://developer.android.com/about/versions/14/behavior-changes-all)
- [Apple Developer Forums: iOS MTU exchange](https://developer.apple.com/forums/thread/721541)
- [Nordic DevZone: iOS MTU 185 bytes](https://devzone.nordicsemi.com/f/nordic-q-a/44825/ios-mtu-size-why-only-185-bytes/176057)
- [Web Bluetooth discussion: MTU on Windows, macOS, Linux](https://lists.w3.org/Archives/Public/public-web-bluetooth-log/2020Feb/0004.html)
- [BlueZ att-types.h](https://coral.googlesource.com/bluez-imx/+/refs/tags/5.27/src/shared/att-types.h)
- [Zephyr l2cap.h: L2CAP header, RX/TX MTU macros](https://github.com/zephyrproject-rtos/zephyr/blob/main/include/zephyr/bluetooth/l2cap.h)
- [Zephyr att_internal.h: local ATT MTU](https://github.com/zephyrproject-rtos/zephyr/blob/main/subsys/bluetooth/host/att_internal.h)
- [Zephyr Kconfig.l2cap: TX MTU range](https://github.com/zephyrproject-rtos/zephyr/blob/main/subsys/bluetooth/host/Kconfig.l2cap)
- [Zephyr controller Kconfig: BT_CTLR_DATA_LENGTH_MAX default](https://github.com/zephyrproject-rtos/zephyr/blob/main/subsys/bluetooth/controller/Kconfig)
- [Zephyr gatt.c: 512-byte receive check](https://github.com/zephyrproject-rtos/zephyr/blob/main/subsys/bluetooth/host/gatt.c)
