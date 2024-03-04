Git 설치
=============
### 1. Homebrew 설치
Homebrew Page :   https://brew.sh/ko/
```
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
* Spotlight -> 터미널(terminal) -> 붙여넣기(past) -> enter

### 2. git 설치
```
$ brew install git
```
* password 입력 -> enter

### 3. Flutter 설치
Flutter Page (Mac IOS) :   https://docs.flutter.dev/get-started/install/macos/mobile-ios?tab=download
```
$ sudo softwareupdate --install-rosetta --agree-to-license
```
* 설치

### 4. X code
* app Store -> 좌측 [개발자] -> download
* 

### 4-1. X code 오류 해결
* Unable to get list of installed Simulator runtimes.
```
$ xcodebuild -downloadPlatform iOS
```

* Xcode installation is incomplete;
```
$ sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
$ sudo xcodebuild -runFirstLaunch
```

* CocoaPods not installed.
```
$ sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
$ sudo xcodebuild -runFirstLaunch
```


### 5. Android Studio
* 버전 맞게 설치 후 실행
* 실행 -> 좌측 [Plugins] -> Featured 내 Flutter Install

### 5-1. Android Studio 오류 해결
* Unable to locate Android SDK.


### rbenv

### cocoapods
