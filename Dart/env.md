## Flutter 설치
  1. [Flutter 공식 홈페이지](https://flutter-ko.dev/get-started/install) 을 통해 압축파일 다운로드 및 압축해제 후 프로그램 폴더 경로 지정 (본인의 경우에는 'C:\Program Files\Flutter' 로 저장하였음)
  2. [Visual Studio 2022 다운로드](https://visualstudio.microsoft.com/ko/vs/community/) (Visual Studio Code 아님.)
  3. [Andorid Studio 다운로드](https://developer.android.com/studio/install)
  4. SDK 설치 (...)


#### 1. Flutter 환경변수 설정
  - 'C:\Program Files\Flutter' 플러터 파일이 생성되어 있다고 가정하자.
    ```
    C:\Program Files\Flutter\bin
    ```
    을 시스템 변수 Path에 추가한다.


#### 2. Flutter 설치현황 확인
  - 설치가 잘 되어있는지 *간단히*  확인할 수 있는 명령어
    ```
    flutter doctor
    ```
  - 설치가 잘 되어있는지 *자세히*  확인할 수 있는 명령어 (설치된 경로 조회 시 유용)
    ```
    flutter doctor -v
    ```

#### 3. Dart 버전 확인
  ```
  dart --version
  ```

#### 4. Flutter 업그레이드 
  - Dart/Flutter 버전 업데이트 필요 시 사용.
  - Flutter 버전이 패치될 때 마다 홈페이지에서 다운로드할 필요는 없다.
  ```
  flutter upgrade
  ```
  
 #### 5. Dart 프로젝트 폴더 생성
  - [참조](https://dart.dev/tutorials/server/get-started#3-create-a-small-app)
  ```
  cd C:\Study\Dart
  dart create -t console 프로젝트명
  ```
