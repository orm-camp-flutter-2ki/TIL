Date : 20240306  

># Dart?
2011년 처음 공개된 자바스트립트를 대체하기 위해 탄생한 언어  
객체지향 및 함수형 프로그래밍을 지원한다.  

># 문법 기초 알아보기
- 다트의 함수  
  
  ~~~
  // 함수의 형태 :  y = f(x)

  int f(int x) {
      return 3 * x;
  }
  ~~~
- 변수  
  - 데이터를 담는 상자. 기본 자료형을 사용하거나 새용자가 새로운 타입을 정의 할 수 있다.
  ~~~
  var name = 'mimi';
  String name = 'nini';
  ~~~

- 기본 자료형  
int : 정수, double : 실수(소수점), string : 문자열, bool : 참 또는 거짓(진위)


- 문자열
   - 작은 따옴표 또는 큰따옴표 사용 가능 하지만 작은따옴표를 쓰는 것이 표준이다.  
  인용문을 쓸 때는 따옴표 3개짜리를 쓴다.
~~~
String _name = '김둘리'
String _name = "김둘리"  

print(''' "안녕"이라고 말했다 ''');
~~~  
- 문자열 포멧  
  - $를 사용하여 변수를 결합해서 쓴다.  

  ~~~
  String _name ='jane';
  int _age = '10';
  
  void main(){
    print ('$_name은 $_age살 입니다.');
  }
  ~~~  

- 진위  
  - true 또는 false 값을 가진다.  
  
  ~~~
  bool isOpen = true; // 참
  bool small = i < 10; // i는 10 보다 작다.
  ~~~
  
- 숫자  
정수 int, 실수 double, 숫자 num
num은 int, double 둘 다 사용 가능  
int와 double은 교집합이 없으므로 형변환이 자동으로 되지 않아서 따로 해줘야 한다.  
int로 선언한 변수에는 double을 못 넣는다는 말. 반대로도 마찬가지.  
일부 언어에서는 더 큰 자료형인 double 타입에 int 타입을 대입하는 자동 형변환을 지원하기도 하지만 다트에서는 지원하지 않는다.

    ![alt text](image-3.png)  
    ~~~
    int _age = 10; // 정수
    double _height = 145.3; // 실수
    num _weight = 45.2; // 실수
    num _size = 100; // 정수

    double a = _age; // error!
    
    double a = Int.parse(_age); // OK!    
    ~~~

- 타입 추론
  - 개발자가 변수를 선언 할 때 타입을 쓰지 않아도 컴파일 할 때 알아서 타입을 판단하여 넣어주는 것.
  var
  ~~~
  var i = 10; // int
  var d = 10.0; // double
  var s = 'hello'; // String
  var b = true; // bool
  ~~~  
- 상수  
  final
  - [const와 final 의 차이점](https://discordapp.com/channels/1209290144444846140/1209312602891747408/1214915284171886654)
  ~~~
  final String name = 'mikey';
  name = 'mini'; // error
  ~~~

- 산술연산자  
  +, -, / 나누기(double), ~/ 몫(int), % 나머지(int)  
    
- 증감연산자  
int num = 0;  
num++ -> 나중에 계산, 일반적  
++num -> 계산 먼저  
   ~~~
    // 아래는 모두 같은 값을 가진다.
    num++
    num = num+1
    num +=1
    ~~~
- 비교연산자  
   ==　같다 　　!=　다르다　　>　더 크다　　　<　더 작다  
   　　　　>=　크거나 같다　　　<= 　 작거나 같다

- 논리연산자   
&&　 그리고　　　||　 또는　　　　== 　같다　　　! 　부정　　　!=　 다르다  

- 타입검사 
  - is 　　 　타입이 같으면 true 
  - is! 　　 　타입이 다르면 true  
  ~~~
  int a = 10;
  if(a is int){
    print('정수');
  }

  String text = 'hello';
  if(text is! int){
    print('it isn't number');
  }
  ~~~

- 형변환  
명시적 : as 사용
암시적 : 포함관계 일 경우 as 생략 가능  
    ~~~
    var c =30.5;
    int d = c as int; // 에러
    num n = d; // as num; 생략 가능
    ~~~
    형변환이 불가능 할 경우 에러가 발생한다.  
    강제 형변환이므로 터진다. 날 믿고 그냥 형태 바꿔 컴퓨터야~ 하고 명령하는 것.


- print함수  
  - 반환값이 void인 대표적인 함수
  ~~~
  print('Hello');
  ~~~  

----
>조건문  

- 분기 if문
  ~~~
   String text = 'Hello;

   if(text is int){
    print('int');    
   } else if(text is double){
    print('double;);
   }else{
    print('not int or double');
   }
  ~~~  

- 삼항연산 활용 분기
    ~~~
    // 공식
    [진위 값] ? [true 일 때 값] : [false 일 때 값];

    bool isRainy = true;
    String result = '';

    var todo = isRainy? '빨래 안할래':'빨래 할래';

    // if문으로 표현하면 아래와 같다.
    if(isRainy){
        result = '빨래 할래';
    }else{
    result= '빨래 안할래';
    }

    ~~~ 

- switch case  
  - enum(열거형)과 함께 사용시 모든 케이스 검사 강제성이 생김.  
  - 사람의 실수를 미연에 방지 할 수 있음

    ~~~
    enum Status {Ready, Start, Stop, Pause}

    void main(){
        var status = Status.Start;
        switch(status){
           case Status.Ready:
            print('준비');
            break;
           case Status.Start:
            print('시작');
            break;
         case Status.Stop:
            print('멈춤');
            break;
         case Status.Pause:
            print('일시정지');
            break;            
        }
    }
    ~~~

----
> 반복문

- for 문  

    ~~~
     var items = ['apple','banana','mango'];

     for(int i =0; i < items.length; i++){
        print(items[i]);
     }
    ~~~
    
    이 구문은 몇 번 루프를 돌까요?
    ~~~
    for(;;){
        print('!!!!');
    }
    for(변수초기화;조건;변수조작)
    ~~~ 
    정답은 무한으로 돈다..!  
    조건을 쓰지 않으면 true로 인식하기 때문에.

    - dart에는 없는 forEach 문법 대체하기  
    ~~~
    for(String item in items){}
    
    list.forEach(e){}
    ~~~
    ---- 

- named parameter (매개변수)
    ~~~
    // named parameter 를 쓸 때는 기본값을 꼭 넣어줘야 한다.
    void something({String name =10 , int age='', String hobby=''}){}
    something(name:'joy',hobby:'soccer'); // 순서가 바뀌어도 이름을 적어주기 때문에 OK!
    
    // 이렇게 named와 아닌 것을 섞어서도 쓸 수 있다.
    void something(String name, {int age='', String hobby=''}){} 
    
    ~~~

 - 매개변수 vs 인자 = parameter vs argument
    ~~~
    void myMethod(int myParam){} => 매개변수

    int myArgument = 3;
    myMethod(myArgument) => 인자

    ~~~ 

---- 
> [ 컴파일 언어와 인터프리터 언어]  
인터프리터 언어 : 한 줄 읽으면서 바로 실행하는 것  
컴파일 언어 : 전체를 다 읽고 실행하는 것
----
----
----

## 오늘의 블로깅 
- [객체지향형 프로그래밍과 절차지향형  프로그래밍 그리고 함수형 프로그래밍](https://somarok.tistory.com/4)
- [컴파일 타임과 런타임](https://somarok.tistory.com/5)
- [const와 final의 차이점](https://somarok.tistory.com/6)