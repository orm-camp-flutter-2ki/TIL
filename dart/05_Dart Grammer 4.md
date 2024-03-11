### 단축키

`alt + shift + 위,아래` : 코드를 위아래로 배치할 수 있음

`Command + d` : 코드 한줄 복사

### Test 파일 생성 및 테스트 방법
![스크린샷 2024-03-11 오전 10 37 45](https://github.com/jungeun272/TIL/assets/131224099/8b20cf99-293a-4296-8b4a-944083cbbe52)


### 캡슐화(encapsulation)

- 실수로 속성을 덮어 쓰거나, 잘못된 조작 하는 등의 휴먼 에러 (human error) 를 완전히 없앨 수는 없다.
그래서 Dart 에는 실수를 미연에 방지하는 “캡슐화" 라는 방법이 있다.
- 클래스에서도 접근지어도 킴

### Class diagram

![스크린샷 2024-03-11 오전 11 26 45](https://github.com/jungeun272/TIL/assets/131224099/3d8b9cb7-e5f4-4bbe-8e0d-b0ab79c52425)


### 컬렉션

- `List`
    - 순서대로 쌓여있는 구조
- `Map`
    - key와 value 의 쌍으로 저장
- `Set`
    - 순서가 없는 집합

### Var vs dynamic

- `dynamic`
    - 런타임에 타입이 결정됨
    - 위험함 → 조심히 활용
- `var`
    - 컴파일에 타입에 결정됨

### Set

- 중복값을 허용하지 않는 집합
