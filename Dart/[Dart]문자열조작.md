> #### 🙋🏻  왜？ 문자열 조작을 해야하나요?
텍스트 처리(Text Processing) : 문서 입력,텍스트 데이터처리 용이
데이터 변환(Data Transformation) : 날짜,숫자를 문자열로 변환
문자열 검색 및 필터링(String Searching and Filtering) :검색, 특정패턴 찾는 작업
데이터 표시(Data Presentation) :사용자에게 안내메세지

> ###  종류
#### 1) 문자열 결합 (String Concatenation)
- 두 개의 문자열을 결합할 때는 + 연산자를 사용합니다.
```Dart
String greeting = "Hello";
String name = "John";
String message = greeting + ", " + name + "!";
print(message); // 출력: Hello, John!
```
#### 2)문자열 길이 확인 (Length of a String)
- 문자열의 길이는 length 속성을 사용하여 확인할 수 있습니다.
length : 길이
isEmpty : 길이가 0인지
```dart
String str = "Dart is fun!";
int length = str.length;
print("Length of the string: $length"); // 출력: Length of the string: 12
```
#### 3)부분 문자열 추출 (Substring Extraction)
- substring() 메서드를 사용하여 원하는 부분 문자열을 추출할 수 있습니다.
```dart
String str = "Dart Programming";
String substr = str.substring(5, 12); // 인덱스 5부터 11까지의 부분 문자열 추출
print(substr); // 출력: Programming
```
#### 4)문자열 검색 (String Search)
contains() 메서드를 사용하여 특정 문자열이 포함되어 있는지 여부를 확인할 수 있습니다.
contains() : 포함 관계
endsWith() : 끝나는 단어가 맞는지
indexOf() : 단어가 몇 번째에 있는지
lastIndexOf() : 뒤에서 몇 번째에 단어가 있는지
```dart
String str = "Hello, Dart!";
bool containsDart = str.contains("Dart");
print(containsDart); // 출력: true
```
#### 5)문자열 치환 (String Replacement)
- replaceAll() 메서드를 사용하여 문자열 내에서 특정 문자열을 다른 문자열로 대체할 수 있습니다.
```dart
String str = "Dart is awesome!";
String newStr = str.replaceAll("awesome", "amazing");
print(newStr); // 출력: Dart is amazing!
```
#### 6)문자열 분할 (String Splitting)
- split() 메서드를 사용하여 문자열을 특정 구분자를 기준으로 분할할 수 있습니다.
```dart
String sentence = "Hello, how are you?";
List<String> words = sentence.split(" ");
print(words); // 출력: [Hello,, how, are, you?]
```
