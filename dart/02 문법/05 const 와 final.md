const 와 final
=============
### 변수와 상수
- 변수(variable): 변하는 수   
- 상수(constant): 변하지 않는 고정된 값을 가짐  

### 변수 변경자 (modifiers)  
- 값를 변경하지 못하게 상수화 하는 변경자 키워드  

### const 상수
```dart  
 const (double) PI = 3.14;  
 PI = 1.45; // error

 const int phoneNum; // error  
```  
- 컴파일타임(기계어로 번역되는 순간)에 값이 결정된다.   
- 변수 선언 시 값이 반드시 필요하다.  

### final 상수
 ```dart     
 final (int) age = 20;  
 age = 21; // error  

 final (String) birth;   
 birth = '1999-09-19';   
 ```
- 런타임(코드가 실행되는 순간)에 값이 결정된다.   
- 선언 시 초기 값이 할당되지 않아도 된다.   
- 필요한 시점에 값 결정이 가능하다.   

