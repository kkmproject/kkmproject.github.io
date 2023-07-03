---
layout: article
---

# Title: {{ page.title }}

> Spring(boot) + PostgreSQL 를 이용하여 확인 가능한 간단한 웹 서비스 구축 후, 해당 프로젝트를 Synology NAS를 이용하여 호스팅하는 과정을 나타낸다.
> 최종적으로는, 사용자 도메인을 이용하여 Synology NAS에 호스팅한 웹 서비스에 접속하는 것을 목표로 한다.

---

**index**
1. Synology NAS
2. Web Service
3. DNS 설정
4. 결과물

---

# 1. Synology NAS

해당 글에서 진행할 Synology NAS는 'DS220+' 모델이며, DSM 버전은 "DSM 7.2-64570 Update 1" 이다.

## 1.1. 패키지 설치

### 1.1.1. Container Manager 설치

**path: NAS > 메인메뉴 > 패키지 센터 > 모든 패키지 > 검색: Container Manager > 설치**

Container Manager 패키지는 Synology NAS에서 기존 Docker 패키지가 업데이트되며 명칭 변경과 함께 특정 기능들이 추가된 패키지이다. 쉽게 Docker GUI서비스라고 생각해도 무방하다.

###  1.1.2. Web Station 설치

**path: NAS > 메인메뉴 > 패키지 센터 > 모든 패키지 > 검색: Web Station > 설치**

이후 과정에서 역방향프록시 설정을 간단히 처리하기 위해 설치하는 패키지이다. ~~Synology NAS에 자체 역방향프록시가 있으며, 이를 사용해도 괜찮다.~~

## 1.2. 레지스트리 다운로드

### 1.2.1. ngnix

**path: NAS > Container Manager 실행 > 레지스트리 > 검색: nginx > 다운로드 > 태그: latest**

Web Station 패키지와 유사하게, 역방향 프록시 설정을 간단히 처리하기 위해 Web Server로 nginx를 사용한다.

### 1.2.2. postgres

**path: NAS > Container Manager 실행 > 레지스트리 > 검색: postgres > 다운로드 > 태그: latest**

이후 과정에서 Web Service 구축시에 사용하고자 하는 Database로 사용자가 선호하는 다른 레지스트를 다운로드하여도 무방하다.

## 1.3. 이미지 실행

### 1.3.1. nginx

**path: NAS > Container Manager 실행 > 이미지 > nginx > 실행**

***\* 일반설정***
```
- 이미지 : nginx:latest
- 컨테이너 이름 : {container name}
- 리소스 제한 활성화 : null
- 자동 재시작 활성화 : null
- Web Station을 통해 웹 포털 설정
  - 컨테이너 포트: 80 - HTTP
```

***\*고급설정***
```
- 포트설정 : Web Station의 경우 - 80 - HTTP
- 볼륨설정(+폴더추가) : /docker/{folder name} - {folder name} - 읽기/쓰기
- 환경
    - PATH : /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    - NGINX_VERSION : 1.25.1
    - NJS_VERSION : 0.7.12
    - PKG_RELEASE : 1~bookworm
- 기능
    - 기능 구성 : 기본설정
- 네트워크
    - 네트워크 : bridge
```

### 1.3.2. postgres

**path: NAS > Container Manager 실행 > 이미지 > postgres > 실행**

***\* 일반설정***
```
- 이미지 : postgres:latest
- 컨테이너 이름 : {container name}
- 리소스 제한 활성화 : null
- 자동 재시작 활성화 : null
```

***\*고급설정***
```
- 포트설정 : {로컬 포트} - {컨테이너 포트} - HTTPS
- 볼륨설정(+폴더추가) : /docker/{folder name} - {folder name} - 읽기/쓰기
- 환경
  - PATH : /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/lib/postgresql/15/bin
  - GOSU_VERSION : 1.16
  - LANG : en_US.utf8
  - PG_MAJOR : 15
  - PG_VERSION : 15.3-1.pgdg120+1
  - PGDATA : /var/lib/postgresql/data
  - POSTGRES_USER : {username}
  - POSTGRES_PASSWORD : {password}
- 기능
  - 기능 구성 : 기본설정
- 네트워크
  - 네트워크 : bridge
```

## 1.4. Web Station 설정

**path: NAS > Web Station 실행 > 웹 포털 > 포털 만들기 마법사 > 웹 서비스 포털 설정**

***\*웹 서비스 포털 설정***
```
- 서비스 : {container name}
- 포털 유형 : 이름 기반
- 호스트 이름 : {domain name (ex.blog.kkmproject.com)}
- 포트 : 80/443
- HTTPS 설정: check
```

## 1.5. nginx 설정
- `$ service nginx status`  : nginx 상태 확인 
- `$ service nginx restart` : nginx 재실행
- `$ service nginx reload`  : nginx 재실행(미중지)
- `$ service nginx stop`    : nginx 중지

### 1.5.1. SSH 접속
```bash
# ssh 접속 ###########################################################
$ ssh -p {nas dsm port} {nas id}@{nas ip}
$ docker ps -all
$ docker exec -itu 0 {container name} /bin/bash
$ service nginx status
nginx is running.



# java 설치 ##########################################################
$ apt-get update
$ apt-get upgrade
$ apt-get install openjdk-17-jdk



# vim 설치 ###########################################################
$ apt-get install vim



# nginx reverse proxy 설정 ###########################################
# if OS is Cent ? /etc/nginx/conf.d #################################
# if OS is Ubuntu/Debian ? /etc/nginx/site-available ################
$ cd /etc/nginx/conf.d
$ vi default.conf
...
  location / {
    proxy_pass http://localhost:8080
    ...
  }
...
```

## 1.6. 방화벽 설정

# 2. 웹 사이트 구축

## 2.1. spring initializer

## 2.2. DB 연결 테스트

## 2.3. Local환경 테스트

## 2.4. Jar

##
`Synology NAS`를 이용하여 웹 호스팅하는 과정을 나타내는 것에 중점을 두기 때문에, 확인 가능한 간단한 웹 사이트를 구축한다.

# 3. DNS 설정

- 타입 : A
- 호스트 : nas
- 값/위치 : {공인IP}
- TTL : 1800

