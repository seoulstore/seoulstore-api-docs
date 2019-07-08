# FAQ

자주 묻는 질문에 대한 답변입니다.

### Q. 서울스토어 상품 관련 아이디는 무엇을 의미하나요?

A. 서울스토어 API에서 볼 수 있는 각각의 Id들은 다음을 의미합니다. 

**사이트 상품 아이디 (siteProductId)**

서울스토어 사이트에 전시되는 상품의 아이디 입니다. 서울스토어 웹사이트에서 이 아이디로 상품을 조회할 수 있습니다. 
eg. https://www.seoulstore.com/products/1034006/detail, url의 `1034006`이 `siteProductId`가 됩니다. 

**상품 아이디 (productId)**

사이트 상품의 원본이 되는 데이터입니다. 상품에 대한 옵션과 아이템은 모두 상품 아이디를 참고하고 있습니다. 

**상품 옵션 (productOptionId)**

서울스토어에서 상품의 옵션은 색상, 사이즈 등과 같이 상품을 구성하는 요소를 가리킵니다. 상품옵션에는 각각에 해당하는 값(productOptionValueId)들을 입력할 수 있고 이것을 조합하여 완성된 상품을 나타내는 상품 아이템 (productItemId)을 만들고 있습니다.

예를들어 상품 옵션에는 색상과 사이즈가 있고, 색상의 값이 빨강과 파랑, 사이즈의 값이 S, M, L이 있다고 생각을 하면 빨강-S, 빨강-M, 빨강-L, 파랑-S, 파랑-M, 파랑-L 총 여섯개의 상품 아이템(productItem)이 생성됩니다. 상품 아이템은 실제 물건을 나타내므로 재고는 여기에 설정할 수 있게 됩니다.

**상품 아이템 (productItemId)**

상품 아이템은 입력된 옵션의 조합으로 실제 고객이 주문하고 받는 상품입니다. 따라서 이 데이터는 상품의 수량이나 바코드 등을 설정할 수 있습니다. 

### Q. 서울스토어에 상품을 생성하는 순서는 어떻게 되나요?

A. 서울스토어에 상품을 생성하는 순서는 다음과 같은 순서로 해주시면 됩니다. 

* 상품 등록: POST /products 
  이 요청은 siteProductId를 반환합니다. 이 아이디는 상품의 조회, 수정을 할 때 이용할 수 있습니다.
* 상품 옵션 등록: POST /products/:siteProductId/options
  이 요청은 상품에 옵션을 입력하게 됩니다. 
* 상품 아이템 조회: GET /products/:siteProductId/items
  이 요청은 입력된 옵션으로 생성된 상품의 아이템을 조회할 수 있습니다. productItemId들을 반환합니다.
* 상품 아이템 수정: PATCH /products/:siteProductId/items/:productItemId
  바코드나 추가금액 설정 등은 이 API를 통해서 할 수 있습니다.
* 상품 재고 수정: PATCH /products/:siteProductId/items/:productItemId/stock
  상품의 재고를 변경할 수 있습니다.

### Q. 아직 승인되지 않은 상품을 사이트에서 미리 볼 수 있나요?

A. 상품 URL 뒤에 `/force`를 붙여서 브라우저 주소창에 입력하면 아직 승인 나지 않은 상품도 미리 열람할 수 있습니다.

eg. 
* 스테이지의 경우 https://yangju.seoulstore.com/products/`:siteProductId`/detail/force
* 프로덕션의 경우 https://www.seoulstore.com/products/`:siteProductId`/detail/force
