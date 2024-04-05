# Container (class)
[공식문서](https://api.flutter.dev/flutter/widgets/Container-class.html) 

painting, positioning, sizing 위젯이 결합된 편리한 위젯이다.

Container는 자식 위젯을 padding으로 감싼다. 그 후, 패딩된 범위에 추가적인 constraints를 적용한다(null이 아닌, width와 height를 통합하여 constraint로 적용한다). container는 margin이라고 하는 추가적인 여백으로 둘러쌓여져 있다.

painting이 진행되는 동안, container 주어진 transform을 적용하고, decoration을 paint하여 패딩된 범위를 채운다. 이 후, 자식 위젯을 paint하고, 마지막으로 foregroundDecoration을 paint하고 패딩된 공간을 채운다.

> transform: conatiner를 painting하기 전에 적용 되는 transformation matrix(Matrix4)
> => 위젯의 3차원 위치(회전)에 관여

> foregroundDecoration: 자식 위젯의 앞을 paint하는데 사용되는 decoration  
> final Decoration? foregroundDecoration;

자식 위젯이 없는 Container는 가능한 최대의 크기를 가지려고 한다.  
(부모로 지정된 constraint가 제한이 없다면, 가능한 최소의 크기를 가지려고 한다.)  

자식 위젯이 있는 Container는 자식의 크기에 맞춰진다. 단, 생성자의 width, height, constraint 인자가 지정되면 이 규칙보다 우선시된다.

기본적으로 container는 모든 hit 테스트에서 false를 리턴한다. 만약, color 속성이 지정된다면, ColoredBox에 의해 hit 테스트가 이루어지고 항상 결과는 true를 반환한다. 만약 decoration 혹은 foregroundDecoration 속성이 지정되었다면, hit 테스트는 Decoration.hitTest에 의해 이루어진다.


### Layout의 동작

box layout model 이해의 시작으로 BoxConstraints를 먼저 볼 것.


Container는 각각 고유한 layout 동작을 가진 여러 위젯을 결합하므로 Container의 layout 동작은 복잡하다.

**요약**: Container는 다음을 순서대로 시도한다: 정렬을 준수하려 한다. 자식의 크기에 맞추려한다. width/height와 constraint를 준수하려 한다. 부모의 크기에 맞추려한다. 최소의 크기를 가지려한다.

좀 더 구체적으로 알아보자
 
- 자식이 없고, height/width가 없고, constraint가 없고, 부모가 unbounded constraint를 제공한다면, Container는 가능한 최소의 크기를 가지려 한다.  

- 자식이 없고, 정렬이 없고, height/width나 constraint가 주어지는 경우, Container는 부모의 constraint와 자신의 constraint의 결합에서 가능한 최소의 크기를 가지려 한다.  

- 자식이 없고, height/width가 없고, constraint가 없고, 정렬이 없지만, 부모가 bounded constraint를 제공하는 경우, Container는 부모의 크기에 맞춰진다.

- 정렬이 있고, 부모가 unbounded constraint를 제공하는 경우, Container는 자식의 크기에 맞춰진다.  

- 정렬을 가지고 있고, 부모가 bounded constraint를 제공하는 경우, Container는 부모의 크기에 맞춰진다. 또한 자식을 정렬에 맞춰 위치시킨다.

- 반면에, 자식이 있고, height/width가 없고, constraints가 없고, 정렬이 없는 경우, Container는 부모에게서 받은 constraint를 자식에게 전달하고, 자신은 자식의 크기에 맞춰진다.

- 문서에 설명한대로, margin과 padding 속성 또한 layout에 영향을 준다. 또한,  decoration이 암시적으로 padding을 증가시키기도 한다(예, BoxDecoration의 border는 padding에 영향을 준다). 


### Inheritance
Object > DiagnosticableTree > Widget > StatelessWidget > Container