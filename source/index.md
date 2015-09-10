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

# 톡 X 장소정보(POI) 레버리징 API

## Objects

### kakaoplace

> Example for KakaoPlace object

```json
{
  "placeId": 1234,
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
  "webUrl": "http://blog.naver.com/PostView.nhn?blogId=sayaka17&logNo=220402985131", 
  "downloadId": "com.kakao.place"
}
```

Name | Type | Description
--------- | --------- | ---------
placeId | Long | 장소의 Id (로컬, 플레이스 연동용)
title | String | 장소명
imageUrl | String | 장소 대표 이미지
address | String | 장소에 대한 주소
new_address | String | 장소에 대한 도로명 주소
rating | Float | 장소에 대한 평가 점수
reviews | Integer | 장소에 대한 리뷰 수 
bookmarks | Integer | 장소에 대한 북마크 수
phoneNumber | String | 장소에 대한 전화번호
isPlaceUser | Boolean | 사용자의 카카오플레이스 가입여부
isBookmarked? | Boolean | 카카오플레이스 사용자일 경우 해당 장소를 북마크했는지 여부
hasReputation | Boolean | rating, reviews가 있는지 여부. 이 변수를 통해 phoneNumber를 보여줄지 rating/reviews를 보여줄지 판단함.
url | String | 앱스킴
webUrl | String | 앱이 설치되어 있지 않을 경우 연결할 모바일웹 주소
downloadId | String | 앱 설치 여부를 판단하기 위한 downloadId

### kakaomap

> Example for KakaoMap object

```json
{
  "url": "http://m.map.daum.net/place?confirmid=17011742",
  "webUrl": "http://m.map.daum.net/place?confirmid=17011742",
  "downloadId": "com.kakao.map"
}
```

Name | Type | Description
--------- | --------- | ---------
url | String | 앱스킴
webUrl | String | 앱이 설치되어 있지 않을 경우 연결할 모바일웹 주소
downloadId | String | 앱 설치 여부를 판단하기 위한 downloadId

### banner

> Example for banner object

```json
{
  "eventId": "kakaopay-release-20150804",
  "bannerType": 0,
  "imageUrl": "http://img.talk.kakao.co.kr/images/banners/1439450445.png",
  "url": "",
  "webUrl": "http://paybiz-web.kakao.com/event/kakaopay/index201508/kakaopay_event_cgv.html",
  "downloadId": "",
  "service": "kakaopay",
  "extra": {
    "relation": 0
  }
}
```

Name | Type | Description
--------- | --------- | ---------
eventId | String | 인앱 레버리지 배너에 대한 고유 아이디
bannerType | Integer | 배너 타입<br>0: 하단배너, 1: 전면배너
imageUrl | String | 배너 이미지 url
url | String | 앱스킴 (앱스킴 연동이 필요한 경우)
webUrl | String | 앱스킴이 존재하는 경우, 앱이 없을 때, 그렇지 않은 경우 웹페이지로 이동할 url 
downloadId | String | 앱스킴이 있는 경우 앱 설치 여부를 판단하기 위한 downloadId
service | String | 배너 레버리지 서비스명
extra? | Hash | 노출 대상에 대한 추가 정보 

### bannerExtra

> Example for bannerExtra object

```json
{
  "relation": 0
}
```

Name | Type | Description
--------- | --------- | ---------
relation | Integer | 서비스와 사용자의 관계에 대한 노출조건을 나타냄.<br>0: 모든 대상에게 노출<br>1: 유저가 서비스와 관계가 없을 경우에만 노출 (미가입자 혹은 친구 아님, 서비스->사용자 단방향 친구 개념)<br>2: 유저가 서비스와 관계가 있을 경우에만 노출 (가입자 혹은 친구 관계, 서비스<->사용자 쌍방 친구 개념) 

### PlusFriend

> Example for plusfriend object

```json
{
  "userId": 53247774,
  "type": "p",
  "imageUrl": "/talkp/wkiOEvV5mo/LgBrddHUXckl6eCZA96gJ0/3wyzxf_110x110_c.jpg",
  "url": "kakaoplus://plusfriend/friend/@나이키닷컴",
  "webUrl": "",
  "downloadId": "com.kakao.talk",
  "title": "나이키닷텀",
  "status": "세상의 편견에 너의 목소리로 답해줘",
  "action": 0,
  "relation": 1
}
```

