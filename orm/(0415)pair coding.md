## pair coding

### 1. mapper에서 형 변환 시 `tryParse` 사용  
=> parse와 같지만, `FormatException을 발생한 경우 tryParse는 null을 반환`한다.

<br></br>

### 2. data source의 api에서는 데이터 전체를 받아 Dto로 반환하도록 했다.  
repository에서 리스트 메서드가 필요하다면, 전체 데이터를 받아온 후 리스트에 담아 리턴하도록 했다.

```dart
 @override
Future<List<SubwayModel>> getArrivals() async {
  List<SubwayModel> dataList = [];
  final subwayData = await _subwayApi.getRealTimeStationArrival();

  if (subwayData.realtimeArrivalList == null) {
    return dataList;
  }
  dataList =
      subwayData.realtimeArrivalList!.map((e) => e.toSubway()).toList();

  return dataList;
}
```

<br></br>

### 3. SafeArea
운영체제의 침입을 피하기 위한 패딩을 넣어주는 위젯이다.  
MediaQuery로 화면과 가장자리의 면적을 잰 후, 앱의 화면을 알맞게 맞춰준다.  

예를 들어, 화면 상단의 상태 표시줄(알림바, 조절키 등)을 피할 수 있을 만큼 자식을 들여쓰기한다.  
또한 iPhone X의 노치나 디스플레이의 기타 유사한 창의적인 물리적 기능을 피하는 데 필요한 양만큼 하위 항목을 들여쓰기한다.  
사용할 면적을 직접 지정해줄 수도 있다.

```dart
SafeArea(
  child: ListView(),
  top: true,
  bottom: true,
  left: false,
  right: true,
)
```

<img width="350" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/92d254b3-9632-4053-b996-24a811f9aeae">
<img width="350" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/92cedffe-163f-4252-a48a-5ccd767173ae">
<img width="350" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/c75482b4-609c-4ff6-980f-7295e49464e8">
<img width="350" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/d307ca2f-6fdf-426f-a85a-eef6ff6fe5a8">

<br></br>

### 4. ListView 와 ListView.builder
#### ListView
* 정적인 데이터를 불러올 때 간단하고 효과적으로 사용할 수 있다.
* 디스플레이나 화면에 보이지 않더라도 모든 리소스들을 한 번에 렌더링한다.

#### ListView.builder
* 데이터의 크기나 개수에 따라 동적으로 항목을 생성할 수 있어 ListView보다 성능의 이점이 있다.
* builder를 사용해서 화면에 보여지는 것만 렌더링한다.
* 화면 밖으로 벗어나지는 위젯들은 삭제하기 때문에 속도나 메모리 측면에서 유리하다.


```dart
 Expanded(
    child: ListView(
      children: [
        Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: viewModel.subways
              .map((e) => SizedBox(
                    height: 50,
                    child: Row(
                      mainAxisAlignment:
                          MainAxisAlignment.spaceBetween,
                      children: [
                        // 위치
                        Expanded(
                          flex: 1,
                          child: Text(
                            e.arrvalMessage,
                            textAlign: TextAlign.center,
                            overflow: TextOverflow.ellipsis,
                            style: TextStyle(
                              color: viewModel.subways[0] == e
                                  ? Colors.red
                                  : Colors.black,
                            ),
                          ),
                        ),

                        (...)

                      ],
                    ),
                  ))
              .toList(),
        )
      ],
    ),
  ),
```

```dart
Expanded(
    child: ListView.builder(
      itemCount: viewModel.subways.length,
      itemBuilder: (context, index) {
        return Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            SizedBox(
              height: 50,
              child: Row(
                mainAxisAlignment: MainAxisAlignment.spaceBetween,
                children: [
                  // 위치
                  Expanded(
                    flex: 1,
                    child: Text(
                      viewModel.subways[index].arrvalMessage,
                      textAlign: TextAlign.center,
                      overflow: TextOverflow.ellipsis,
                      style: TextStyle(
                        color:
                            index == 0 ? Colors.red : Colors.black,
                      ),
                    ),
                  ),

                  (...)

                ],
              ),
            )
          ],
        );
      },
    ),
  ),
```
