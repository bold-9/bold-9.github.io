# 자사몰 연동 API

- 신규 주문 & 확정된 주문(발주처리 된 주문)

- 주문 확정하기

- 송장 정보 등록

* 취소 주문 확인

  - 취소 된 주문
  - 취소 요청 된 주문

---

## 신규 주문 & 확정된 주문(발주처리 된 주문)

> order_status에 맞는 주문 데이터 조회

**요청 파라미터**

```js
start_date; // 주문 조회 시작 날짜 (예_2021-01-01T00:00:00)
end_date; // 주문 조회 종료 날짜
order_status; // 주문 상태 (예_ 결제완료, 발주처리(주문확정), 배송중 등)
date_type; // 검색 날짜 유형 (예_ 주문완료일, 결제완료일)
```

**응답 데이터**

```js
  {
	  orderNumber    // 주문번호
	  orderedDate   // 주문완료 날짜
	  paidDate    // 결제완료 날짜
	  senderName   // 보내는분
	  senderTel   // 보내는분 전화번호
	  senderTel2? // 보내는분 전화번호2
	  receiverName // 받는분
	  receiverTel // 받는분 전화번호
	  receiverTel2? // 받는분 전화번호2
	  zipCode // 우편주소
	  receiverAddress // 받는분 주소
	  shippingMemo // 배송 메모
	  productNumber // 상품 번호
	  productName // 상품명
	  productOptionNumber? // 상품 옵션 번호
	  productOptionName // 상품 옵션명
	  productQuantity // 상품 수량
	  productPriceAmount // 배송비를 제외한 상품 총 가격
	  isShippingFeePaid // 배송비 선결제 여부
	  shippingFee // 배송비
	  isOverseas // 해외배송여부
	  remoteShippingFee // 제주/도서 추가 배송비
	  productPrice? // 판매 단가
	  salesCommissionFee? // 판매 수수료
	  sellerDiscountPriceAmount? // 판매자 할인 금액
	  mallDiscountPriceAmount? // 쇼핑몰 할인 금액
	  optionPriceAmount? // 옵션 금액
  }
```

---

## 주문 확정하기

> 신규주문(결제완료)을 확정처리 합니다. (발주처리)

**요청 파라미터**

```js
orderNumber; // 주문 번호
```

**응답 데이터**

```js
{
  response; // 확정 성공 실패 여부
  reason; // 실패 이유
}
```

---

## 송장 정보 등록

**요청 파라미터**

```js
{
  tracking_no; // 송장 번호
  shipping_company_code; // 택배사 코드
  orderNumber; // 주문 번호
}
```

**응답 데이터**

```js
{
  response; // 등록 성공 실패 여부
  reason; // 실패 이유
}
```

### 택배사 코드

> shipping_company_code params에 할당 될 택배사 코드

### 코드 값

CJ : CJ 택배

LOTTE : 롯데 택배

---

## 취소 주문 확인

**요청 파라미터**

```js
{
  start_date; // 취소 주문 조회 시작 날짜 (예_2021-01-01T00:00:00)
  end_date; // 취소 주문 조회 종료 날짜
  order_status; // 주문 상태 (예_ 결제완료, 상품준비 중, 배송 중, 취소요청,취소완료 등)
  date_type; // 검색 날짜 유형 (주문완료일, 결제완료일, 취소요청일, 취소완료일)
}
```

**응답 데이터**

```js
// 주문 데이터에 취소 정보를 추가합니다.
{
    orderNumber // 주문번호
    paidDate  // 주문날짜
    senderName // 보내는분
    senderTel // 보내는분 전화번호
    senderTel2? // 보내는분 전화번호2
    receiverName // 받는분
    receiverTel // 받는분 전화번호
    receiverTel2? // 받는분 전화번호2
    zipCode // 우편주소
    receiverAddress // 받는분 주소
    shippingMemo // 배송 메모
    productNumber // 상품 번호
    productName // 상품명
    productOptionNumber? // 상품 옵션 번호
    productOptionName // 상품 옵션명
    productQuantity // 상품 수량
    productPriceAmount // 배송비를 제외한 상품 총 가격
    isShippingFeePaid // 배송비 선결제 여부
    shippingFee // 배송비
    isOverseas // 해외배송여부
    remoteShippingFee // 제주/도서 추가 배송비  productPrice // 판매 단가
    salesCommissionFee? // 판매 수수료
    sellerDiscountPriceAmount? // 판매자 할인 금액
    mallDiscountPriceAmount? // 쇼핑몰 할인 금액
    optionPriceAmount? // 옵션 금액
    canceled:{ // 예시
      cancellationRequestDate // 취소 요청일
      cancelReason // 취소 사유
      cancelCompletedDate // 취소 완료일
      cancelApprovalDate // 취소 승인일
             }
}

```

### API Docs 참고 문서

- [Coupang Open API](https://developers.coupangcorp.com/hc/ko)
- [11번가 Open API](https://openapi.11st.co.kr/openapi/OpenApiFrontMain.tmall)
- [Cafe24 Open API](https://developers.cafe24.com/docs/api/admin/)
