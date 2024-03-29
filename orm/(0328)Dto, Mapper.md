## DTO(Data Transfer Object)

데이터 소스를 모델 클래스에서 변환하는 과정에서 순수하게 클래스에 담기 위한 중간 전달 객체  

Json -> DTO -> Model Class

잘못된 데이터 소스(Json)를 받더라도 안 터지게 하려는 클라이언트 개발자의 방어 수단  
✅ **fromJson, toJson도 여기에 만든다.**

특징
* 모든 클래스가 nullable 변수
* 직렬화, 역직렬화 제공

### DTO가 도입된다면 역할 분담이 가능하다.
* DTO: fromJson(), toJson()
* 모델 클래스: 불변 객체(+ 나머지 4개는 옵션)

### DTO 쉽게 만들기
JsonToDart 플러그인 설치  
<img width="730" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/76c1435e-6ad5-4151-a66f-4a80e41e1bf6">
<img width="730" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/aa05672e-0f03-4a19-b917-b7e695e73697">  
세팅  
<img width="659" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/c94a4031-555c-4399-a51f-859e2976a89e">

### DTO가 필요한 이유
* Model class는 non-nullable 한 값만 가지고 있도록 한다.
* Json 데이터가 null 값을 포함하고 있을 가능성도 있기 때문이다.
* Map -> Model class 변환 시 nll 값 등의 예외를 사전에 걸러내기 용이하다.
* Json 값에 예외가 없다면 반드시 DTO를 도입할 필요는 없다.

### 모델 클래스 다시 정리
* 모든 클래스가 non-nullable 상수
* 직렬화
* 역직렬화
* ==
* hashCode 재정의
* toString() 재정의
* 깊은 복사 제공 copyWith()

* Json을 그냥 받지 않고 내 앱에서 필요한 형태로 필드를 수정할 수 있다.
* 데이터 소스의 모양을 확인하지 않고 미리 정의할 수 있다.
* Dto를 모델로 변환해서 사용해야 한다.

### DTO를 모델 클래스로 변환
fromJson(), toJson()처럼 변환 기능이 필요하다. => **mapper!**

<img width="885" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/5e9bab90-b605-40aa-990a-cc3330d71d40">

DTO -> mapper(변환) -> model class

<br></br>

## Mapper 작성법
* Mapper는 DTO를 모델 클래스로 변환하는 유틸 메서드이다.
* toJson()도 Mapper다. 이와 비슷하게 만들어도 된다.
* nullable을 non-Nullable로 변환하는 것이 핵심(내가 사용하기 편하니까)
* 필요한 부분만 변환한다.
* extension을 활용하여 기능 분리를 추천
    * DTO는 자동으로 만들고 다른 코드 개입이나 수정하지 않는다.
    * mapper는 복잡한 로직이 포함될 수 있고 직접 작성한다.
    * DTO와 mapper 코드를 분리할 수 있다.

### Mapper 코드 예시
<img width="347" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/ac74c065-8b3c-477c-9513-d10961930256">

### 데이터의 흐름
<img width="314" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/84677f4f-fec7-4629-8d68-e391f60992a3">
Json -> DTO -> Mapper를 활용하여 모델 클래스로 변환 -> 모델 클래스

## Extension
[확장 메서드 공식 문서](https://dart-ko.dev/language/extension-methods)
* extension은 이미 존재하는 라이브러리에 기능을 추가한다.
* ✅ on + 확장 클래스

```dart
// 42를 숫자로 바꿔주는 기존의 함수를
int.parse('42')

// extension 키워드를 사용해 String을 확장자로 받아 새 메서드를 생성하면
extension NumberParsing on String {
  int parseInt() {
    return int.parse(this);
  }
  // ···
}

// 아래와 같이 사용할 수 있다.
import 'string_apis.dart';
// ···
print('42'.parseInt()); // Extension 메서드 사용.
```

```dart
// 수업 시간에 사용한 extension을 활용한 mapper
// DTO를 모델 클래스로 변환하기 위한 mapping
extension MaskDtoToMask on MaskDto {
  Mask toMask() {
    return Mask(
      count: count ?? 0,
      stores: stores ?? <StoreDto>[],
    );
  }
}

// extension 메서드 사용하여 DTO 요소들을 모델 클래스에 넣는다.
Future<List<Store>> getMaskStores() async {
    try {
      final storeDtoList = await _maskApi.getMaskStores();
      final stores = storeDtoList
          .map((e) => e.toStore())
          .toList();

      return stores;
    } catch (e) {
      return Future.error('GetMaskStores ERROR: $e');
    }
  }
```

<br></br>

## 기타
### Utillity Method
주로 특정 작업이나 계산을 수행하기 위한 간단한 함수  
여러 곳에서 반복적으로 사용되거나, 특정 작업을 수행하기 위해 일반적으로 동작을 추상화하고 단순화하는 데 사용된다.
* 다른 클래스나 모듈에 종속되지 않는다.
* 보다 일반적인 기능을 수행하거나, 특정 작업을 단순화하기 위해 설계된다.
* 보통은 클래스의 인스턴스를 만들 필요가 없어 정적(static) 메서드로 구현된다.
* 여러 번 호출될 수 있고, 코드의 재사용성과 가독성을 향상시킬 수 있다.
* 문자열을 변환하는 메서드, 숫자를 계산하는 메서드, 날짜를 다루는 메서드 등

```dart
// 예시: 문자열을 대문자로 변환하는 유틸 메서드
String toUpperCase(String str) {
  return str.toUpperCase();
}

void main() {
  String text = "hello";
  String upperText = toUpperCase(text);
  print(upperText); // 출력: HELLO
}
```
