## 레퍼런스 타입과 참조

### Dart에서는 모든 타입이 레퍼런스 타입이다.
- int 형, doubl 형 같은 기본형(primitive type) 뿐만 아니라 String도 Hero()와 같은 **"레퍼런스 타입"** 이다.

<img width="400" alt="스크린샷 2024-03-08 오후 4 41 43" src="https://github.com/NalaJang/TIL/assets/73895803/d127cae9-ddaa-41d0-a196-26c49fdc1e60">

<img width="400" alt="스크린샷 2024-03-08 오후 4 43 33" src="https://github.com/NalaJang/TIL/assets/73895803/0b6f53ea-df7e-417b-ad74-082b882d3f96">

<br></br>

* Code  
실행할 프로그램의 코드(함수, 제어문, 상수)

* Data  
초기화된 전역 변수, 정적 변수

* BSS(Blocked Stated Symbol)  
선언하고 초기화 안된 전역 변수(프로그램 시작 시 모두 0으로 초기화)
전역 변수를 초기화를 하지 않았으면 분명 변수에 값을 넣어주는 과정이 필연적으로 필요하다.
따라서, 0으로 초기화가 되려면 '변수'가 위치한다.

* Heap  
동적 할당, Cleric()

* Stack  
지역 변수, 매개 변수 등

<img width="411" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/c846c467-97ce-436a-a13a-761c309c11b5">

<br></br>

**Q. bss 와 data 영역의 차이?**  
bss 영역의 초기화되지 않은 변수의 값은 실행 도중 채워질 것이므로 변수의 값을 따로 기억할 필요가 없다.  
그렇기 때문에 메모리의 어떤 위치를 차지하지만 디스크 공간은 필요하지 않고, 프로그램의 크기(= exe 파일의 크기)를 늘리지 않는다.  

[참고]  
<https://dev-game-standalone.tistory.com/71>  
<https://stackoverflow.com/questions/16557677/difference-between-data-section-and-the-bss-section-in-c>

<br></br>

## Named Parameter 다시 정리

<img width="550" alt="스크린샷 2024-03-08 오전 11 43 54" src="https://github.com/NalaJang/TIL/assets/73895803/3cc41e21-0f0e-47c9-961f-c75f8474710b">



필수 파라미터와 named(옵션) 파라미터와 동시에 사용할 수 있다.  
**이런 경우에는 필수 파라미터가 앞에 와야 한다.**

```dart
class Hero {
  String name;
  int hp;
  Sword? sword;
  
  Hero(this.name, this.hp, {this.sword});
}
```

<img width="352" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/33af7dac-41a2-4d46-9f2a-3b4acddfcff8">


<br></br>

## 정적 메소드 안에서 액세스 할 수 있는 것은 정적 멤버만 가능

<img width="400" alt="스크린샷 2024-03-08 오후 12 31 25" src="https://github.com/NalaJang/TIL/assets/73895803/41714636-a5f7-4510-a9dd-9052182f6111">
