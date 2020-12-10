---
title: "오라클 DECODE와 CASE "
categories:
  - Tech
tags: 
  - SQL
  - 오라클
  - 금융IT
toc: true
toc_sticky: true
toc_label: 목차
popular: true
---

이번 포스트는 오라클 DECODE와 CASE 사용법과 자주 실수하는 부분에 대해 써보려 합니다.

그에 앞서 잡담 하나 하고 시작하겠습니다.

증권차세대 프로젝트에 참여해 프로그래밍을 하다보면, 연차가 높은 분들은 SQL로 프로그램 개발을 선호하고, 신입 개발자는 SQL보다는 JAVA나 C언어를 선호하는 편입니다. 연차가 높은 개발자들이 SQL을 선호하는 이유는 증권 AS-IS 프로그램이 PL/SQL로 개발된 환경에서 개발 경험과 노하우가 많고, 프로그래밍언어는 프로젝트 마다 달라도 SQL은 크게 다르지 않아서 아닐까 생각됩니다.

## 오라클 DECODE와 CASE 문 사용법

### **DECODE**

- 프로그램밍 언어의 IF ELSE문을 SQL 또는 PL/SQL에서 사용하기 위해 만들어진 함수
- **사용법:** DECODE(컬럼, 조건1, 값1, 조건2, 값2, ..., DEFAULT)

### CASE

- DECODE 함수가 '='비교를 통해 조건과 일치하는 경우만 값을 RETURN 하지만, CASE 함수는 산술,관계,논리 연산등 다양한 비교가 가능
- **사용법:** 

```
     CASE WHEN 컬럼 = 조건1 THEN 값1
          WHEN 컬럼 = 조건2 THEN 값2
          WHEN 컬럼 = 조건3 THEN 값3
          WHEN 컬럼 = 조건4 THEN 값4
          ELSE DEFAULT
      END
```

DECODE와 CASE 은 둘 다 프로그래밍 언어 IF ELSE문을 표현한 것이며, SQL FROM 절을 제외한  모든곳에서 사용 할수 있습니다.

그럼 아래 예제를 살펴 볼까요

**주의! <예제 3>을 <예제4> 처럼 작성하는 개발자들이 의외로 많습니다.**

#### **<예제1>**

```SQL
/* IF문 사용법*/
IF A=B THEN
   RETURN 'X'
END IF 

/* DECODE문 사용법*/
DECODE(A, B, 'X')

/* CASE문 사용법*/
CASE WHEN A= B THEN 'X'
 END
```

#### <예제2>

```
/*IF문 사용법*/
IF A= B THEN
   RETURN 'X'
ELSEIF A= C THEN
   RETURN 'Y'
ELSE 
   RETURN 'Z'
END IF   

/*DECODE문 사용법*/
DECODE(A,B, 'X',C,'Y','Z')

/*CASE문 사용법*/
CASE WHEN A=B THEN 'X'
     WHEN A=C THEN 'Y'
     ELSE 'Z'
 END
```

#### <예제3>

```SQL
/*IF문 사용법*/
IF A = B AND B = C THEN
   RETURN 'X'
ELSEIF A = B AND B !=C THEN
   RETURN 'Y'
ELSE 
   RETURN 'Z'
END IF

/*DECODE문 사용법*/
DECODE( A, B, (DECODE( B,C,'X','Y'), 'Z')  

/*CASE문 사용법*/
CASE WHEN A = B AND B = C THEN 'X'
     WHEN A = B AND B!= C THEN 'Y'
     ELSE 'Z'
 END
```

#### <예제4> 잘못된 프로그램

```SQL
/* 잘못된 CASE 문*/
CASE WHEN A = B THEN
     CASE WHEN B = C THEN          
               RETURN 'X'
          ELSE
               RETURN 'Y'
     ELSE 'Z'
     END
 END

/*위 CASE문을 IF문으로 바꾸면*/
IF A = B THEN
   IF B = C THEN
      RETURN 'X'
   ELSE
      RETURN 'Y'
   END IF
ELSE 'Z'
END IF
```

< 예제4> 의 CASE문은 <예제3> 처럼 CASE WHEN ... WHEN ... WHEN END 식으로 작성하는 편이 좋습니다. 위 코드처럼 CASE절 안에 CASE를 사용하게 조건 몇개만 추가되도 소스도 길어지고, 가독성이 낮은 코드를 만들게 되며, 결국 유지보수성이 낮은 프로그램이 되버립니다.

> 작은 차이가 명품을 만듭니다.

 