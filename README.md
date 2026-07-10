# TP-Link AX3000 Wi-Fi Settings Guide

This repository turns a personal TP-Link AX3000 / Wi-Fi 6 router settings note into a public, privacy-safe guide.

The main lesson is not that every home should copy one exact configuration. The better starting point is to separate devices by trust and purpose:

- **Home network:** laptops, phones, workstations, NAS, and trusted local services
- **IoT network:** smart appliances, sensors, and home automation devices
- **Guest network:** visitors who only need internet access

All private SSIDs, passwords, device names, screenshots, and identifying details have been removed or generalized.

## Recommended Topology

```text
Internet
  |
  +-- TP-Link AX3000
        |
        +-- Home network
        |     Security: WPA3-Personal if all devices support it
        |     Devices: laptop, phone, workstation, NAS
        |
        +-- IoT network
        |     Security: WPA3-Personal + WPA2-PSK(AES)
        |     Devices: smart home and appliance devices
        |
        +-- Guest network
              Security: WPA3-Personal + WPA2-PSK(AES)
              Access: internet only, isolated from the private LAN
```

## Start With The Boundary

Before changing channels or renaming SSIDs, ask one question:

> Does this device need access to my private LAN?

If the answer is yes, it belongs on the Home network. Examples include a laptop that connects to a NAS, a workstation that runs local services, or a phone that controls trusted local devices.

If the answer is "not really," it is a good candidate for the IoT network. Smart bulbs, appliances, sensors, and similar devices often need internet access, but they usually do not need broad access to private computers and servers.

If the answer is no, it belongs on the Guest network. Guest devices should normally have internet access only.

Speed is a comfort feature. Boundaries are a safety feature.

## Security Mode

For the Home network, start with:

```text
WPA3-Personal
```

If all main devices support WPA3 reliably, this is the cleanest choice.

For IoT devices, compatibility matters more. Many smart home devices still behave better with WPA2-AES support available. A practical IoT setting is:

```text
WPA3-Personal + WPA2-PSK(AES)
```

This is not a failure to be modern. It is a realistic compromise for mixed-generation home devices. The important part is to keep lower-trust devices on their own network and avoid giving them unnecessary LAN access.

The Guest network can use the same mixed mode, but it should be isolated from the private LAN.

## Do Not Treat Hidden SSID As Security

Hidden SSIDs are often mistaken for a security feature. In practice, they usually make the network harder to manage without providing meaningful protection.

Better protections are:

- Use a long, non-guessable Wi-Fi password.
- Disable WPS.
- Use WPA2-AES or WPA3.
- Isolate guest access from the private LAN.
- Keep IoT devices on a separate SSID or network.
- Avoid publishing real SSIDs, Wi-Fi QR codes, router screenshots, MAC addresses, and device identifiers.

Security is not hiding the network name. Security is preventing the wrong devices from getting meaningful access.

## 2.4 GHz Settings

2.4 GHz is not the speed band. Its strengths are range, wall penetration, and compatibility.

Recommended starting point:

```text
Channel width: 20/40 MHz Auto
Channel: Auto
Mode: 802.11b/g/n/ax
```

If the local Wi-Fi environment is crowded, manually test:

```text
1 / 6 / 11
```

For IoT devices, 2.4 GHz is often more useful than 5 GHz. Most IoT devices do not need high throughput. They need stable, predictable connectivity.

## 5 GHz Settings

5 GHz is better for devices that actually benefit from higher throughput and lower latency, such as laptops, phones, workstations, streaming devices, and local file transfers.

Recommended starting point:

```text
Channel width: 80 MHz
Channel: Auto
Mode: 802.11a/n/ac/ax
```

If manual channel testing is needed, start with:

```text
36 / 149
```

The goal is to reserve the faster band for devices that can use it well, instead of letting every low-bandwidth device compete for the same space.

## OFDMA

OFDMA is one of the useful Wi-Fi 6 features on an AX3000-class router.

In simple terms, OFDMA helps the router serve multiple devices more efficiently. Instead of treating every device as a separate full-sized turn, the router can divide channel resources into smaller units and schedule traffic more effectively.

This matters in real homes because the network is rarely just one laptop doing one large download. It is usually a mix of phones, IoT devices, tablets, workstations, background sync, and streaming traffic.

Recommended setting:

```text
OFDMA: On
```

If a specific old device behaves poorly, troubleshoot that device. For a modern mixed-device home network, OFDMA is a reasonable default to enable.

## TWT

TWT means Target Wake Time. It lets compatible devices coordinate when they wake up to send or receive data.

The practical benefit is power efficiency and cleaner airtime usage, especially for mobile and IoT devices. A device does not need to keep waking up randomly if it can coordinate timing with the access point.

Recommended setting:

```text
TWT: On
```

Like OFDMA, this is a Wi-Fi 6 feature worth enabling by default unless a specific compatibility issue appears.

## Smart Connect

Smart Connect lets the router present one network name and automatically steer devices between 2.4 GHz and 5 GHz.

That is convenient for simple households. Everyone joins one SSID and the router decides where each device should go.

But Smart Connect is not always the best fit when you want predictable segmentation or easier troubleshooting. Consider turning it off if:

- IoT devices should stay on 2.4 GHz.
- Workstations or laptops should stay on 5 GHz.
- You want to quickly identify whether a problem is band-specific.
- You run local services such as NAS, Home Assistant, Proxmox, or an AI workstation.
- You want a clear boundary between Home, IoT, and Guest devices.

In that case, separate SSIDs are easier to reason about:

```text
Home-2G
Home-5G
IoT
Guest
```

These names are examples only. Do not publish real SSIDs in public documentation.

## Final Checklist

| Item | Recommendation |
| --- | --- |
| Home security | Prefer `WPA3-Personal`; use `WPA3-Personal + WPA2-PSK(AES)` only if needed for compatibility |
| IoT security | `WPA3-Personal + WPA2-PSK(AES)` |
| Guest security | `WPA3-Personal + WPA2-PSK(AES)` with private LAN isolation |
| SSID visibility | Visible, not hidden |
| 2.4 GHz width | `20/40 MHz Auto` |
| 2.4 GHz channel | `Auto`; test `1 / 6 / 11` if crowded |
| 2.4 GHz mode | `802.11b/g/n/ax` |
| 5 GHz width | `80 MHz` |
| 5 GHz channel | `Auto`; test `36 / 149` if needed |
| 5 GHz mode | `802.11a/n/ac/ax` |
| OFDMA | On |
| TWT | On |
| Smart Connect | Off when predictable band separation is more important than simplicity |
| WPS | Off |

## Related Publication

An English Medium version of this guide will be linked here after publication.

## Project Files

- [Settings checklist](docs/settings-checklist.md)
- [Privacy notes](docs/privacy.md)

## Privacy Notes

This repository intentionally avoids publishing:

- real Wi-Fi SSIDs
- Wi-Fi passwords
- MAC addresses
- router admin screenshots
- private IP layout details
- account identifiers
- hostnames
- device identifiers
- home layout or location hints

All names and topology examples are generalized.

## Disclaimer

This is a personal network settings guide, not a universal rule. The best Wi-Fi configuration depends on building layout, neighboring Wi-Fi interference, device age, router firmware, ISP equipment, and the level of segmentation you actually need.