Name | Type | Description
--------- | --------- | ---------
userId | Integer | 플러스친구 userId (친구여부 확인 및 프로필 연결 정보)
type | String | 플러스친구 or 옐로아이디 구분 (p|y)
imageUrl | String | 플러스친구 프로필 이미지 url (kage profile)
url | String | 앱스킴
webUrl | String | 앱스킴이 동작하지 않을 경우 실행
downloadId | String | webUrl이 비어있고 앱이 설치되지 않은 경우 다운로드를 위한 Id
title | String | 플러스친구 이름
status | String | 플러스친구 상태메세지 또는 입력한 문구
action | Integer | 동작 타입<br>0: userId를 이용한 프로필 열기<br>(가정)1: 앱스킴을 이용한 프로필 열기<br>(가정)2: 앱스킴을 이용한 기타 행위
relation | Integer | 서비스와 사용자의 관계에 대한 노출조건을 나타냄.<br>0: 모든 대상에게 노출<br>1: 유저가 서비스와 관계가 없을 경우에만 노출 (미가입자 혹은 친구 아님, 서비스->사용자 단방향 친구 개념)<br>2: 유저가 서비스와 관계가 있을 경우에만 노출 (가입자 혹은 친구 관계, 서비스<->사용자 쌍방 친구 개념)


## /:agent/inapp_widget/more.json

> Response Example

```json
{
  "status": 0,
  "type": 1,
  "attachment": {
    "kakaoplace": KakaoPlaceObject,
    "kakaomap": KakaoMapObject,
    "banners": [BannerObject],
    "plusfriend": PlusFriendObject
  }
}
```

* 인앱브라우저 레버리징 API
* Domain : katalk.kakao.com
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
type | Integer | 1: location<br>2: banner<br>3: plusfriend
attachment | Hash of leveraging objects | 레버리징 요소들의 속성을 포함함 * kakaoplace * kakaomap

## /:agent/inapp_widget/more_action.json

* 인앱브라우저 레버리징 API (위젯에 사용자 액션이 존재하는 경우에 사용함)
* Domain : katalk.kakao.com
* Request Headers : A S
* Method : POST
* Request Parameters

Name | Type | Description
--------- | --------- | ---------
service | String | 어느 서비스에 대한 액션인지 명시 (more.json의 응답으로 받은 객체명을 보냄 ex. kakaoplace)
action | String | 액션명<br>kakaoplace: add(북마크하기) / delete(북마크해제)
place_id? | Long | kakaoplace에 대한 요청일 경우 필수값이며 받은 값을 그대로 올린다.
 
* Response

Name | Type | Description
--------- | --------- | ---------
status | Integer | 0: 정상<be>-500: 실패

# 프로필 피드 개선 API

## Objects

### Feed

> Example for Feed object

```json
{
  "id": "1:1234_567890",
  "serviceName": "카카오스토리",
  "typeIconUrl": "http://mud-kage.kakao.co.kr/dn/bLZVrN/btqb8k7gArn/EWMuWsk1BYN10XcCSKAwOK/image.png",
  "downloadId": "486244601",
  "contents": [ContentItem, ContentItem],
  "url": "kakaostory://profile?id=53329&name=이경원&from=talk",
  "serviceUrl": "kakaostory://profile?idtype=0&from=talk&id=1030539",
  "webUrl": "https://story.kakao.com/leegeng?_r=talk",
  "serviceWebUrl": "https://story.kakao.com/leegeng?_r=talk",
  "updatedAt": 1438838295,
  "feedMessage": "스토리 게시물을 등록했습니다.",
  "permission": 0,
  "type": 1,
  "extra": {}
}
```

Name | Type | Description
--------- | --------- | ---------
id | String | 피드의 고유 id
serviceName | String | 피드 제공 서비스명
typeIconUrl | String | 피드 제공 서비스 아이콘 url
downloadId | String | 피드 제공 서비스의 download id (설치 유무 및 마켓 이동을 위한 정보)
contents | Array of ContentItem | 피드 구성 요소 리스트
url | String | 피드를 눌렀을 때 이동할 앱스킴
serviceUrl | String | 피드 제공 서비스 아이콘을 눌렀을 때 이동할 앱스킴
webUrl? | String | 피드를 눌렀을 때 앱이 없을 경우 인앱브라우저로 오픈할 웹페이지
serviceWebUrl? | String | 피드 제공 서비스 아이콘을 눌렀을 때 앱이 없을 경우 인앱브라우저로 오픈할 웹페이지
updatedAt | Integer | 피드 콘텐츠의 update 시간
feedMessage | String | 피드 헤더에 출력되는 메세지
permission? | Integer | 공개범위 (본인 피드에만 내려옴)
type | Integer | 피드 템플릿 타입 (참고: xxx)
extra | FeedExtra | 부가 정보 필드 ...

