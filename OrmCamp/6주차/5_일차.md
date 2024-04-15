## 📖 ViewModel 개선
<br>

### 📄 UI 상태
- UI를 설명하는 속성
- Screen UI state : UI를 표시하기 위한 데이터들(ViewModel의 변수들)
- UI element state : Widget들의 상태를 관리하는 요소들(TextEditingController 등)


<br>

### 📄 로직
- UI 상태는 정적인 속성이 아님 (변수)
- 시간이 흐름에 따라 사용자 액션에 따라 변경되며 그 로직은 VIewModel이 담당


<br>

### 📄 UI 레이어의 로직 적용 흐름

![Pasted image 20240414205155](https://github.com/hwangtaewook/TIL/assets/87569211/ad8ed4cd-e6bb-4546-8679-b51de826e6c3)



<br>

### 📄 UI 상태 홀더
- 간단한 UI
- 유지관리
- 테스트 가능성
- 가독성
- Screen UI State(VM)
