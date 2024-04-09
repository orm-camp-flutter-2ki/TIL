# mvvm
> view → viewModel → model  
view ← viewModel ← model
>

<div align="center">
<img width="888" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/38bd41a0-3997-40cc-8483-ac3e22b3382a">
</div>

## view
- ui 화면 (그냥 껍데기)
- viewModel의 데이터에 의해 자동으로 화면 갱신
- 수동적인…
<br/>

## viewModel
- view(화면)의 모델
( data를 가지고 있는게 좋다? 데이터를 관리해야 하니까..? ? )
- Business Logic을 처리/담당 한다
- 변수는 `viewModel` 에만 있다. 변수를 관리하는게 상태관리… 어디가 잘못되거나 수정해야 할 때, `viewModel` 만 보면 되도록 하는 것
- `view` 에서해야할 동작들을 정의, 데이터(model)가 변경되면 `view`에 알림
- 데이터를 조작만 하고 절대 다시 `model`에 `return`하지 않는다

### 왜 viewModel을 사용할까?
- repository에 역할을 쪼개서 business Logic만 담당하는 `viewModel`을 만든 것
- 

### 주의할 점
- viewModel은 단지 화면(view)하나에 대한 로직(model)일
- 하나의 화면(view)에 하나의 viewModel 가 일반적
<br/>

## medel
- Data Business Logic
- DB, File, Server와의 통신 등
- 주로 repository라고 함 (그러나 repository는 아닌…?)
<br/>

## ChangeNotifier class
[[🔗 dev_ChangeNotifiet 공식 문서]](https://api.flutter.dev/flutter/foundation/ChangeNotifier-class.html)

- flutter에만 있음 dart에 없음
- 옵저버 패턴을 구현하고 있는 상태 알림이
    - `notifyListeners()` 를 호출하여 변경사항을 알림
    - 데이터 바인딩 구현의 핵심
- 로직 안에서 `state`가 변경될 때 알려주는
- `setState()`를 사용하지 않아도 자동으로 처리할 수 있게 ← 이러한 것을 [🔗 **상태관리](https://docs.flutter.dev/data-and-backend/state-mgmt/options)** 라고 함
    - `notifyListeners()`
    - `addListener()`
        - `initState()` 안에서 호출
        - 내부에 값이 변경될 때 마다 어떤 동작을 할 지 처리할 수 있음
        - 여기에 `setState()` 를 해서 화면을 갱신해버림
    - `removeListener()`
        - `dispose()` 안에서 호출
        - addList가 길수록 removeList 하는 시간이 오래 걸린다
        - 따라서 add 하고 바로 remove 할 수 있도록 하기
        - 잊게 되면 메모리 Leak이 발생될 수 있음
<br/>

## mixins
- 다수의 클래스 계층에서 클래스의 코드를 재사용 할 수 있는 방법
- Mixins은 일괄적인 멤버 구현을 제공
- 한 개 이상의 mixins 이름과 함께 `with` 키워드를 적용하여 mixin을 사용
- `with` 키워드와 사용 할 mixins의 이름을 명시하면 됨
<br/>

## Listenable
- 관찰 가능한 객체

## ListenableBuilder
