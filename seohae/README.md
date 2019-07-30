# SEOULSTORE's SEOHAE API Documentation

이 문서는 서울스토어 서해API 입니다.
서울스토어에서 제공하는 서비스 중, 일부만 발췌하여 문서화 되었습니다.

## API 접근권한

서울스토어 서해API에 접근하기 위해서는 기본적으로 access 키값이 있어야 합니다. 키값에 대해서는 별도 문의를 통해 알려 드립니다.

## API 목록

### 카테고리

**GET /seohae/categories**

_out put_

```json
{
    "categories": [
        {
            "siteCategoryId": 1000,
            "isDisplay": 1,
            "parentSiteCategoryId": 0,
            "sortOrder": 0,
            "name": "여성",
            "child": []
        },
    ]
}
```

### 상품 조회

**GET /seohae/products/list**

_input_

| Parameter | Type    | Required | Description                                 |
| --------- | ------- | -------- | ------------------------------------------- |
| start     | Integer |          | 리스트의 offset 입니다. `default: 0`        |
| count     | Integer |          | 응답받을 아이템의 갯수입니다. `default: 10` |

_out put_

```json
{
    "total": 10000,
    "start": 0,
    "count": 5,
    "products": [
        {
            "productId": 1084068,
            "brandId": 959,
            "channelId": 1504,
            "isDeleted": 0,
            "isSoldOut": false,
            "salePrice": 8000,
            "minimum": 0,
            "maximum": 0,
            "categoryId": 1274,
            "channelName": "에뛰드하우스",
            "categoryName": "뷰티",
            "productName": "투톤 트리트먼트 헤어 컬러",
            "productDescription": "<table id=\"Table_01\" class=\" cke_show_border\" border=\"0\" cellspacing=\"0\" cellpadding=\"0\">\n<tbody>\n<tr>\n<td><img src=\"http://etude.speedgabia.com/webcatalogue/2018/06/two_tone_hair/images/two_tone_hair_img1.jpg\" data-cke-saved-src=\"http://etude.speedgabia.com/webcatalogue/2018/06/two_tone_hair/images/two_tone_hair_img1.jpg\" /></td>\n</tr>\n<tr>\n<td><img src=\"http://etude.speedgabia.com/webcatalogue/2018/06/two_tone_hair/images/two_tone_hair_img2.jpg\" data-cke-saved-src=\"http://etude.speedgabia.com/webcatalogue/2018/06/two_tone_hair/images/two_tone_hair_img2.jpg\" /></td>\n</tr>\n<tr>\n<td><img src=\"http://etude.speedgabia.com/webcatalogue/2018/06/two_tone_hair/images/two_tone_hair_img3.jpg\" data-cke-saved-src=\"http://etude.speedgabia.com/webcatalogue/2018/06/two_tone_hair/images/two_tone_hair_img3.jpg\" /></td>\n</tr>\n<tr>\n<td><img src=\"http://etude.speedgabia.com/webcatalogue/2018/06/two_tone_hair/images/two_tone_hair_img4.jpg\" data-cke-saved-src=\"http://etude.speedgabia.com/webcatalogue/2018/06/two_tone_hair/images/two_tone_hair_img4.jpg\" /></td>\n</tr>\n<tr>\n<td><img src=\"http://etude.speedgabia.com/webcatalogue/2018/06/two_tone_hair/images/two_tone_hair_img5.jpg\" data-cke-saved-src=\"http://etude.speedgabia.com/webcatalogue/2018/06/two_tone_hair/images/two_tone_hair_img5.jpg\" /></td>\n</tr>\n<tr>\n<td><img src=\"http://etude.speedgabia.com/webcatalogue/2018/06/two_tone_hair/images/two_tone_hair_img6.jpg\" data-cke-saved-src=\"http://etude.speedgabia.com/webcatalogue/2018/06/two_tone_hair/images/two_tone_hair_img6.jpg\" /></td>\n</tr>\n<tr>\n<td><img src=\"http://etude.speedgabia.com/webcatalogue/2018/06/two_tone_hair/images/two_tone_hair_img7.jpg\" data-cke-saved-src=\"http://etude.speedgabia.com/webcatalogue/2018/06/two_tone_hair/images/two_tone_hair_img7.jpg\" /></td>\n</tr>\n<tr>\n<td><img src=\"http://etude.speedgabia.com/webcatalogue/2018/06/two_tone_hair/images/two_tone_hair_img8.gif\" data-cke-saved-src=\"http://etude.speedgabia.com/webcatalogue/2018/06/two_tone_hair/images/two_tone_hair_img8.gif\" /></td>\n</tr>\n<tr>\n<td><img src=\"http://etude.speedgabia.com/webcatalogue/2018/06/two_tone_hair/images/two_tone_hair_img9.jpg\" data-cke-saved-src=\"http://etude.speedgabia.com/webcatalogue/2018/06/two_tone_hair/images/two_tone_hair_img9.jpg\" /></td>\n</tr>\n<tr>\n<td><img src=\"http://etude.speedgabia.com/webcatalogue/2018/06/reset_tissue/images/reset_tissue_co.jpg\" data-cke-saved-src=\"http://etude.speedgabia.com/webcatalogue/2018/06/reset_tissue/images/reset_tissue_co.jpg\" /></td>\n</tr>\n</tbody>\n</table>",
            "productTags": [
                "에뛰드",
                "에뛰드하우스",
                "투톤",
                "헤어컬러",
                "염색",
                "염색약"
            ],
            "images": {
                "list": "https://images.seoulstore.com/products/c60e2ea0437ab30a15363dc311989b71.jpg"
            }
        },
        
        ...
    ]
}
```

