---
  title: "access connect postgresql"
  categories:

    - Tech
  tags: 
    - 개발목록관리
    - access
    - 금융IT
  toc: true
  toc_sticky: true
  toc_label: 목차
  popular: true
---

access connect postgresql

프로젝트 수행시 일정 및 범위 산정시 중요한 자료가 프로그램 개발목록 입니다. 앞서 [개발목록 ](https://py0777.github.io/tech/tech-dev-list/)포스트에도 언급했지만, 개발자들은 자신이 개발해야 하는 목록및 개발진척 등록 목적으로 사용하고 있고, 품질 담당자는 모든 개발자의 개발목록을 취합해 관리자에게 프로젝트 진행상황을 보여줄 수 있는 자료로 활용하고 있습니다.

개인적인 경험상 MS의 쉐어포인트로 개발목록을 관리하는 것이 쉽고, 개발목록 작업시 많은 시간을 절약해 주었습니다. 하지만 MS라이센스비용을 지불해야 함으로 다른방법들이 고려하게 되었습니다.

이번 프로젝트에선 개발목록을 회사에서 개발한 PMS(Project Managerment System)으로 관리하고 있습니다. 자바와 PostgreSql로 만들어진 PMS는 관리자에게 개발진척사항을 보여주기는 쉽지만, 여러 개발자가 개발목록 등록 및 일정 수정작업이 수월하지 않습니다.  그래서 ACCESS파일에서 PostgreSql 프로그램개발목록 테이블을 odcb로 연동해 개발자들은 각자의 ACCESS 파일에 작업을 하면 실시간으로 PMS에 보여지도록하는 작업을 진행 중 입니다.

## **작업순서**

**1. PC에 MS ACCESS 프로그램이 설치되어 있어야 합니다.**

**2. PostgreSql odbc driver설치
아래위치에서 PostgreSql 버전에 맞는 odbc driver 다운로드 및 설치**
위치: http://www.postgresql.org/ftp/odbc/versions/msi/

**3. 제어판 -> 관리도구 -> 데이터원본(ODBC) 실행
(WINDOW7 64bit이면서 ACCESS 2007 인 경우는 C:\Windows\SysWOW64\odbcad32.exe 실행
\- 이유는 제어판으로 들어가는 방법은 64bit 드라이버만 보이는데, Access2007은 32bit라서 32bit driver가 보이지 않는다고 합니다.
그래서 Windows에 들어가서 odbcad32.exe를 실행해야 32bit 드라이버를 설정가능하다고 합니다.)**

**4. 추가버튼 클릭**

(![image](https://py0777.github.io/assets/image/tech-access/tech-access_1.jpg)

**5. PostgreSQL 드라이버 선택 후 마침버튼 클릭**

(![image](https://py0777.github.io/assets/image/tech-access/tech-access_2.jpg)

**6. 서버에 설치된 PostgreSql 접속정보를 입력 후 Test 버튼 클릭**

**- PostgreSql 관리자는 외부접속 가능하도록 열어져 있어야합니다. (postgresql.conf 파일과 pg_hba.conf 파일 설정)**

(![image](https://py0777.github.io/assets/image/tech-access/tech-access_3.jpg)

**7. 메시지를 확인 확인 후 Save 버튼을 클릭합니다.**

(![image](https://py0777.github.io/assets/image/tech-access/tech-access_4.jpg)
 

**8. ODBC 데이터 원본 관리자에서 추가한 드라이버를 선택하고 확인버튼 클릭**

(![image](https://py0777.github.io/assets/image/tech-access/tech-access_5.jpg)
 

**9. ACCESS파일을 열고, 외부데이터-> ODBC데이터베이스 선택**

(![image](https://py0777.github.io/assets/image/tech-access/tech-access_6.jpg)
**10. 연결 테이블을 만들어 데이터 원본에 연결 선택 후 확인버튼 클릭**

(![image](https://py0777.github.io/assets/image/tech-access/tech-access_7.jpg)

**11. 컴퓨터 데이터 원본 탭에서 PostgreSQL 선택 후 확인버튼 클릭**
(![image](https://py0777.github.io/assets/image/tech-access/tech-access_8.jpg)
 

**12. 연결할 테이블 선택 후 확인버튼 클릭**
(![image](https://py0777.github.io/assets/image/tech-access/tech-access_9.jpg)
 

**13. ACCESS 화면 좌측에 PostgreSql test테이블이 보이고, 데이터 시트엔 test 의  레코드가 보입니다.**

**( ACCESS에서 데이터수정및 추가가 가능합니다. 단, 추가를 하기위해서 test테이블은 pk가 존재하는 테이블이어야 합니다.)**
(![image](https://py0777.github.io/assets/image/tech-access/tech-access_10.jpg)

 

**14. PostgreSql에서 데이터를 확인해 봅니다.**
(![image](https://py0777.github.io/assets/image/tech-access/tech-access_11.jpg)