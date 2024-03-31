firebase.google.com
# google login 문서1
## 시작하기

https://firebase.google.com/docs/auth/flutter/federated-auth?hl=ko

flutter pub add fireabase_auth



# firebase console
## Authentication 탭

구글 선택하고
이메일 저장하면 이렇게 나옴

![[Pasted image 20240401002834.png]]

# google login 문서2
## 제휴 ID 및 소셜
flutter pub add google_sign_in

login에 예시 코드 붙여넣고 fireabse_auth import



### 오류
메시지
```
Failed to read key AndroidDebugKey from store "C:\Users\User\.android\debug.keystore": No key with alias 'AndroidDebugKey' found in keystore C:\Users\User\.android\debug.keystore
```
  keytool -changealias -alias mykey -destalias AndroidDebugKey -keystore debug.keystore

keytool -importkeystore -srckeystore debug.keystore -destkeystore AndroidDebugKey.p12 -srcstoretype JKS -deststoretype PKCS12

해결
지우고 다시 만드는 게 최고

#### 삭제
keytool -delete -alias AndroidDebugKey -keystore debug.keystore

#### 생성
keytool -genkey -v -keystore debug.keystore -alias AndroidDebugKey -storepass android -keypass android -keyalg RSA -keysize 2048 -validity 999999 -dname "CN=Android Debug,O=Android,C=US"

#### 조회
대소문자는 구분 있음!
keytool -list -v -alias androiddebugkey -keystore debug.keystore
keytool -list -v -alias AndroidDebugKey -keystore debug.keystore

keytool -list -v -alias androidreleasekey -keystore release.keystore

key 찾기
PS D:\source\flutter\flutter_git_blog> cd .\android\
PS D:\source\flutter\flutter_git_blog\android> ./gradlew signingReport