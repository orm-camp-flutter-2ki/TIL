## 다트 문법

### `Null 이란?`

- 값이 존재하지 않는다.
- 값자체가 할당되지 않은 상태
- Null 의 값을 허용하려면 ? 를 붙인다.
- String 과 String? 은 다른 타입이다.

```dart
void main() {
String name;
} //예시

int? i = null; //null의 값을 허용
int? i; //도 ok

String? //String과 Null 둘다 가능

int value = nullableValue ?? //앞에 객체가 null 인 경우

int value = nullableValue!; //내가 보증할게 null 아니야 (런타임에 터짐) 추천 X

int? nullableValue = 10;
print(nullableValue?.toString()); //10 출력

int? nullableValue = null;
print(nullableValue?.toString()); //null 출력
```

### `용어 정리`

- 오브젝트 → 현실 세계의 모든 객체
- 클래스 → 오브젝트를 가상세계 용으로 구체화 한것 (붕어빵 틀)
- 인스턴스 → 클래스를 활용해 메모리 상에 만들어 낸 것 (붕어빵)
