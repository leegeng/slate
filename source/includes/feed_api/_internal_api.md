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
  "cursor": 1438838295123,
  "feedMessage": "",
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
cursor | Long | 피드 콘텐츠의 update 시간 millisecond
feedMessage | String | 피드 헤더에 출력되는 메세지 (커스텀)
permission? | Integer | 공개범위 (본인 피드에만 내려옴)
type | Integer | 피드 템플릿 타입 (참고: http://wiki.daumkakao.com/pages/viewpage.action?pageId=332048927)
extra | FeedExtra | 부가 정보 필드

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
  "feeds": {
    "last": true,
    "feeds": [Feed]
  },
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

Name | Type | Description
--------- | --------- | ---------
checkProfile2Photos | Boolean | (Optional) 사용자가 Profile2의 Photo 컨텐츠가 있는지 확인이 필요할 경우

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

Name | Type | Description
--------- | --------- | ---------
id | Integer | 친구의 userId

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
status | Integer | 0: 정상<br>-400: 잘못된 요청<br>-404: 없는 피드<br>-500: 에러

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
