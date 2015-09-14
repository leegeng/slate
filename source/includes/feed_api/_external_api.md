# 프로필 피드 외부 API 스펙

톡 프로필의 피드 정보는 사전에 협의된 서비스들로부터 정보를 수신하며 연동 방식(async, sync)에 따라 정해진 형식의 argument를 받음. 

## Async

비동기 연동의 경우, 지정된 exchange(topic.async_task)에 routing-key(None.Profile3TalkProfileFeedTask)를 지정하여 다음과 같은 Argument를 받음. (상세 메세지 형식은 <a href="https://github.daumkakao.com/kakaotalk-spam/async_task/wiki/Protocol-Guide-For-Third-party-Developer" />Protocol Guide For Third party Developer</a>)
 
 
Service provider -> 카카오톡 MQ


### MQ server information
 
phase | hosts | port | vhost
--------- | --------- | --------- | ---------
alpha | <li>talksrv-mq.krane.iwilab.com</li><li>talksrv-mq2.krane.iwilab.com</li> | 5672 | inni_worker_alpha
sandbox | <li>talksrv-mq.krane.iwilab.com</li><li>talksrv-mq2.krane.iwilab.com</li> | 5672 | inni_worker_sandbox
beta/release | temq-g.iwilab.com | 5672 | inni_worker

### Argument Type 

Name | Type | Description
--------- | --------- | ---------
action | String | 'create' - 새 Feed 입력<br>'update' - Feed 정보 수정<br>'delete' - Feed 제거<br>'delete_all' - 해당 사용자의 서비스 피드 모두 제거
feed | Feed | Feed Object

### Feed Object

> Example of Feed object

```json
{
  "urls": {"root": "kakaostory://profile?id=73328833&name=에리츄&from=talk", "web": "https://story.kakao.com/exolechue"},
  "account_id": 78806689, 
  "updated_at": "2015-09-14T06:48:17Z", 
  "media_type":"image", 
  "image_url": "http://dn-l0-story.kakao.co.kr/dn/byy3jl/hygzGpUHv1/h0UIahVetlRNPG0z3IQ9V0/img_l.jpg?width=480&height=578", 
  "created_at": "2015-09-14T06:48:17Z", 
  "text": "", 
  "thumbnail_url": "http://dn-s-story.kakao.co.kr/dn/byy3jl/hygzGpUHv1/h0UIahVetlRNPG0z3IQ9V0/img_m.jpg?width=480&height=578", 
  "client_id": 86680234706731008, 
  "client_pk": "73328833_00000000000000001"
}
```

* create/update request

Name | Type | Description
--------- | --------- | ---------
account_id | Long | 사용자의 account_id
client_id | Long | 카카오계정에서 사용하는 서비스의 ID
client_pk | String | 콘텐츠 고유의 ID
image_url | String | 원본 이미지 Url
thumbnail_url | String | 썸네일 이미지 Url
urls | Object | 랜딩 url 주소
text | String | 콘텐츠의 텍스트
updated_at | String | 콘텐츠가 update된 시간<br>"yyyy-MM-dd'T'HH:mm:ssZ" 포맷
created_at | String | 콘텐츠가 create된 시간<br>"yyyy-MM-dd'T'HH:mm:ssZ" 포맷

* delete request

Name | Type | Description
--------- | --------- | ---------
account_id | Long | 사용자의 account_id
client_id | Long | 카카오계정에서 사용하는 서비스의 ID
client_pk | String | 콘텐츠의 고유 ID

* delete_all request

Name | Type | Description
--------- | --------- | ---------
account_id | Long | 사용자의 account_id
client_id | Long | 카카오 계정에서 사용하는 서비스의 ID

### Url Object

Name | Type | Description
--------- | --------- | ---------
root  | String | iOS와 Android 모두 같은 app scheme을 사용할 경우
ios | String | iOS용 app scheme
android | String | Android용 app scheme
web | String | 웹 url

## Sync

동기 연동의 경우, 게임과 같이 보상을 위해 응답을 꼭 받아야하는 케이스가 아니면 사용을 지양함. 


Service provider -> 다음카카오 API Hub -> iceland-papi

 
iceland-papi thrift client를 이용하여 아래와 같은 메소드를 호출함.

### Argument Type

Action | Method
--------- | ---------
Create | updateProfileFeed 
Update | updateProfileFeed
Delete | deleteProfileFeed
Delete | deleteAllProfileFeed

### Feed Object

### Example