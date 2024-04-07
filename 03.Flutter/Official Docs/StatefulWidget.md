---
title: StatefulWidget
author: Kim Donghyeok
created_at: 2024-04-07
updated_at: 2024-04-07
tags:
  - 생존코딩
  - 오름캠프
  - flutter
source: https://api.flutter.dev/flutter/widgets/StatefulWidget-class.html
---

# Stateful Widget

> 변경 가능한 상태를 가지는 위젯

State 는 다음과 같은 정보이다.

1. 위젯이 빌드될 때 동기적으로 읽을 수 있는 정보
2. 위젯의 life cycle 동안 변경 될 수 있는 정보

State.setState 를 이용하여 어떠한 상태가 변경 될 때 State 에 즉시 알리는 것은 위젯의 구현체의 책임이다.

StatefulWidget은 사용자 인터페이스를 보다 구체적으로 묘사하는 위젯의 집합을 구성하여, 사용자 인터페이스의 일부를 형성하는 위젯이다. 사용자 인터페이스에 대한 묘사가 완전히 구체화 될 때 까지 위젯의 building process 는 재귀적으로 계속된다.

StatefulWidget 은 설명하려는 사용자 인터페이스의 일부가 internal clock-driven state 또는 일부 system state 로 인해 동적으로 변경될 수 있을 때 유용하게 사용 할 수 있다.  object 자체의 구성 정보 또는  위젯이 확장되는 [[BuildContext]] 에만 의존하는 구성요소 의 경우 StatelessWidget 의 사용을 고려해야 한다.

StatefulWidget 인스턴스 자신은 immutable 이며 mutable state를  createState 메소드에 의해 생성된 별개의 [[State]] 객체 또는 State 를 subscribe 하는 객체에 저장한다. 이러한 객체에 대한 참조는 StatefulWidget 의 final 필드에 저장된다.

프레임워크 StatefulWidget 이 확장될 때마다 createState 를 호출한다. 즉, 위젯이 tree의 여러 위치에 삽입된 경우, 여러 개의 State 객체가 같은 StatefulWidget 과 연관될 수 있음을 의미한다. 마찬가지로 StatefulWidget 이 tree에서 삭제 될 때나 나중에 tree에 삽입 될 때도 프레임워크는 createState 를 호출하여 새로운 State 객체를 생성해  State 객체의 생명주기를 단순화한다.

> *위젯이 확장됨, 확장되다. (inflated, inflating)*
>
> *createState() 메소드를 이용하여 StatefulWidget에 속성이나 상태 정보가 추가(adding) 되는 것을 의미한다.*

## Methods

createState () -> State\<StatefulWIdget>

- 트리의 지정된 위치에 이 위젯을 위한 변경 가능한 상태를 만든다.