### FeedExtra

> Example for FeedExtra object

```json
{
  "profileImagePath": "/talkp/wkka1wrLYf/5VV1GnauTwKAgRkBGEZhI0/uphy4g.jpg",
  "extraImages": 5,
  "backgroundImagePath": "http://th-p.talk.kakao.co.kr/talkp/wkkLnFWcjv/pRktMkmNRMJjnsvWSeRLC1/up1m4v.jpg",
  "from": {
    "downloadId": "com.kakao.story",
    "url": "kakaostory://profile?idtype=0&from=talk&id=491632",
    "webUrl": "https://alpha-story-web.kakao.com/_FTCzg4?_r=talk"
  }
}
```

Name | Type | Description
--------- | --------- | ---------
profileImagePath | String | 프로필 이미지 변경 피드의 경우, update_settings.json으로 바로 넘길 수 있는 path를 내려줌.
extraImages | Integer | blog type 피드의 경우, 원본 게시물이 두 개 이상의 이미지가 있을 경우 추가 이미지 여부를 알려줄 수 있도록 이미지 수를 내려줌.
backgroundImagePath | String | 상태메세지 변경 피드의 경우, 변경 시점의 backgroundImagePath를 가지고 있음.
from | Hash | 프사/배경 이미지의 경우 다른 서비스에서 가져온 경우 값을 가짐.

### ContentItem

> Example for ContentItem object

```json
{
  "type": "image",
  "value": "http://dn-s-story.kakao.co.kr/dn/eREGp/hyfWkuyk67/UwQ4G5QhJOcDde6knRJULK/img_m.jpg?width=720&height=960"
}
```

Name | Type | Description
--------- | --------- | ---------
type | String | ContentItem의 타입 명시 자세한 스펙은 () 참조
value | Object(String or Array of ContentItems) | 각 타입에 대한 속성값

### Profile

> Example for Profile object

```json
{
  "backgroundImageUrl": "~~~",
  "feeds": [Feed],
  "profileFeeds": {
    "tatalCnt": 123,
    "feeds": [Feed]
  },
  "backgroundFeeds": {
    "totalCnt": 123,
    "feeds": [Feed]
  },
  "action": Action,
  "event": Event,
  "birthday": "0128",
  "allowStory": true,
  "storyUrl": "~~~",
  "storyWebUrl": "~~"
}
```

Name | Type | Description
--------- | --------- | ---------
backgroundImageUrl | String | 배경이미지 url
feeds? | Array of Feed | 전체 타입의 최근 피드 n개
profileFeeds? | Hash | 프로필 이미지 타입의 최근 피드 m개<br>* totalCnt: 해당 타입 피드의 수<br>* feeds: 해당 타입의 피드 리스트
backgroundFeeds? | Hash | 배경이미지 타입의 최근 피드 m개<br>* totalCnt: 해당 타입 피드의 수<br>* feeds: 해당 타입의 피드 리스트
action? | Action | action object (프로필 상단 영역)
event? | Event | event object (프로필 상단 영역)
birthday? | String | user의 생일 정보 (MMDD) - 생일 당일에만 내려감.
allowStory? | Boolean | 스토리 버튼 노출 여부, <br>allowStory=true이면 스토리 버튼을 노출하고 storyUrl의 값을 링크로 연결함.<br>allowStory=false 이면 스토리 버튼을 노출하지 않음. <br>allowStory가 클라에 저장되어 있지 않을 때는 feeds가 있을 경우에만 스토리 버튼을 노출하고,<br> storyUrl은 kakaostory://profile?idtype=0&from=talk&id=account_id 로 링크를 연결함
storyUrl? | String | 스토리 프로필 url - allowStory가 false 인 경우에는 내려가지 않음
storyWebUrl? | String | 스토리 프로필 web url - allowStory가 false 인 경우와 데이터가 없는 경우에는 내려가지 않음

## /:agent/profile3/me.json

> Response Example for /:agent/profile3/me.json

```json
{
  "userId": 1234,
  "profile": Profile
}
```

* 내 프로필 내려받기
* Domain : katalk.kakao.com
* Request Headers : A S
* Method : GET
* Request Parameters
* Response

Name | Type | Description
--------- | --------- | ---------
status | Integer | 0: 정상, -500: 에러
profile | Profile | Profile 데이터

## /:agent/profile3/friend.json

> Response Example for /:agent/profile3/friend.json

```json
{
  "userId": 1234,
  "profile": Profile
}
```

