# Introduction

此份文件為串接 VM5 廣告投放系統之 API 文件 (v0.1)

# HTTP API Parameters

## 範例連結

```
<url prefix>?partner=vm5&osType=ios&adId=72f0a6d5-e2a1-4e77-bcfa-b244483f8727&orientation=portrait&lang=zh-tw&netType=wifi&timezone=8&appKey=586b4c115282dd5165fbdf7e&bundleId=com.vm5.sampleapp&appName=VMFive%20Sample%20App&placement=586b590d5282dd5165fbdf9b
creativeFormat=richmedia&creativeType=native&ip=8.8.8.8&dnt=0
```

## 必要欄位

* partner
    * 合作夥伴名稱
    * Example: vm5   

* osType
    * 裝置作業系統
    * Example: ios/android

* adId
    * 裝置 UUID (使用者 AD ID)
    * Example: 72f0a6d5-e2a1-4e77-bcfa-b244483f8727

* orientation
    * 螢幕方向
    * Example: portrait/landscape

* lang
    * 裝置語言
    * Example: en/zh-tw

* netType
    * 裝置網路類型
    * Example: wifi/3g/4g

* timezone
    * 時區
    * Example: 8

* appKey
    * App Key (VMFive 於介面註冊後提供)
    * Example: 586b4c115282dd5165fbdf7e

* bundleId
    * App Bundle ID (若無法提供，請填 appKey)
    * Example: com.vm5.sampleapp

* appName
    * App名稱
    * Example: VMFive Sample App

* placement
    * 版位 ID (VMFive 於介面註冊後提供)
    * Example: 586b590d5282dd5165fbdf9b

* creativeFormat
    * 廣告格式
    * Example: vm5/vast/richmedia

* creativeType
    * 版位類型
    * Example: native/interstitial

* ip
    * 用戶 IP (填入 private ip 會被拒絕)
    * Example: 8.8.8.8

* dnt
    * Do not track 設定
    * Example: 1 (使用者設定不允許追蹤)

## 選填欄位

* unixMillis
    * 請求時間戳記
    * Example: 1504087073222

* osVersion
    * 作業系統版本
    * Example: 10.3.2

* vendor
    * 裝置製造商
    * Example: apple/samsung/htc

* deviceType
    * 裝置類別
    * Example: phone/tablet

* xPixel
    * 螢幕寬
    * Example: 1242

* yPixel
    * 螢幕高
    * Example: 2208

* density
    * 螢幕密度
    * Example: 1

* lat
    * 地理位置資訊緯度
    * Example: 121.5528094

* lng
    * 地理位置資訊經度
    * Example: 25.0663508

* carrier
    * 電信商名稱
    * Example: 中華電信/CHT

* mnc
    * 行動裝置網路代碼 (Mobile Network Code)
    * Example: 7

* mcc
    * 行動裝置國家代碼 (Mobile Country Code) 
    * Example: 460

----

# API Response

## richmedia

### Successful Response with Creative

```
{
    "adContent": {
        "html": "<html tag>",
        "icon": "<icon url>",
        "coverImage": "<cover image url>",
        "title": "<title text>",
        "ctaText": "<cta text>",
        "clickUrl": "<click url>"
    }
}
```

* clickUrl: 偵測到使用者點擊時跳轉至該 URL

### No-Ad Response

```
{
    "status": "<message>"
}
```