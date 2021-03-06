---
title: "거래내역 취소여부"
categories:
  - Tech
tags: 
  - 거래내역취소
  - 취소거래
  - 금융IT
toc: true
toc_sticky: true
toc_label: 목차
popular: true
---

## 거래내역 취소여부

### 특징

-  거래내역은 당일 취소만 가능합니다. 이유는 회계처리 및 집계처리가 일별마감을 하기때문에, 과거일자 거래를 취소 할 수 없습니다.
-  거래내역 취소시, 취소할 거래를 삭제하지 않습니다.(삭제할 경우 이력관리가 되지 않음)

### 거래내역 취소여부관리는 보통 2가지 방식으로 관리 함.

**첫 번째 방식**은 취소여부와 유효여부 속성을 둬서, 유효여부를 가지고 이 거래가 원거래인지, 취소거래인지 판단하는 방식
**두 번째 방식**은 취소여부만 두고, 취소여부가 N이면 정상거래, 취소여부가 Y이면 취소된 거래로 판단. 취소된 거래중 원거래번호가 0 이면, 원거래이고, 원거래번호가 0보다 크면, 원거래를 취소한 취소거래로 판단함.
나는 개인적으로 위 두 방식중 두번째 방식을 선호한다.

1.  거래내역의 유효여부를 삭제 함으로 관리할 컬럼이 줄어든다.
2. SQL작성시 가독성이 좋다. 방식 1로 관리하는 테이블의 정상거래를 찾으려면 WHERE절에 유효여부가 ='Y' 인것으로 찾아야하지만, 방식2로 관리하면 취소여부가 'N'인 것으로 찾을 수 있다.

**방식 1.**
거래내역 취소시는 취소건를 생성하여 원건과 취소건 2건으로 관리함.

- 유효여부와 취소여부로 거래 유효성 및 취소거래여부 관리.
- 유효여부: 취소 안된 원거래건만 유효여부 'Y' 값을 가짐.
- 취소여부: 취소거래로 생성된 거래만 취소여부 'Y' 세팅

|            | 유효여부       | 취소여부     | 거래번호    | 원 거래번호|
|----------  |---------     | ----------- |----------- |----------- |
|원거래       | **Y**        |N            | 1          | 0|
|취소 처리된 원거래 | **N** |N| 1 | 0     |
|취소처리    | N    | Y  | 2 | 1|

**방식 2**
유효여부는 삭제하고, 취소여부와 원 거래번호를 통해 취소거래여부 관리

- 취소여부: 정상거래는 N 취소된 거래는 Y로 관리

|            |  취소여부     | 거래번호    | 원 거래번호|
|----------  |---------     | ----------- |----------- |
|취소 처리된 원거래 | **Y**  | 1      | 0|
|취소처리    | Y  | 2 | 1|