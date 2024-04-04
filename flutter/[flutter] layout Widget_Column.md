>[**공식문서**](https://api.flutter.dev/flutter/widgets/Column-class.html)

- Column
하위 항목을 수직 배열로 표시하는 위젯
  - (ListView) 스트롤 사용 무제한 증식가능
  - (SingChildScrollView) 스크롤 컨테이너 내에서 스크롤가능
  - (Expended) 확장 일정 부분 확장가능
  - (Flex) 확장 가로,세로 미리 알수 없으나 확장
  - (Specer) flex값에 비례하여 공간 차지
  - 항목정렬
  1) crossAxisAlignment 
  2) MainAsisAlignment
  - 항목크기
  1) mainAxisSize


>레이아웃은 6단계로 진행됩니다.
1) 무한한 수직 제약 조건과 들어오는 수평 제약 조건을 사용하여 null 또는 0 플렉스 팩터(예: Expanded 가 아닌 요소)를 사용하여 각 하위 항목을 레이아웃합니다 . 
crossAxisAlignment 가 CrossAxisAlignment.stretch 인 경우 대신 들어오는 최대 너비와 일치하는 엄격한 수평 제약 조건을 사용합니다.
2) Flex Factor가 0이 아닌 자식(예: Expanded 인 자식 ) 사이에 남은 수직 공간을 Flex Factor에 따라 나눕니다. 예를 들어, Flex Factor가 2.0인 어린이는 Flex Factor가 1.0인 어린이보다 두 배의 수직 공간을 받게 됩니다.
3) 1단계와 동일한 수평 제약 조건을 사용하여 나머지 하위 항목을 각각 레이아웃합니다.
단, 무한한 수직 제약 조건을 사용하는 대신 2단계에서 할당된 공간 크기에 따라 수직 제약 조건을 사용합니다. FlexFit.tight 인 FlexFit.fit 속성을 가진 하위 항목 은 엄격한 제약이 주어지면(즉, 할당된 공간을 채우도록 강제됨) FlexFit.loose 인 Flex.fit 속성을 가진 하위 항목에는 느슨한 제약이 부여됩니다(즉, 할당된 공간을 채우도록 강요되지 않음).
4) 열의 너비는 자식의 최대 너비입니다(이는 항상 들어오는 수평 제약 조건을 충족합니다).
5) Column 의 높이는 mainAxisSize 속성 에 의해 결정됩니다 . mainAxisSize 속성이 MainAxisSize.max 인 경우 열의 높이는 들어오는 제약 조건의 최대 높이입니다. mainAxisSize 속성이 MainAxisSize.min 이면 열의 높이는 자식 높이의 합입니다(수신 제약 조건에 따라 다름).
6) mainAxisAlignment 및 crossAxisAlignment 에 따라 각 하위 항목의 위치를 결정합니다 . 예를 들어, mainAxisAlignment 가 MainAxisAlignment.spaceBetween 인 경우 하위 항목에 할당되지 않은 수직 공간은 균등하게 나누어 하위 항목 사이에 배치됩니다.
