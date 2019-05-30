# SEOULSTORE's API Documentation

이 저장소는 [서울스토어](https://www.seoulstore.com)의 API 문서를 담고 있습니다.

**Contents**
* 기본사항
* API 목록
  * 상품
  * 상품 옵션
  * 주문
  * 교환/반품
  * 기타
* 부록
  * 상품구조

## 기본사항

**Note**

현재 서울스토어의 API는 화이트리스트에 등록된 클라이언트만 사용이 가능합니다. 화이트리스트에 등록되면 self-issued access token을 발급해드리며 이것을 이용하여 서울스토어의 API를 호출할 수 있습니다.

### Request

모든 요청은 Authorization 헤더를 가져야 하며 Bearer 타입의 인증이 필요합니다. 발급받은 _access token_ 을 이용해주세요.

* Host: https://sanggye-stage.seoulstore.com 
* Request Header: Authorization: Bearer _access_token_

_Example Request_

```
POST /products HTTP/1.1
Host: sanggy-stage.seoulstore.com
Authorization: Bearer <Token>
Content-Type: application/json
Accept: application/json
Accept-Charset: utf-8

{
  "supplyPrice": 100,
  "salePrice": 100,
  "channelId": 1881,
  "attributes": {
    "name": "my first product"
  }
}

```

### Response

응답에 대한 코드는 일반적인 http Response Status Code 규격을 따릅니다.

* 200 Success
* 201 Created
* 204 No Content
* 304 Not Modified
* 400 Bad Request
* 401 Unauthorized
* 403 Forbidden
* 404 Not Found
* 500 Internal Server Error
* 502 Bad Gateway
* 503 Service Unavailable

## API 목록

다음은 호출 가능한 API 목록입니다. 

### 상품

#### 상품등록

**POST /products**

| Parameter | Type | Required | Description |
|---|---|---|---|
|supplyPrice|Integer|o|공급가격|
