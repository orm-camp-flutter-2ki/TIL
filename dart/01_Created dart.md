### 플러터 닥터시 Cocapad에 문제가 있는 경우

```coq
brew install cocoapods
```

를 터미널에 구동하면 완료

### 맥 환경변수 등록

터미널 이름이 .zsh 이면

```coq
open ~/.zshrc
```

터미널 이름이 bash면

```coq
open ~/.bash_profile
```

```coq
export PATH="$PATH:플러터폴더경로/bin"
```

저장하고 닫기 -> flutter doctor로 확인

에러뜨면 컴퓨터재시작 후

```coq
softwareupdate --install-rosetta
```

입력 후 flutter doctor

### 플러터 설치 잘 되어있는지 체크리스트

- Android studio / VS code 설치 완료 확인
- 환경변수 등록/설정 잘 되어있나 확인
- flutter doctor로 flutter 설치 완료 확인

### Dart Create a small app

https://dart.dev/tutorials/server/get-started#3-create-a-small-app

```jsx
dart create -t console cli
```

- VS Code 에서는 command+p를 해서 >dart project 를 하면 Create cil를 하여 저장할 곳을 지정하면 할 수 있다.

### 터미널에서 폴더 경로 아는법

- 폴더 우클릭 에서 터미널 열고
- pwd 치면 경로 알 수 있음

### dart 파일 생성시
- 모두 소문자로 만든다.

### **Introduction to Dart**


타입 중 이 세가지만 소문자임
`int`
`double`
`bool`

타입을 써야지 함수가 됨

### 변수,상수

- 변수는 값이 변함
- 상수는 값이 안변함 (final 로 하면 안변함) final 과 const의 차이는 중요함
