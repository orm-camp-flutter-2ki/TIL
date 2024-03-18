# Generic
- type 을 나중에 원하는 형태로 정의할 수 있다.
- type safe (타입안전) 효과를 기대할 수 있다.
- < > 안에 원하는 형태로 정의한다.
  ```
  List<E> class    // E = Element
  Map<K, V> class

  
  // 제네릭을 사용하여 Pocket 클래스 정의
  class Pocket<E> {
    E? _data;
  
    void put(E data) {
      _data = data;
    }

    E? get() {
      return _data;
    }
  }


  // 이용 가능한 type 에 제약을 추가할 수도 있다.
  class Pocket<E extends Book> {
    E? _data;
  
    void put(E data) {
      _data = data;
    }

    E? get() {
      return _data;
    }
  }
  ```
# 열거형 (enum)
- 정해둔 값만 넣어둘 수 있는 type
- bool 값으로 가능하면 상관 없지만 그 이상의 선택을 해야할 경우 사용 할 수도 있다.
- enum 과 switch 문을 세트로 잘 쓴다.
  ```
  enum AuthState {
    authenticated,
    unauthenticated,
    unknown,
  }

  AuthState authState = AuthState.unknown;

  switch (authState) {
    case AuthState.authenticated:
      print('authenticated');
      break;
    case AuthState.unauthenticated:
      print('unauthenticated');
      break;
    case AuthState.unknown:
      print('unknown');
      break;
  }
  ```
