## Result
### 에러 처리
기본적으로 예외는 try - catch 를 활용하여 처리한다.  
하지만 런타임 에러뿐만 아니라 논리적인 오류나 예외 상황에 대한 처리를 하기에는 부족하다.  
✅ Result 패턴은 성공, 실패 시 처리에 유용한 패턴이다.

### 성공과 실패 중 하나를 리턴하는 Result 클래스 예시
* Result 클래스는 성공 시에는 데이터를, 실패 시에는 Exception(또는 String)을 담는 객체를 정의한다.
* 이 외에도 더 많은 반환 케이스가 필요하면 추가한다.
* sealed 클래스는 타입 봉인 효과를 가진다.(enum하고 비슷)

```dart
```
### 사용 예시
* 응답 객체를 Result 클래스로 랩핑하기
<img width="683" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/1543806d-966d-44ed-9feb-0964e01a92a8">

* 예외가 예상되는 지점에서 try - catch 사용하기

### Result 패턴 사용 시 효과
* enum과 동일하게 switch 문과 조합하여 case를 강제할 수 있다.
* 3개 이상의 성공과 실패를 처리할 수 있다.

<br></br>

## freezed 라이브러리
freezed = json_serializable + Equatable(==, hashCode, toString, copy) + immutable
* 선언된 필드들의 getter를 만들어서 외부에서 값을 변경할 수 없도록 한다.
* sealed class 작성을 편하게 해준다.
```dart
dart pub add freezed
```



<br></br>

## (필수) 과제 1. 이미지 검색 API 검토
DataSource -  https://pixabay.com/  
가입하여 Image Search API 사용법을 터득할 것. PostMan 등을 활용하여 결과 확인. TIL 에 과정 정리

### pixabay 사용 설명서

<img width="115" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/504da3ee-8e9c-4aed-b9a2-8cc18e1b3b7e">

If you make use of the API, show your users where the images and videos are from, whenever search results are displayed. That's the one thing we kindly request in return for free API usage.
> 이미지 출처를 표기해야 한다.

Hotlinking  
Returned image URLs may be used for temporarily displaying search results. However, permanent hotlinking of images (using Pixabay URLs in your app) is not allowed. If you intend to use the images, please download them to your server first. Videos may be embedded directly in your applications. Yet, we recommend storing them on your server.
> 반환된 이미지 URL은 일시적으로 검색결과를 표시하는 데 사용될 수 있다.  
> 그러나 이미지의 영구적인 핫링크(앱에서 Pixabay URL 사용)는 허용되지 않는다.  
> 영구적으로 이미지를 사용하려면 먼저 서버에 저장하는 것을 추천

### 이미지 검색
#### 1. 이미지 검색을 위한 baseUrl
```dart
https://pixabay.com/api/
```

#### 2. 본인의 API 키를 추가한다.
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

1. `New`, `HTTP`를 클릭한다.
<img width="480" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/aae31589-40f2-4150-90ff-6a1bf5c6a740">
<img width="530" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/14332754-04cd-4525-ae62-06dcbaebee1b">


2. 이미지를 `GET`하기 위한 주소를 입력하고 `Send` 클릭
<img width="586" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/c0b393a4-b62d-46a8-b2c5-b1642ef583b5">

3. 통신이 완료되면 200 응답과 코드들이 출력된다.
<img width="585" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/3040e6a5-0c07-49fe-8c11-1d6c157cd95b">

4. 그 중 첫 번째 이미지
<img width="583" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/1cca39e3-6b24-4983-ae2f-f8f02ba9c292">

