---
title: API Reference

language_tabs:
  - json

toc_footers:
  - <a href='https://github.daumkakao.com/KakaoTalk-server/maldive_webapp/wiki/protocol-v31'>maldive_webapp protocol v31</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

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

```json
{
  "status": 0,
  "type": 1,
  "attachment": {
    "kakaoplace": {
      "title": "RUFXXX",
      "imageUrl": "http://mud-kage.kakao.co.kr/14/dn/btqbnuv1UPZ/Jb6Ao5o9g7DGxikFnUzkM0/o.jpg",
      "address": "분당구 삼평동",
      "new_address": "분당구 판교역로",
      "rating": 3.5,
      "reviews": 444,
      "bookmarks": 1024,
      "phoneNumber": "031-123-1234",
      "isPlaceUser": true,
      "isBookmarked": true,
      "hasReputation": true,
      "url": "kakao8491b6cd700e2b9afcdc88ea07ebd4b8://kakaolink?place_id=1463661&",
      "webUrl": "http://blog.naver.com/PostView.nhn?blogId=sayaka17&logNo=220402985131"
    },
    "kakaomap": {
      "iconUrl": "",
      "url": "http://m.map.daum.net/place?confirmid=17011742",
      "webUrl": "http://m.map.daum.net/place?confirmid=17011742"
    }
  },
  "layout": ["kakaoplace", "kakaomap"]
}
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

# 프로필 피드 개선 API

## Objects

### Feed

> Example for Feed object

```json
{
  "id": 150708982,
  "serviceName": "카카오스토리",
  "typeIconUrl": "http://mud-kage.kakao.co.kr/dn/bLZVrN/btqb8k7gArn/EWMuWsk1BYN10XcCSKAwOK/image.png",
  "downloadId": "486244601",
  "imageUrl": "http://dn-l1-story.kakao.co.kr/dn/eREGp/hyfWkuyk67/UwQ4G5QhJOcDde6knRJULK/img_l.jpg?width=720&height=960",
  "thumbnailImageUrl": "http://dn-s-story.kakao.co.kr/dn/eREGp/hyfWkuyk67/UwQ4G5QhJOcDde6knRJULK/img_m.jpg?width=720&height=960",
  "text": "",
  "url": "kakaostory://profile?id=53329&name=이경원&from=talk",
  "serviceUrl": "kakaostory://profile?idtype=0&from=talk&id=1030539",
  "webUrl": "https://story.kakao.com/leegeng?_r=talk",
  "serviceWebUrl": "https://story.kakao.com/leegeng?_r=talk",
  "updatedAt": 1438838295,
  "likeUserIds": [1,2,3,4,5],
  "feedMessage": "스토리 게시물을 등록했습니다.",
  "permission": 0,
  "liked": false,
  "type": 1,
  "metas": {}
}
```

Name | Type | Description
--------- | --------- | ---------
id | Integer | 피드의 id
serviceName | String | 피드 제공 서비스명
typeIconUrl | String | 피드 제공 서비스 아이콘 url
downloadId | String | 피드 제공 서비스의 download id (설치 유무 및 마켓 이동을 위한 정보)
imageUrl? | String | 피드의 메인 이미지 url
thumbnailImageUrl? | String | 피드의 메인 이미지의 썸네일 url
text? | String | 피드의 텍스트
url | String | 피드를 눌렀을 때 이동할 앱스킴
serviceUrl | String | 피드 제공 서비스 아이콘을 눌렀을 때 이동할 앱스킴
webUrl? | String | 피드를 눌렀을 때 앱이 없을 경우 인앱브라우저로 오픈할 웹페이지
serviceWebUrl? | String | 피드 제공 서비스 아이콘을 눌렀을 때 앱이 없을 경우 인앱브라우저로 오픈할 웹페이지
updatedAt | Integer | 피드 콘텐츠의 update 시간
likeUserIds | Array of Integer | 피드에 좋아요한 친구 리스트
feedMessage | String | 피드 헤더에 출력되는 메세지
permission? | Integer | 공개범위 (본인 피드에만 내려옴)
liked? | Boolean | 좋아요 여부 (친구 피드에만 내려움)
type | Integer | 피드 템플릿 타입 (참고: xxx)
metas | FeedMeta | 부가 정보 필드 ...

### FeedMeta

## /:agent/profile3/my_feeds.json

> Response Example for /:agent/profile3/my_feeds.json 

```json
{
  "status": 0,
  "feeds": [{FEED}, {FEED}],
  "cursor": 123
}
```

* 내 프로필 피드
* Domain : katalk.kakao.com
* Request Headers : A S
* Method : GET
* Request Parameters

Name | Type | Description
--------- | --------- | ---------
cursor | Integer | 페이징을 위한 next cursor
type? | String | 'profile' 일 경우 프로필 이미지 변경 피드만 내려줌. 

* Response

Name | Type | Description
--------- | --------- | ---------
status | Integer | 0: 정상, -500: 에러
feeds | Array of Feed | Feed 데이터
cursor | Integer | 페이징을 위한 next cursor. 0일경우에는 다음 피드 없음.

## /:agent/profile3/friend_feeds.json

> Response Example for /:agent/profile3/friend_feeds.json

```json
{
  "status": 0,
  "feeds": [{FEED}, {FEED}],
  "cursor": 123
}
```

* 친구 프로필 피드
* Domain : katalk.kakao.com
* Request Headers : A S
* Method : GET
* Request Parameters

Name | Type | Description
--------- | --------- | ---------
id | Integer | 친구의 user_id
cursor | Integer | 페이징을 위한 next cursor
type? | String | 'profile' 일 경우 프로필 이미지 변경 피드만 내려줌.

* Response

Name | Type | Description
--------- | --------- | ---------
status | Integer | 0: 정상, -500: 에러
feeds | Array of Feed | Feed 데이터
cursor | Integer | 페이징을 위한 next cursor. 0일경우에는 다음 피드 없음.

## /:agent/profile3/like.json

## /:agent/profile3/unlike.json

## /:agent/profile3/change_feed_permission.json

## /:agent/profile3/remove_feed.json

## /:agent/profile3/like_members.json

