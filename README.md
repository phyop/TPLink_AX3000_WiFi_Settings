# TP-Link AX3000 Wi-Fi 設定整理

這個專案把一份家用 TP-Link AX3000 / Wi-Fi 6 路由器設定筆記，整理成可公開閱讀的版本。

原始筆記的重點不是「每個人都應該照抄同一組參數」，而是把家用網路拆成三個清楚的使用情境：

- 主要裝置：電腦、手機、NAS、工作站
- IoT 裝置：家電、感測器、智慧家庭設備
- 訪客裝置：只需要上網，不應該碰到內網資源

公開版已移除真實 SSID、個人裝置名稱、住家情境細節與任何可識別資訊。

## 建議架構

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

## 核心設定

| 項目 | 建議 |
| --- | --- |
| Home 安全性 | 優先使用 `WPA3-Personal`；若相容性不足，改用 `WPA3-Personal + WPA2-PSK(AES)` |
| IoT 安全性 | `WPA3-Personal + WPA2-PSK(AES)` |
| Guest 安全性 | `WPA3-Personal + WPA2-PSK(AES)` |
| SSID | 建議顯示，不建議隱藏 |
| 2.4 GHz 頻寬 | `20/40 MHz Auto` |
| 2.4 GHz 頻道 | `Auto`；擁擠環境可手動測試 `1 / 6 / 11` |
| 2.4 GHz 模式 | `802.11b/g/n/ax`，除非確定不需要舊裝置 |
| 5 GHz 頻寬 | `80 MHz` |
| 5 GHz 頻道 | `Auto`；需要手動時可從 `36` 或 `149` 開始測試 |
| 5 GHz 模式 | `802.11a/n/ac/ax` |
| OFDMA | 開啟 |
| TWT | 開啟 |
| Smart Connect | 若需要固定分流，建議關閉 |
| WPS | 關閉 |

## 為什麼不建議隱藏 SSID

隱藏 SSID 常被誤解成安全功能，但它通常只會讓連線體驗變差。

對家用與小型工作環境來說，更實用的做法是：

- 使用足夠強的 WPA2/WPA3 密碼
- 避免 WPS
- 讓訪客網路與內網隔離
- 為 IoT 裝置建立獨立網段或獨立 SSID
- 定期檢查路由器韌體更新

## 為什麼 Smart Connect 不一定適合

Smart Connect 會讓路由器自動替裝置選擇 2.4 GHz 或 5 GHz。這對一般家庭很方便，但對有 NAS、AI 工作站、IoT 或需要穩定區分頻段的環境，可能反而不透明。

如果你想明確控制裝置位置，建議分開 SSID：

```text
Home-2G
Home-5G
IoT
Guest
```

這樣做的好處是：

- IoT 可以固定在覆蓋較遠的 2.4 GHz
- 工作站、手機、筆電可以優先使用 5 GHz
- 訪客流量不會進入私人 LAN
- 除錯時能更快判斷問題在頻段、DNS、裝置或路由器設定

## Public Files

- [Medium 文章草稿](medium-tplink-ax3000-wifi-settings.md)
- [設定檢查表](docs/settings-checklist.md)
- [隱私處理說明](docs/privacy.md)

## Privacy Notes

這個專案不公開：

- 真實 Wi-Fi SSID
- Wi-Fi 密碼
- MAC address
- 路由器管理頁截圖
- 私人 IP 配置細節
- 個人帳號、主機名稱、裝置識別碼

所有名稱都已改寫為泛用名稱。

## Disclaimer

這是一份個人網路設定整理，不是所有環境的唯一最佳解。不同房屋格局、鄰近 Wi-Fi 干擾、裝置年代、韌體版本與 ISP 設備都會影響最佳設定。

