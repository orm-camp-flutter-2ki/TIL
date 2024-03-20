> ####  🙋🏻Iterable?
 Iterable은 데이터 컬렉션을 나타내는 `추상 인터페이스`입니다. <br>
 Iterable은 여러 개의 요소를 `순회`할 수 있는 객체를 정의하며,<br>
 많은 **Dart 내장 클래스**와 사용자 정의 클래스가 Iterable을 구현


>**forEach**)<br>
Iterable의 각 요소에 대해 주어진 `함수를 실행`합니다<br>
ex) 값을 출력할때 사용<br>

>**map**) <br>
Iterable의 각 요소에 주어진 `함수를 적용`한 후, 그 결과로 `새로운 Iterable을 생성`합니다.<br>
_Tip) 변환작업 목적_<br>

>**where**)
주어진 `조건`에 따라 요소를 `필터링`하여 새로운 Iterable을 생성합니다.<br>
_Tip) 선택 목적_<br>

>**reduce**)
요소를 결합하여 `단일 값`으로 줄입니다.<br>
_ex) 최댓값,최솟값구하기_<br>

>**toList, toSet**)<br>
Iterable을 리스트나 집합(Set)으로 변환합니다.<br>

>**any, every**)<br>
주어진 `조건을 만족하는 요소`가 있는지 확인<br>
_ex) any 는 true만 뽑아서 반환 가능 <br>
    every는 true,false 가능_<br>
    
>**fold)**<br>
주어진 초기값과 함수를 사용하여 ,`모든 요소를 결합하여 단일 값`으로 반환<br>
_ex) 접으면서 값 확인 : 리스트의 모든요소 더하거나 곱하기_<br>

>_diagram)_
![](https://velog.velcdn.com/images/hee462/post/5ee9af9d-98e8-479b-baa2-1b1bac569548/image.png)
