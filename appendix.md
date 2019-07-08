# 부록

### 상품 기본 형태

서울스토어 API 응답중 상품에 나타나는 필드는 다음을 의미합니다.

| Parameter             | Description                                                                                                                                   |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| siteProduct           | 사이트에 등록되는 상품의 id 입니다. 웹사이트에서 이 아이디로 상품을 조회할 수 있습니다. eg. `https://www.seoulstore.com/products/9314/detail` |
| supplierId            | 상품을 등록한 입점사의 id 입니다.                                                                                                             |
| isSale                | 상품이 사이트에서 판매중인지를 보여줍니다. 판매중은 `1`로 표시되고, 판매가 중지된 상품은 `0`으로 표시됩니다.                                  |
| IsDisplay             | 진열여부를 보여줍니다. `1`은 사이트에 보여지고 있을때 나타나는 값이고 `0`은 진열중이지 않을 때 나타납니다.                                    |
| minimum.              | 최소 구매수량                                                                                                                                 |
| maximum               | 최대 구매수량                                                                                                                                 |
| regDatetime           | 상품이 등록된 날짜입니다.                                                                                                                     |
| editDatetime          | 상품이 수정된 날짜입니다.                                                                                                                     |
| deleteDatetime        | 상품이 삭제된 날짜입니다.                                                                                                                     |
| discountRate          | 할인 비율                                                                                                                                     |
| discountBeginDatetime | 할인을 시작하는 시간입니다.                                                                                                                   |
| discountEndDatetime   | 할인을 종료하는 시간입니다.                                                                                                                   |
| discountPrice         | 할인가                                                                                                                                        |
| isIgnorePromotion     | 프로모션 무시여부                                                                                                                             |
| channelId             | 상품이 속해있는 채널의 id                                                                                                                     |
| parentChannelId       | 부모 채널 id                                                                                                                                  |
| orderCountSp          | 주문 수                                                                                                                                       |
| isLock                | 상품 수정 금지여부                                                                                                                            |
| confirmStatus         | 상품 승인여부, 0:요청 / 1:재승인요청 / 2:승인 / 3:승인거절                                                                                    |
| sortDatetime          | 상품 진열 정렬 순서                                                                                                                           |
| attributes            | 상품 추가정보                                                                                                                                 |
| description           | 상품 상세설명                                                                                                                                 |
| items                 | 상품 item Array                                                                                                                               |
| items.options         | 상품 item 옵션 Array                                                                                                                          |
| items.options.option  | 상품 item 옵션명                                                                                                                              |
| items.options.value   | 상품 item 옵션값                                                                                                                              |
| items.productItemId   | item id                                                                                                                                       |
| items.isManageStock   | 재고 사용여부, 0: 사용안함 / 1: 사용                                                                                                          |
| items.quantity        | 수량                                                                                                                                          |
| items.orderQuantity   | 주문수량                                                                                                                                      |
| items.price           | item 추가금액                                                                                                                                 |
| images                | 상품 이미지 Object                                                                                                                            |
| images.list           | 상품 목록 이미지 url Array                                                                                                                    |
| images.add            | 상품 추가 이미지 url Array                                                                                                                    |
| tags                  | 상품 검색 태그 Array                                                                                                                          |

**상품 응답 데이터 예제**

```json
{
  "siteProductId": 9314,
  "supplierId": 220,
  "isDeleted": 0,
  "isSale": 1,
  "isDisplay": 1,
  "supplyPrice": "78000.0000",
  "salePrice": "78000.0000",
  "minimum": 1,
  "maximum": 0,
  "regDatetime": "2015-12-10T07:22:01.000Z",
  "editDatetime": "2016-08-24T06:17:53.000Z",
  "deleteDatetime": null,
  "discountRate": "70.00",
  "discountBeginDatetime": "2017-08-07T16:00:00.000Z",
  "discountEndDatetime": "2017-08-17T20:00:00.000Z",
  "discountPrice": "23400.0000",
  "isIgnorePromotion": 0,
  "channelId": 231,
  "parentChannelId": 0,
  "parentSiteProductId": 0,
  "orderCountSp": 1,
  "isLock": 0,
  "confirmStatus": 2,
  "sortDatetime": "2015-12-10T07:22:01.000Z",
  "attributes": { "name": "BETTER ORIGINAL FOOD (가자미베지믹스)" },
  "description": "",
  "items": [
    {
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
          "option": "색상",
          "value": "빨강"
        },
        {
          "option": "사이즈",
          "value": "L"
        }
      ]
    }
  ],
  "images": {
    "add": ["https://images"],
    "list": ["https://images"]
  },
  "tags": ["태그", "태그2"]
}
```

### 교환/반품 기본 형태

서울스토어 API 응답중 교환/반품에 나타나는 필드는 다음을 의미합니다.

