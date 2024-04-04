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

자식 위젯이 있는 Container는 자식의 크기에 맞춰진다.

단, 생성자의 width, height, constraint 인자가 지정되면 이 규칙보다 우선시된다.

### Layout의 동작 (이해 불가..)

box layout model 이해의 시작으로 BoxConstraints를 먼저 볼 것.

...