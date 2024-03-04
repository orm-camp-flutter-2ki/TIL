Git
=============
Spotlight -> 터미널(terminal) -> 붙여넣기(past) -> enter


1.Homebrew 설치
-------------
Homebrew :  https://brew.sh/ko/
### 1) Install
```
>$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

>### 2) mac 암호 입력 후 enter... 다시 ~ % 나오면
```
$ (echo; echo 'eval "$(/usr/local/bin/brew shellenv)"') >> /Users/(사용자마다 다르니 요부분 수정)/.zprofile
$ eval "$(/usr/local/bin/brew shellenv)"
```
경우에 따라 Three commands 일 수도 있음...

### 3)설치확인
```
$ brew --version
```


2.Git 설치
-------------
### 1) Install
```
$ brew install git
```
### 2) 설치확인
```
$ git --version 
```

