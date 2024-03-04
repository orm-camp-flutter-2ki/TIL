# Mac에서 Flutter 초기 환경설정
### 1. FlutterSDK 다운로드 받아야함.
- brew로 설치도 가능함. 나는 다운로드받아서 함.
- 아래링크참조
[Flutter 공식 SDK설치](https://docs.flutter.dev/get-started/install/macos/mobile-ios?tab=download#install-the-flutter-sdk) 
- 설치 후 압축 풀기

### 2. PATH 환경변수 설정
- 터미널에서 Flutter 명령을 실행하려면 PATH환경 변수에 Flutter를 추가해야하기 때문임.(선행되어야 flutter doctor 같은 명령어를 사용 가능)
- terminal 에서 zshrc 입력
```
vi ~\.zshrc
```
- 최하단으로 이동하여 환경변수코드(o) 추가해줌 (esc -> :wq)
```
export PATH=$HOME/Documents(경로)/flutter/bin:$PATH
```
- 터미널 종료 후, 플러터닥터 명령어 입력 후 미설치항목 확인 (노란색or빨간색이면 충족되지못한거)
```
flutter doctor
```
### 3. Xcode 설치
- 앱스토어에서 알아서 다운받으라

### 4. Android Studio 설치
- 안드스튜디오 공식홈페이지에서 설치
- 실행 후, Plugin에서 Dart, Flutter 2개를 설치
![스크린샷 2024-03-04 오후 6.06.26](https://hackmd.io/_uploads/r1O61MXa6.png)
- 재실행 했을때, 안드스튜디오 켜면 New Flutter Proj 나오면 잘된거임

### 5. Android Studio 세부 설정
![image](https://hackmd.io/_uploads/BkNeEGmTp.png)
- More Actions -> SDK Manager -> SDKTools에서
- CommendlineTool, Emulator, SDK Platform Tool, NDK 4개를 Apply하기
- 이후에 Android SDK Location을 복사하라 그리고 아래 명령어를 활용하여 기입해주라.
```
vi ~\.zshrc
내부에서 아래 문구를 추가 후 저장
export ANDROID_HOME=/Users/hyeonung-seo/Library/Android/sdk
```
- 이 행위는 ANDROID_HOME을 설정하는 것. ANDROID_HOME은 안드로이드 개발 환경에서 중요한 변수 중 하나이며, 안드로이드 SDK가 설치된 디렉토리의 경로를 지정하는 작업임
![image](https://hackmd.io/_uploads/SygkOHzQpT.png)


### 6. flutter doctor 다시 명령해보기
![image](https://hackmd.io/_uploads/rkOduMmTp.png)

- 나의 경우에 cocoaPods이 오래됬다고 업데이트 하라고 한다. 업데이트해주자.
```
sudo gem install cocoapods
```
- 설치가 완료되면 flutter doctor를 다시 명령해본다.
- 노란체크박스가 모두 사라질 것이다.
![image](https://hackmd.io/_uploads/HyBItGX6a.png)
