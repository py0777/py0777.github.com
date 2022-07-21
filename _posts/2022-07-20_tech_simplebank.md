---
    title:  "simplebank"
    
    categories: 
    
      - Tech
    tags:
      - programming
      - homework
    toc: true
    toc_sticky: true
    toc_label: "목차"
    popular: true
---

# SIMPLE BANK

## 01.1 증권사 업무
![D](images/kis.jpg)  
![D](images/msa_step.jpg)  
## 01.2 증권사 인프라
:::{admonition} 인프라 역할
|**`파트`**|역할| 비고|
|:---|:---|:---|
|**`TA      `**| 프레임웍                 |  |
|              | 대외계(FEP/시스템 공통)   |       |
|**`서버    `**| HW - 서버, 스토리지 설치  |       |
|              | SW - OS(unix/linux/window) 설치 및 환경구성  |       |
|              | IDC 관리                 |       |
|**`DB      `**| DB (ORACLE, ALTIBASE, MYSQL) 설치/생성/관리    |  |
|              | DBA/ DA                  |       |
|**`MW      `**| WAS(웹스피어, 턱시도)     | |
|              | 배치스케쥴 관리, 형상관리, TR모니터링 | |
|**`NW      `**| HW- 네트워크 장비 설치    |  |
|              | SW- 방화벽               |  |
|**`보안    `**| 서버보안- ex) DBSafer, 페트라 |  |
|              | 단말보안- 개인정보 관리    |  |
:::  


## 02.1 논리 ERD
![D](images/erd.jpg)  
* `회원가입을 해야 계좌를 만들 수 있다.` - 고객은 별도 프로젝트로 분리함.

## 02.2 DDL
``` sql

-- 1. 데이터베이스 생성
  -- create database SB;
-- 2. 계정생성
  -- create user msa2022;
-- 3. 테이블 삭제 
drop table sb.CIA1000;
drop table sb.ACA0100;
drop table sb.RPD0100;  
drop table sb.RPA0100;
drop table sb.RPB1000;
drop table sb.RPD1000;
drop table sb.RPD1010;

-- 4. 테이블생성

/* 고객기본- 회원가입할 때 생성- 정보계*/
CREATE TABLE SB.CIA1000(
  CUST_ID       VARCHAR(50)   NOT NULL comment '고객ID'
, CUST_NM       VARCHAR(50)            comment '고객명'
, HPNO          VARCHAR(11)            comment '휴대전화번호'
, EMAIL         VARCHAR(50)            comment '이메일주소'
, TR_ID         VARCHAR(8)             comment '거래ID'
, OPRT_TR_DTM   VARCHAR(16)            comment '조작거래일시'
, PRIMARY KEY (CUST_ID)
);

/*계좌번호 채번, SEQL를 사용*/
CREATE TABLE SB.ACA0100(
  ACNO          INT(10)        NOT NULL AUTO_INCREMENT PRIMARY KEY
, CUST_ID       VARCHAR(50)   NOT NULL comment '고객ID'
, TR_ID         VARCHAR(8)             comment '거래ID'
, OPRT_TR_DTM   VARCHAR(16)            comment '조작거래일시'
);

/*1.채번 - 계좌개설시 생성, 거래발생시 갱신*/
CREATE TABLE SB.RPD0100(
  ACNO         VARCHAR(11)   NOT NULL comment '계좌번호'
, LAST_TR_NO    INT(8)       NOT NULL comment '최종거래번호'
, LAST_TR_DT    VARCHAR(8)   NOT NULL comment '최종거래일자'
, TR_ID         VARCHAR(8)            comment '거래ID'
, OPRT_TR_DTM  VARCHAR(16)            comment '조작거래일시'
, PRIMARY KEY (ACNO)
);


/*2.적요코드 - 공통코드*/
CREATE TABLE SB.RPA0100(
  SYNS_CD       VARCHAR(3) NOT NULL comment '적요코드'
, SYNS_NM       VARCHAR(20)         comment '적요명'
, TR_TP_DCD     VARCHAR(2)          comment '거래유형구분코드'
, CNCL_SYNS_NM  VARCHAR(20)         comment '취소적요명'
, TR_ID         VARCHAR(8)          comment '거래ID'
, OPRT_TR_DTM   VARCHAR(16)         comment '조작거래일시'
, PRIMARY KEY (SYNS_CD)
);

/*3.예수금잔고 - 계좌개설시 생성, 거래발생시 갱신*/
CREATE TABLE SB.RPB1000(
  ACNO          VARCHAR(11)  NOT NULL comment '계좌번호'
, DACA          BIGINT(18)            comment '예수금'
, CUST_ID       VARCHAR(50)           comment '고객ID'
, TR_ID         VARCHAR(8)            comment '거래ID'
, OPRT_TR_DTM   VARCHAR(16)           comment '조작거래일시'
, PRIMARY KEY  (ACNO)
);

/*4.거래내역 - 거래발생시 갱신*/
CREATE TABLE SB.RPD1000(
  TR_DT        VARCHAR(8) NOT NULL  comment '거래일자'
, ACNO         VARCHAR(11) NOT NULL comment '계좌번호'
, TR_NO        INT(8) NOT NULL      comment '거래번호'
, SYNS_CD      VARCHAR(3)           comment '적요코드'
, TR_TP_DCD    VARCHAR(2)           comment '거래유형구분코드'
, TR_AMT       BIGINT(18)           comment '거래금액'
, BF_DACA      BIGINT(18)           comment '이전예수금'
, AF_DACA      BIGINT(18)           comment '이후예수금'
, CNCL_YN      VARCHAR(1) NOT NULL  comment '취소여부'
, STRT_TR_NO   INT                  comment '시작거래번호'
, ORGN_TR_NO   INT                  comment '원거래번호'
, CLNT_NM      VARCHAR(50)          comment '의뢰인명'
, REAL_TR_DTM  DATE                 comment '실제거래일시'
, TR_ID         VARCHAR(8)          comment '거래ID'
, OPRT_TR_DTM  VARCHAR(16)          comment '조작거래일시'
, PRIMARY KEY (TR_DT,ACNO,TR_NO)
);

/*5.연계거래내역 -  당행/타행 거래발생시 갱신*/
CREATE TABLE SB.RPD1010(
  TR_DT            VARCHAR(11) NOT NULL comment '거래일자'
, ACNO             VARCHAR(11) NOT NULL comment '계좌번호'
, TR_NO            INT(8)     NOT NULL  comment '거래번호'
, REL_TR_DT        VARCHAR(8)           comment '연계거래일자'
, OPNT_ACNO        VARCHAR(11)          comment '상대계좌번호'
, OPNT_TR_NO       INT(8)               comment '상대거래번호'
, REL_COM_ACTNO    VARCHAR(20)          comment '연계기관계좌번호'
, OPNT_ACT_NM      VARCHAR(50)          comment '상대계좌명'
, REL_COM_CD       VARCHAR(10)          comment '연계기관코드'
, TR_ID            VARCHAR(8)           comment '거래ID'
, OPRT_TR_DTM      VARCHAR(16)          comment '조작거래일시'
, PRIMARY KEY (TR_DT,ACNO,TR_NO)
);

INSERT INTO SB.RPA0100 ( SYNS_CD, SYNS_NM , TR_TP_DCD , CNCL_SYNS_NM , OPRT_TR_DTM) VALUES ('001', '입금', '01', '입금취소', DATE_FORMAT(SYSDATE(),'%Y%m%d%H%i%s'));
INSERT INTO SB.RPA0100 ( SYNS_CD, SYNS_NM , TR_TP_DCD , CNCL_SYNS_NM , OPRT_TR_DTM) VALUES ('002', '출금', '02', '출금취소', DATE_FORMAT(SYSDATE(),'%Y%m%d%H%i%s'));
INSERT INTO SB.RPA0100 ( SYNS_CD, SYNS_NM , TR_TP_DCD , CNCL_SYNS_NM , OPRT_TR_DTM) VALUES ('003', '대체입금', '01', '대체입금취소', DATE_FORMAT(SYSDATE(),'%Y%m%d%H%i%s'));
INSERT INTO SB.RPA0100 ( SYNS_CD, SYNS_NM , TR_TP_DCD , CNCL_SYNS_NM , OPRT_TR_DTM) VALUES ('004', '대체출금', '02', '대체출금취소', DATE_FORMAT(SYSDATE(),'%Y%m%d%H%i%s'));

/*데이터베이스 사용*/
USE SB;
```
## 02.3 과제 biz설계
### 02.3.1 계좌 개설
* 계좌번호 채번과 거래번호 채번 예수금 잔고 테이블에 INSERT가 된다.
* 계좌번호는 SEQ를 사용한다- 그래야 계좌개설 업무에 LOCK이 발생하지 않는다.
  * 대부분의 증권사는 연번이다. ( 토스뱅크, 카카오페이증권은 SEQ)

