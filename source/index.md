---
title: API Reference

language_tabs:
  - shell
  - ruby
  - python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

<aside class="notice">
본 API 문서는 톡+파트에서 개발하는 새로운 스펙에 대한 것만 포함하고 있으며, maldive_webapp의 원본 문서는 https://github.daumkakao.com/KakaoTalk-server/maldive_webapp/wiki/protocol-v31 를 참조해주세요.
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

# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Isis",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Isis",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">If you're not using an administrator API key, note that some kittens will return 403 Forbidden if they are hidden for admins only.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

