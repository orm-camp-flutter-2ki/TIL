## (필수) 과제 1. 이미지 검색 API 검토
DataSource -  https://pixabay.com/  
가입하여 Image Search API 사용법을 터득할 것. PostMan 등을 활용하여 결과 확인. TIL 에 과정 정리

### 1. 이미지를 검색하기 위한 baseUrl
```dart
https://pixabay.com/api/
```

### 2. 본인의 API 키를 추가한다.
```dart
https://pixabay.com/api/?key=43171022-dca0290df38de24cd7ba6ed14
```

### 3. 원하는 이미지를 필터하기 위해 `q` 뒤에 조건들을 붙여준다.
100자 이하로 입력 가능하다.
```dart
예시) q=flowers+cat+home&image_type=photo&pretty=true

flowers+cat+home : 꽃, 고양이, 집

image_type : 사진

pretty : JSON 코드를 이쁘게 들여쓰기
```

<br></br>

### Postman에서 결과 확인하기

1. 이미지를 `GET`하기 위한 주소를 입력하고 `Send` 클릭
<img width="586" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/c0b393a4-b62d-46a8-b2c5-b1642ef583b5">

2. 통신이 완료되면 200 응답과 코드들이 출력된다.
<img width="585" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/3040e6a5-0c07-49fe-8c11-1d6c157cd95b">

3. 그 중 첫 번째 이미지
<img width="583" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/1cca39e3-6b24-4983-ae2f-f8f02ba9c292">

