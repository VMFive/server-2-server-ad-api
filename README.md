# Introduction

此份文件為串接 VMFive 廣告投放系統之 API 文件 (v0.1.7)

# HTTP API Request Parameters

## Fetch Ads Request URL

```
https://[host][path]?appKey=592f800a224d071b3b3d08f4&placement=5959e8be40ee97f124765c7d&creativeFormat=richmedia&creativeType=native&osType=ios&bundleId=s2s-demo.com
```

## Query Parameters

OpenRTB BidRequest 欄位表示為定義**最接近**的欄位，定義或內容格式未必完全相同。

| OpenRTB BidRequest *     | Parameter Name   | Type                  | Definition                                             | Example                                                      |
| ------------------------ | ---------------- | :-------------------- | ------------------------------------------------------ | ------------------------------------------------------------ |
|                          | `partner`        | string; default `vm5` | SSP 合作夥伴                                           | enum: [vm5, ...]                                             |
| `site`/`app`             | `platform`       | string; default `app` | 使用者平台                                             | enum: [app, web]                                             |
| `site.page`/`app.bundle` | `bundleId`       | string; **required**  | App Bundle ID; 若無法提供，請與 VMFive 聯繫            | `com.vm5.sampleapp`<br />` s2s-demo.com` in this case        |
| `site.id`/`app.id`       | `appKey`         | string; **required**  | App Key (VMFive 於介面註冊後提供)                      | 592f800a224d071b3b3d08f4                                     |
| `site.id`/`app.id`       | `placement`      | string; **required**  | 版位 ID (VMFive 於介面註冊後提供)                      | 5959e8be40ee97f124765c7d                                     |
| `site.name`/`app.name`   | `appName`        | string                | 網頁標題/App名稱                                       | s2s demo application                                         |
| `app.ver`                | `appVersion`     | string                | App版本                                                | 1.0.0                                                        |
|                          | `creativeFormat` | string; **required**  | 廣告格式                                               | enum: [video, richmedia]                                     |
|                          | `creativeType`   | string; **required**  | 廣告呈現                                               | enum: [native, interstitial, web_native, web_impressive]     |
| `device.ua`              | `ua`             | string; recommended   | User-Agent, 若透過瀏覽器將可自動從 Request Header 帶入 | Mozilla/5.0 (iPhone; CPU iPhone OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Version/9.0 Mobile/13B143 Safari/601.1 |
| `device.geo.lat`         | `lat`            | float                 | 地理位置資訊緯度                                       | 121.5528094                                                  |
| `device.geo.lon`         | `lng`            | float                 | 地理位置資訊經度                                       | 25.0663508                                                   |
| `device.dnt`             | `dnt`            | string                | Do Not Track 設定                                      | 0: 使用者設定允許追蹤;<br />1: 使用者設定不允許追蹤          |
| `device.ip`              | `ip`             | string; recommended   | 裝置 IP ，若填寫 private ip 將會被拒絕                 |                                                              |
| `device.devicetype`      | `deviceType`     | string                | 裝置類別                                               | enum: [phone, tablet]                                        |
| `device.make`            | `vendor`         | string                | 裝置製造商                                             | apple / Sony / HTC                                           |
| `device.os`              | `osType`         | string; **required**  | 裝置作業系統，需與投放系統註冊內容一致                 | enum: [ios, android, web]                                    |
| `device.osv`             | `osVersion`      | string                | 裝置作業系統版本                                       | 10.3.2                                                       |
| `device.hwv`             | `deviceTerm`     | string                | 裝置名稱                                               | iPhone7,1 / D6503                                            |
| `device.h`               | `yPixel`         | integer               | 螢幕解析度-高度                                        | 1920                                                         |
| `device.w`               | `xPixel`         | integer               | 螢幕解析度-寬度                                        | 1080                                                         |
| `device.pxratio`         | `density`        | float                 | 螢幕解析度-密度                                        | 1                                                            |
| `device.language`        | `lang`           | string                | 裝置語言                                               | en / zh-tw                                                   |
| `device.carrier`         | `carrier`        | string                | 電信商名稱                                             | 中華電信 / CHT                                               |
| `device.mccmnc`          | `mcc`            | string                | 行動裝置國家代碼 (Mobile Country Code)                 | 460                                                          |
| `device.mccmnc`          | `mnc`            | string                | 行動裝置網路代碼 (Mobile Network Code)                 | 7                                                            |
| `device.connectiontype`  | `netType`        | string                | 裝置網路類型                                           | enum: [wifi, 3g, 4g, ...]                                    |
| `device.ifa`             | `adId`           | string; recommended   | 裝置 UUID (使用者 AD ID e.g.:IDFA/GAID...)             |                                                              |

# HTTP API Response

- Response content type depends on the route of request.
- Single route with content negotiation is not supported yet.

## Richmedia (Path: `/v1/richmedia`)

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

## VAST (Path: `/v1/vast`)

### Standard VAST 3.0 Ad Response:

```xml
<VAST version="3.0">
	<Ad id="...">
		<InLine>
			<AdSystem>
				<![CDATA[VMFive AdServer]]>
			</AdSystem>
			<AdTitle></AdTitle>
			<Impression>
				<![CDATA[https://...]]>
			</Impression>
			<Creatives>
				<Creative id="...">
					<Linear>
						<Duration>00:00:29.733</Duration>
						<TrackingEvents>
							<Tracking event="progress" offset="00:00:02">
								<![CDATA[https://...]]>
							</Tracking>
							<Tracking event="start">
								<![CDATA[https://...]]>
							</Tracking>
							<Tracking event="firstQuartile">
								<![CDATA[https://...]]>
							</Tracking>
							<Tracking event="midpoint">
								<![CDATA[https://...]]>
							</Tracking>
							<Tracking event="thirdQuartile">
								<![CDATA[https://...]]>
							</Tracking>
							<Tracking event="complete">
								<![CDATA[https://...]]>
							</Tracking>
						</TrackingEvents>
						<VideoClicks>
							<ClickThrough>
								<![CDATA[http://...]]>
							</ClickThrough>
							<ClickTracking>
								<![CDATA[https://...]]>
							</ClickTracking>
						</VideoClicks>
						<MediaFiles>
							<MediaFile delivery="progressive" type="video/mp4" width="852" height="480" maintainAspectRatio="true">
								<![CDATA[https://....mp4]]>
							</MediaFile>
						</MediaFiles>
					</Linear>
					<CreativeExtensions></CreativeExtensions>
				</Creative>
			</Creatives>
			<Description></Description>
			<Survey></Survey>
			<Extensions></Extensions>
		</InLine>
	</Ad>
</VAST>
```
