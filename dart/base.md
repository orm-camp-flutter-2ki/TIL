#### 산술 연산자
/  나누기 (double 타입 반환)
~/ 몫 (int 타입 반환)
%  나머지 (int 타입 반환)


#### String to int
String str = '';
int num = int.parse(str);
#### as
- 관련 에러
A value of type 'num' can't be assigned to a variable of type 'int'.

**일부 언어에서는 더 큰 자료형인 double 타입에 int 타입을 대입하는 자동 형변환을 지원하기도 하지만 다트에서는 지원하지 않음**

#### 형변환

### 런타임 / 컴파일

int.parse(str) 도 runtime E 남
toInt()와 다름
만약 문자열이 숫자가 아닐 때(숫자가 아닌 문자가 포함) `FormatException`이 발생합니다.

### 매개변수 vs. 인자(parameter vs. argument)
매개변수 : 함수를 정의할 때 사용하는 변수 (=인자)
인자 : 실제로 함수를 호출할 때 넘기는 변수값

### named parameter
#### 초기값
예전에는 
```
void something({int age, String name})
```
도 가능했으나
dart 업데이트 이후에는
```
void something({int age = 10, String name = 'john'})
```
처럼 초기값 넣어야 함

단, nullable하면 초기값 안넣어도 됨

### nullSafety
* value가 null이면 0
```
int value = nulllableValue ?? 0
```

* 널이 아님을 보장함. 고수 이하 쓰지 말 것
```
int value = nullableValue!;
```

* null 검사한 거라 안전함
```
int value = nulllableValue ?? 0
```


<br>
* String과 String?은 다른 타입이라고 봐도 됨
앞으로 할 건 ?를 떼는 방법을 배워야함
<br>

## 클래스

### 클래스 작성

* 필드 (=멤버변수=전역변수(global variable))

### 함수 vs. 메소드
클래스 안의 함수 = 메소드
<> 최상위 함수(main)

### 클래스 정의에 따른 효과
인스턴스 생성
ㄴ 인스턴스 => 메모리 사용

int, String, double, bool 외의 인스턴스 만드려고 할 때 class 만드는 것