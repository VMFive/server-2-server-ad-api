# Introduction

此份文件為串接 VMFive 廣告投放系統之 API 文件 (v0.1.5)

# HTTP API Parameters

## 範例連結

```
<api route>?partner=vm5&appName=VMFive%20Sample%20App&bundleId=com.vm5.sampleapp&appKey=586b4c115282dd5165fbdf7e&placement=586b590d5282dd5165fbdf9b&creativeFormat=richmedia&creativeType=native&timezone=8&lang=zh-tw&adId=72f0a6d5-e2a1-4e77-bcfa-b244483f8727&osType=ios&ip=8.8.8.8&orientation=portrait
```

## Parameters

| category  | parameter name | required | description                       | example                                  | default value |
| --------- | -------------- | :------: | --------------------------------- | ---------------------------------------- | ------------- |
| exchange  | partner        |   yes    | 合作夥伴名稱                            | enum: [vm5, ...]                         |               |
| app       | platform       |    -     | 使用者平台                             | enum: [app, web]                         | app           |
| app       | bundleId       |   yes    | App Bundle ID; 若無法提供，請與 VMFive 聯繫 | com.vm5.sampleapp                        |               |
| app       | appKey         |   yes    | App Key (VMFive 於介面註冊後提供)         | 586b4c115282dd5165fbdf7e                 |               |
| app       | appName        |   yes    | App名稱                             | VMFive Sample App                        |               |
| app       | appVersion     |          | App版本                             | 1.0.0                                    |               |
| app       | placement      |   yes    | 版位 ID (VMFive 於介面註冊後提供)           | 586b590d5282dd5165fbdf9b                 |               |
| campaign  | creativeType   |   yes    | 版位類型                              | enum: [native, interstitial, web_interstitial] |               |
| campaign  | creativeFormat |   yes    | 廣告格式                              | enum: [vm5, vast, richmedia]             |               |
| user ctx  | unixMillis     |          | 請求時間戳記                            | 1414213562373                            |               |
| user ctx  | timezone       |   yes    | 時區                                | 8                                        |               |
| user ctx  | lang           |   yes    | 裝置語言                              | en / zh-tw                               |               |
| user ctx  | lat            |          | 地理位置資訊緯度                          | 121.5528094                              |               |
| user ctx  | lng            |          | 地理位置資訊經度                          | 25.0663508                               |               |
| user id   | dnt            |          | Do Not Track 設定                   | 0: 使用者設定允許追蹤; 1: 使用者設定不允許追蹤              |               |
| user id   | adId           |   yes    | 裝置 UUID (使用者 AD ID)               | 72f0a6d5-e2a1-4e77-bcfa-b244483f8727     |               |
| device    | vendor         |          | 裝置製造商                             | apple / Sony / HTC                       |               |
| device    | deviceType     |          | 裝置類別                              | enum: [phone, tablet]                    |               |
| device    | deviceTerm     |          | 裝置名稱                              | iPhone7,1 / Sony D6503                   |               |
| device os | osType         |   yes    | 裝置作業系統                            | enum: [ios, android]                     |               |
| device os | osVersion      |          | 裝置作業系統版本                          | 10.3.2                                   |               |
| network   | ip             |   yes    | 裝置 IP ，若填寫 private ip 將會被拒絕       | 8.8.8.8                                  |               |
| network   | netType        |          | 裝置網路類型                            | enum: [wifi, 3g, 4g, ...]                |               |
| network   | mcc            |          | 行動裝置國家代碼 (Mobile Country Code)    | 460                                      |               |
| network   | mnc            |          | 行動裝置網路代碼 (Mobile Network Code)    | 7                                        |               |
| network   | carrier        |          | 電信商名稱                             | 中華電信 / CHT                               |               |
| screen    | orientation    |   yes    | 螢幕方向                              | enum: [portrait, landscape]              |               |
| screen    | density        |          | 螢幕解析度-密度                          | 1                                        |               |
| screen    | xPixel         |          | 螢幕解析度-寬度                          | 1080                                     |               |
| screen    | yPixel         |          | 螢幕解析度-高度                          | 1920                                     |               |
| web       | ua             |          | User-Agent                        | Mozilla/5.0 (iPhone; CPU iPhone OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Version/9.0 Mobile/13B143 Safari/601.1 |               |

# API Response

## richmedia

### Successful Response with Creative

```json
{
    "adContent": {
        "campaignId": "<campaign id>",
        "audienceGroupId": "<audiencegroup id>",
        "creativeId": "<creative id>",
        "html": "<html tag>",
        "icon": "<icon url>",
        "coverImage": "<cover image url>",
        "title": "<title text>",
        "ctaText": "<call to action text>",
        "clickUrl": "<click url>"
    }
}
```

* clickUrl: 偵測到使用者點擊時跳轉至該 URL

### No-Ad Response

```json
{
    "status": "<message>"
}
```
