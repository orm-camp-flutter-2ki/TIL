> ### 🙋🏻 불변성(immutable)?
데이터가 생성된 후에 수정할수 없음을 의미함

> #### String의 불변성
```dart
String originalString = "Dart is fun";
String newString = originalString.replaceAll("Dart is fun", "hello");
print(newString); // 출력: hello
```
![](https://velog.velcdn.com/images/hee462/post/b2a746f7-6968-42fd-ac22-43dc29562b61/image.png)











> ####  ⭐️ 한줄정리!
이렇게 String이 불변하다는 것은 우리가 한 번 만들면 그 안의 내용을 바꿀 수 없고, 새로운 String을 만들어야 한다는 것이에요. 이것이 불변성의 아주 간단한 개념입니다!