### 02.3.2 입금 출금 이체/대체
* 거래번호 채번을 한다. (일자,계좌로 MAX+1)
  * `테이블 lock을 잡는다`.- 잔고의 변동 채번으로 막는다.
* 예수금을 잔고를 변경한다.
* 거래내역을 생성한다.
  * 적요코드를 넣는다.- 일별집계와 회계처리시 적요코드 별로 계정집계를 한다.
* 이체또는 대체 거래는 연계거래내역을 생성한다.
  * 상대계좌가 당사면 출금, 입금 계좌 모두 생성하고
  * 상대계좌고 타사면 출금 계좌만 생선한다.
  
### 02.3.3 잔고 조회
* 고객별 잔고는 예수금잔고 테이블의 고객id로 group by 해서 조회
* 계좌별 잔고는 계좌기준으로 예수금잔고 테이블 조회

### 02.3.4 거래내역 조회
* 계좌와 기간을 입력값으로 받아서, 조회 한다.

## 03 개발 ###

### 03.1 개발 환경 ###
- 프레임웍: STS4, myBatis
- DB mariaDB
- 스웨거 사용 - 스프링부트 버전을 2.5.2로 낮춰야 사용가능 했음.(버전 호환성-VERSION HELL)

### 03.2 개발 표준 ###

### 03.2.1 서비스 구조 ###
![D](images/call_service.jpg)  

- 컨트롤러
  - REST API로 제공할 서비스를 등록  
  
- 서비스
  - 서비스에서 서비스는 호출 할 수 없다.
  - 인터페이스를 통해 XML을 호출 할 수 있다.  
  - 공통 모듈을 조합해 업무를 설계할 수 있다.
- VO
  - 컨트롤러에서 서비스, 서비스에서 인터페이스, 서비스에서 모듈간 데이터를 주고받을 데이터르 정의해둠
- 인터페이스
  - @Mapper 어노테이션을 사용해 xml에서 구현한 sql한다.
- 모듈
  - 타 서비스에서도 사용할 수 있는 기능은 모듈로 분리
  - 모듈에서 모듈 호출이 가능하다.
  - 인터페이스를 호출할 수 있다.
- XML
  - 인터페이스에서 정의한 메소드를 구현한다.

## 04 테스트 ###
### 04.1 스웨거 ###
![D](images/swagger.jpg)  
### 04.2 프롬프트 ###
![D](images/cmd.jpg)  

### 04.3 toad sql ###
![D](images/toad_sql.jpg)  
### 04.4 콘솔 ###
![D](images/console.jpg)  