* 친구 프로필 내려받기
* Domain : katalk.kakao.com
* Request Headers : A S
* Method : GET
* Request Parameters
* Response

Name | Type | Description
--------- | --------- | ---------
status | Integer | 0: 정상, -500: 에러, -1002 (E_NO_SUCH_USER_FOUND) : 유저 없음 (이 경우 delete.json을 호출하도록 함)
profile | Profile | Profile 데이터

## /:agent/profile3/my_feeds.json

> Response Example for /:agent/profile3/my_feeds.json 

```json
{
  "status": 0,
  "feeds": [{FEED}, {FEED}],
  "last": false,
  "tatalCnt": 10
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
type? | Integer | 1=프로필 피드만, 3=커버 피드만, 없거나 다른값이면 모든 피드

* Response

Name | Type | Description
--------- | --------- | ---------
status | Integer | 0: 정상, -500: 에러
feeds | Array of Feed | Feed 데이터
last | boolean | 다음 피드가 있는지 여부
totalCnt | Integer | 전체 피드 갯수. type=1 or 3 일 때만 전체 갯수이고 다른 경우에는 항상 0이다.

## /:agent/profile3/friend_feeds.json

> Response Example for /:agent/profile3/friend_feeds.json

```json
{
  "status": 0,
  "feeds": [{FEED}, {FEED}],
  "last": true,
  "tatalCnt": 10
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
type? | Integer | 1=프로필 피드만, 3=커버 피드만, 없거나 다른값이면 모든 피드

* Response

Name | Type | Description
--------- | --------- | ---------
status | Integer | 0: 정상, -500: 에러
feeds | Array of Feed | Feed 데이터
last | boolean | 다음 피드가 있는지 여부
totalCnt | Integer | 전체 피드 갯수. type=1 or 3 일 때만 전체 갯수이고 다른 경우에는 항상 0이다.

## /:agent/profile3/feed.json

* 단일 프로필 피드 정보 요청
* Domain : katalk.kakao.com
* Required Headers : A, S
* Method : GET
* Request Parameters

Name | Type | Description
--------- | --------- | ---------
user_id? | Integer | 친구의 user_id
feed_id | String | Feed의 id

* Response

Name | Type | Description
--------- | --------- | ---------
status | Integer | 0: 정상, -500: 에러
feed | Feed | Feed 데이터

## /:agent/profile3/change_feed_permission.json

* 프로필 피드의 공개 범위 변경
* Domain : katalk.kakao.com
* Required Headers : A, S
* Method : POST
* Request Parameters

Name | Type | Description
--------- | --------- | ---------
feed_id | String | Feed의 id
permission | Integer | 공개범위

* Response

Name | Type | Description
--------- | --------- | ---------
status | Integer | 0: 정상, -500: 에러

## /:agent/profile3/remove_feed.json

* 프로필 피드 삭제
* Domain : katalk.kakao.com
* Required Headers : A, S
* Method : POST
* Request Parameters

Name | Type | Description
--------- | --------- | ---------
feed_id | String | Feed의 id

* Response

Name | Type | Description
--------- | --------- | ---------
status | Integer | 0: 정상, -500: 에러

# 톡 X 스토리 레버리징 1차(프로필 배경/프사 이미지) API

## /:agent/profile3/get_story_profile_bg_image.json

> Response Example

```json
{
  "status": 0,
  "url": "http://alpha-api1-kage.kakao.com/dn/hFeAL/oWajbsbKKX/bxUkoZOud0zTqX4LuK65Y0/img_xl.jpg?width=1707&height=1281"
}
```

* 스토리에 설정된 배경 이미지 URL 가져오기
* Domain : katalk.kakao.com
* Request Headers : A S
* Method : GET
* Response

Name | Type | Description
--------- | --------- | ---------
status | Integer | 0: 정상<br>-500: 실패
url | String | 현재 스토리에 설정된 배경 이미지의 URL

## /:agent/profile3/get_story_profile_image.json

> Response Example

```json
{
  "status": 0,
  "url": "http://alpha-api1-kage.kakao.com/dn/bWhRXQ/oWaOIJSfiE/81js2k5Tftr4QHBX2qMWTk/img_xl.jpg?width=1281&height=1707"
}
```

* 스토리에 설정된 프사 이미지 URL 가져오기
* Domain : katalk.kakao.com
* Request Headers : A S
* Method : GET
* Response

Name | Type | Description
--------- | --------- | ---------
status | Integer | 0: 정상<br>-500: 실패
url | String | 현재 스토리에 설정된 프사 이미지의 URL
