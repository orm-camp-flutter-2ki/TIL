> ### 🙋🏻 불변성(immutable)?
데이터가 생성된 후에 수정할수 없음을 의미함

> #### String의 불변성
```dart
String originalString = "Dart is fun";
String newString = originalString.replaceAll("Dart is fun", "hello");
print(newString); // 출력: hello
```
![](https://velog.velcdn.com/images/hee462/post/b2a746f7-6968-42fd-ac22-43dc29562b61/image.png)

> ####  ⭐️ 한줄정리!<br>
이렇게 String이 불변하다는 것은 우리가 한 번 만들면 그 안의 내용을 바꿀 수 없고, 새로운 String을 만들어야 한다는 것이에요. <br>
이것이 불변성의 아주 간단한 개념입니다!<br>

> 
🙋🏻 String Buffer?<br>
• 미리 메모리를 확보해놓고(List처럼 만들어 놓고) 거기에 붙이는 것<br>
• new를 하는 것에 비용이 발생함<br>
• final, const 사용하는 것도 이러한 비용을 줄이려고 하는 것<br>
• String Buffer의 경우(위경우보다 1000배 빠름)<br>
 
> ⭐️ 차이점 정리!<br>
String, StingBuilder, StringBuffer의 차이<br>
• String이 느리고 Buffer가 빠름<br>
• String이 불변이라서 느림.<br>
• String은 new로 새로운 것을 만들기 때문에<br>
• 알고리즘에서 쓸 일은 있어도 앱만들면서 StringBuffer 쓸 일은 없다.<br>