**GET /seohae/products/:productId**

_out put_

```json
{
    "product": {
        "productId": 963700,
        "brandId": 443,
        "channelId": 470,
        "isDeleted": 0,
        "isSoldOut": false,
        "salePrice": 42000,
        "settlementPrice": 37800,
        "minimum": 0,
        "maximum": 0,
        "categoryId": 1000,
        "channelName": "어나더프레임",
        "categoryName": "여성",
        "productName": "[어나더프레임] ANOTHER FRAME - AF LABEL STRIPE T-SHIRT (BLUE/BEIGE) 긴팔 긴팔티 티셔츠",
        "productDescription": "",
        "productTags": [
            "쭉티",
            "긴팔티",
            "긴팔티셔츠",
            "스트라이프",
            "티셔츠",
            "긴팔",
            "단가라"
        ],
        "images": {
            "add": []
        },
        "items": {
            "options": [
                {
                    "productOptionId": 2358501,
                    "productOptionText": "SIZE",
                    "optionValues": [
                        {
                            "productOptionValueId": 5958517,
                            "productId": 957958,
                            "productOptionId": 2358501,
                            "isDeleted": 0,
                            "sortOrder": 0,
                            "optionValueText": "MF"
                        },
                        {
                            "productOptionValueId": 5958518,
                            "productId": 957958,
                            "productOptionId": 2358501,
                            "isDeleted": 0,
                            "sortOrder": 1,
                            "optionValueText": "BF"
                        }
                    ]
                }
            ],
            "values": [
                {
                    "productItemId": 5638099,
                    "addPrice": 0,
                    "salePrice": 42000,
                    "settlementPrice": 37800,
                    "barcode": "",
                    "isSoldOut": false,
                    "optionValueIds": [
                        5958517
                    ]
                },
                {
                    "productItemId": 5638100,
                    "addPrice": 0,
                    "salePrice": 42000,
                    "settlementPrice": 37800,
                    "barcode": "",
                    "isSoldOut": false,
                    "optionValueIds": [
                        5958518
                    ]
                }
            ]
        }
    }
}
```
