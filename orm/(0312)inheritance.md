## 1. Named constructors

- Named constructor는 클래스에 여러 개의 생성자를 정의하는 방법 중 하나이다.  
- 클래스에 이름을 지정하여 여러 생성자를 만든다.  
- 다양한 입력 유형을 처리하거나 더 직관적인 인스턴스 생성에 유용하다.  

```dart
class MyClass {

  int studentCount;

  // 기본 생성자
  MyClass(this.studentCount);

  // Named constructor 1: 학생 수를 두 배로 설정
  myClass.doubleCount(int originalCount) {
    this.studentCount = originalCount * 2;
  }

  // Named constructor 2: 특정 값을 가진 인스턴스 생성
  myClass.fixedCount() {
    this.studentCount = 100;
  }
}

void main() {

  // 기본 생성자 사용
  myClass instance1 = myClass(50);
  print(instance1.studentCount); // 출력: 50

  // Named constructor 1
  myClass instance2 = myClass.doubleCount(30);
  print(instance2.studentCount); // 출력: 60

  // Named constructor 2
  myClass instance3 = myClass.fixedCount();
  print(instance3.studentCount); // 출력: 100
}

```

<br></br>

## 2. 상속(inheritance)

* 상속 관계의 표현 방법  
<img width="300" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/f4e57b29-2f43-48e9-97c8-e971698276dd">  

* 올바른 상속
올바른 상속은 "is-a원칙"이라고 하는 규칙에 따른 상속을 말한다.  
```
  Superman is a Hero.  
```

* 잘못된 상속을 하면 `다형성`을 이용할 수 없게 된다.

* 부모 클래스일수록 `추상화`, `일반화` 되고, 자식 클래스일수록 `구체화`된다.

<br></br>

### 오버라이드(override)

override는 부모 클래스에서 이미 정의된 메서드를 자식 클래스에서 재정의(override)할 때 'override'라는 어노테이션(annotation)을 사용한다.  
이것은 상속 관계에서 메서드를 다시 구현하거나 변경하고자 할 때 사용된다.  
어노테이션은 주석문이라는 뜻으로 '@' 키워드가 사용된다.

```dart
class Animal {
  void makeSound() {
    print('일반 동물 소리');
  }
}

class Cat extends Animal {
  @override
  void makeSound() {
    print('야옹');
  }
}

```

<br></br>

## 3. UML 다이어그램 만들기

1. 플러그인에서 UML을 다운 받는다.

<img width="550" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/c473472b-a9ff-43e2-bf86-e55c2f1827a7">

<br></br>

2. 새 UML 파일을 생성한다.

<img width="550" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/a94f6efc-9596-4525-921d-3710e5704c5c">
<img width="376" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/0fdcbebf-30e8-4f5d-a677-0bb54153594e">

<br></br>

3. 작성 예시
<img width="827" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/426c2211-f2ef-44d4-a286-f9b2d2d161f9">

<br></br>

[참고]  
[클래스 다이어그램 구문 및 기능](https://plantuml.com/ko/class-diagram)

