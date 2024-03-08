# 2일차

Dart는 언어
flutter는 프레임워크

참고로 맥 환경변수 관련해서 경로와 어떻게 설정하는지에 대해서 경로와
파일편집 내용 예시


![Untitled](https://github.com/happysong3914/TIL/assets/130008915/18c48c9a-ef88-4dee-b83f-c42a723dc0b8)


환경변수란 특정폴더에 있는 명령어를 OS에서 어느폴더에서나 전역적으로 사용하기 위해 

설정하는 것

참고로 안드로이드 스튜디오에서 dart프로젝트 만들기 참고화면

![Untitled 1](https://github.com/happysong3914/TIL/assets/130008915/3626e82a-be02-4e89-9075-7b39fbd41cec)


참고로 간혈적으로 chocolatey 로 flutter sdk 잡으면 간헐적으로 환경변수가 틀어지는 문제 발생확인

플러터및 다트 설치 관련 

참고로 플러터를 설치하면 그안에 다트가 있으므로 플러터만 설치하면 된다.

플러터 파일 여기서 다운로드 한뒤

![Untitled 2](https://github.com/happysong3914/TIL/assets/130008915/5fe0c0a3-99e8-4932-bf0d-aedda097bfed)



설치하려고 하는 위치에 다운로드한 파일의 압축을 풀기한뒤
제어판>시스템>고급 시스템 설정> 고급탭에 환경변수 > ~에 대한 사용자변수
항목에서 Path 클릭후  편집 버튼 클릭

![Untitled 3](https://github.com/happysong3914/TIL/assets/130008915/ae2cd9a0-9a06-4838-b7d2-58ad383cc46e)



환경변수 설정의 경우 dart의 경우는 플러터 폴더 압축푼 폴더아래 추가 경로로 flutter/bin/cache/dart-sdk/bin 환경변수를 설정해주면 되고

플러터는 플러터 폴더 압축푼 폴더아래 여기 까지만 환경변수를 설정해주면 됩니다.
flutter/bin

