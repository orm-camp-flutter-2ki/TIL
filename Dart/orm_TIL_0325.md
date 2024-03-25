240325 (Mon)

플러터 과정 16일차

늘 상기시켜야 할 메모
-
데이터 클래스에는 6종을 꼭 추가할 것

1. toString()

2. HashCode

3. ==

4. toJson

5. fromJson

6. copyWith

예시)
```dart
class Data {
int number;
String name;
String title;

Data(this.number, this.name, this.title);

Map<String, dynamic> toJson() => {
        'number': number,
        'name': name,
        'title': title,
      };

  Data.fromJson(Map<String, dynamic> json)
      : number = json['number'],
        name = json['name'],
        title = json['title'];
        

  Data copyWith({int? number, String? name, String? title}) {
    return Data(
      number ?? number!,
      name ?? name!,
      title ?? title!,
    );
  }

  @override
  String toString() {
    return 'Data{number: $number, name: $name, title: $title}';
  }

  @override
  bool operator ==(Object other) =>
      identical(this, other) ||
      other is Data &&
          runtimeType == other.runtimeType &&
          number == other.number &&
          name == other.name &&
          title == other.title &&
          

  @override
  int get hashCode =>
      number.hashCode ^ name.hashCode ^ title.hashCode;
```

## http 설치법

https://pub.dev/ 에 들어간다.

검색창에 http를 검색한다.

![스크린샷 2024-03-25 115817](https://github.com/BAUu/TIL/assets/44741680/105a5f9c-543a-41d6-baba-facd57413f2a)

후에 'http' 클릭

![스크린샷 2024-03-25 115911](https://github.com/BAUu/TIL/assets/44741680/7bf736f7-d92a-453a-b75d-19dfcffa7e8a)

installing 클릭

![스크린샷 2024-03-25 232356](https://github.com/BAUu/TIL/assets/44741680/03182272-e737-4f47-9863-8746b3ba3968)

dart와 flutter에 설치시 필요한 코드를 확인후 상황에 따라 복사

![스크린샷 2024-03-25 232559](https://github.com/BAUu/TIL/assets/44741680/11e556de-371f-44ce-ab73-3e97af44416f)

android studio 실행 후 터미널에 이전에 복사했던 코드 적은 후 엔터로 설치
![스크린샷 2024-03-25 233131](https://github.com/BAUu/TIL/assets/44741680/487dc952-e5b2-46a9-a9ce-fdb1ea621a48)

설치 후 pubspec.yaml 파일에 설치가 완료됐는지 확인!
![스크린샷 2024-03-25 233806](https://github.com/BAUu/TIL/assets/44741680/a259a46e-d4e1-46eb-b3ee-61fd659a46f7)


### 만약 데이터 class 안에 있는 다른 class를 사용할 때 주의점

데이터 클래스 안에 있는 다른 클래스를 사용할 때 toJson이나 fromJson을 사용할 때 함수의 타입이 다르기 때문에 오류가 난다.

그래서 사용하기 위해서는 그 클래스에도 6종의 코드를 사용한 뒤에 toJson에는 **data: data.toJson();**을 넣어서 그 클래스를 json 형태로 만들어 준다.

fromJson에서는**data = Data.fromJson(json['data']);** <= 이런 형태로 사용하면 된다.
