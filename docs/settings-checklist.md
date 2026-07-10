# TP-Link AX3000 Settings Checklist

## Network Segmentation

- [ ] Home network contains only trusted primary devices.
- [ ] IoT network contains smart home and lower-trust devices.
- [ ] Guest network provides internet access only.
- [ ] Guest network is isolated from the private LAN.

## Security

- [ ] Home network uses WPA3-Personal where supported.
- [ ] Mixed WPA3-Personal + WPA2-PSK(AES) is used only where compatibility requires it.
- [ ] IoT network uses WPA3-Personal + WPA2-PSK(AES).
- [ ] Guest network uses WPA3-Personal + WPA2-PSK(AES).
- [ ] WPS is disabled.
- [ ] Wi-Fi passwords are long and not guessable.

## SSID

- [ ] SSIDs are visible, not hidden.
- [ ] Public documentation does not include real SSIDs.
- [ ] Home, IoT, and Guest names clearly describe their purpose.

## 2.4 GHz

- [ ] Channel width: 20/40 MHz Auto.
- [ ] Channel: Auto.
- [ ] If crowded, channels 1 / 6 / 11 have been tested manually.
- [ ] Mode: 802.11b/g/n/ax.

## 5 GHz

- [ ] Channel width: 80 MHz.
- [ ] Channel: Auto.
- [ ] If needed, channels 36 / 149 have been tested manually.
- [ ] Mode: 802.11a/n/ac/ax.

## Wi-Fi 6 Features

- [ ] OFDMA is enabled.
- [ ] TWT is enabled.

## Smart Connect

- [ ] Smart Connect is enabled only when simplicity is more important than predictable band placement.
- [ ] Smart Connect is disabled when IoT, workstation, or troubleshooting needs require separate SSIDs.

