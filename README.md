# SEOULSTORE's API Documentation

이 저장소는 [서울스토어](https://www.seoulstore.com)의 공개 API 문서를 담고 있습니다. 
API와 관련된 문의사항이 있는 경우 [자주 묻는 질문](faq.md)을 확인하시거나 [이슈](https://github.com/seoulstore/seoulstore-api-docs/issues)를 생성해주세요.

**Contents**

- [기본사항](#기본사항)
- [API 목록](#API-목록)
  - [사용자](#사용자)
  - [입점사](#입점사)
  - [상품](#상품)
  - [상품 옵션](#상품-옵션)
  - [상품 아이템](#상품-아이템)
  - [주문](#주문)
  - [교환 반품](#교환-반품)
  - [게시판 (wip)] (#게시판)
- [자주 묻는 질문](faq.md)
- [부록](appendix.md)

## 기본사항

**Note**

현재 서울스토어의 API는 화이트리스트에 등록된 클라이언트만 사용이 가능합니다. 화이트리스트에 등록되면 _self-issued access token_ 을 발급해드리며 이것을 이용하여 서울스토어의 API를 호출할 수 있습니다. 발급한 _access token_ 은 외부에 노출되지 않도록 주의하시기 바랍니다.

### Request

모든 요청은 Authorization 헤더를 가져야 하며 Bearer 타입의 인증이 필요합니다. 발급받은 _access token_ 을 이용해주세요.

- Host: https://sanggye-stage.seoulstore.com
- Request Header: Authorization: Bearer _access_token_

_Example Request_

```json
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

## API 목록

다음은 호출 가능한 API 목록입니다.

## 사용자

### 사용자 정보

**GET /users/me**

_output_

```json
{
  "status": "success",
  "data": {
    "adminId": 1309,
    "supplierUserId": 2332,
    "supplierId": 1201,
    "supplierUserType": "M",
    "supplierUserLoginId": "admin",
    "supplierUserName": "관리자",
    "supplierUserPhone": "***-***-****",
    "supplierUserEmail": "abc@abc.com",
    "isUse": 1,
    "isSystemManager": 3,
    "regDatetime": "2019-03-19T08:42:49.000Z",
    "editDatetime": "2019-03-19T08:42:49.000Z",
    "useSmsCertification": "T"
  }
}
```

## 입점사

### 입점사 채널 목록

**GET /suppliers/:supplierId/channels**

_input_

| Parameter | Type    | Required | Description                                 |
| --------- | ------- | -------- | ------------------------------------------- |
| start     | Integer |          | 리스트의 offset 입니다. `default: 0`        |
| count     | Integer |          | 응답받을 아이템의 갯수입니다. `default: 10` |

_output_

```json
{
  "status": "success",
  "data": {
    "items": [
      {
        "channelId": 1881,
        "channelCode": "filakorea",
        "channelDescription": [
          {
            "key": "channel_name_eng",
            "value": "FILA"
          },
          {
            "key": "instagram_account",
            "value": "fila_korea"
          },
          {
            "key": "facebook_account",
            "value": ""
          },
          {
            "key": "ignore_article_period",
            "value": "0"
          },
          {
            "key": "channel_name",
            "value": "휠라"
          },
          {
            "key": "channel_contents",
            "value": "FILA KOREA는 1911 이탈리아에서 탄생산 스포츠 브랜드로,<br />100년 이상의 휠라 고유의 헤리티지를 컨템포러리 감성과 스포츠 스트리트 감성을<br />조화롭게 믹스하여 휠라만의 스포츠 스트리트 웨어를 제안한다."
          },
          {
            "key": "channel_contents_2",
            "value": ""
          },
          {
            "key": "channel_banner",
            "value": ""
          },
          {
            "key": "channel_notice",
            "value": ""
          }
        ]
      }
    ],
    "start": 0,
    "count": 10,
    "total": 1
  }
}
```

### 입점사 채널 정보

**GET /suppliers/:supplierId/channels/:channelId**

_output_

```json
{
  "status": "success",
  "data": { Channel }
}
```

## 상품

### 상품 카테고리

**GET /categories**

_output_

```json
{
  "status": "success",
  "data": {
    "items": [ Categories ... ],
    "count": 365
  }
}
```

### 상품 등록

**POST /products**

_input_

| Parameter            | Type    | Required | Description                     |
| -------------------- | ------- | -------- | ------------------------------- |
| supplyPrice          | Integer | `true`   | 공급가격                        |
| salePrice            | Integer | `true`   | 판매가격                        |
| channelId            | Integer | `true`   | 판매채널 아이디                 |
| attributes           | Object  | `true`   | 상품의 속성                     |
| attributes.name      | String  | `true`   | 상품의 이름                     |
| attributes.userCode1 | String  |          | 상품의 코드 1                   |
| attributes.userCode2 | String  |          | 상품의 코드 2                   |
| attributes.weight    | Integer |          | 상품 무게                       |
| attributes.volumeX   | Integer |          | 부피 - x                        |
| attributes.volumeY   | Integer |          | 부피 - y                        |
| attributes.volumeH   | Integer |          | 부피 - h                        |
| description          | String  |          | 상품 상세설명                   |
| tags                 | String  |          | 상품 검색 태그, ^로 구분합니다. |
| categories           | Array   |          | 상품 카테고리                   |
| images               | Object  |          | 상품 이미지                     |
| images.list          | Array   |          | 상품 목록이미지 url             |
| images.add           | Array   |          | 상품 추가이미지 url             |

_output_

```json
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
    "regDatetime": "2019-05-29T15:35:54.805Z",
    "options": [],
    "images": [],
    "tags": [],
    "attributes": []
  }
}
```

### 상품 목록

**GET /products**

_input_

| Parameter | Type    | Required | Description                                 |
| --------- | ------- | -------- | ------------------------------------------- |
| start     | Integer |          | 리스트의 offset 입니다. `default: 0`        |
| count     | Integer |          | 응답받을 아이템의 갯수입니다. `default: 10` |

_output_

```json
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

### 상품 조회

**GET /products/:siteProductId**

_output_

```json
{
  "status": "success",
  "data": { Product }
}
```

### 상품 수정

**PATCH /products/:siteProductId**

PATCH로 동작하기 때문에 업데이트가 필요한 필드만 넘겨주시면 됩니다.

_input_

| Parameter            | Type    | Required | Description                     |
| -------------------- | ------- | -------- | ------------------------------- |
| supplyPrice          | Integer |          | 공급가격                        |
| salePrice            | Integer |          | 판매가격                        |
| channelId            | Integer |          | 판매채널 아이디                 |
| attributes           | Object  |          | 상품의 속성                     |
| attributes.name      | String  |          | 상품의 이름                     |
| attributes.userCode1 | String  |          | 상품의 코드 1                   |
| attributes.userCode2 | String  |          | 상품의 코드 2                   |
| attributes.weight    | Integer |          | 상품 무게                       |
| attributes.volumeX   | Integer |          | 부피 - x                        |
| attributes.volumeY   | Integer |          | 부피 - y                        |
| attributes.volumeH   | Integer |          | 부피 - h                        |
| description          | String  |          | 상품 상세설명                   |
| tags                 | String  |          | 상품 검색 태그, ^로 구분합니다. |
| categories           | Array   |          | 상품 카테고리                   |
| images               | Object  |          | 상품 이미지                     |
| images.list          | Array   |          | 상품 목록이미지 url             |
| images.add           | Array   |          | 상품 추가이미지 url             |

_output_

```json
{
  "status": "success",
  "data": { Product }
}
```

### 상품삭제

**DELETE /products/:siteProductId (TBD)**

## 상품 옵션

### 상품 옵션 등록

**POST /products/:siteProductId/options**

_input_

| Parameter  | Type   | Required | Description       |
| ---------- | ------ | -------- | ----------------- |
| optionName | String | `true`   | 상품 옵션명       |
| values     | Array  | `true`   | 상품 옵션 정보    |
| values[x]  | String | `true`   | 상품 옵션 값 이륾 |

```json
[
  { "optionName": "color", "values": ["white", "gold"] },
  { "optionName": "size", "values": ["S", "M", "L"] }
]
```

_output_

```json
{
  "status": "success",
  "data": {
    "items": [Option...]
  }
}
```

### 상품 옵션 목록

**GET /products/:siteProductId/options**

_output_

```json
{
  "status": "success",
  "data": {
    "items": [Option...]
  }
}

```

## 상품 아이템

### 상품 아이템 목록

**GET /products/:siteProductId/items**

_output_

```json
{
  "status": "success",
  "data": {
    "items": [
      Option...
    ],
    "total": 4,
    "start": 0,
    "count": 10
  }
}
```

### 상품 단일 아이템 조회

**GET /products/:siteProductId/items/:productItemId**

_output_

```json
{
  "status": "success",
  "data": {
    "productItemId": 4694133,
    "isManageStock": 0,
    "price": 0,
    "point": 0,
    "productItemUserCode1": "",
    "productItemUserCode2": "",
    "productItemCode": "",
    "barcode": "",
    "qrcodeImage": "",
    "regDatetime": "2019-05-31T11:08:59.000Z",
    "editDatetime": null,
    "deleteDatetime": null,
    "externalStockCode": "",
    "supplyPrice": "0.0000",
    "orderQuantity": 0,
    "quantity": 0,
    "options": [
      {
        "productOptionId": 1,
        "productOptionValueId": 1,
        "option": "색상",
        "value": "빨강"
      },
      {
        "productOptionId": 2,
        "productOptionValueId": 2,
        "option": "사이즈",
        "value": "L"
      }
    ]
  }
}
```

### 상품 아이템 수정

**PATCH /products/:siteProductId/items/:productItemId**

_input_

| Parameter            | Type   | Required | Description |
| -------------------- | ------ | -------- | ----------- |
| barcode              | String |          |             |
| externalStockCode    | String |          |             |
| isManageStock        | String |          |             |
| point                | String |          |             |
| price                | String |          |             |
| productItemCode      | String |          |             |
| productItemUserCode1 | String |          |             |
| productItemUserCode2 | String |          |             |
| qrcodeImage          | String |          |             |
| supplyPrice          | String |          |             |

_output_

```json
{
  "status": "success",
  "data": {
    "productItemId": 1,
    "isManageStock": 0,
    "price": -2000,
    "point": 10000,
    "productItemUserCode1": "",
    "productItemUserCode2": "",
    "productItemCode": "",
    "barcode": "abcdef",
    "qrcodeImage": "abcdefghijk",
    "regDatetime": "2019-06-04T08:47:08.000Z",
    "editDatetime": "2019-06-04T08:47:08.000Z",
    "deleteDatetime": null,
    "externalStockCode": "",
    "supplyPrice": "0",
    "orderQuantity": 0,
    "quantity": 0,
    "options": [
      {
        "productOptionId": 1,
        "productOptionValueId": 1,
        "option": "size",
        "value": "S"
      },
      {
        "productOptionId": 2,
        "productOptionValueId": 2,
        "option": "color",
        "value": "white"
      }
    ]
  }
}
```

### 상품 재고 수정

**PATCH /products/:siteProductId/items/:productItemId/stock**

_input_

| Parameter | Type    | Required | Description                                                             |
| --------- | ------- | -------- | ----------------------------------------------------------------------- |
| type      | String  | `true`   | 추가인 경우 `IN`, 차감인경우 `OUT` 을 넘겨주세요.                       |
| status    | String  | `true`   | ADD / BROKEN / CANCEL / EDIT / EXCHANGE / LOSE / ORDER / RESTORE / SALE |
| quantity  | Integer | `true`   | 변경 수량입니다. type에 따라서 현재 재고에 추가하거나 차감합니다.       |

### 상품 아이템 삭제

아래 API는 상품의 모든 옵션 및 아이템을 삭제하여 초기화 시킵니다.

**DELETE /products/:siteProductId/items**

## 주문

### 주문 상품 목록

**GET /suppliers/:supplierId/order-products**

_input_

| Parameter | Type    | Required | Description                                                                                                                                                     |
| --------- | ------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| start     | Integer |          | 리스트의 offset 입니다. `default: 0`                                                                                                                            |
| count     | Integer |          | 응답받을 아이템의 갯수입니다. `default: 10`                                                                                                                     |
| stateCode | String  |          | 주문 상태 값입니다. payment_complete (결제 완료) / product_request(상품 요청) / shipping(배송 중) / shipping_complete(배송 완료) / cancel(취소). `default: ALL` |
| channelId | Integer |          | 판매채널 아이디입니다. `default: ALL`                                                                                                                           |

_output_

```json
{
  "status": "success",
  "data": {
    "items": [
      {
        "orderId": 1342028,
        "orderProductId": 1790661,
        "productId": 1049156,
        "productItemId": 4683169,
        "stateCode": "PAYMENT_COMPLETE",
        "itemQuantity": 1,
        "orderShippingId": 1614629,
        "siteProductId": 1057338,
        "payAmount": 56430,
        "order": {
          "orderId": 1342028,
          "orderNo": "190527DWC6O14D31X",
          "orderDateTime": "2019-05-27 02:13:01"
        },
        "orderShippingAddress": {
          "orderShippingAddressId": 1614510,
          "orderShippingId": 1614629,
          "shippingCompanyId": 1,
          "shippingCompanyName": "업체별배송",
          "name": "***",
          "phone": "82 ***********",
          "address": "서울 강남구",
          "postcode": "01234"
        },
        "orderShippingMessage": {
          "orderShippingMessageId": 1614585,
          "orderShippingId": 1614629,
          "message": "부재시 경비실에 맡겨 주세요."
        }
      }
    ],
    "total": 638,
    "start": 0,
    "count": 10
  }
}
```

### 주문 상세 조회

**GET /suppliers/:supplierId/orders/:orderId**

_output_

```json
{
  "status": "success",
  "data": {
    "orderId": 1341583,
    "orderNo": "1905260E00O24S31B",
    "memberId": 123456,
    "orderDateTime": "2019-05-26 23:45:17",
    "member": {
      "memberId": 123456,
      "name": "***"
    },
    "orderProducts": [
      {
        "orderId": 1341583,
        "orderProductId": 1790010,
        "productId": 1049156,
        "productItemId": 4683169,
        "stateCode": "PAYMENT_COMPLETE",
        "itemQuantity": 1,
        "orderShippingId": 1614184,
        "siteProductId": 1057338,
        "payAmount": 56430,
        "channelId": 2041,
        "orderShipping": {
          "orderShippingId": 1614184,
          "shippingCompanyId": 1,
          "invoiceNo": "",
          "shippingCompanyName": "업체별배송",
          "orderShippingAddress": {
            "orderShippingId": 1614184,
            "orderShippingAddressId": 1614065,
            "name": "***",
            "phone": "82 ***********",
            "email": "****@gmail.com",
            "postCode": "12345",
            "address": "서울시 송파구"
          },
          "orderShippingMessage": {
            "orderShippingId": 1614184,
            "orderShippingMessageId": 1614140,
            "message": "A동 무인택배함에 넣어주세요 감사합니다"
          }
        },
        "ProductItem": {
          "productItemId": 4683169,
          "ProductItemStock": {
            "orderQuantity": 3,
            "quantity": 5
          }
        }
      }
    ]
  }
}
```

### 상품 요청 처리

**PATCH /suppliers/:supplierId/order-products/packing**

_input_

| Parameter  | Type   | Required | Description       |
| ---------- | ------ | -------- | ----------------- |
| orderProductIds | Array | `true`   | 품목 주문 일련번호       |

```json
{ "orderProductIds": ["2784584"] }
```

_output_

```json
{
  "status": "success",
  "data": {
    "items": [
      {
        "orderId": 1337861,
        "orderProductId": 2784584,
        "productId": 1014459,
        "productItemId": 4656601,
        "stateCode": "PRODUCT_REQUEST",
        "itemQuantity": 1,
        "orderShippingId": 1610439,
        "siteProductId": 1021541,
        "payAmount": 61750,
        "order": {
          "orderId": 1337861,
          "orderNo": "1905250M1AB14M31M",
          "orderDateTime": "2019-05-25 17:43:19"
        }
      }
    ]
  }
}
```

### 배송 처리 (송장 등록)

**PATCH /suppliers/:supplierId/order-products/shipping**

_input_

| Parameter  | Type   | Required | Description       |
| ---------- | ------ | -------- | ----------------- |
| orderProductIds | Array | `true`   | 품목 주문 일련번호       |
| shippingCompanyId | Integer | `true`   | 배송 업체 일련번호       |
| invoiceNo | String | `true`   | 송장 번호       |

```json
{
  "orderProductIds": ["2784584"],
  "shippingCompanyId": 1,
  "invoiceNo": "123456789034"
}
```

_output_

```json
{
  "status": "success",
  "data": {
    "items": [
      {
        "orderId": 1337861,
        "orderProductId": 2784584,
        "productId": 1014459,
        "productItemId": 4656601,
        "stateCode": "SHIPPING",
        "itemQuantity": 1,
        "orderShippingId": 1610439,
        "siteProductId": 1021541,
        "payAmount": 61750,
        "order": {
          "orderId": 1337861,
          "orderNo": "1905250M1AB14M31M",
          "orderDateTime": "2019-05-25 17:43:19"
        }
      }
    ]
  }
}
```

### 취소 처리

**PATCH /suppliers/:supplierId/order-products/cancel**

_input_

| Parameter  | Type   | Required | Description       |
| ---------- | ------ | -------- | ----------------- |
| orderProductIds | Array | `true`   | 품목 주문 일련번호       |

```json
{ "orderProductIds": ["2784584"] }
```

_output_

```json
{
  "status": "success",
  "data": {
    "items": [
      {
        "orderId": 1337861,
        "orderProductId": 2784584,
        "productId": 1014459,
        "productItemId": 4656601,
        "stateCode": "CANCEL",
        "itemQuantity": 1,
        "orderShippingId": 1610439,
        "siteProductId": 1021541,
        "payAmount": 61750,
        "order": {
          "orderId": 1337861,
          "orderNo": "1905250M1AB14M31M",
          "orderDateTime": "2019-05-25 17:43:19"
        }
      }
    ]
  }
}
```

## 교환 반품

### 교환 / 반품 목록 조회

**GET /suppliers/:supplierId/returns[?channelId=&start=&count]**

_input_

| Parameter | Type    | Required | Description                                 |
| --------- | ------- | -------- | ------------------------------------------- |
| start     | Integer |          | 리스트의 offset 입니다. `default: 0`        |
| count     | Integer |          | 응답받을 아이템의 갯수입니다. `default: 10` |
| channelId | Integer |          | 판매채널 아이디입니다. `default: ALL`       |

_output_

```json
{
  "status": "success",
  "data": {
    "items": [
      ReturnRequest...
    ],
    "total": 2237,
    "start": 0,
    "count": 10
  }
}
```

### 교환 / 반품 단일아이템 조회

**GET /suppliers/:supplierId/returns/`:orderReturnRequestId`**

_output_

```json
{
  "status": "success",
  "data": ReturnRequest
}
```

### 반품상품 배송등록 

**PATCH /suppliers/`:supplierId`/returns/`:orderReturnRequestId`/return-products/`:orderReturnRequestOrderProductId`/invoice**

_input_

| Parameter         | Type    | Required | Description   |
| ----------------- | ------- | -------- | ------------- |
| invoiceNo         | String  | `true`   | 송장번호      |
| shippingCompanyId | Integer | `true`   | 배송회사 번호 |

_output_

```json
{
  "status": "success",
  "data": {
    "channelReturnShippingPrice": 5000,
    "isShippingComplete": "N",
    "orderReturnRequestOrderProductId": 55177,
    "orderProductId": 1777076,
    "quantity": 1,
    "orderReturnRequestId": 49668,
    "statusCode": "COLLECT",
    "channelId": 123,
    "supplierId": 456,
    "invoiceNo": 123,
    "shippingCompanyId": 2,
    "completeDatetime": null
  }
}
```

### 교환상품 배송등록 (송장등록)

**PATCH /suppliers/`:supplierId`/returns/`:orderReturnRequestId`/return-products/`:orderReturnRequestOrderProductId`/exchange-products/`:exchangeProductId`/invoice**

_input_

| Parameter         | Type    | Required | Description   |
| ----------------- | ------- | -------- | ------------- |
| invoiceNo         | String  | `true`   | 송장번호      |
| shippingCompanyId | Integer | `true`   | 배송회사 번호 |

_output_

```json
{
  "status": "success",
  "data": {
    "exchangeProductId": 13878,
    "orderReturnRequestId": 49668,
    "orderReturnRequestOrderProductId": 55177,
    "siteProductId": 1050725,
    "orderProductId": 1777076,
    "quantity": 1,
    "productItemId": 4246920,
    "invoiceNo": 123,
    "shippingCompanyId": 2,
    "isShippingComplete": "N",
    "deliveryStartDatetime": "2019-06-21T05:37:17.335Z",
    "deliveryCompleteDatetime": null
  }
}
```

### 반품상품 상태 변경

**PATCH /suppliers/`:supplierId`/returns/`:orderReturnRequestId`/return-products/`:orderReturnRequestOrderProductId`/status**

_input_

| Parameter | Type   | Required | Description                      |
| --------- | ------ | -------- | -------------------------------- |
| status    | String | `true`   | 변경할 상태 'COMPLETE', 'REJECT' |

_output_

```json
{
  "status": "success",
  "data": {
    "channelReturnShippingPrice": 5000,
    "isShippingComplete": "Y",
    "orderReturnRequestOrderProductId": 55177,
    "orderProductId": 1777076,
    "quantity": 1,
    "orderReturnRequestId": 49668,
    "statusCode": "COMPLETE",
    "channelId": 282,
    "supplierId": 271,
    "invoiceNo": "123",
    "shippingCompanyId": 2,
    "completeDatetime": "2019-06-21T05:36:43.000Z"
  }
}
```

## 게시판

### 공지사항

**GET /suppliers/:supplierId/boards/notices**

_description_

입점사 전용 공지사항 게시판입니다.

_output_

```json
{
    "status": "success",
    "data": {
        "items": [
            {
                "boardId": 2,
                "boardArticleId": 3579,
                "supplierId": 0,
                "siteProductId": null,
                "orderProductId": null,
                "type": "ETC",
                "isFinish": 0,
                "subject": "[알림] 서울스토어X샵링커 시스템 연동 안내",
                "contents": "안녕하세요 서울스토어 입니다.<br />이번에 샵링커와 시스템 연동을 완료 하였습니다.<br />앞으로 많은 이용 바랍니다.<br />시스템 연동방법은 샵링커 사이트에서 확인 가능합니다.<br /><br />현재 연동 가능한 SCM 업체는 사방넷,이지어드민,샵링커 입니다.<br />해당 SCM 사용 입점사들께서는 시스템 연동을 통해 업무에 도움이<br />되셨으면 합니다.<br /><br />감사합니다.",
                "adminId": 472,
                "regDatetime": "2018-05-02T06:45:32.000Z",
                "editDatetime": "2018-05-02T06:45:32.000Z",
                "typeText": "기타",
                "writer": "서울스토어",
                "supplier": {
                    "name": "입점사 전체"
                },
                "siteProduct": {},
                "order": {}
            },
            ...
            
        ],
        "start": 0,
        "count": 10,
        "total": 8
    }
}

```

### 입점사 문의 게시판

**GET /suppliers/:supplierId/boards/qna**

_description_

서울스토어와 입점사 간의 게시판 입니다.

_output_

```json
{
    "status": "success",
    "data": {
        "items": [
            {
                "boardId": 1,
                "boardArticleId": 5696,
                "supplierId": 761,
                "siteProductId": 1050664,
                "orderProductId": 1731844,
                "type": "RETURN",
                "isFinish": 1,
                "subject": "[서울스토어] 반품건",
                "contents": "안녕하세요:)<br />자녀분 주문건으로 서울스토어에서 반품접수가 불가능하다고 하셔서, 게시판 문의글에 답변 주신 반품처 주소지로 5천원 동봉하여 발송 요청 드렸습니다.<br />17일 배송완료건이나 전산상 접수내역 확인이 안되어 전달드리니, 반품입고 확인되시면 환불처리 부탁드리겠습니다.",
                "adminId": 1167,
                "regDatetime": "2019-05-23T02:18:45.000Z",
                "editDatetime": "2019-05-23T02:18:45.000Z",
                "typeText": "반품",
                "writer": "서울스토어",
                "supplier": {
                    "name": "주식회사 올아이원트"
                },
                "siteProduct": {
                    "siteProductId": 1050664,
                    "siteProductName": "나이키 반바지 (Swoosh)",
                    "channelId": 1174,
                    "channelName": "나이키"
                },
                "order": {
                    "orderId": 1301968,
                    "orderNo": "1905126XACC14Q31O",
                    "productName": "나이키 반바지 (Swoosh)",
                    "productItemId": 4228623,
                    "productItemOptionValues": [
                        {
                            "productOptionId": 2057051,
                            "productOptionValueId": 4925087,
                            "productOptionDescription": "색상",
                            "productOptionValueDescription": "블랙"
                        },
                        {
                            "productOptionId": 2057052,
                            "productOptionValueId": 4925094,
                            "productOptionDescription": "사이즈",
                            "productOptionValueDescription": "80 (95 size)"
                        }
                    ]
                }
            }
        ],
        "start": 0,
        "count": 10,
        "total": 1
    }
}
```

### 고객 주문 문의

**GET /suppliers/:supplierId/boards/orders**

_output_

```json
{
    "status": "success",
    "data": {
        "items": [
            {
                "boardArticleId": 347990,
                "boardId": 11,
                "boardCategoryId": 37,
                "subject": "배송문의요",
                "memberId": 1273218,
                "editDatetime": "2019-07-04T05:22:53.000Z",
                "commentCount": 5,
                "siteProductId": 1012643,
                "orderProductId": 1722743,
                "regDatetime": "2019-05-09T15:08:52.000Z",
                "boardCategoryText": "배송",
                "writer": "G1",
                "siteProduct": {
                    "siteProductId": 1012643,
                    "siteProductName": "SEXY CHAMPION DUCK2",
                    "channelId": 1098,
                    "channelName": "섹시챔피온"
                },
                "order": {
                    "orderId": 1295803,
                    "orderNo": "190510DB35L14N31I",
                    "productName": "SEXY CHAMPION DUCK2",
                    "productItemId": 3110682,
                    "productItemOptionValues": [
                        {
                            "productOptionId": 1766666,
                            "productOptionValueId": 3978523,
                            "productOptionDescription": "사이즈",
                            "productOptionValueDescription": "L"
                        }
                    ]
                },
                "contents": "주문한 두 제품 내일 바로 당일배송인가요?"
            },
            ...
        ],
        "start": 0,
        "count": 10,
        "total": 35
    }
}
```

###  고객 상품 문의

**GET /suppliers/:supplierId/boards/orders**

_output_

```
고객 주문 문의와 동일 합니다.
```


### 입점사 게시판 질문 타입

**GET /boards/types**

_output_

```json
```


### 고객 문의 게시판 카테고리

**GET /boards/categories**

_output_

```json
```

### 입점사 게시판 게시물 등록

**POST /suppliers/:supplierId/boards/qna**

_input_

| Parameter | Type   | Required | Description                      |
| --------- | ------ | -------- | -------------------------------- |
| orderProductId    | Number | `true`   | 주문 상품 시퀀스 |
| type | String |   | default `ETC` |
| subject | String | `true` | 게시 제목 |
| contents | String | `true` | 게시 내용 |


_output_

```json
```


### 입점사 게시판/고객 게시판 문의 답변

**POST /suppliers/:supplierId/boards/[qna|products|orders]/articles/:boardArticleId**

_input_

| Parameter | Type   | Required | Description                      |
| --------- | ------ | -------- | -------------------------------- |
| contents | String | `true` | 답변 내용 |

_output_

```json
```
