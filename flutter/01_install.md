## Flutter install for Mac


<br/>
1. Flutter 공식 링크에서 SDK파일을 다운받는다.  https://docs.flutter.dev/get-started/install  <br/>          
2. Android Studio를 설치한다. https://developer.android.com/studio  <br/>
    2-1. Android Studio pugins에서 Dart,Flutter 설치한다.  <br/>
    2-2. SDK Manager - SDK Tools 눌러서 Android SDK Command-line Tools 설치  <br/>  
3. 환경변수를 등록한다.  <br/>   
   3-1. 터미널에서
```
   $ open ~/.zshrc
```
<br/>
   3-2.
```
export PATH="$PATH:플러터폴더경로/bin"
```
저장 후 닫기  <br/> 
   3-3. 터미널에서 flutter doctor로 확인   <br/>
   3-4. 추가적으로 Xcode 설치 및 Homebrew로 cocoapods 설치한다.     
