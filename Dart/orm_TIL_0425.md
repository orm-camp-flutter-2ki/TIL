240424 (Thu)

플러터 과정 33일차

Injectable
=
https://pub.dev/packages/injectable
Get_It 패키지를 좀 더 DI용으로 사용하기 편하게 하는 코드 제네레이터
네이티브 안드로이드의 Hilt 와 유사함
Nest.js 의 injectable과 동일함

내가 작성한 클래스에만 어노테이션을 붙일 수 있다
외부 라이브러리를 주입하려면 module 을 구성한다

![image](https://github.com/BAUu/TIL/assets/44741680/98ede2cf-7982-4bca-860e-16446ff5327f)

![image](https://github.com/BAUu/TIL/assets/44741680/d1bdd0c9-572e-48ca-967a-5cfabcaa7e3b)


3rd 파티 패키지의 의존성 주입을 위해 module 을 구성하는 방법
-
각 모듈에 @module 를 추가
@singleton 으로 싱글턴 객체 생성

![image](https://github.com/BAUu/TIL/assets/44741680/8e5c0724-cd1e-4880-bb9b-76ff7e2e5eac)

주의점
-

Future 타입의 객체가 섞여있다면
@preResolve를 사용하고

초기화 부분도 Future 타입으로 정의한다

![image](https://github.com/BAUu/TIL/assets/44741680/d92bb341-0c3c-4b05-8bfc-755218e3c0a4)

위 예시에서는 dev와 prod 두 가지 환경을 구성한 예시이다


------------
git hub issue , commit tag 붙이기

- feat: 새로운 기능 추가, 요구 사항 변경으로 인해 기존 기능 변경
- fix: 버그 수정
- docs: 문서 추가 및 수정 (주석 등)
- style: 코드 스타일 수정 (포매팅, 세미콜론 누락 등)
- refactor: 프로덕션 코드 리팩토링 (버그 수정이나 기능 추가를 제외한 코드 변경)
- test: 테스트 코드 추가 및 리팩토링 (기능을 구현할 때 테스트 코드를 함께 작성했다면 feat 사용)
- chore: 빌드, 배포 등 기타 작업들을 추가 및 수정
- rename: 파일명 변경
- remove: 파일 삭제
- revert: 작업 되돌리기
