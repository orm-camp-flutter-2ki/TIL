
> 현재 이러한 데이터를 통신연결하여 데이터 변환을 하려고 한다
![](https://velog.velcdn.com/images/hee462/post/0932c639-17f0-4c60-8f24-96551072375b/image.png)\

> 1)모범 디렉토리 형식으로 파일을 준비한다
![](https://velog.velcdn.com/images/hee462/post/0e5255a4-2da2-457b-b6b7-48fe4302251d/image.png)

> 2)JSON data의 형태를 보고 Data class(DTO)를 생성한다.
tip) toString(), get, ==operator,toJson, fromJson,copyWith
![](https://velog.velcdn.com/images/hee462/post/6888c3fa-5231-43cd-adae-b18c4a6ca61d/image.png)


> 3) data_source에 라이브러리를 사용하여 연결한다
tip) `dart pub add http`
![](https://velog.velcdn.com/images/hee462/post/575c8cf4-10a6-4d4c-a8cf-b88961f80763/image.png)

> 4) 연결이 잘되어 있는지 Test 하여 값이 맞는지 비교한다!
![](https://velog.velcdn.com/images/hee462/post/b9439ba4-eba4-4e58-9b60-73f41e8e1890/image.png)

> 만약 오류가 났다면?
![](https://velog.velcdn.com/images/hee462/post/1e624895-57b7-42cc-ae43-8444f49b2d37/image.png)
![](https://velog.velcdn.com/images/hee462/post/b5857a82-313b-44a8-ab82-b9317181a23e/image.png)
아래의 코드에 초록색으로 표시되어있는 부분과 json의 key값이 일치하는지 확인 할것!



>  5) 마지막 확인까지 해주세요!
![](https://velog.velcdn.com/images/hee462/post/79c4f980-03c8-4afc-8e55-a0c9e35a4768/image.png)




