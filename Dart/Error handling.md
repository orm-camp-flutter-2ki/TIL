# Error handling
[공식문서](https://dart.dev/language/error-handling)  

예외는 예상치 못한 무언가가 발생했음을 알리는 에러이다.  
- 예외가 처리되지 않으면 예외가 발생한 isolate는 suspend되고, 일반적으로 isolate와 프로그램은 종료된다.  
- 자바와 달리 모든 Dart의 예외는 unchecked 예외이다. 메서드는 자신이 던지는 예외를 명시하지 않으며, 그 어떤 예외도 개발자가 직접 처리할 필요가 없다.  
- Dart는 Exception과 Error의 타입(미리 정의된 하위 타입 포함)을 제공한다. (직접 예외를 정의할 수도 있다)  
- Dart는 Exception과 Error 객체뿐만 아니라 non-nullable한 모든 객체를 예외로 던질 수 있다.

<br>

## Throw
다음과 같이 예외를 던질(발생시킬) 수 있다.  
```dart
throw FormatException('알맞지 않은 형식');
```
임의의 객체를 던질 수도 있다.

```dart
throw '던졌다. 나의 예외';
```
예외 역시 표현식이기 때문에, 값으로써 할당할 수 있다.
```dart
void distanceTo(Point other) => throw UnimplementedError();
```

<br>

## Catch
- 예외를 잡음(catching)으로써 예외의 전파를 중지시킬 수 있고, 예외를 처리할 기회를 제공한다.  
- 한가지 타입 이상의 예외를 발생시킬 수 있는 코드를 처리하기 위해 여러 catch 절을 선언할 수 있다.  
    => catch 절에 예외 타입을 명시하지 않으면, 모든 thrown 객체를 처리할 수 있다.  
- `on` 키워드를 사용하여 예외의 타입을 지정할 수 있다.  
- `catch` 키워드를 사용하여 예외 객체를 직접 다룰 수 있다.  

    ```dart
    try {
      breedMoreLlamas();
    } on OutOfLlamasException {
      // A specific exception
      buyMoreLlamas();
    } on Exception catch (e) {
      // 어떤 것이든 예외 타입 객체면 일단 다 catch
      print('Unknown exception: $e');
    } catch (e) {
      // 타입 지정없이 그냥 전부 다 catch
      print('Something really unknown: $e');
    }
    ```
- `catch()`에 `발생한 예외 객체`, `StackTrace 객체`를 명시할 수 있다.  
    => 각각 `e`, `s`로 나타내며, `s`는 생략 가능

    ```dart
    try {
      // ···
    } on Exception catch (e) {
      print('Exception details:\n $e');
    } catch (e, s) {
      print('Exception details:\n $e');
      print('Stack trace:\n $s');
    }
    ```

<br>

### rethrow
`rethrow` 키워드를 통해 예외의 전파를 중지시키지 않고 부분적인 예외처리를 할 수 있다.
```dart
void misbehave() {
  try {
    dynamic foo = true;
    print(foo++); // Runtime error
  } catch (e) {
    print('misbehave() partially handled ${e.runtimeType}.');
    rethrow; // 예외를 처리하였지만, 상위 메서드(호출부)로 예외를 다시 던진다.
  }
}

void main() {
  try {
    misbehave();
  } catch (e) {
    print('main() finished handling ${e.runtimeType}.');
  }
}
```

<br>

## Finally
finally 절을 통해 예외 발생 여부와 관계 없이 항상 실행이 보장되는 코드를 작성할 수 있다.  
- 매칭되는 catch절이 있는 경우, catch 절이 실행된 후에 finally 절이 실행된다.
    ```dart
    try {
      breedMoreLlamas();
    } catch (e) {
      print('Error: $e'); // catch한 예외를 일단 먼저 처리한 후에,
    } finally {
      cleanLlamaStalls(); // finally 절이 실행된다.
    }
    ```

- 매칭되는 catch절이 없는 경우, 예외는 finally 절이 실행된 후에 전파된다.  
    ```dart
    try {
      breedMoreLlamas();
    } finally {
      // catch 절이 없기 때문에 try{}에서 예외가 발생할 경우, finally이 모두 끝난 후, 예외가 전파된다.
      cleanLlamaStalls();
    }
    ```

<br>

## Assert
`assert(조건, optional message)`  

개발 과정에서는 assert구문을 통해 false인 조건에 대해 예외를 발생시킬 수 있다.
```dart
// Make sure the variable has a non-null value.
assert(text != null);

// Make sure the value is less than 100.
assert(number < 100);

// Make sure this is an https URL.
assert(urlString.startsWith('https'));
```
배포 버전의 코드에서 assert는 모두 무시된다.  
(assert의 평가 자체가 일어나지 않음)