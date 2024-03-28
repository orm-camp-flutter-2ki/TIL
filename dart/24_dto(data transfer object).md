## DTO (Data Transfer Object)
DTO란?
> 데이터 소스를 모델 클래스로 변환하는 과정에서 비즈니스 로직 같은 복잡한 코드는 없고 순수하게 클래스에 담기 위한 중간 전달 객체. 주로 클라이언트와 서버가 데이터를 주고받을 때 사용하는 객체이다.
<br/>

DTO를 쓰는 이유
> 이렇게 작성하면 서버로 부터 잘못된 데이터 소스(Json)를 받더라도 안 터질 수 있게 방어하는 코드를 짤 수 있다.
<br/>

기존 작성하던 모델클래스와 다른점
>DTO에는 fromJson과 toJson만 있고 모든 필드가 Nullable변수 이다. 모델클래스에는 4종세트 + Non-nullable변수.

<img width="500" alt="image" src="https://github.com/Gunbam27/TIL/assets/95085649/efd25215-1f95-46e4-b084-069240a32414"/>
<img width="500" alt="image" src="https://github.com/Gunbam27/TIL/assets/95085649/d6008c72-eca5-4958-afa5-d47f694da9a5"/>

### DTO 가 필요한 이유
- Json 데이터는 null 값을 포함할 수 있는데, mapper에서 null값이 들어올때의 예외처리를 해줄 수 있다.
- 불완전한 코드가 포함될 것 같다면 Dto를 도입하자.
- Json 값에 예외가 없다면 반드시 Dto를 도입할 필요는 없다.

### Mapper란?
api를 통해 데이터로 받고 fromJson으로 구현해낸 DTO객체를 Model클래스에 맞게 '변환' 해주는 작업을 하는 메서드.<br/>
아래와 같은 이유로 mapper는 extension으로 작성한다.
- DTO 는 자동으로 만들 것이다. (무지성, 다른 코드 개입 no)
- mapper 는 복잡한 로직이 포함될 수 있고 인간이 작성
- DTO와 mapper 코드를 분리
  
```dart
//mapper 예시
extension StoreDtoToStore on StoreDto {
  Store toStore() {
    return Store(
      address: addr ?? '',
      code: code ?? '',
      created_at: createdAt ?? '',
      lat: lat ?? -1,
      lng: lng ?? -1,
      name: name ?? '',
      remain_stat: remainStat ?? '',
      stock_at: stockAt ?? '',
      type: type ?? '',
    );
  }
}
```
