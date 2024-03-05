# Dart의 Main이 뭘까?
### Dart
```dart
// 1. 파라미터 없는 main() 함수
void main() {
  print("Hello wolrd!")
}

// 2. 파라미터 있는 main() 함수
void main(List<String> arguments) {
  print(arguments);

  assert(arguments.length == 2);
  assert(int.parse(arguments[0]) == 1);
  assert(arguments[1] == 'test');
}

```
- Dart의 main을보고 Swift의 `@main` 키워드가 떠올랐다.
- 우선, 앱의 진입점 역할을 하는 최상위 함수라는 것은 동일한 것 같다. 하지만, 인자를 받을 수 있도록 하는것과 같이 Swift와는 다소 다른 모습을 보이고있더라고여

### Swift
```swift
@main
class AppDelegate: UIResponder, UIApplicationDelegate { ... }
```
- 앱의 진입점을 관리하는 AppDelegate의 `@main`과 매우 관련이 있지않을까? 하는 의문이 들었음.
- 그 전에 `@__` 의 의미는 뭐임?
[docs Swift: Attribute](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/attributes/#main) 이 문서를 참조하면 알 수 있다.
- Add information to declarations and types. 즉, 선언 및 유형에 정보를 추가할 수 있다고 함.
- 예를들면 우리가 자주봤던 것 처럼 아래와 같은것들 말이다.
```swift
@<#attribute name#>
@<#attribute name#>(<#attribute arguments#>)

@available(iOS 10.0, macOS 10.12, *)
@objc , @propertyWrapper
@dynamicCallable 
```
- 그 중 하나가 `@main` 이였다는거죠.
- [Swift-evolution - @main](https://github.com/apple/swift-evolution/blob/main/proposals/0281-main-attribute.md#main-type-based-program-entry-points) 위 문서에서는 실제로 Apple에서는 프레임워크 내부에 아래와 같이 구현되어있다고 이야기 했습니다.
```swift
// 프레임워크내부:
public protocol ApplicationRoot { ... }

extension ApplicationRoot {
    public static func main() { ... }
}

// In MyProgram.swift:
@main 
struct MyProgram: ApplicationRoot { ... }
```
> 결론: 
> 1. 진입점이라는 것은 두언어에서 모두 동일하다.
> 2. Swift의 @main은 프레임워크 수준에서 정의하고 있기에 사용자가 이것을 직접적으로 수정하거나 하는 행위는 허용하지않는다. 
> 3. 하지만, Dart의 main() 함수는 사용자가 커스텀 가능한 것으로 보인다. 
> 4. 두 언어를 비교했을 때 main은 어떻게 구현되어있나의 차이일 뿐 동일한 것이라고 볼 수 있다.
