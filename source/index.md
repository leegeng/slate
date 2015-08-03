---
title: API Reference

language_tabs:
  - ruby

toc_footers:
  - <a href='https://github.daumkakao.com/KakaoTalk-server/maldive_webapp/wiki/protocol-v31'>maldive_webapp protocol v31</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:

search: true
---

# Introduction

<aside class="notice">
본 API 문서는 톡+파트에서 개발하는 새로운 스펙에 대한 것만 포함하고 있으며, maldive_webapp의 원본 문서는 <a href='https://github.daumkakao.com/KakaoTalk-server/maldive_webapp/wiki/protocol-v31'>maldive_webapp protocol v31</a> 를 참조해주세요.
</aside>

# Preparation

## Domain

Phase | Prefix | Example
--------- | ------- | -----------
alpha | alpha- | alpha-katalk.kakao.com
sandbox | sandbox- | sandbox-katalk.kakao.com
beta | beta- | beta-katalk.kakao.com
release |  | katalk.kakao.com

## HTTP Header

### A

* Request Header
* Client Agent Information
* 모든 리퀘스트에 반드시 존재해야 함.
* Separator: '/'

Index | Name | Example | Description
--------- | --------- | --------- | ---------
1 | os_name | ios, android, bada, wp | OS Name
2 | app_version | 3.1.0 | KakaoTalk Application Version
3 | lang | ko, en, ja | User Language
4 | build_version | 1234 | app_version 은 바꾸지 않고 패치하는 경우, 패치전후 이용자규모를 파악하기 위해

```
iPhone : 'ios/2.2.1/ko'
Android : 'android/3.1.0/en'
```

### S

* Request Header
* 마이그레이션 절차를 거쳐서 Authorization header를 사용하기 전까지는 S header를 사용한다.
* 또한 available2 플래그의 13번째 bit가 OFF일 때는 S header를 사용한다.
* Session Information, 사용자를 구분할 수 있는 세션키와 디바이스아이디를 가지고 있음.
* Separator: '-'

Index | Name | Description
--------- | --------- | ---------
1 | session_key | 서버에서 발급한 SessionKey
2 | device_uuid | SHA Hash UUID<br>클라이언트에서 DeviceUUID 를 알 수 없는 경우에는 'e2dc694aee2540c2de6b4a8be2d7718846a0dfb9' 로 강제지정함.

<aside class="success">
안드로이드 클라이언트에서는 DeviceUUID 를 다음룰에 의해 가져온다.<br>

1. Telephony.getDeviceId()<br>
2. 없을 경우, getprop 'ro.serialinfo'<br>
3. 없을 경우, '없음'을 뜻하는 해싱값 'e2dc694aee2540c2de6b4a8be2d7718846a0dfb9'
</aside>

# 톡 X 장소정보(POI) 레버리징 API

## /:agent/scrap/more.json

> Response Example

```ruby
response = {
  'status' => 0,
  'type' => 1,
  'attachment' => {
    'kakaoplace' => {
      'title' => 'RUFXXX',
      'imageUrl' => 'http://~~~.jpg',
      'address' => '분당구 삼평동',
      'new_address' => '분당구 판교역로',
      'rating' => 3.5,
      'reviews' => 444,
      'bookmarks' => 1024,
      'phoneNumber' => '031-123-1234',
      'isPlaceUser' => true,   # 북마크 버튼 노출을 판단하기 위한 플래그
      'isBookmarked' => true,  # place user일 경우 해당 poi를 북마크했는지 여부
      'hasReputation' => true, # false일 경우 phoneNumber를 출력하고, phoneNumber가 비어있을 경우 영역을 비워둠
      'url' => 'kakaoplace://~~~',
      'webUrl' => 'https://place.kakao.com/~~~'
    },
    'kakaomap' => {
      'iconUrl' => 'http://~~~.png',
      'url' => 'kakaomap://~~~',
      'webUrl' => 'https://~~~'
    }
  },
  'layout' => ['kakaoplace', 'kakaomap']
}
# 아이폰은 약간 구조가 달라서 layout에 대해서는 응답이 달라질 수 있음.
```

* 인앱브라우저 레버리징 API
* Domain : sc-talk.kakao.com
* Request Headers : A S
* Method : POST
* Request Parameters

Name | Type | Description
--------- | --------- | ---------
url | String | url
aa | String | uuid (adid)

*  Response

Name | Type | Description
--------- | --------- | ---------
status | Integer | 0: 정상<br>-500: 실패
type | Integer | 1: location
attachment | Hash of leveraging objects | 레버리징 요소들의 속성을 포함함 * kakaoplace * kakaomap
layout | Array of String | type에 대한 템플릿 레이아웃에 콘텐츠가 들어가는 순서를 명시함. ex. ['kakaoplace', 'kakaomap']

# 프로필 피드 개션 API

To be updated.

