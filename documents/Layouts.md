* 위젯은 UI를 구축하는데 사용되는 클래스
* 위젯은 레이아웃과 ui 요소 모두에 사용
* 간단한 위젯을 구성하여 복잡한 위젯을 구축

Use a Container when you want to add padding, margins, borders, or background color, to name some of its capabilities.
: 패딩, 여백, 테두리 또는 배경색을 추가하고 일부 기능의 이름을 지정하려면 컨테이너를 사용하세요

A child property if they take a single child—for example, Center or Container
: 싱글 child를 가져갈 경우의 child 속성, Center, Container

Cupertino apps
Unlike Material, it doesn’t provide a default banner or background color. You need to set these yourself.


## Lay out multiple widgets vertically and horizontally(여러 위젯을 수직 및 수평으로 배치)
One of the most common layout patterns is to arrange widgets vertically or horizontally. 
You can use a Row widget to arrange widgets horizontally, and a Column widget to arrange widgets vertically.
> 가장 일반적인 레이아웃 패턴 중 하나는 위젯을 수직 또는 수평으로 배열하는 것입니다. Row 위젯을 사용하면 위젯을 가로로 정렬할 수 있고, Column 위젯을 사용하면 위젯을 세로로 정렬할 수 있습니다.

<img width="863" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/871d9b7a-7793-4627-890a-5908f356f1d6">

> * Row 와 Column은 가장 일반적으로 사용되는 레이아웃 패턴 중 두 가지입니다.
> * 각 각 Row, Column은 하위 위젯 목록을 가져옵니다.
> * 하위 위젯은 그 자체가 Row, Column 또는 기타 복잡한 위젯일 수 있습니다.
> * Row 또는 Column의 하위 항목을 수직 및 수평으로 정렬하는 방법을 지정할 수 있습니다.
> * 특정 하위 위젯을 늘리거나 제한할 수 있습니다.
> * Row나 Column의 하위 위젯의 사용 가능한 공간을 사용하는 방법을 지정할 수 있습니다.

To create a row or column in Flutter, you add a list of children widgets to a Row or Column widget. 
In turn, each child can itself be a row or column, and so on. 
The following example shows how it is possible to nest rows or columns inside of rows or columns.
> Flutter에서 행이나 열을 만들려면 Row 또는 Column 위젯에 children 목록 위젯을 추가하세요.  
> 차례로 각 하위 항목 자체가 행이나 열이 될 수 있습니다.
> 다음 예에서는 행이나 열 내부에 행이나 열을 중첩하는 방법을 보여줍니다.

This layout is organized as a Row. The row contains two children: a column on the left, and an image on the right:
> 이 레이아웃은 Row로 구성되어 있습니다. 행에는 두 개의 하위 항목(왼쪽 열, 오른쪽 이미지)이 포함되어 있습니다.

<img width="865" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/decf1a1f-340e-4940-8f0f-3ef863e46b22">

The left column’s widget tree nests rows and columns.
> 왼쪽 열의 위젯 트리는 행과 열을 중첩합니다.

<img width="860" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/25b7ad15-c3d8-44c2-a10a-d6fc6d6554fb">

You’ll implement some of Pavlova’s layout code in Nesting rows and columns.
> 행과 열이 중첩되어 있는 Pavlova의 레이아웃 코드 중 일부를 구현합니다.

<img width="863" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/55e7650e-66c3-44b9-af71-c12958137c42">
