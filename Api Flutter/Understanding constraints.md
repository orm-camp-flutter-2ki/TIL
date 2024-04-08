# Understanding constraints
[공식문서](https://docs.flutter.dev/ui/layout/constraints) 

Flutter를 배우는 누군가가 당신에게 '왜 몇몇 위젯은 width 100의 크기를 가졌지만 왜 실제로 100의 넓이를 가지지 않나요?' 라고 질문한다면, 일반적인 답변은 '위젯을 Center에 넣어봐'일 것이다.

**그러지마라**

그렇게 대답하단면, 그들은 다시, 다시 찾아와서 왜 몇몇은 FittedBox는 정상적으로 동작(부모의 크기에 확장)하지 않는지, 왜 Column은 overflowing(부모의 크기 or 화면의 크기를 넘어감)하는지, IntrinsicWidth는 어떻게 동작되는지 질문할 것이다.

>IntrinsicWidth/Height: 부모가 설정한 constraints 안에서 자식 위젯이 최대의 widht/height를 갖게하는 위젯

'위젯을 Center에 넣어봐' 대신 먼저 말해줘야 하는 것은, 'Flutter의 layout은 HTML layout과 매우 다르고 아래 규칙을 따르는 것을 명심해라' 이다.

**Constaint는 자식에게 적용되고, Size는 부모에게 전달되며, Parent가 자식의 위치를 결정한다.**

Flutter layout은 이 규칙을 배제하고는 이해하기 힘들기 때문에, Flutter 개발자라면 먼저 이것을 학습해야한다.

### More detail
- 위젯은 부모 위젯으로 부터 constraint를 받는다. constraint는 4개의 실수(minimumWidth/Height, maximumWidth/Height)의 집합이다.
- 그 다음 위젯은 자신의 자식들을 하나하나에게 constraint를 알려주고 자식들이 어떤 Size를 갖기를 원하는지 확인한다.
- 이 후, 위젯은 자식 위젯들의 위치(x축에 대한 수직 위치와 y축에 대한 수평 위치)를 지정한다.
- 마지막으로 위젯은 부모에게 자신의 Size를 알려준다.  
=> 부모가 준 constraint 내에서 위젯이 자신의 자식들을 배치한 후, 자신의 크기를 알려주는 것

<br>

## 한계

Flutter의 layout 엔진은 one-pass 프로세스로 설계되어 있다.이는 Flutter가 자신의 위젯을 매우 효율적으로 배치하지만 몇가지 한계가 있다는 것을 의미한다.  

- 위젯은 부모 위젯으로 부터 주어진 constraint 내에서 자신의 크기를 결정할 수 있다. 즉, 위젯은 일반적으로 **자신이 원하는 크기를 가질 수 없다**.
- 부모 위젯이 자식 위젯의 위치를 결정하기 때문에, 자식 위젯은 **화면에서 자신의 위치를 알 수도, 결정할 수도 없다**.
- 부모 위젯의 크기와 위치 또한 해당 위젯의 부모 위젯에 의해 결정되기 때문에, 위젯 tree 전체를 고려하지 않고는 그 어떤 위젯의 크기와 위치를 정확하게 정의할 수 없다.
- 만약 자식 위젯이 부모가 결정한 크기와 다른 크기를 얻기를 원하고, 부모 위젯에는 해당 크기를 정렬할 충분한 정보가 없다면, 자식의 크기는 무시된다.  
=> **정렬을 정의할 때는 구체적으로 정의해야 한다**.

Flutter에서 위젯들은 자신 아래에 있는 RenderBox 객체에 의해 그려진다(rendering).  
Flutter의 많은 box들(특히 하나의 자식 위젯만을 갖는 box)은 자신의 constraint를 자식의 자식들에게 전달한다.

일반적으로 constraint를 처리하는 방법에 따른 3가지 종류의 box가 있다.
- 가능한 최대의 크기를 가지려는 box  
=> 예, Center나 ListView에 의해 사용되는 box
- 자식과 동일한 크기를 가지려는 box  
=> 예, Transform이나 Opacity에 의해 사용되는 box  
- 특정한 크기를 가지려는 box  
=> 예, Image나 Text에 의해 사용되는 box

Container와 같은 몇몇 위젯들은 생성자의 인자에 따라 그 유형이 달라진다. Constraint 생성자는 기본값으로 가능한 최대의 크기를 가지려한다. 하지만 width가 주어진다면 해당 값에 맞춰진 크기를 가지려한다.

이 외의 Row나 Column(flex box)은 그들에게 부과되는 constraint에 따라 달라진다.  
(자세한 내용은 Flex에서)