# protocol vs abstract interface

## 1. 기본사용
**swift**
```swift
protocol HeaderViewProtocol {
    var contents: Content { get set }
    func configureView(data: Content)
    func configureLayout()
}

final class HeaderView: HeaderViewProtocol {
    var contents: Content
    
    init(contents: Content) {
        self.contents = contents
    }
    
    func configureView(data: Content) {
        print("데이터 컨피규어되었어.")
    }
    
    func configureLayout() {
        print("레이아웃도 정상적용되었어")
    }
}
```

**dart**
```dart
abstract interface class HeaderViewInterface {
  Content get content;
  set content(Content content);
  configureView(Content content);
  configureLayout();
}

class HeaderView implements HeaderViewInterface {
  @override
  Content content;

  HeaderView(this.content);
  
  @override
  configureView(Content content) {
    print('데이터 컨피규어되었어');
  }

  @override
  configureLayout() {
    print('레이아웃도 정상적용되었어');
  }
}
```
- 기본적으로 둘 다 청사진으로서의 역할 자체는 동일하게보인다.

## 2. extension 사전구현 가능 여부
**swift (가능)**
```swift
extension HeaderViewProtocol {
    func configureView(data: Content) {
        print("익스텐션에서 다 구현해보림 ㅎㅎ")
    }
    
    func configureLayout() {
        print("나두 익스텐션에서 다 해버림")
    }
}

final class HeaderView: HeaderViewProtocol {
    var contents: Content
    
    init(contents: Content) {
        self.contents = contents
    }
}
```
- 이 기능은 HeaderView1, HeaderView2, HeaderView3 ... 등 이들이 HedaerViewPorotocol을 모두 채택한다면 
- 각각 구현 해주는 건 귀찮기에 한번에 프로토콜에서 공통구현해주는 기능이다.


**dart (불가능)**
```dart
extension HeaderViewInterfaceExtension on HeaderViewInterface {
  configureView(Content content) {
    print("익스텐션에서 다 구현해보림 ㅎㅎ");
  }

  configureLayout() {
    print("나두 익스텐션에서 다 해버림");
  }
}

class HeaderView implements HeaderViewInterface {
  @override
  Content content;

  HeaderView(this.content);
}
```

> // Missing concrete implementations of 'HeaderViewInterface.configureLayout' and 'HeaderViewInterface.configureView'.

- 근데 사전구현을 하는 뭔가 다른 방법이 있어보인다.
- 아직 그까지는 진도를 나가지않아서.. 잘 몰게따

## 3. 타입으로 선언하기
**Swift (가능)**
```swift
let headerView: HeaderViewProtocol = HeaderView(contents: Content())

func something(headerView: HeaderViewProtocol) -> HeaderViewProtocol {
    return HeaderView(contents: Content())
}
```

**Dart (가능)**
```dart
final HeaderViewInterface headerView = HeaderView(Content());

HeaderViewInterface something(HeaderViewInterface headerView) {
  return HeaderView(Content());
}
```

## 4. 다중상속
```swift=
protocol Aprotocol {}
protocol Bprotocol {}
protocol Cprotocol {}

class Star: Aprotocol, Bprotocol, Cprotocol {}
```


```dart
abstract interface class Ainterface{ }
abstract interface class Binterface{ }
abstract interface class Cinterface{ }

class Star implements Ainterface, Binterface, Cinterface {}
```
- 이정도면 거의 동일한 개념과 특성이라고 봐도 좋을 듯하다.
