# TP-Link AX3000 Wi-Fi Settings Guide

## Project Overview

This repository documents a practical TP-Link AX3000 / Wi-Fi 6 configuration for a home or small studio network. The core engineering idea is simple: separate devices by trust and purpose before tuning channels, bands, or Wi-Fi 6 features.

The configuration is not meant to be copied blindly into every building. It is a repeatable decision model for deciding which devices belong together:

- **Home network:** laptops, phones, workstations, NAS, and trusted local services.
- **IoT network:** smart appliances, sensors, and home automation devices.
- **Guest network:** visitors who only need internet access.

The authoring stance is practical systems thinking from a Senior Software Engineer / AI Software Engineer / AI Agent Developer perspective: make the boundary visible, document the tradeoff, then tune the implementation.

## Features

- Defines a three-zone topology for Home, IoT, and Guest devices.
- Recommends WPA3-first security while keeping a realistic WPA2-AES compatibility path for mixed-generation devices.
- Explains why hidden SSIDs are not meaningful security controls.
- Provides starting settings for 2.4 GHz and 5 GHz bands on AX3000-class hardware.
- Enables useful Wi-Fi 6 features: OFDMA and TWT.
- Clarifies when Smart Connect is convenient and when separate SSIDs are easier to operate.
- Preserves a complete implementation checklist for repeatable router configuration.

## Tech Stack

| Layer | Tooling / Standard | Purpose |
| --- | --- | --- |
| Router class | TP-Link AX3000 | Wi-Fi 6 home / small office access point and router |
| Wireless standard | 802.11ax with legacy modes | Modern Wi-Fi with backward compatibility |
| Security | WPA3-Personal, WPA2-PSK(AES) | Authentication and encryption choices |
| Documentation | Markdown, Mermaid | Public GitHub and Medium-ready technical writing |
| Operating model | Network segmentation | Trust-based separation of devices and access |

## Architecture

```mermaid
flowchart TD
    Internet((Internet)) --> Router[TP-Link AX3000]

    Router --> Home[Home network]
    Home --> HomeSecurity[Security: WPA3-Personal if all devices support it]
    Home --> HomeDevices[Devices: laptop, phone, workstation, NAS, trusted local services]

    Router --> IoT[IoT network]
    IoT --> IoTSecurity[Security: WPA3-Personal + WPA2-PSK(AES)]
    IoT --> IoTDevices[Devices: smart home appliances, sensors, automation devices]

    Router --> Guest[Guest network]
    Guest --> GuestSecurity[Security: WPA3-Personal + WPA2-PSK(AES)]
    Guest --> GuestAccess[Access: internet only, isolated from private LAN]
```

## Folder Structure

```text
.
|-- README.md
|-- medium-tplink-ax3000-wifi-settings-article.md
`-- docs
    |-- content-pack.md
    `-- settings-checklist.md
```

## Installation

This is a documentation repository. No package installation is required.

```bash
git clone <repo-url>
cd 260710_TPLink_AX3000_WiFi_Settings
```

To preview the Markdown locally, open `README.md`, `docs/settings-checklist.md`, `docs/content-pack.md`, or `medium-tplink-ax3000-wifi-settings-article.md` in any Markdown viewer.

## Usage

Use this guide as a router configuration runbook.

### 1. Start With The Boundary

Before changing channels or renaming SSIDs, ask one question:

> Does this device need access to my private LAN?

If the answer is yes, put the device on the Home network. Examples include a laptop that connects to a NAS, a workstation that runs local services, or a phone that controls trusted local devices.

If the answer is "not really," treat it as an IoT candidate. Smart bulbs, appliances, sensors, and similar devices often need internet access, but they usually do not need broad access to private computers and servers.

If the answer is no, put it on the Guest network. Guest devices should normally have internet access only.

Speed is a comfort feature. Boundaries are a safety feature.

### 2. Choose Security Mode

For the Home network, start with:

```text
WPA3-Personal
```

If all main devices support WPA3 reliably, this is the cleanest choice.

For IoT devices, compatibility matters more. Many smart home devices still behave better when WPA2-AES support is available. A practical IoT setting is:

```text
WPA3-Personal + WPA2-PSK(AES)
```

This is not a failure to be modern. It is a realistic compromise for mixed-generation home devices. The important part is to keep lower-trust devices on their own network and avoid giving them unnecessary LAN access.

The Guest network can use the same mixed mode, but it should be isolated from the private LAN.

### 3. Do Not Treat Hidden SSID As Security

Hidden SSIDs are often mistaken for a security feature. In practice, they usually make the network harder to manage without providing meaningful protection.

Better protections are:

- Use a long, non-guessable Wi-Fi password.
- Disable WPS.
- Use WPA2-AES or WPA3.
- Isolate guest access from the private LAN.
- Keep IoT devices on a separate SSID or network.
- Avoid publishing real SSIDs, Wi-Fi QR codes, router screenshots, MAC addresses, and device identifiers.

