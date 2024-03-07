# Null
    말 그래도 값이 '없다.'
    값이 0 이란 뜻이 아니라 아예 없는 것.
```
    String name = '';    // null 이 아니다. 공백의 값이 있다.
    String name;         // null
```

  ## 연산자
```
  String name;
  
  int? a;                            // nullable. null 사용 가능
  int! a;                            // a 는 null 이 아니라고 개발자가 보증. 잘못 쓰면 runtime 시 펑!
  print(name ?? "비어있다.");         // ?? 좌항 / 우항 중 null 이 아닌 값을 선택해 print 한다.
```
