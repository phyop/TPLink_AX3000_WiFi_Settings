# TP-Link AX3000 設定檢查表

## Network Segmentation

- [ ] Home network 只放主要信任裝置
- [ ] IoT network 放智慧家電與低信任裝置
- [ ] Guest network 只提供網際網路
- [ ] Guest network 已隔離私人 LAN

## Security

- [ ] Home network 優先使用 WPA3-Personal
- [ ] 舊裝置不相容時，使用 WPA3-Personal + WPA2-PSK(AES)
- [ ] IoT network 使用 WPA3-Personal + WPA2-PSK(AES)
- [ ] Guest network 使用 WPA3-Personal + WPA2-PSK(AES)
- [ ] WPS 已關閉
- [ ] Wi-Fi 密碼夠長且不可猜

## SSID

- [ ] SSID 顯示，不隱藏
- [ ] 公開文件不包含真實 SSID
- [ ] IoT、Guest、Home 命名能清楚辨識用途

## 2.4 GHz

- [ ] Channel width: 20/40 MHz Auto
- [ ] Channel: Auto
- [ ] 擁擠環境已測試 1 / 6 / 11
- [ ] Mode: 802.11b/g/n/ax

## 5 GHz

- [ ] Channel width: 80 MHz
- [ ] Channel: Auto
- [ ] 必要時已測試 36 / 149
- [ ] Mode: 802.11a/n/ac/ax

## Wi-Fi 6 Features

- [ ] OFDMA enabled
- [ ] TWT enabled

## Smart Connect

- [ ] 一般簡化需求：可開啟 Smart Connect
- [ ] 需要固定分流、IoT 分區或除錯透明度：建議關閉 Smart Connect

