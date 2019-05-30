# 부록

### 상품 기본 형태

서울스토어 API 응답중 상품에 나타나는 필드는 다음을 의미합니다.

| Parameter             | Description |
|-----------------------|---------|
| siteProduct           | 사이트에 등록되는 상품의 id 입니다. 웹사이트에서 이 아이디로 상품을 조회할 수 있습니다. eg. `https://www.seoulstore.com/products/9314/detail` |
| supplierId            | 상품을 등록한 입점사의 id 입니다. |
| isSale                | 상품이 사이트에서 판매중인지를 보여줍니다. 판매중은 `1`로 표시되고, 판매가 중지된 상품은 `0`으로 표시됩니다. |
| IsDisplay             | 진열여부를 보여줍니다. `1`은 사이트에 보여지고 있을때 나타나는 값이고 `0`은 진열중이지 않을 때 나타납니다.   |
| minimum.              | 최소 구매수량  |
| maximum               | 최대 구매수량  |
| regDatetime           | 상품이 등록된 날짜입니다.  |
| editDatetime          | 상품이 수정된 날짜입니다.  |
| deleteDatetime        | 상품이 삭제된 날짜입니다.  |
| discountRate          | 할인 비율 |
| discountBeginDatetime | 할인을 시작하는 시간입니다. |
| discountEndDatetime   | 할인을 종료하는 시간입니다. |
| discountPrice         | 할인가  |
| isIgnorePromotion     | 프로모션 무시여부   |
| channelId             | 상품이 속해있는 채널의 id  |
| parentChannelId       | 부모 채널 id   |
| orderCountSp          | 주문 수   |
| isLock                | 상품 수정 금지여부 |
| confirmStatus         | 상품 승인여부, 0:요청 / 1:재승인요청 / 2:승인 / 3:승인거절 |
| sortDatetime          | 상품 진열 정렬 순서 |
| attributes            | 상품 추가정보 |
| description           | 상품 상세설명 |
| options               | 상품 옵션 Array |
| options.option        | 옵션 이름 ex) 사이즈 |
| options.value         | 옵션 값 ex) S / M / L |
| options.productItemId | 옵션 id |
| options.isManageStock | 재고 사용여부, 0: 사용안함 / 1: 사용 |
| options.quantity      | 수량 |
| options.orderQuantity | 주문수량 |
| options.price | 옵션 추가금액 |

**상품 응답 데이터 예제**

```
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
  "attributes": {"name": "BETTER ORIGINAL FOOD (가자미베지믹스)"},
  "description": ""
  "options": [
      {
        "option": "OPTION",
        "value": "선택1",
        "productItemId": 1234,
        "isManageStock": 0,
        "quantity": 0,
        "orderQuantity": 0,
        "price": 5000,
      }
    ]
}
```