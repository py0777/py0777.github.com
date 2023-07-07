---
  title: "aws에 jenkins 설치"
  categories:

    - Tech
  tags: 
    - aws에 jenkins 설치
    - aws
    - jenkins
  toc: true
  toc_sticky: true
  toc_label: 목차
  popular: true
---

# AWS에 jenkins 설치

## 1. AWS | EC2에  JAVA 설치
아래 블로그를 참고 바란다. 

[aws ec2 java설치](https://gaemi606.tistory.com/entry/AWS-EC2%EC%97%90-JAVA%EC%84%A4%EC%B9%98-%EB%B0%8F-%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98-%EC%84%A4%EC%A0%95){: .btn.btn-default target="_blank" }

## 2. AWS JENKINS 설치
아래 블로그를 참고 바란다. 

[aws ec2 JENKINS설치](https://goddaehee.tistory.com/82){: .btn.btn-default target="_blank" }

기존 : 8080 --> 9100 으로 변경은 
```bash
$ sudo vi /etc/sysconfig/jenkins
```
JENKINS_PORT="8080"=> JENKINS_PORT="9100" 

참고로 aws port 오픈은 aws 관리화면에서 진행하기 바란다. firewall 명령어가 정상작동하지 않는다.

## 3. jenkins 시작과 종료
```bash
$ sudo service jenkins start //시작
$ sudo service jenkins stop //종료
$ ps -ef | grep Jenkins //프로세스 확인
```
## 4. 열린포트 확인
```bash
$ netstat -tnl
```

## 5. 기타
[centOS 포트변경](https://kim-jong-hyun.tistory.com/129){: .btn.btn-default target="_blank" }
[centOS 포트오픈](https://sd23w.tistory.com/465){: .btn.btn-default target="_blank" }