Security is not hiding the network name. Security is preventing the wrong devices from getting meaningful access.

### 4. Configure 2.4 GHz

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

### 5. Configure 5 GHz

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

### 6. Enable OFDMA

OFDMA is one of the useful Wi-Fi 6 features on an AX3000-class router.

In simple terms, OFDMA helps the router serve multiple devices more efficiently. Instead of treating every device as a separate full-sized turn, the router can divide channel resources into smaller units and schedule traffic more effectively.

This matters in real homes because the network is rarely just one laptop doing one large download. It is usually a mix of phones, IoT devices, tablets, workstations, background sync, and streaming traffic.

Recommended setting:

```text
OFDMA: On
```

If a specific old device behaves poorly, troubleshoot that device. For a modern mixed-device home network, OFDMA is a reasonable default to enable.

### 7. Enable TWT

TWT means Target Wake Time. It lets compatible devices coordinate when they wake up to send or receive data.

The practical benefit is power efficiency and cleaner airtime usage, especially for mobile and IoT devices. A device does not need to keep waking up randomly if it can coordinate timing with the access point.

Recommended setting:

```text
TWT: On
```

Like OFDMA, this is a Wi-Fi 6 feature worth enabling by default unless a specific compatibility issue appears.

### 8. Decide Whether To Use Smart Connect

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

### 9. Apply The Complete Checklist

This checklist is also maintained in `docs/settings-checklist.md`.

#### Network Segmentation

- [ ] Home network contains only trusted primary devices.
- [ ] IoT network contains smart home and lower-trust devices.
- [ ] Guest network provides internet access only.
- [ ] Guest network is isolated from the private LAN.

#### Security

- [ ] Home network uses WPA3-Personal where supported.
- [ ] Mixed WPA3-Personal + WPA2-PSK(AES) is used only where compatibility requires it.
- [ ] IoT network uses WPA3-Personal + WPA2-PSK(AES).
- [ ] Guest network uses WPA3-Personal + WPA2-PSK(AES).
- [ ] WPS is disabled.
- [ ] Wi-Fi passwords are long and not guessable.

#### SSID

- [ ] SSIDs are visible, not hidden.
- [ ] Public documentation does not include real SSIDs.
- [ ] Home, IoT, and Guest names clearly describe their purpose.

#### 2.4 GHz

- [ ] Channel width: 20/40 MHz Auto.
- [ ] Channel: Auto.
- [ ] If crowded, channels 1 / 6 / 11 have been tested manually.
- [ ] Mode: 802.11b/g/n/ax.

#### 5 GHz

- [ ] Channel width: 80 MHz.
- [ ] Channel: Auto.
- [ ] If needed, channels 36 / 149 have been tested manually.
- [ ] Mode: 802.11a/n/ac/ax.

#### Wi-Fi 6 Features

- [ ] OFDMA is enabled.
- [ ] TWT is enabled.

#### Smart Connect

- [ ] Smart Connect is enabled only when simplicity is more important than predictable band placement.
- [ ] Smart Connect is disabled when IoT, workstation, or troubleshooting needs require separate SSIDs.

## Result

No screenshots or router UI exports are included in this repository.

- Images: N/A
- Primary checklist: `docs/settings-checklist.md`
- Medium article draft: `medium-tplink-ax3000-wifi-settings-article.md`
- Portfolio content pack: `docs/content-pack.md`

## Lessons Learned

- Network design starts with trust boundaries, not with radio tuning.
- WPA3 is the preferred Home network baseline, but WPA3 + WPA2-PSK(AES) is a practical compatibility bridge for IoT and Guest networks.
- Hidden SSID is operational friction, not real security.
- 2.4 GHz is still valuable for range, wall penetration, and IoT stability.
- 5 GHz should be reserved for devices that benefit from higher throughput and lower latency.
- OFDMA and TWT are reasonable Wi-Fi 6 defaults unless a specific device compatibility issue appears.
- Smart Connect is useful for simplicity, but separate SSIDs are better for predictable placement and troubleshooting.

## Future Improvements

- Add device-specific validation notes for common smart home devices.
- Add a before/after network diagram with real SSIDs redacted.
- Add an interference survey workflow for apartments and dense neighborhoods.
- Add a router firmware checklist covering update cadence, admin password rotation, and backup/restore.
- Turn the checklist into an AI-assisted home network audit template.

## Related Publication

- [TP-Link AX3000 Wi-Fi Settings Guide](https://medium.com/p/257fcc7cc9b7)

## Disclaimer

This is a personal network settings guide, not a universal rule. The best Wi-Fi configuration depends on building layout, neighboring Wi-Fi interference, device age, router firmware, ISP equipment, and the level of segmentation you actually need.
