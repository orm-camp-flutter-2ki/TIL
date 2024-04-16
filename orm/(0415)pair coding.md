## pair coding

### SafeArea
* 디바이스의 둥근 모서리, 스피커, 노치 등을 피해 화면 설계가 필요할 때
* SafeArea 위젯이 MediaQuery로 가장 자리 면적을 잰 후, 앱의 화면을 알맞게 맞춰준다.

<img width="400" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/92d254b3-9632-4053-b996-24a811f9aeae">
<img width="400" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/92cedffe-163f-4252-a48a-5ccd767173ae">
<img width="400" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/c75482b4-609c-4ff6-980f-7295e49464e8">
<img width="400" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/d307ca2f-6fdf-426f-a85a-eef6ff6fe5a8">

<br></br>

### ListView 와 ListView.builder

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
