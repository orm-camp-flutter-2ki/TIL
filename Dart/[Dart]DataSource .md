>** 🙋🏻DataSource?**
- 데이터의 근간이 되는 원천재료
- 프로그램이 사용하는 원천 데이터 모든것이 해당 함
_ex) 밀가루과자 -> 밀가루
	찰흙 집 -> 흙_
    
데이터 소스로 무얼 하지?
공공포털 데이터로 -> 버스앱, 지하철 앱, 날씨 기타등등
데이터 소스만 있다면 다양한 방식으로 사용가능<br>
즉) DataSource 에서 추출한 가공되지 않은 데이터를 사용가능한 데이터로 변환하여 여러방면으로 사용가능함

> DataSource의 종류<br>
- Text
- File
- JSON
- XML
- CSV
- RDBMS
- NoSQL 
기타등등 


> 이렇게 컴퓨터와 통신을 위한 라이브러리를 사용하여 데이터를 변환하자 
![](https://velog.velcdn.com/images/hee462/post/2df0bf82-79c3-44ef-9229-47ac89ec8942/image.png)
`dart pub add http` : 가장 근본이 되는 라이브러리
    
> ex)![](https://velog.velcdn.com/images/hee462/post/0fedad61-0f56-42e7-a32a-e1af2cf9c4f8/image.png)
위에처럼 then() 사용도 가능하지만 아래의 코드가 이해하기가 쉽다.


### [⭐️ 추가예시](https://velog.io/@hee462/Dart-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EB%B3%80%ED%99%98JSON%ED%86%B5%EC%8B%A0%EB%B0%9B%EC%95%84%EC%84%9C-%EB%B3%80%ED%99%98)

tip)<br>
json 제외하고도 다양한 라이브러리가 있어 xml,csv가 있지만,<br>
거의 95% 정도는 json을 사용하며, <br>
csv는 key :value 값을 두개다 저장하지 않기 때문에 , 많은 양의 데이터라면 csv를 활용하는 편이니 익혀두면 더 좋다<br>
