## 상태 관리 라이브러리

<p align="center"><img width="563" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/4f7c2c15-c2f1-4fe3-aea9-429a171afa94"></p>

...
in Flutter it's okay to rebuild parts of your UI from scratch instead of modifying it. 
Flutter is fast enough to do that, even on every frame if needed.
Flutter is declarative. This means that Flutter builds its user interface to reflect the current state of your app:

When the state of your app changes, you change the state, and that triggers a redraw of the user interface.  
There is no imperative changing of the UI itself (like widget.setText)—you change the state, and the UI rebuilds from scratch.  

The declarative style of UI programming has many benefits. Remarkably, there is only one code path for any state of the UI. 
You describe what the UI should look like for any given state, once—and that is it.

> Flutter에서는 UI를 수정하는 대신 UI의 일부를 처음부터 다시 빌드해도 괜찮다. Flutter는 필요한 경우 모든 프레임에서라도 이를 수행할 수 있을 만큼 빠르다.  
> Flutter는 선언적이다. 이는 Flutter가 앱의 현재 상태를 반영하기 위해 사용자 인터페이스를 구축한다는 것을 의미한다.  
> 앱 상태가 변경되면, 상태가 변경되고 이로 인해 사용자 인터페이스가 다시 그려진다.
> UI 자체(예: widget.setText)를 반드시 변경할 필요는 없다. 상태를 변경하면 UI가 처음부터 다시 빌드된다.
> UI 프로그래밍의 선언적 스타일에는 많은 이점이 있다. 놀랍게도 UI의 모든 상태에 대한 코드 경로는 단 하나뿐이다.  
> 주어진 상태에 대해 UI가 어떤 모습이어야 하는지를 한 번만 설명하면 그게 전부이다.

### UI 변경 시 Imperative(명령형)와 Declarative(선언형)의 차이

<img width="379" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/56466c52-d34d-45e1-a9ec-b808f1d559b1">

```dart
// Imperative style
b.setColor(red)
b.clearChildren()
ViewC c3 = new ViewC(...)
b.add(c3)
```

```dart
// Declarative style
return ViewB(
  color: red,
  child: const ViewC(),
);
```

Imperative는 개발자가 UI 요소의 상태를 관리하면서 직접 상태를 변경해주는 방식이고
Declarative 방식은 특정 UI 요소의 변경이 필요할 때마다 해당 UI 요소를 새로 만들어 내는 방식이다. 
사실 Declarative 방식이 매번 새로 만드니까 느릴것 같은 느낌이 드는데, 그럼에도 Flutter는 왜 후자를 선택한걸까?

모든 UI 요소를 변경 불가능(Immutable)하게 만들어서 개발자가 UI 요소들의 상태를 관리하는 부담을 덜어준다.
선언적으로 UI 요소를 표현하므로 레이아웃 구성을 직관적으로 프로그래밍 가능하다.
반면 매번 UI 요소를 새로 구성함으로 인해 우려되는 성능의 문제는 flutter 프레임워크 내부에서 구조적으로 해결해 준다. 
내부적으로 위젯 트리, 엘리먼트 트리, 렌더 트리라는 세 개의 트리를 거쳐 렌더링이 수행되는데 그 과정에서 위젯 트리를 캐싱하여 재활용 가능한 구조로 만들어져 있다. 
#### 따라서 개발자는 매번 UI 요소를 새로 만드는 것 같지만, 실제는 재활용 가능한 캐싱된 UI 요소는 새로 만들지 않고 재활용을 하게 된다. 

