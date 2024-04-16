240416(Tue)

플러터 과정 26일차

## 오늘 한 일
ExchangeRate_api를 활용하여 환율 앱을 만들었다.

freezed 사용 중에 오류가 발생해서 고치는 것이 힘들었다.

이번 자료중에서 json 파일에 list 없이 json안에 json의 형태여서

자료를 정제하는데 고민이 있었다. 
conversionRate가 환율의 중요한 비율 값이였는데
이게 리스트가 아닌 json 형태여서 값을 가져온뒤에 fromJson과 toJson을 사용해서
데이터를 잘 가져왔다.

conversionRate에 국가 통화 이름 중에 try가 있어서 오류가 있었다.
dart내에서는 try가 함수로 있어서 이름을 바꿀 필요가 있었다.
