> ** ⭐️ 데이터 종류**
#### CSV : 데이터 콤마(,)로 나눈 형식
ex) ```Stirng str ="홍길동,한석봉,신사임당";```
#### 프로퍼티 형식의 파일 읽기
Properties클래스를 사용하여 key와 value의 쌍으로 읽고 쓰기가 가능
ex) ata.properties 파일의 내용
 	heroHp=100
	heroMp=10
#### XML 형식
- <> 태그를 활용한 기술 방식 
- 포함관계를 기술할 수 있음
![](https://velog.velcdn.com/images/hee462/post/d1e4a1c3-b567-4bcb-99f8-1fe00bf09f1f/image.png)
- DOM Parser, SAX Parser 등을 통해 파서를 제작할 필요가 있음
#### JSON 형식
- 네트워크 통신에서 가장 많이 사용되고 있음
- XML에 비해 적은 용량
- [   ] 로 리스트, { } 로 객체를 표현
키(key): 값(value) 형태
   ![](https://velog.velcdn.com/images/hee462/post/f62cb159-d9a1-4d01-ad1c-36f387b1f408/image.png)
Dart 의 Map<String, dynamic> 과 똑같이생겨 활용해서 바로 사용가능

> **원래 컴퓨터에서의 직렬화의 의미는**<br>
- 데이터 구조나 객체 상태를 저장하고 나중에 재구성할 수 있는 포맷으로 변환하는 과정<br>
- 객체를 파일의 형태 등으로 저장하거나, 통신하기 쉬운 포맷으로 변환하는 과정을 의미<br>
- 클래스 내부의 필드에 다른 클래스가 있다면 모두 직렬화 처리를 해 줘야 함<br>

> **Dart의 직렬화 (Serialization)**
직렬화(serialization,  encoding와 의미적으로 비슷) : <br>
`클래스` -> `Json`<br>
역직렬화(desirialization,  decoding와 의미적으로 비슷) : <br>
`Json` -> `클래스`<br>
