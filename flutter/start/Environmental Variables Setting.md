# 안드로이드 환경변수 설정

<br/>

# 📌 1. 환경변수 설정

설정 -> 시스템 -> 정보 -> 고급 시스템 설정

![image](https://github.com/jiwonHub/TIL/assets/118645166/09f690f3-318a-4390-9332-5be9ce4b46a4)

환경 변수 클릭.

![image](https://github.com/jiwonHub/TIL/assets/118645166/19838e96-9ecf-4bfe-9ed7-820f55760077)

사용자 변수에서 새로 만들기 클릭. 

## ANDROID_HOME

![image](https://github.com/jiwonHub/TIL/assets/118645166/65a48b03-56eb-48d1-9381-52c67bb0317e)

이름 : ANDROID_HOME, 값 : 아까 복사한 SDK경로 입력.

이번엔 시스템 변수에서 새로 만들기 클릭.

## ANDROID_SDK_ROOT

![image](https://github.com/jiwonHub/TIL/assets/118645166/12535629-5369-4619-b473-00193f593430)

이름 : ANDROID_SDK_ROOT, 값 : 아까 복사한 SDK경로 입력.

사용자 변수에 Path를 찾아 더블 클릭. 

![image](https://github.com/jiwonHub/TIL/assets/118645166/5c5773af-e8c7-451b-b788-ed03d4167655)


emulator, platform-tools, tools 경로를 필자와 같이 환경변수에 추가한다.


# 📌 2. jdk 다운받기 

[오라클 공식 사이트](https://www.oracle.com/kr/java/technologies/downloads/#java21)에서 자신의 컴퓨터 사양의 맞게 다운로드 받는다. (저는 17받았습니다.)

마찬가지로 jdk 다운받은 경로를 저장 후, 시스템 변수에 저장한다.

## JAVA_HOME

![image](https://github.com/jiwonHub/TIL/assets/118645166/3e390446-5193-413f-abfe-a29b09dddcb2)

그리고 시스템 변수 'Path'에 '%JAVA_HOME%\bin'을 추가한다.
