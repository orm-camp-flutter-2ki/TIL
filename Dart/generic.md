- 타입이 없을 때 문제점
  - 타입이 없다 = dynamic(NO!!), var는 이미 컴파일에서 알고 있으므로 타입이 없는게 아님.
    - 런타임 에러 나기 쉽다.
    - IDE가 컴파일 에러를 미리 찾을 수 없음

# 제네릭(Generic)
- 타입을 나중에 원하는 형태로 정의할 수 있음
- 타입 안전(type safe) 효과

<제네릭을 사용한 pocket 클래스>
```
class Pocket<E> {
    E? _data;

    void put(E data) {
        _data = data;
    }

    E? get() {
        return _data;
    }
}
```
# enum 열거형 - 정해둔 값만 넣어둘 수 있는 타입
````
enum AuthState {
    a,
    b,
    c,
}

//switch와의 조합으로 모든 케이스 강제작성
switch(state) {
    case Authstate.a :
    // TODO : Handle this case.
    case Authstate.b :
     // TODO : Handle this case.
    case Authstate.c :
     // TODO : Handle this case.
}

````

## 문자열 처리
- 일부 떼어내기(substring)
```
const string = 'HELLO';
print(string.substring(0,2)); //'HE'
```
- 일부 치환(replaceAll)
```
cons string = 'HELLO';
print(string.replaceAll('LL',XX')); //'HEXXO'
```
- 분리(split)
```
final string = '1,2,3';

final splited = string.split(',');
//리스트 형식으로 splited에 들어감
splited.forEach((e) {
    print(e);
 });
```

## String = 불변!, String이 제공하는 모든 메서드는 엑세서(값을 변화시키지 않음!!)
- 레퍼런스는 바뀌지만 가리키는 값 자체는 바뀌지 않음, 그래서 new String으로 새로 만들기 때문에 처리 시간 오래 걸림
- 계속 메모리 차지하며 있다가, 메모리 청소부(GC)가 청소함
-> StringBuffer로 처리하면 훨씬 빠름