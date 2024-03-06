데이터 타입(Data Type)
=============
  
<br/>

## 기본 데이터 타입
### int: 정수형  
> ```
> int age = 10;
> ```

<br/>

### double: 실수형  
> ```
> double PI = 3.14;
> ```
>✔️ Dart에서는 double 에서 int 포함하지 않음 (교집합이 없음)   

<br/>

### num: 숫자 포함 관계
> ```
> num i = 1;
> num j = 4.2;
> ```
>✔️ int, double 선언 가능   

<br/>

### String: 문자열  
> ```
> String name = 'myName'; // 큰 따옴표도 가능하지만, 작은 따옴표가 표준
> int age = 20;
> pint($name은 $age살 입니다..);
> pint($name은 ${name.langth}글자 입니다..);
> ```

<br/>

### bool: 참-거짓(bloolea, true-false)  
> ```
> bool isClean = false;
> ```

<br/>

### List: 순서가 있는 변수들의 집합
> ```
> // 생성과 함께 초기화
> List<int> numbers = [1, 2, 3, 4, 5];
> ```
> ```
> // 리스트에 값, 요소, 데이터, 변수 추가
> numbers.add(6);
>
> // 리스트의 특정 인덱스에 접근
> int firstNumber = numbers[3]; // 4;
>
> // 리스트의 길이 확인
> int M = numbers.length; // M == 6
>
> // 리스트 출력
> print(numbers); // 출력 결과: [1, 2, 3, 4, 5, 6]
> ```
>✔️ 순서(Index)가 있음 (0부터 시작)  
>✔️ 같은 리스트 내 다양한 데이터 타입 포함 가능   
>✔️ 필요에 따라 항목을 추가하거나 삭제 가능  

<br/>

### Map: 키-값의 쌍 (key-valued)  
> ```
> // 이름(key)과 나이(value)를 매핑
> Map<String, int> person = {
>   'John': 30,
>   'Alice': 25,
> };
> ```
> ```
> // 요소 추가
> person['Bob'] = 35; // 'Bob' 추가
>
> // 요소 제거
> person.remove('Alice'); // 'Alice' 삭제
>
> // 맵의 모든 요소 제거
> person.clear();
>
> // 특정 키의 값
> int johnAge = person['John'];
>
> // 모든 키값
> Set<String> keys = person.keys;
> ```
>✔️ 키에 해당하는 값, 특정 키를 사용하여 해당하는 값을 가져옴

<br/>

