## 📌 Model Class
> 모델 클래스란 데이터를 표현하고 처리하는 데 사용되는 클래스다.

+ 애플리케이션에서 사용되는 데이터를 **구조화**한다.
+ 데이터의 속성을 정의하고, 해당 속성을 조작하기 위한 메서드(모델 클래스 6종 세트)를 제공한다.
+ 데이터의 상태 관리
+ 데이터의 특정 표현을 캡슐화하므로, 여러 부분에서 재사용될 수 있다.<br/>

#### MaskModel.dart
```dart
class MaskModel {
  final String addr;
  final String code;
  final double lat;
  final double lng;
  final String name;
  final String type;
  final String? created_at;
  final String? remain_stat;
  final String? stock_at;

//<editor-fold desc="Data Methods">
  const MaskModel({
    required this.addr,
    required this.code,
    required this.lat,
    required this.lng,
    required this.name,
    required this.type,
    this.created_at,
    this.remain_stat,
    this.stock_at,
  });

  @override
  bool operator ==(Object other) =>
      identical(this, other) ||
      (other is MaskModel &&
          runtimeType == other.runtimeType &&
          addr == other.addr &&
          code == other.code &&
          created_at == other.created_at &&
          lat == other.lat &&
          lng == other.lng &&
          name == other.name &&
          remain_stat == other.remain_stat &&
          stock_at == other.stock_at &&
          type == other.type);

  @override
  int get hashCode =>
      addr.hashCode ^
      code.hashCode ^
      created_at.hashCode ^
      lat.hashCode ^
      lng.hashCode ^
      name.hashCode ^
      remain_stat.hashCode ^
      stock_at.hashCode ^
      type.hashCode;

  @override
  String toString() {
    return 'MaskModel{ addr: $addr, code: $code, created_at: $created_at, lat: $lat, lng: $lng, name: $name, remain_stat: $remain_stat, stock_at: $stock_at, type: $type,}';
  }

  MaskModel copyWith({
    String? addr,
    String? code,
    String? created_at,
    double? lat,
    double? lng,
    String? name,
    String? remain_stat,
    String? stock_at,
    String? type,
  }) {
    return MaskModel(
      addr: addr ?? this.addr,
      code: code ?? this.code,
      created_at: created_at ?? this.created_at,
      lat: lat ?? this.lat,
      lng: lng ?? this.lng,
      name: name ?? this.name,
      remain_stat: remain_stat ?? this.remain_stat,
      stock_at: stock_at ?? this.stock_at,
      type: type ?? this.type,
    );
  }

  Map<String, dynamic> toJson() {
    return {
      'addr': addr,
      'code': code,
      'created_at': created_at,
      'lat': lat,
      'lng': lng,
      'name': name,
      'remain_stat': remain_stat,
      'stock_at': stock_at,
      'type': type,
    };
  }

  factory MaskModel.fromJson(Map<String, dynamic> map) {
    return MaskModel(
      addr: map['addr'],
      code: map['code'],
      created_at: map['created_at'],
      lat: map['lat'],
      lng: map['lng'],
      name: map['name'],
      remain_stat: map['remain_stat'],
      stock_at: map['stock_at'],
      type: map['type'],
    );
  }

}
```

## 📌 Repository
> 레포지토리란 애플리케이션의 데이터를 관리하고 조작하는 디자인 패턴이다.

+ 애플리케이션의 데이터를 관리한다. 이는 데이터의 생성, 조회, 업데이트, 삭제를 의미한다
+ 데이터를 가져오고 저장하기 위해 데이터 소스와 상호작용한다. 데이터베이스, 외부 API, 파일 시스템 등 다양한 소스에서 데이터를 가져오고 저장한다.
+ 비즈니스 로직과데이터 엑세스 로직을 분리하여 애플리케이션의 유지 보수성을 높인다. 잘게 쪼개는것이 큰 프로젝트 일수록 좋다.
+ 데이터 엑세스 로직을 추상화하여 테스트하기 쉽게 만든다. mock객체로 대체하여 테스트할 수 있으므로 테스트 용이성이 높아진다.

#### MaskRepositoryImpl.dart, MaskRepository.dart
```dart
abstract interface class MaskRepository {
  Future<List<MaskModel>> getMasks();
}

class MaskRepositoryImpl implements MaskRepository {
  final MaskApi _api;

  MaskRepositoryImpl(this._api);

  @override
  Future<List<MaskModel>> getMasks() => _api.getMasks();
}
```

## 📌 Mock객체
> Mock은 라이브 웹 서비스 또는 데이터베이스를 에뮬레이션하고 상황에 따라 특정 결과를 반환할 수 있다.

레포지토리와 같은 외부 의존성이 있는 컴포넌트를 테스트할 때 유용하게 사용됨.

+ 테스트 중에 실제 데이터베이스나 외부 서비스에 의존하지 않고, 대신에 모의 객체를 사용하여 테스트할 수 있다. 이는 테스트가 외부 환경에 독립적으로 실행되도록 보장한다.
+ 모의 객체를 사용하면 테스트 코드를 더 간결하게 유지할 수 있다. 실제 데이터베이스나 외부 서비스를 사용하는 대신, 모의 객체를 사용하여 테스트 시나리오를 정확하게 제어할 수 있음.
+ 테스트 속도가 빨라진다. 실제 데이터베이스나 외부 서비스를 엑세스할 필요가 없기 때문이다.
+ 실제 데이터베이스나 외부 서비스는 테스트 시나리오에 영향을 줄 수 있는 여러가지 요소를 포함할 수 있다. 모의 객체를 사용하면 이러한 변수를 제거하여 테스트에 안정성을 부여한다.

이후 mock객체를 사용하여 테스트코드를 짜봤으나 테스트에 실패했다. main에선 출력이 잘되는데 mock객체를 잘 사용을 못했는지 전혀 모르겠다. 내일 과제 리뷰 때 집중해서 결함을 찾아야겠다.
