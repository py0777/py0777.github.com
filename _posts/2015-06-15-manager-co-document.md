---
title: "프로젝트 우선 협상 단계"
categories:
  - Manage
tags: 
  - 협업문서
  - cowork
  - document
  - version_manage
toc: true
toc_sticky: true
toc_label: 목차
popular: true
---
![image](https://py0777.github.io/assets/image/co-document/co-document_1.png)
협업 문서작성

프로젝트를 진행하다 보면 여러사람이 하나의 문서를 작업 하는 일이 자주 있습니다. 예를 들어 프로그램 개발 목록, 컬럼맵핑정의서 같은 것들 입니다. 여러사람이 한 문서를 사용하기 위해서 예전엔 파일서버에 엑셀파일을 공유파일로 등록해  함께 사용했지만, 최근 많은회사들이 문서보안 프로그램을 설치하면서 엑셀 공유작업이 되지않게 되었습니다. 또한, 이 방법 역시 여러사람이 작업하다 보니, 엑셀 서식이 깨지거나 다른사람이 덮어써서 내용이 지워지는 경우가 자주있었죠.

이러한 문제를 해결하기 위해 이전 프로젝트에선 MS의 SHARE POINT라는 프로그램을 설치한 서버에 오피스문서를 올려두면, MS OFFICE프로그램을 설치하지 않은 PC에서도 웹으로 OFFICE 문서들을 함께 작업할 수 있게되었습니다. 그러나 라이센스 비용 지불이라는 문제로 이번 프로젝트에선 사용하지 못하게 되었죠. 대신해 구글DOCS를 사용하면 좋겠지만, 아쉽게도 금융권 프로젝트이기 때문에 인터넷은 안됩니다.

그래서 엑셀이나 워드문서를 웹에서 공유할 수 있는 프로그램을 찾아보니, 무료로 제공하는 프로그램은 찾을 수 없었고, 오픈소스로도 찾기 어려웠습니다. 최근엔 VISUAL STUDIO 가 무료로 사용할 수 있게 되면서 VB나 C#으로 개발 하려고 하다보니, 그것 역시 만만치 않은 작업이 될 것 같더군요. 그래서 차선으로 선택한 방법이 MS 엑세스입니다. 엑세스 파일은 문서보안이 안 걸리는 경우가 많고, 여러사람이 같이 작업을 한다고 하더라도 DB이기 때문에 LOCK이 잡히지 않습니다. 엑세스를 좀 더 잘 활용해 더 수월하게 사용하고 싶지만 현재는 락이 잡히지 않는다는 것으로 만족합니다.

프로젝트를 수행할때 마다 협업문서 작성은 고민했던 문제인데, 어떻게 하면 여러사람이 공동으로 작업하는 문서작업이 엑셀처럼 쉽고, 웹처럼 접근하기 쉬우며, DB처럼 안정적으로 작동할 수 있을까요? 그리고 이런 기능을 제공하는 프로그램은 언제쯤 오픈소스로 풀리게 될지 궁금합니다.