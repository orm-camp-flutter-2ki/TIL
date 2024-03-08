## Class 클래스
1. 필드(Field)
  - 클래스에서 쓰일 변수를 등록하는 곳
2. 메서드(Method)
  - 클래스의 기능이다. 단독으로 동작할 수 없기에 함수와 구별한다.
3. 생성자(Constructor)
  - 인스턴스를 생성하는 방법을 제공
4. 인스턴스(instance)
  - 정의한 클래스로 인스턴스를 생성 할 수 있다
  - 새로운 변수의 타입이 이용 가능해 진다. (Hero 클래스를 정의하면 Hero 타입의 변수가 이용 가능)
    
![image](https://github.com/Gunbam27/TIL/assets/95085649/a3e4000f-b10b-4652-a97b-d9d312253ad6)

인스턴스 생성

![image](https://github.com/Gunbam27/TIL/assets/95085649/89ead404-d3a3-49bb-9037-c5da88bd3220)
<br/>
<br/>

## 레퍼런스 타입과 참조

Dart는 모든 타입이 레퍼런스 타입이다.

레퍼런스 타입이란?
> 객체(Object)는 Class의 인스턴스로 특정 메모리 슬롯에 저장된다.
참조(Reference)는 'Object 변수나 함수'가 저장된 곳의 주소를 일련의 bit로 가지고 있는 것이다.
<br/>
메모리 구조

![image](https://github.com/Gunbam27/TIL/assets/95085649/8c36e65c-2e1b-416d-b2d3-f440a88dac2b)

- Code :
함수, 제어문, 상수 등이 저정됨
- Data :
초기화된 전역 변수와 static 변수가 할당되는 영역
- BSS :
초기화 안된 전역변수
- Heap :
힙은 동적으로 할당된 메모리를 저장하는 곳. 인스턴스가 이곳에 할당된다.
- Stack :
함수 호출 시 생성되는 지역 변수와 매개 변수가 저장되는 영역


## 파라미터(parameter)
```dart

//고정값으로 이루어져 있는 형태. 쓸 일은 없을 것 같다.
void main(){
  Slime killLime = Slime();
}
class Slime{
  String name = '킬라임';
  int hp = 50;

  Slime();
}

//형식 매개변수 (formal parameters)
void main(){
  Wizard killdong = Wizard('킬동', 50, 200);
}

class Wizard {
  String name;
  int hp;
  int mp;

  Wizard(this.name, this.hp , this.mp);
}

//named parameter
//생성자에 { } 를 사용하면 named parameter 임
//데이터 타입이 Null을 허용하지 않으면 required 를 붙여야 함
//값을 지정할때는 js 객체처럼 쓴다. key:value

void main(){
  Hero superman = Hero(name:'슈퍼맨',hp:50);
}

class Hero{
  String name;
  int hp;
  Sword? sword;
  
  Hero({required this.name,required this.hp,this.sword,});
}

```


