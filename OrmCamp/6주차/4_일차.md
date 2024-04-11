## 📖 Provider
<br>

### 📄 Provider 사용 이유
- InheritedWidget과 가장 흡사함
- 제약이 많음 : 에러 내기가 어려움
- 구글에서 공식적으로 밀고 있음
- 다른 라이브러리를 제대로 알고 쓰지 않으면 코드가 꼬임
<br>

### 📄 ChangeNotifierProvide

- Model에서 notifyListers()를 통해 변경을 통지
- 최상단 위젯트리에 설정한 ChangeNotifierProvider가 ChangeNotifer를 감시
- 변경이 필요한 위젯만 자동 갱신
