## 📖 Result 패턴
<br>


### 📄 Result  클래스 예시
<br>


```dart
import 'package:freezed_annotation/freezed_annotation.dart';  
  
part 'result.freezed.dart';  
  
@freezed  

sealed class Result<T> with _$Result<T> {  

  const factory Result.success(T data) = Success;  
  
  const factory Result.error(String e) = Error;  
  
}
```
- Result 클래스는 성공시에는 데이터를 실패시에는 String을 담는 객체를 정의


```dart
Future<<List<Hits>> getPhotos(String query) //Result 랩핑

Future<Result<List<Hits>>> getPhotos(String query)
```
- 응답 객체를 Result로 랩핑하여 사용
<br>

### 📄 Result 패턴 사용 효과
<br>

```dart
final photos = await PhotoRepositoryImpl().getPhotos('flower');  

final test;  

switch (photos) {  

  case Success<List<Hits>>():  
  
    test = photos.data[0];  
    
  case Error<List<Hits>>():  
  
    test = photos.e;  
    
}
```
- switch문과 조합하여 모든 처리를 강제할 수 있음
- 여러가지 3개 이상의 성공과 실패를 처리할 수 있음
<br>
<br>
