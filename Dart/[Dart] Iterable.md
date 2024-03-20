> ####  🙋🏻Iterable?
 Iterable은 데이터 컬렉션을 나타내는 `추상 인터페이스`입니다.<br>
 Iterable은 여러 개의 요소를 `순회`할 수 있는 객체를 정의하며, <br>
 많은 **Dart 내장 클래스**와 사용자 정의 클래스가 Iterable을 구현


>**forEach**)<br>
Iterable의 각 요소에 대해 주어진 `함수를 실행`합니다.<br>
ex) 값을 출력할때 사용<br>

>**map**) <br>
Iterable의 각 요소에 주어진 `함수를 적용`한 후, 그 결과로 `새로운 Iterable을 생성`합니다.<br>
_Tip) 변환작업 목적_<br>
![](https://velog.velcdn.com/images/hee462/post/e93838fb-31dc-4c53-9a0c-18ec73abf7e0/image.png)



>**where**)<br>
주어진 `조건`에 따라 요소를 `필터링`하여 새로운 Iterable을 생성합니다.<br>
_Tip) 선택 목적_<br>
![](https://velog.velcdn.com/images/hee462/post/04196690-186e-4bba-8eb0-b624722683b5/image.png)

>**reduce**)<br>
요소를 결합하여 `단일 값`으로 줄입니다.<br>
_Tip) max,min으로 최댓값,최솟값 한번에 알 수 있음 <br>
import:Math.io_
![](https://velog.velcdn.com/images/hee462/post/95e9c148-dcc6-432a-8995-fa8b777a8870/image.png)



>**toList, toSet**)<br>
Iterable을 리스트나 집합(Set)으로 변환합니다.<br>
![](https://velog.velcdn.com/images/hee462/post/ecbf9b0e-39e2-42b8-b9e5-fe367c222d46/image.png)
![](https://velog.velcdn.com/images/hee462/post/e2a9d64f-9323-4f6d-9895-227ab11f8831/image.png)

>**any, every**)<br>
주어진 `조건을 만족하는 요소`가 있는지 확인<br>
_ex) any 는 true만 뽑아서 반환 가능 <br>
    every는 true,false 가능_<br>
    ![](https://velog.velcdn.com/images/hee462/post/c69684a7-0481-463f-908b-15f984604d91/image.png)

>**fold)**<br>
주어진 초기값과 함수를 사용하여 ,`모든 요소를 결합하여 단일 값`으로 반환<br>
_ex) 접으면서 값 확인 : 리스트의 모든요소 더하거나 곱하기_<br>

>_ex)diagram_
![](https://velog.velcdn.com/images/hee462/post/5ee9af9d-98e8-479b-baa2-1b1bac569548/image.png)
