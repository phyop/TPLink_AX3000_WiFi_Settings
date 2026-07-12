# Content Pack: TP-Link AX3000 Wi-Fi Settings

## Resume Bullets

- **Situation:** Home and small studio Wi-Fi settings were difficult to reason about because trusted devices, IoT devices, and guest devices shared similar access assumptions. **Task:** Create a public technical guide that converted router configuration into a clear systems design problem. **Action:** Documented a TP-Link AX3000 topology with Home, IoT, and Guest segmentation, WPA3-first security, WPA2-AES compatibility paths, band settings, OFDMA, TWT, and Smart Connect tradeoffs. **Result:** Produced a reusable checklist that preserves 25 operational configuration items for safer, more maintainable network setup.
- **Situation:** Consumer router guides often over-index on speed tuning while under-explaining trust boundaries. **Task:** Reframe Wi-Fi setup for engineers and technical readers. **Action:** Organized the guide around the question "Does this device need access to my private LAN?" and mapped device classes to Home, IoT, and Guest networks. **Result:** Made security recommendations easier to apply before channel, band, and Wi-Fi 6 feature tuning.
- **Situation:** Mixed-generation IoT devices can fail with modern-only Wi-Fi settings. **Task:** Balance WPA3 adoption with practical compatibility. **Action:** Recommended WPA3-Personal for trusted Home devices and WPA3-Personal + WPA2-PSK(AES) for IoT and Guest networks, with WPS disabled and guest LAN isolation enabled. **Result:** Preserved a realistic security posture without breaking common smart home devices.
- **Situation:** Public technical writing can accidentally expose sensitive network identifiers. **Task:** Publish a useful network guide without leaking operational details. **Action:** Added explicit guidance to avoid publishing real SSIDs, Wi-Fi QR codes, router screenshots, MAC addresses, and device identifiers. **Result:** Turned a router settings note into safer public documentation suitable for GitHub, Medium, and portfolio reuse.

## LinkedIn Post

I rewrote a small TP-Link AX3000 Wi-Fi settings project as an engineer-oriented network design guide.

The main lesson: home Wi-Fi configuration should start with trust boundaries, not channel tuning.

Instead of asking "Which router option is fastest?", I framed the setup around one systems question:

Does this device need access to my private LAN?

That question creates a cleaner topology:

- Home network for trusted laptops, phones, workstations, NAS, and local services.
- IoT network for smart appliances, sensors, and home automation devices.
- Guest network for visitors who need internet access only.

From there, the technical choices become easier to explain. Use WPA3-Personal for trusted Home devices where supported. Use WPA3-Personal + WPA2-PSK(AES) for IoT and Guest networks when compatibility matters. Keep Guest isolated from the private LAN. Disable WPS. Use long, non-guessable passwords. Do not treat hidden SSIDs as security.

The guide also documents practical AX3000 defaults:

- 2.4 GHz: 20/40 MHz Auto, Auto channel, 802.11b/g/n/ax, with manual 1 / 6 / 11 testing if crowded.
- 5 GHz: 80 MHz, Auto channel, 802.11a/n/ac/ax, with manual 36 / 149 testing if needed.
- OFDMA: On.
- TWT: On.
- Smart Connect: convenient for simplicity, but off when predictable band placement and troubleshooting matter.

This is the same thinking I use in software and AI systems: make the boundary explicit, reduce blast radius, document the tradeoff, then tune the implementation.

Small infrastructure decisions compound. A router setup can be a tiny architecture exercise.

## Conventional Commit Message

```text
docs: rewrite tplink ax3000 guide and content pack
```

## PR Description

### Summary

Rewrites the TP-Link AX3000 public documentation into an engineer-oriented GitHub README, a story-form Medium article draft, and a reusable portfolio content pack.

### Changes

- Expanded `README.md` with Project Overview, Features, Tech Stack, Mermaid Architecture, Folder Structure, Installation, Usage, Result, Lessons Learned, and Future Improvements.
- Preserved the complete 25-item router settings checklist inline in the README and kept `docs/settings-checklist.md` as the primary checklist file.
- Added `medium-tplink-ax3000-wifi-settings-article.md` with title options, opening problem, background, step-by-step process, solution, lessons, pitfalls, conclusion, SEO metadata, and tags.
- Added `docs/content-pack.md` with STAR resume bullets, LinkedIn copy, Conventional Commit message, PR description, and future project extensions.

### Testing

- Verified the original checklist item count from `docs/settings-checklist.md`.
- Verified the rewritten README preserves all 25 checklist items.
- Reviewed required README, Medium, and content-pack sections.
- Inspected the git diff for accidental loss of technical settings.

### Screenshots

N/A. This is a Markdown documentation update and no router UI images are included.

### Future Work

- Add redacted router UI screenshots.
- Add a Wi-Fi interference survey workflow.
- Add firmware update and admin hardening checklist.
- Add an AI-assisted network audit template.

## Future Project Extensions

### AI Software Engineer

- Build a Markdown-based network audit generator that converts a device inventory into Home, IoT, and Guest placement recommendations.
- Add a structured JSON schema for router settings so an AI assistant can validate security mode, band, and segmentation choices.
- Create a prompt pack for reviewing home network documentation before public release to catch leaked SSIDs, QR codes, MAC addresses, screenshots, and device identifiers.

### Software Architect

- Extend the guide into a small reference architecture for home lab networks that includes NAS, Home Assistant, Proxmox, AI workstation, IoT devices, and guest access.
- Model network zones, device classes, and access rules as architecture decision records.
- Add a risk matrix comparing simplicity, compatibility, performance, and isolation across Smart Connect and separate-SSID designs.

### AI Agent Consultant

- Build an agent workflow that interviews a user about devices, building layout, router model, firmware, and privacy constraints, then produces a tailored setup checklist.
- Add an agent validation step that flags insecure recommendations such as hidden-SSID-as-security, WPS enabled, guest LAN access, weak passwords, or public exposure of router identifiers.
- Package the workflow as a consulting demo: intake questionnaire, generated network plan, human review checklist, and final implementation notes.