| Parameter                                                               | Description               |
| ----------------------------------------------------------------------- | ------------------------- |
| orderNo                                                                 | 주문 코드                 |
| memberName                                                              | 주문자                    |
| orderReturnRequestCode                                                  | 반품 코드                 |
| orderReturnRequestId                                                    | 반품 번호                 |
| memberId                                                                | 회원번호                  |
| regDatetime                                                             | 반품 신청일시             |
| statusCode                                                              | 반품 상태 코드            |
| requestType                                                             | 교환/반품 타입            |
| completeDatetime                                                        | 교환/반품 완료일시        |
| isDeleted                                                               | 삭제여부                  |
| OrderReturnRequestAddress                                               | 배송지 정보               |
| OrderReturnRequestAddress.phone                                         | 수령인 연락처             |
| OrderReturnRequestAddress.name                                          | 수령인                    |
| OrderReturnRequestAddress.postcode                                      | 우편번호                  |
| OrderReturnRequestAddress.address                                       | 주소                      |
| OrderReturnRequestAddress.detailAddress                                 | 상세주소                  |
| OrderReturnRequestAddress.message                                       | 요청 메시지               |
| Memo                                                                    | 교환 반품 사유, 설명      |
| Memo.REASON                                                             | 교환 반품 사유            |
| Memo.CONTENTS                                                           | 교환 반품 설명            |
| OrderReturnRequestFile                                                  | 첨부파일                  |
| OrderReturnRequestOrderProduct                                          | 반품상품 정보             |
| OrderReturnRequestOrderProduct.supplierName                             | 반품상품 입점사 명        |
| OrderReturnRequestOrderProduct.channelName                              | 반품상품 채널 명          |
| OrderReturnRequestOrderProduct.productName                              | 반품상품 상품명           |
| OrderReturnRequestOrderProduct.productItemId                            | 반품상품 아이템 번호      |
| OrderReturnRequestOrderProduct.item                                     | 반품상품 옵션, 옵션값     |
| OrderReturnRequestOrderProduct.isShippingComplete                       | 반품상품 배송 완료 여부   |
| OrderReturnRequestOrderProduct.channelId                                | 반품상품 채널id           |
| OrderReturnRequestOrderProduct.completeDatetime                         | 반품상품 배송 완료일시    |
| OrderReturnRequestOrderProduct.invoiceNo                                | 반품상품 송장번호         |
| OrderReturnRequestOrderProduct.orderProductId                           | 반품상품 상품 주문번호    |
| OrderReturnRequestOrderProduct.quantity                                 | 반품상품 수량             |
| OrderReturnRequestOrderProduct.shippingCompanyId                        | 반품상품 배송사 번호      |
| OrderReturnRequestOrderProduct.statusCode                               | 반품상품 배송상태         |
| OrderReturnRequestOrderProduct.supplierId                               | 반품상품 입점사 id        |
| OrderReturnRequestOrderProduct.ExchangeProduct                          | 반품상품 교환상품 정보    |
| OrderReturnRequestOrderProduct.ExchangeProduct.quantity                 | 교환상품 수량             |
| OrderReturnRequestOrderProduct.ExchangeProduct.productItemId            | 교환상품 아이템 번호      |
| OrderReturnRequestOrderProduct.ExchangeProduct.invoiceNo                | 교환상품 송장번호         |
| OrderReturnRequestOrderProduct.ExchangeProduct.shippingCompanyId        | 교환상품 배송사 번호      |
| OrderReturnRequestOrderProduct.ExchangeProduct.isShippingComplete       | 교환상품 배송사 완료 여부 |
| OrderReturnRequestOrderProduct.ExchangeProduct.deliveryStartDatetime    | 교환상품 배송 시작일시    |
| OrderReturnRequestOrderProduct.ExchangeProduct.deliveryCompleteDatetime | 교환상품 배송 완료일시    |
| OrderReturnRequestOrderProduct.ExchangeProduct.item                     | 교환상품 옵션, 옵션값     |

**교환/반품 응답 데이터 예제**

```json
{
  "orderNo": "1905153R8AR14L31M",
  "memberName": "가나다",
  "orderReturnRequestCode": "RT_49134_20190520",
  "orderReturnRequestId": 49134,
  "orderId": 1310122,
  "memberId": 1276135,
  "regDatetime": "2019-05-20T02:26:03.000Z",
  "statusCode": "COMPLETE",
  "requestType": "REFUND",
  "completeDatetime": "2019-05-23T06:01:20.000Z",
  "isDeleted": 0,
  "OrderReturnRequestAddress": {
    "phone": "01044670823",
    "memberId": 1234,
    "name": "가나다",
    "postcode": "34359",
    "address": "서울 강남구 도산대로 210",
    "detailAddress": "의화빌딩 5층",
    "message": "오늘 늦게 들어갈 것 같아서 택배기사님을 오늘 말고 내일 보내주실 수 있으시면 감사하겠습니다. "
  },
  "Memo": {
    "REASON": "PRODUCT_FAULT",
    "CONTENTS": "로고 프린팅이 제대로 찍히지 않은 것 같습니다. 상세 설명에 있는 사진에는 선명하게 프린팅이 되어있는데 받은 상품은 프린팅 된 부분들이 거의 다 깔끔하지 않게 되어있습니다."
  },
  "OrderReturnRequestFile": [
    "media_order_test/a7fb0a341108eaf636c07cf58d436390.jpeg"
  ],
  "OrderReturnRequestOrderProduct": [
    {
      "supplierName": "서울스토어",
      "channelName": "서울스토어",
      "productName": "[서울스토어단독] 치어 서클 로고 티셔츠",
      "productItemId": 4125275,
      "item": {
        "색상": "코발트",
        "사이즈": "L"
      },
      "isShippingComplete": "Y",
      "channelId": 282,
      "completeDatetime": "2019-05-23T06:01:20.000Z",
      "invoiceNo": "123456789",
      "orderProductId": 1743950,
      "quantity": 1,
      "shippingCompanyId": 3,
      "statusCode": "COMPLETE",
      "supplierId": 271,
      "ExchangeProduct": {
        "quantity": 1,
        "productItemId": 4125275,
        "invoiceNo": null,
        "shippingCompanyId": null,
        "isShippingComplete": "N",
        "deliveryStartDatetime": null,
        "deliveryCompleteDatetime": null,
        "item": {
          "색상": "코발트",
          "사이즈": "L"
        }
      }
    }
  ]
}
```
