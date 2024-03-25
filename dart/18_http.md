## 데이터 소스
- 프로그램이 사용하는 모든 원천 데이터
- 데이터소스에서 가공되지 않은 데이터를 추출해서 사용 가능한 데이터로 변환 -> 이 데이터를 활용해 뭐든 만들 수 있다.
- 대부분 서버와의 통신은 이전에 배운 JSON 을 사용

## jsonDecode() 함수
- 서버에서 데이터를 요청하면 json String 형태로 받는다.
- 이걸 Map<String, dynamic> 형태로 바꿀 수 있는 함수
- 일련의 과정 : 서버에 요청 -> json String 받음 -> 받은 json String 을 jsonDecoede() 를 사용해 Map<String, dynamic> 형태로 변환 -> 클래스에서 정의한 fromJson() 을 활용해 Map 을 객체에 넣음 -> 데이터 사용

## json List String 을 List<모델> 로 변경하려면 map() 을 활용
  ```
  if (response.statusCode == 200) {
      List jsonList = jsonDecode(response.body);
      return jsonList.map((e) => User.fromJson(e)).toList();
  } else {
      throw Exception('응답없음');
  }
  ```
- response.statusCode == 200 이면 성공했을 경우
- json String 을 List 에 넣고 map 을 사용
