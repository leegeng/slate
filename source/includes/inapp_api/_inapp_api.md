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
  "relation": 0
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
relation | Integer | 서비스와 사용자의 관계에 대한 노출조건을 나타냄.<br>0: 모든 대상에게 노출<br>1: 유저가 서비스와 관계가 없을 경우에만 노출 (미가입자 혹은 친구 아님, 서비스->사용자 단방향 친구 개념)<br>2: 유저가 서비스와 관계가 있을 경우에만 노출 (가입자 혹은 친구 관계, 서비스<->사용자 쌍방 친구 개념)  

### PlusFriend

> Example for plusfriend object

```json
{
  "userId": 53247774,
  "type": "p",
  "imageUrl": "http://sandbox-th-p.talk.kakao.co.kr/talkp/wkaIAuovUl/L3DlacPpWKUiN5MtOazb0k/jmryu2.jpg",
  "url": "",
  "webUrl": "",
  "downloadId": "com.kakao.talk",
  "title": "나이키닷텀",
  "status": "세상의 편견에 너의 목소리로 답해줘",
  "action": 0,
  "relation": 1,
  "uuid": "@나이키닷컴"
}
```

Name | Type | Description
--------- | --------- | ---------
userId | Integer | 플러스친구 userId (친구여부 확인 및 프로필 연결 정보)
type | String | 플러스친구 or 옐로아이디 구분 (p | y)
imageUrl | String | 플러스친구 프로필 이미지 url
url | String | 앱스킴
webUrl | String | 앱스킴이 동작하지 않을 경우 실행
downloadId | String | webUrl이 비어있고 앱이 설치되지 않은 경우 다운로드를 위한 Id
title | String | 플러스친구 이름
status | String | 플러스친구 상태메세지 또는 입력한 문구
action | Integer | 동작 타입<br>0: userId를 이용한 친구 추가<br>(가정)1: 앱스킴을 이용한 프로필 열기<br>(가정)2: 앱스킴을 이용한 기타 행위
relation | Integer | 서비스와 사용자의 관계에 대한 노출조건을 나타냄.<br>0: 모든 대상에게 노출<br>1: 유저가 서비스와 관계가 없을 경우에만 노출 (미가입자 혹은 친구 아님, 서비스->사용자 단방향 친구 개념)<br>2: 유저가 서비스와 관계가 있을 경우에만 노출 (가입자 혹은 친구 관계, 서비스<->사용자 쌍방 친구 개념)
uuid | String | 플러스친구 uuid


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
