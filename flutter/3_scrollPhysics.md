## ScrollPhysics

ScrollPhysics 타입 :

1. NeverScrollableScrollPhysics

2. AlwaysScrollableScrollPhysics

3. BouncingScrollPhysics

4. ClampingScrollPhysics

5. FixedExtentScrollPhysics
   
6. PageScrollPhysics

7. RangeMaintainingScrollPhysics

<br/>

#### NeverScrollableScrollPhysics
스크롤되는 것을 방지할 수 있다.

#### AlwaysScrollableScrollPhysics
이는 스크롤 가능한 위젯의 내용이 화면 높이를 초과하지 않는 경우에도 강제로 스크롤시킨다. RefreshIndicator로 감싸려는 경우 반드시 사용해야 한다.

#### BounceScrollPhysics
스크롤된 콘텐츠는 끝(상단 또는 하단)에 도달하면 튕기는 듯한 효과를 준다. 이는 iOS 에서 볼 수 있는 기본 동작이다.

#### ClampingScrollPhysics
콘텐츠를 벗어나는 스크롤을 방지하므로 기본적으로 BounceScrollPhysics에서 나타나는 동작을 방지한다. 이는 Android 에서 볼 수 있는 기본 동작이다 .

#### FixedExtentScrollPhysics
스크롤을 멈추지 않고 약간의 스냅효과로 목록 항목을 중앙에 놓는다. 

#### PageScrollPhysics
PageView에서 사용하는 스크롤효과. 정확한 스냅효과로 목록 항목을 중앙에 놓는다. ListView에서는 인식을 잘 못하는 것 같다.

#### RangeMaintainingScrollPhysics
UI적으로는 ClampingScrollPhysics과 같은 형태이다. 차이점은 overscroll이 발생하지 않는다. ClampingScrollPhysics은 끝부분에 도달했을 때 애니메이션과 함께 약간의 overscroll이 발생한다. 
