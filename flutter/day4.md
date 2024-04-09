# MVVM 패턴

- Model은 애플리케이션의 데이터와 비즈니스 로직을 담당합니다. 사용자 인터페이스(UI)나 UI 로직과 직접적인 상호작용을 하지 않습니다.
- View는 사용자에게 보이는 UI를 담당합니다. 사용자의 입력을 받고, 사용자에게 데이터를 표시하지만, 데이터를 직접 처리하지는 않습니다.
- ViewModel은 Model과 View 사이의 중재자 역할을 합니다. 데이터 바인딩을 통해 View에 데이터를 제공하고, 
사용자의 액션을 Model에 전달합니다. ViewModel은 Model로부터 데이터를 가져와서 사용자가 이해하기 쉬운 형태로 가공하여 View에 전달합니다.

model - viewModel - view

# ChangeNotifier
- notifyListeners() 를 호출하여 변경사항을 알림
- 데이터 바인딩 구현의 핵심

