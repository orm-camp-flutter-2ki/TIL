## silver appbar
[[🔗 dev_silver appbar]](https://api.flutter.dev/flutter/material/SliverAppBar-class.html)
- 슬리버 앱 바(Sliver app bars)는 일반적으로 `CustomScrollView`의 first child으로 사용
</br>

## 속성
### floating  
`floating`  
- 기본값 : `false`
- 이 속성을 `true`로 설정 : 스크롤이 내려갈 때 앱 바가 화면 위에 떠 있게 된다
- 사용자가 스크롤을 올리면 앱 바가 다시 화면 위로 올라온다
- 스크롤 위치에 따라 앱 바가 동적으로 표시되거나 숨겨진다
</br>

### pinned  
`pinned`  
- 기본값 : `true`
- 이 속성을 `true`로 설정 : 스크롤 되는 동안 앱 바가 화면 위에 고정
- 사용자가 스크롤을 올리거나 내릴 때 앱 바가 항상 화면 상단에 고정
- 스크롤 되는 내용은 앱 바 아래에 표시
</br>

### snap
`snap`
- 기본값 : `false`
- 이 속성을 `true`로 설정 : 스크롤이 중간에 멈추면 앱 바가 자동으로 가장 가까운 고정된 위치로 스냅된다
- 사용자가 스크롤을 놓으면 앱 바가 가장 가까운 고정 위치로 자동으로 이동
- pinned가 true일 때만 동작
</br>

### 예
`floating: false`, `pinned: false`, `snap: false` 일 때
- 스크롤 되는 앱 바가 화면에 고정
- 사용자가 스크롤을 올리거나 내릴 때 앱 바는 항상 화면 상단에 표시
- 스크롤이 중간에 멈추면 자동으로 스냅되지 않는다.
<br/>

