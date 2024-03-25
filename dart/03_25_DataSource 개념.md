## 📌 데이터 소스
+ 애플리케이션이 데이터를 가져오는 위치 또는 방법을 가리킴.
+ 외부 RESTfrul API로부터 데이터를 가져와야 할 때, 해당 API에 HTTP요청을 보내고 응답을 처리하여 데이터를 추출하는 클래스 또는 모듈이 데이터 소스에 해당된다.
+ 대부분 서버와의 통신은 Json으로 이루지기 때문에 직렬화와 역직렬화를 잘 구현하여 상호작용을 해야함.

### Json과 데이터 클래스의 상호변환

#### jsonDecode

```dart
final Map<String, dynamic> json = jsonDecode(response.body);
```

+ 서버로부터 받아온 json 데이터를 다트의 Map으로 변환해야한다. jsonDecode로 디코딩하여 다트에서 가공할 수 있는 상태로 만든다.
+ 그 후 역직렬화를 통해 데이터를 가공한다.

#### fromJson, toJson
```dart
GeoModel.fromJson(Map<String, dynamic> json)
      : lat = json['lat'],
        lng = json['lng'];

Map<String, dynamic> toJson() {
    return {
      'lat' : lat,
      'lng' : lng
    };
  }
```

+ fromJson생성자를 생성해서 Map타입의 json데이터를 클래스 필드에 각각 할당. (역직렬화)
+ toJson메서드로 Map타입의 json데이터로 반환. (직렬화)

### XML과 데이터 클래스의 상호변환

```dart
static List<SubwayModel> fromXml(String xmlString) {
    final document = xml.XmlDocument.parse(xmlString);
    final rowElements = document.findAllElements('row');

    List<SubwayModel> subwayModels = [];

    for (final rowElement in rowElements) {
      final subwayModel = SubwayModel(
        rowNum: rowElement.findElements('rowNum').single.text,
        selectedCount: rowElement.findElements('selectedCount').single.text,
        trainLineNm: rowElement.findElements('trainLineNm').single.text,
        statnNm: rowElement.findElements('statnNm').single.text,
      );
      subwayModels.add(subwayModel);
    }

    return subwayModels;
  }
```

+ XmlDocument.parse : 주어진 XML문자열을 분석하여 XML문서 객체를 생성
+ findAllElements('row'): row요소를 모두 찾아내어 Iterable타입으로 반환.
+ rowNum: rowElement.findElements('rowNum').single.text: 해당 요소의 텍스트 값을 가져온다.
+ 리스트에 add하여 마지막에 리턴.

```dart
final subwayModels = SubwayModel.fromXml(utf8.decode(response.bodyBytes));
```

subwayModels 객체에 fromXml호출. XML은 한글이 왜인지 깨지기 때문에 utf8로 위 처럼 디코딩해야 한글이 깨지지 않는다

### CSV와 데이터 클래스의 상호변환

```dart
static List<CSVModel> fromCSV(String csvString) {
    final List<String> lines = csvString.split('\n');
    final List<CSVModel> data = [];

    for (final line in lines) {
      final parts = line.split(',');
      if (parts.length >= 2) {
        final symbol = parts[1];
        final exchange = parts[2];
        data.add(CSVModel(name: symbol, exchange: exchange));
      }
    }

    return data;
  }
```

+ 주어진 CSV타입의 데이터를 줄넘김으로 분할한다.
+ 다시 그 줄을 ','으로 분할하여 열로 나눈다.
+ 각 줄이 적어도 두 개의 열을 가지고 있는지 확인한다. 두 개는 있어야 데이터를 추출할 수 있다.(필드 변수 2개)
+ parts의 1,2 인덱스에 해당하는 값을 CSVModel타입으로 리스트에 add하고 리턴.

```dart
final csv = File('listing_status.csv');
final lines = await csv.readAsLines();

final List<CSVModel> datas = [];

for (final line in lines) {
  datas.addAll(CSVModel.fromCSV(line));
}
```

+ csv파일을 가져와 줄로 분할.
+ 각 줄을 CSVModel 객체로 변환. addAll함수를 사용하여 리스트에 모든 객체를 추가한다.
