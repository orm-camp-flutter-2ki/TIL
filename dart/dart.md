### 다트로 값 입력 받고 출력하기.

값 입력 받는 방법 : String? input = stdin.readLineSync();
한 줄에 여러 값 입력 받는 방법 : List<String>? input = stdin.readLineSync()?.split(' ');
여러 줄에 여러 값 입력 받는 방법 : 
List<int> list = [];
  for(int i=0;i<5;i++){
    String? input = stdin.readLineSync();
    int? number = input != null ? int.tryParse(input) : null;
    if(number != null){
      list.add(number);
    }
  }
