240404 (Thu)

플러터 과정 24일차

# 위젯
=

**BottomNavigationBar**
-
하단 탭 바이다.

**Column**
-
아래로 정렬되는 레이아웃 위젯이다.
이미지와 텍스트를 정렬할 때 사용한다.

**Row, SizeBox**
-
Row는 수평으로 정렬하기 위한 레이아웃 위젯이다.
mainAxisSize 속성에는 화면에 꽉 채우는 max 또는 내부 아이템의 크기에 맞추는 min을 설정할 수 있다.
mainAixsAligment는 정렬 방법을 결정 합니다. spaceEvenly는 자식 위젯들 간에 적절한 여백을 두며 정렬되므로 유용합니다.

SizedBox는 width, height 속성에 값을 할당하여 크기를 결정하는 위젯이다. 여백을 표현할 때도 사용가능하다. 

**Card**
-
카드 형태의 레이아웃 위젯이다.

**PageView**
-
좌우로 슬라이드되는 화면을 만들 때 유용한 위젯입니다. children 속성에 여러 화면을 배치하면 됩니다.

**Image**
-
프로젝트 내부 이미지를 표시하려면 asset메서드를 네트워크 이미지를 표시하려면 network 메서드를 사용합니다.

SingleChildScrollView
-
화면에 표현할 내용이 많다면 이 위젯으로 감싸서 스크롤을 생기게 할 수 있습니다. chlid 속성에 지식 위젯을 배치하기만 하면 된다.

Opacity
-
위젯에 투명도를 부여합니다. opacity 속성이 0.0 ~ 1.0 까지 설정할 수 있고 0에 가까울 수록 투명, 1에 가까울 수록 불투명합니다.

Divider
-
수평 라인을 표시합니다.

Text
-
글자를 표시합니다.

Expanded
-
child 위젯의 길이를 꽉 채우거나 Expanded끼리 비율을 정할 수 있습니다.

