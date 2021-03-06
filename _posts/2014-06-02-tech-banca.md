---
title: "방카슈랑스 시스템 "
categories:
  - Tech
tags: 
  - 방카슈랑스
  - 은행
  - 금융IT
toc: true
toc_sticky: true
toc_label: 목차
popular: true
---

![image](https://py0777.github.io/assets/image/banca/banca_1.jpg)

매번 증권사 차세대 프로젝트에 투입되어 일해 오다가, 이번에 **우리은행 방카슈랑스 시스템** 오픈 말미에 투입되어 업무를 수행하고 있습니다. 은행권 업무라기 보다 보험쪽업무를 알면서 대 내/외 인터페이스및 전문관리 를 경험해본 개발자면 수월하게 업무진행 할 수 있어보입니다. 작은 시스템치곤 은행에겐 수익을 많이 가져다 주는 업무를 관리하는 시스템이라고 합니다. 구현은 대기업이 아닌 중소기업에서도 패키지 형태로 구현 가능해 보였습니다. 다만, 방카슈랑스 시스템으로 수익을 많이 낼 수 있는 고객이 지점을 많이 보유한 메이져 은행들이라, 고객수가 제한 적으로 보였기 때문에 패키지를 만든다고 하더라도 필요 없을 수도 있겠다는 생각이 듭니다. (증권회사에도 방카슈랑스 시스템이 구축되어 있는 곳도 있지만, 수익이 어느정도인지는 알지 못합니다.)

**1. 방카슈랑스 시스템이란**

* 보험사의 생명보험/손해보험등을 은행/증권사에서 위탁판매 하는 것을 관리하는 목적으로 만들어진 시스템 입니다.

 

**2. 장점은?**

* 보험사에겐 은행을 통해 판매함으로써, 판매 채널을 넓힐 수 있고 은행은 판매수수료를 통해 부가수입을 창출할 수 있습니다. 신문기사를 통해 확인해본 결과 매 분기당 200~300억 정도가 은행의 수익으로 보도되었습니다. 또한, 판매이후 사후 관리는 보험사에서 하기때문에, 은행입장에서 사후관리에 대한 부담이 적어보입니다. 시스템 적으론, 기간계 시스템에 비해 risk가 적지만 수익율이 좋고, 작은 시스템이라 패키지 형태로 구현이 가능해 보입니다.

 

**3. 시스템의 특징**

* 시스템은 청약 및 해지등의 보험사 업무를 관리하는 것과 보험사와 은행간의 정보를 전문 또는 파일 송수신을 하는 것으로 이루어져 있습니다.규모는 200 M/M (20명 10달)정도 될것 같습니다.

 

**4. 진행시 주의사항**

* 보험사와 은행/증권 기간계 사이에 있는 시스템으로 보험사/은행간 전문interface가 잘되는지 점검 해야함.
* 국내 20여개 보험사들과 협업을 해야 함으로 정확한 의사전달이 필요함.
* 구현후 적은인원으로 관리해야 함으로, 관리자용 기능개발에도 신경써야 합니다.