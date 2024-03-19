# 문자열 조작

## 문자열 관련된 여러 프로퍼티들이 있다.
- replaceAll, split...

## 자주쓸거 같은거
- contains : 포함여부
- endsWith : 끝나는 단어가 맞는지여부
- indexOf : 단어가 몇번쨰에 있는지
- lastIndexOf : 뒤에서 몇번쨰에있는지?

## 문자열 결합방법
1. +연산
2. String interpolation
3. String Buffer : write() 메서드로 결합한 결과를 내부 메모리(버퍼)에 담아두고 toString() 으로 결과를 얻음
```dart
final buffer = StringBuffer('Dart');
buffer..write(' and ')..write('Flutter');
//cascade연산자 : void 리턴인 함수앞에 사용하면 해당 객체의 레퍼런스를 반환해서 메서드 체인 사용 가능
```

## 연산자가 느린 이유
- String 인스턴스는 불변 객체다
- 그래서 선언할때마다 새로운 메모리 공간에 생기는것...
- 나중에 gabage collector가 청소함!
- dart는 프로그램이 동적으로 할당된 메모리 영역중에서 더이상 사용하지 않는곳을 찾아내서 해제하는 시스템이 알아서 돌아감. 메모리 신경 안써줘도 되! 하지만 메모리는 아껴써야함..

## 재밋겠다 나중에 해봐야지
- 코드 성능 측정
```dart

final stopwatch = Stopwatch()..start();
//시간 측정할 코드
print(stopwatch.elapsed);
```

## dart에서 불변객체
- int
- String
- double

## 가변객체
- List
- Map
- Set
- 와 같은 컬렉션 타입
- final, const 키워드를 이용한 컬렉션 객체들을 불변으로 만들 수 있음.
- 하지만 final은 런타임에 한번만 할당될 수 있지만 객체 내부는 변화 가능
- const 는 컴파일 당시 할당되고 할당되면 완전히 불변임.
```dart



  final List<int> finalNumbers = [1, 2, 3];
  // finalNumbers = [4, 5, 6]; // 이는 에러를 발생시킴. final 변수에 다시 할당할 수 없음.
  finalNumbers.add(4); // 그러나 내부 상태는 변경할 수 있음.

const List<int> constNumbers = [1, 2, 3];
// constNumbers.add(4); // 이는 에러를 발생시킴. const 리스트는 변경할 수 없음.

```