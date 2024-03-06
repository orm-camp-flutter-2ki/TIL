Git Setting (mac)
=============
```
Spotlight -> 터미널(terminal)
```
1.git 최초 설정
-------------
### 1) window와 mac의 엔터방식(줄바꿈 호환) 차이로 인한 오류 방지
```
$ git config --global core.autocrlf true
```
<br/>

### 2) 사용자 이름, 이메일 주소 설정
```
$ git config --global user.name "(본인 이름)"
$ git config --global user.email "(본인 이메일)"
```
<br/>

### 3) 사용자 이름, 이메일 주소 설정
* 설정 명령어
```
$ git config --global user.name "(본인 이름)"
$ git config --global user.email "(본인 이메일)"
```
* 확인 명령어
```
$ git config --global user.name // 이름 확인
$ git config --global user.email // 이메일 확인
$ git config --global --list // global 설정값 목록 확인
```
<br/>

### 4) 저장소 생성
```
$ git init
```
> - 현재 디렉토리 기준으로 저장소가 생성됨 (IDE 내 터미널에서도 생성 가능
> - 프로젝트 폴더 내 숨김모드로 .git 폴더 생성 확인
> - 숨김파일 보기 : cmd + shift + .
<br/>

### 5) branch 이름 변경
```
$ git config --global init.defaultBranch main
```
  > commit 까지 입력 후 변경 가능
<br/>
