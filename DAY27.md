# [Camera](https://pub.dev/packages/camera)

#### 앱 상단 `DEFBUG`택 제거 하기 
debugShowCheckedModeBanner: false,

# InheritedWidget

# Inflearn
#### My album
##### 1) ImagePicker paeckage 
##### (1) 생성자 등록 및 리스트 추가
```dart
class _MyGalleryAppState extends State<MyGalleryApp> {
  final ImagePicker _picker = ImagePicker();
  List<XFile>? images;
```
##### (2) 앱 실행 시, 바로 이미지를 띄우기 위한 코드 추가
```dart
@override
  void initState() {
    super.initState();

    loadImages(); //로딩시 바로 이미지 띄우기
  }

  Future<void> loadImages() async {
    //로딩시 바로 이미지 띄우기
    images = await _picker.pickMultiImage();
    setState(() {});
  }
```
##### (3) body에 코드 추가
```dart
body: images == null //images 내 자료가 없으면,
          ? Center(child: Text('empty')) //글을 띄우고,
          : if (FutureBuilder<Uint8List>( //자료가 있다면,
              future: images![0].readAsBytes(), //리스트의 0번째 이미지를 가져와
              builder: (context, snapshot) {
                final data = snapshot.data; //data는 스냅샷으로 가져온 데이터이고,
                if (data == null || //없으면 로딩을 띄우고,
                    snapshot.connectionState == ConnectionState.waiting) {
                  return const Center(child: CircularProgressIndicator());
                }
                return Image.memory( // 있다면, 그 data를 꽉채워죠.
                  data,
                  width: double.infinity,
                );
              }) != null) {

 },
```
