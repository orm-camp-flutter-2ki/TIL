## [Flutter 작업환경 설정]

### 1. Flutter 설치
  1. [Flutter 공식 홈페이지](https://flutter-ko.dev/get-started/install) 을 통해 다운로드 및 압축해제 (flutter 폴더가 생성된다.)
  2. [Visual Studio 2022 다운로드](https://visualstudio.microsoft.com/ko/vs/community/) (Visual Studio Code 아님.)
  3. [Andorid Studio 다운로드](https://developer.android.com/studio/install) : [Plugins] 에서 Dart, Flutter 검색하여 설치  

### 2. 환경변수 설정
  - 'C:\Program Files\Flutter' 경로에 플러터 폴더가 위치해있다고 하면, 하위 폴더 bin 까지의 경로를 복사하여
    ```
    C:\Program Files\Flutter\bin
    ```
    을 시스템 변수 Path에 추가한다.


### 3. Flutter 설치현황 확인
  - 설치가 잘 되어있는지 *간단히*  확인할 수 있는 명령어
    ```
    flutter doctor
    ```
  - 설치가 잘 되어있는지 *자세히*  확인할 수 있는 명령어 (설치된 경로 조회 시 유용)
    ```
    flutter doctor -v
    ```

### 4. Dart 버전 확인
  ```
  dart --version
  ```

### 5. Flutter 최신버전 업데이트 ( *필요시 사용* )
  ```
  flutter upgrade
  ```
  
### 6. Dart 프로젝트 폴더 생성 [(참조링크)](https://dart.dev/tutorials/server/get-started#3-create-a-small-app)
  ```
  dart create -t console 프로젝트폴더명
  ```
