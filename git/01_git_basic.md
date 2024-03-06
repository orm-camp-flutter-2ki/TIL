# Git Basic

> Git 기본 사용법

## Git 설치 
https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EC%84%A4%EC%B9%98

## Git 용어
#### 리포지토리(Repository) : 프로젝트 저장소
#### 브랜치(Branch) : '가지'라는 뜻으로 분리하여 작업할 수 있는 개발 라인
#### 포크(Fork) : 다른 리포지토리를 자신에게 복사하는 것
#### 커밋(Commit) : 코드나 파일의 변화를 기록하는 것
#### 푸쉬(Push) : 원격 브랜치의 커밋 상황을 리포지토리로 보내어 리포지토리에 영향을 주는 것
#### 풀(Pull) : 리포지토리의 변경 사항을 원격 브랜치로 병합하는 것
#### 풀 리퀘스트(Pull Request) : 권한자에게 행하는 풀(Pull) 요청, pr


## Git 명령어

**버전 확인**
```
> git --version
git version 2.39.3 (Apple-Git-145)
```
**글로벌 설정**
```
> git config --global user.name “<이름>”
> git config —-global user.email “<이메일>”
```
**글로벌 설정 확인**
```
> git config —-global --list
user.name=<이름>
user.email=<이메일>
```
**현재 디렉토리를 로컬 저장소로 만들기**
```
> git init
```
**원격 저장소 주소 등록**
```
> git remote add origin <git주소>
> git remote add origin https://github.com/chojja7188/TIL.git
```
**푸쉬(Push)**
```
> git push -u origin <브랜치>
```
