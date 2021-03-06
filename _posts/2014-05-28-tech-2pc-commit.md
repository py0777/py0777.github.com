---
title: "2개의 시스템에서 잔고를 관리하는 법"
categories:

  - Tech
tags: 
  - 2pc_commit
  - cdc
  - 증권
  - 금융IT
toc: true
toc_sticky: true
toc_label: 목차
popular: true
---

##  저축은행연계 계좌 입출금 처리

 - 해외 FX계좌 입출금고 처리
 - 보험사마이너스 대출 계좌 입출금 처리

위 나열한 계좌들은 증권사시스템에 계좌잔고를 관리하면서 다른 업체 또는 다른 시스템에서도 잔고를 관리하는 업무들 이다.

1개의 계좌에서 잔고변동이이 발생하면 잔고를 가감하고 거래내역을 생성한다.
이 계좌가 다른시스템에서 잔고를 관리하는 계좌라면, FEP또는 EAI로 해당 시스템에 이 계좌의 잔고변동을 송신한다.
만약, 잔고변동을 송신한 이후 증권사 시스템에서 오류가 발생하게 되면, 거래내역 생성과 잔고변동은 모두 ROLLBACK 되지만,
송신한 내역은 취소하지 못한다. 따라서, 양 시스템간의 잔고차이가 발생하게 된다.

해결방법중 하나가 EAI경의 2PC COMMIT이 있다. 해당 시스템으로 EAI 송신을 대기 하고 있다가, 거래가 정상적으로 종료 될때에 EAI 송신도 COMMIT 하게 되는 방식이다. 하지만, 이 방법은 인프라에서 제공하지 않는 경우가 많다. 어떤 사유인지 몰라도, 시스템 속도가 느려지던지, 부하를 많이 주던지 하는 이유 인듯 보인다.

## 결국, 잔고가 틀린채로 가야하는가?

아직 구현해보진 못했지만, 거래내역 LOG성 테이블을 두고 거래가 정상적으로 끝날때, 로그성 테이블에 업무별 처리여부를 갱신해가며, 전문을 전송하는 방식이 있다. 이 방법으로 구현하게 되면, 증권사 시스템의 거래는 정상 종료가 된 것이니, 타 시스템에선 수신 내역으로 해당 계좌의 잔고를 맞쳐주기만 하면 된다. 집계나, 회계를 생성할때 사용하는 거래내역 로그테이블을 확장해서 사용하면 되니, 어렵지 않게 구현할 수 있어 보인다.

다음번에 위 방법으로 구현해 봐야겠다