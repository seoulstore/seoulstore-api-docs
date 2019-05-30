# SEOULSTORE's API Documentation

이 저장소는 [서울스토어](https://www.seoulstore.com)의 API 문서를 담고 있습니다.

**Contents**
* [기본사항](#기본사항)
* [API 목록](#API-목록)
  * [상품](#상품)
  * [상품 옵션](#상품-옵션)
  * [주문](#주문)
  * [교환/반품](#교환/반품)
  * [기타](#기타)
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

_input_

| Parameter            | Type    | Required | Description |
|----------------------|---------|----------|-------------|
| supplyPrice          | Integer | `true`   | 공급가격      |
| salePrice            | Integer | `true`   | 판매가격      |
| channelId            | Integer | `true`   | 판매채널 아이디 |
| attributes           | Object  | `true`   | 상품의 속성    |
| attributes.name      | String  | `true`   | 상품의 이름    |
| attributes.userCode1 | String  |          | 상품의 코드 1 |
| attributes.userCode2 | String  |          | 상품의 코드 2 |
| attributes.weight    | Integer |          | 상품 무게    |
| attributes.volumeX   | Integer |          | 부피 - x    |
| attributes.volumeY   | Integer |          | 부피 - y    |
| attributes.volumeH   | Integer |          | 부피 - h    |
| description          | String  |          | 상품 상세설명 |
| tags                 | String  |          | 상품 검색 태그, ^로 구분합니다. |
| categories           | Array   |          | 상품 카테고리 |
| images               | Object  |          | 상품 이미지 |
| images.list          | Array   |          | 상품 목록이미지 url|
| images.add           | Array   |          | 상품 추가이미지 url|

_output_

```
{
  "status": "success",
  "data": {
    "siteId": 1,
    "siteProductSetGroupId": 0,
    "siteProductSpecGroupId": 0,
    "siteBrandId": 0,
    "isDeleted": 0,
    "isSale": 0,
    "isDisplay": 0,
    "isUsed": 0,
    "isShippingFree": 0,
    "shippingGroupId": 0,
    "consumerPrice": 0,
    "discountRate": 0,
    "discountBeginDatetime": "0000-00-00 00:00:00",
    "discountEndDatetime": "0000-00-00 00:00:00",
    "discountPrice": 0,
    "siteCommissionId": 0,
    "siteTaxId": 0,
    "isIgnorePromotion": 0,
    "ratingAverage": 0,
    "parentChannelId": 0,
    "parentSiteProductId": 0,
    "orderCountSp": 0,
    "displayCms": 0,
    "isLock": 0,
    "isIgnoreParentContents": 0,
    "confirmStatus": 0,
    "sortDatetime": "2019-05-29T15:35:54.805Z",
    "siteProductId": 1063212,
    "supplierId": 1201,
    "channelId": 1881,
    "salePrice": 20000,
    "maximum": 0,
    "minimum": 0,
    "supplyPrice": 10000,
    "productId": 1054534,
    "editDatetime": "2019-05-29T15:35:54.805Z",
    "regDatetime": "2019-05-29T15:35:54.805Z"
  }
}
```

#### 상품 목록 조회

**GET /products**

_input_

| Parameter            | Type    | Required | Description |
|----------------------|---------|----------|-------------|
| start                | Integer |          | 리스트의 offset 입니다. `default: 0` |
| count                | Integer |          | 응답받을 아이템의 갯수입니다. `default: 10`|

_output_

```
{
  "status": "success",
  "data": {
    "items": [ Product… ],
    "start": 0,
    "count": 10,
    "total": 1
  }
}
```

#### 단일 상품 조회

**GET /products/:siteProductId**

_output_

```
{
  "status": "success",
  "data": { Product }
}
```

#### 상품 수정

**PATCH /products/:siteProductId**

PATCH로 동작하기 때문에 업데이트가 필요한 필드만 넘겨주시면 됩니다. 

_input_

| Parameter            | Type    | Required | Description |
|----------------------|---------|----------|-------------|
| supplyPrice          | Integer |          | 공급가격      |
| salePrice            | Integer |          | 판매가격      |
| channelId            | Integer |          | 판매채널 아이디 |
| attributes           | Object  |          | 상품의 속성    |
| attributes.name      | String  |          | 상품의 이름    |
| attributes.userCode1 | String  |          | 상품의 코드 1 |
| attributes.userCode2 | String  |          | 상품의 코드 2 |
| attributes.weight    | Integer |          | 상품 무게    |
| attributes.volumeX   | Integer |          | 부피 - x    |
| attributes.volumeY   | Integer |          | 부피 - y    |
| attributes.volumeH   | Integer |          | 부피 - h    |
| description          | String  |          | 상품 상세설명 |
| tags                 | String  |          | 상품 검색 태그, ^로 구분합니다. |
| categories           | Array   |          | 상품 카테고리 |
| images               | Object  |          | 상품 이미지 |
| images.list          | Array   |          | 상품 목록이미지 url|
| images.add           | Array   |          | 상품 추가이미지 url|

_output_

```
{
  "status": "success",
  "data": { Product }
}
```

#### 상품삭제

**DELETE /products/:siteProductId (TBD)** 

### 상품 옵션

#### 상품 옵션 등록
**POST /products/:siteProductId/items (WIP)**

#### 상품 옵션 목록 조회
**GET /products/:siteProductId/items**

_output_

```
{
  "status": "success",
  "data": {
    "items": [
      Option...
    ],
    "count": 22
  }
}
```

#### 상품 단일 옵션 조회

**GET /products/:siteProductId/items/:productItemId**

_output_

```
{
  "status": "success",
  "data": {
    "option": "COLOR",
    "value": "BEIGE(쮸리)",
    "itemId": "1113792",
    "isManageStock": 1,
    "quantity": 20,
    "orderQuantity": 0,
    "price": -12500
  }
}
```

#### 상품 재고 수정

**PATCH /products/:siteProductId/items/:productItemId/stock**

_input_

| Parameter            | Type    | Required | Description |
|----------------------|---------|----------|-------------|
| type                 | String  | `true`   | 추가인 경우 `IN`, 차감인경우 `OUT` 을 넘겨주세요. |
| status               | String  | `true`   | ADD / BROKEN / CANCEL / EDIT / EXCHANGE / LOSE / ORDER / RESTORE / SALE |
| quantity             | Integer | `true`   | 변경 수량입니다. type에 따라서 현재 재고에 추가하거나 차감합니다. |

### 기타

#### 사용자 정보

**GET /users/me**

_output_

```
{
  "status": "success",
  "data": {
    "adminId": 1309,
    "supplierUserId": 2332,
    "supplierId": 1201,
    "supplierUserType": "M",
    "supplierUserLoginId": "admin",
    "supplierUserName": "관리자",
    "supplierUserPhone": "010-6444-5743",
    "supplierUserEmail": "dasol_jung@fila.com",
    "isUse": 1,
    "isSystemManager": 3,
    "regDatetime": "2019-03-19T08:42:49.000Z",
    "editDatetime": "2019-03-19T08:42:49.000Z",
    "useSmsCertification": "T"
  }
}
```

#### 입점사의 채널 목록

**GET /suppliers/:supplierId/channels**

_input_

| Parameter            | Type    | Required | Description |
|----------------------|---------|----------|-------------|
| start                | Integer |          | 리스트의 offset 입니다. `default: 0` |
| count                | Integer |          | 응답받을 아이템의 갯수입니다. `default: 10`|

_output_

```
{
 "status": "success",
 "data": {

 }
}
```

