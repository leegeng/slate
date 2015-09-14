# 톡 A/B 테스트 

## /:agent/account/more_settings.json

> Response Example

```json
{
  "abTests": {
    "id": "M.newBadge.150914",
    "type" 0
  }
}
```

* 추가되는 필드만 명시함
* Response

Name | Type | Description
--------- | --------- | ---------
abTests | Array of abTest | A/B 테스트 정보

## abTest object

Name | Type | Description
--------- | --------- | ---------
id | String | A/B 테스트의 고유 id
type | Integer | A/B 테스트 대상 정보<br>0: 실험군<br>1: 대조군