(렌더링: 각 위젯이 실제 화면에 어떻게 그려져야 하는지를 결정하고 화면에 반영하는 과정)  
(위젯 트리를 개싱: 이전에 렌더링된 결과를 저장하고 필요할 때 재사용함)  
✔️ [선언형 UI 소개 문서](https://docs.flutter.dev/get-started/flutter-for/declarative)  
✔️ [참고한 블로그](https://drogrammer.tistory.com/28)  

<br></br>

## (state)에 들어가는 상태의 종류

<img width="723" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/10214fbe-e1a5-4292-bafd-db015ccad137">

<br></br>

## 상태 관리(State Management)
상태 = 데이터 = 변수  
변수를 수정하면 UI도 알아서 바뀌게 하자

<br></br>

## Provider 라이브러리
대부분의 경우 setState()만으로 충분하지만 대규모 프로젝트에서는 관리가 어렵다.  

### ✅ Provider
* Remi가 개발한 Provider(freezed 개발자)
* **근본**인 InheritedWidget과 가장 흡사하다.
* 제약이 많다 = 에러 내기가 어렵다.
* 구글에서 여전히 공식적으로 밀고 있다.

#### Bloc
* 구글이 가장 처음 밀었던 상태 관리 라이브러리
* RxDart, Stream 등의 지식이 필요해서 러닝 커브가 있다.
* 현재도 매니아층이 있고 대형 프로젝트 위주로 사용된다.

#### GetX
* 최근까지도 가장 많이 사용되는 상태 관리 라이브러리
* 상태 관리 초보에게는 잘못된 지식으로 앱을 개발할 수 있기 때문에 비추천
* 잘못된 아키텍처로 갈 수 있는 여지가 상당하다.

#### GetX 사용을 금지하는 이유
* 상태 관리에 대한 이해 부족
* 테스트 어려움
* 근본을 무시하는 여러 가능성
* 유지 보수가 어려움
* 제약이 없다 => 버그 발생률이 높다.

#### Rivderpod
* Provider 철자를 섞은 이름이다.
* 현재 가장 인기있다.
* 코드 제네레이션 기법을 사용하여 런타임 에러를 없앴다.
* Provider의 단점을 보완하려고 만들어졌지만 완전 다른 것이 되었다.
* 근본과 많이 멀어져서 Riverpod 자체를 공부해야 한다.
* 기능 위주로 Top level에 모두 정의해 높고 어디서든 가져다 쓰는 개념이다.
* MVVM, 클릭 아키텍처와는 별개의 리버팟만의 아키텍처 공부가 필요하다.

<br></br>

## Provider 기본 사용법

<p align="center"><img width="650" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/bd3fa7bf-16ab-4478-a865-350562d9f5e1"></p>

#### * watch()는 지속적인 관찰을 하고 변경되면 build()를 리빌드 한다. build() 메서드 내에서 사용된다.
<이미지 검색 예제>  
<img width="517" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/126de8a5-53e2-418f-b2b2-1afaf4ac3842">
<img width="617" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/60863336-92ed-4377-b306-96e255086a1b">


#### * read()는 단발성 접근에 사용된다. initState() 또는 버튼 클릭 등
Provider.of<CunterModel>(context, listen: false).increase(); 와 동일한 코드이다.(legacy 방식)

<이미지 검색 예제(앱 실행하자마자 이미지 불러오기)>
* initState()에서는 다음과 같이 read() 메서드를 사용해야 한다.
* 또는 didChangeDependencies()에서 viewModel 접근이 가능하다.(단, 매번 실행하는 코드는 두면 안된다.)
<img width="487" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/10478317-109b-4766-b4dc-5a83aa02b00c">

#### Consumer
* 원하는 부분만 다시 그리기가 가능하다.
* StreamBuilder, ListenableBuilder 느낌
* UI 성능을 극한으로 끌어올려야 할 때 검토
* 이런게 있다 정도만 알아도 됨
<img width="410" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/d0f67f2c-1d07-4250-ba31-217ae2806e0c">

<br></br>

## 기타
* repository, dataSource 클래스 이름은 추상적으로.
* viewModel class에서 생성한 async 달린 메서드를 뷰에 가져와서 사용할 때 await를 안 붙여도 되는지?  
=> future를 넣지 않음으로써 화면(view)에서 개입이 되게 하지 않게 할 수 있다.
* Build() 안에 쓸 때는 watch
* ChangeNotifier에 관찰 되게 하려면 watch!
* 그 외는 read.
