## InheritedWidget
원하는 위젯으로  
원하는 객체를  
의존성 주입(Dependency Injection)을 해 주는 위젯
> 의존성 주입이란?  
> 어떤 객체가 다른 객체에서 사용되도록 하는 것이다.
> 
> <img width="551" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/0e454aeb-19dd-4c97-9fcd-2e139139e73d">
>
> 생성자를 통해 필요한 객체를 전달하는 것이 일반적인데 이것은 의존성 트리가 깊어질수록 단계를 많이 타야되는 단점이 있다.  
> #### 이러한 단점을 InheritedWidget이 해소해준다.

<br></br>

플러터는 트리 구조인데, 변화가 필요한 위젯이 제일 하위에 있을 경우 필요한 데이터를 받으려면 트리의 Top에서 Bottom까지 생성자를 통한 데이터 전달이 필요하다.  
xxx.of(context) 형태로 아무데서나 사용할 수 있도록 만들려면 InheritedWidget을 사용하면 된다.  
InheritedWidget은 위젯 트리의 상위에서 하위로 데이터를 전달하는 데 사용되는 위젯이다.  
대표적으로 이 경우가 필요한 위젯들  

- MediaQuery
- Theme

MediaQuery, Theme을 사용할 땐, Theme.of(context)의 형태로 context가 필요하다.

InheritedWidget의 'BuildContext.dependentOnInheritedWidgetOfExactType'을 사용하면, 상속된 위젯의 가장 가까운 context를 얻을 수 있다.

* <img width="320" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/e933a600-d170-4913-a401-bcb578654a23">
* <img width="550" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/e2364a15-2e1d-4322-9a95-d780efbbf1c9">

InheritedWidget를 상속한 MyColor()를 제일 탑, 중간에서 불러온 경우, 제일 하위 위젯은 MyColor2()의 context를 참조하게 된다.

InheritedWidget은 앱의 상태를 관리하고 상태가 변경될 때 자동으로 하위 위젯에 변경 사항을 전달하는 데에 유용하다.  
이는 앱에서 상태 관리를 간편하게 하고, 위젯 간에 데이터를 효율적으로 공유할 수 있게 한다.

<br></br>

## 기타

#### changeNotifier, BuildContext, InheritedWidget 딥 다이브 추천
* 지도는 구글맵을 사용하는 것을 추천(네이버나 카맵은 pub.dev에서 개인이 만들어 놓은 것을 사용해야 함)
* 다음 주소 API 라이브러리 : kpostal
* initState()에서 mediaQuery 같은 거 사용하면 안됨. Context 접근 안됨
=> didChangeDependencies()에서 해야함.
* 배포하기 위해 release 생성
* 안드로이드 폴더 경로를 선택하고 다시 프로젝트를 연다. 이렇게 해서 배포하면 편함. 또는 공식 문서대로 따라해도 된다.
  * 안드로이드 아이콘은 안드로이드 프로젝트 안에서 image Assets으로 생성한다.
  * signingKey(서명키) 확인: 터미널에 .android 폴더 경로로 들어가서 debug.keystore 파일 확인.
  * 서명키 만들 때의 비밀번호를 통해 앱 업데이트 등을 진행할 수 있다.
  * alias는 하나만 정하고, 그 밑의 비밀번호도 위와 동일하게 작성. 유효기간은 길게(키 유효기간 연장이 안되기 때문).
