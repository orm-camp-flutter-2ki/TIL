# life cycle
## StatefulWidget
- 상태를 가진 위젯을 나타내는 `class`
- createState, initState, build, setState, dispose는 앱을 만들면서 많이 이용하게 되는 메소드들
> 위젯의 생성부터 파기까지의 위젯의 생명주기가 관리 되어지고 있고, 생명주기의 특정 시점에서 특정 메소드가 호출되어집니다.
> 이러한 라이프사이클의 상태를 이해함으로써 위젯의 정교한 제어가 가능해집니다.
> 위젯을 만들 때 우리가 잘 인식하지 않고 사용하고 있는 `build` 메소드나 `initState` 메소드 역시 라이프사이클과 관련된 메소드 입니다.

<details>
<summary>🔗 참고 링크</summary>
<div>

[참고 링크 1](https://fronquarry.tistory.com/16)  
[참고 링크 2](https://fronquarry.tistory.com/19)  
[참고 링크 3](https://devocean.sk.com/blog/techBoardDetail.do?ID=165205&boardType=techBlog)  
[참고 링크 4](https://velog.io/@gomuzom/Flutter-Stateful-LifeCycle)  

</div>
</details>

<br/>

## 생명주기(lifecycle)를 알아야 하는 이유
- 생명주기를 알아야 언제 데이터를 주고 받을지, 화면이 없어질 때 로직 처리를 어떻게 할 지를 정리할 수 있음
- 화면이 더 이상 필요하지 않은 경우 자원을 해제하고 앱의 성능을 최적화할 수 있음
- 앱이 예기치 않게 종료되거나 오류가 발생할 때 어떤 동작을 취할지(예외 처리) 결정할 수 있음

<br/>

## lifecycle 개요도
> 화면(위젯) 구축 → 재 드로잉(다시 그리기) → 화면(위젯) 파기

<img width="777" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/d2db1412-397c-44ba-bba3-82b3586543ce">

<br/><br/>

## 화면(위젯) 구축
### createState()
- `statefulWidget` 가 최초로 구축될 때 호출
- `StatefulWidget` 의 상태를 관리하는 `state` 객체 생성
- `widget tree` 상태를 만들기 위해 호출
<br/>

### initState()
- `state` 객체가 초기화 될 때 자동으로 호출
    - ex) 초기 데이터 로드, 컨트롤러 초기화
- 단 한 번만 호출됨
    - 일회성 작업을 수행
<br/>

### didChangeDependencies()
- `state` 객체의 종속성이 변경될 때 호출 (상속받은 위젯을 사용 할 때)
- 이전의 의존성이 변경되었을 때 실행
    - 데이터를 가져오거나 업데이트할 때 활용 가능
- `initState` 뒤에 호출되지만, 그 이외에도 호출된다
<br/>

## 재 드로잉
### build()
- `widget` 으로 만든 `UI` 구축
- 다양한 곳에서 상태가 변경될 때마다 반복적으로 호출
    - `state` 에 속한 `widget` 이 업데이트 될 때마다
    - didUpdateWidget(), setState()가 호출될 때마다
- 변경된 부분 트리를 감지하고 대체함
<br/>

### didUpdateWidget()
- `widget` 구성이 변경될 때마다 호출됨
- 상위(부모) 위젯이 변경되고 다시 그려져야 할 때(build) 호출됨
- `oldWidget` 인수를 취득해 비교함
    - 새로운 `widget` 과 이전 `widget` 의 차이점을 처리하는 로직 구현 가능
<br/>

### setState()
- 상태가 변경 되었을 때 프레임 워크에 상태가 변경된 것을 알려줌
- 호출 시 `widget` 을 다시 그리고 화면을 update 함
<br/>

## 화면(위젯) 파기
### deactivate()
- `state` 이 활성 상태가 아니게 되면 호출
- `state` 객체가 tree 로부터 삭제될 때마다 호출
    - 필요한 정리 작업을 수행할 수 있음
- 구성 tree로부터 삭제되어 관리되지는 않으나 메모리 해제까지 된 것은 아니라 사용은 가능
<br/>

### dispose()
- `state` 가 파괴될 때(영구적으로 삭제 될 때, 두 번 다시 build되지 않을 때) 호출
- `state` 객체 정리 작업을 수행하는데 사용
    - ex) 메모리 누수 방지, 리소스 해제, Stream이나 애니메이션 해제
<br/>

## mounted == true / false
- 모든 `widget` 은 this.mounted : bool 속성을 가지고 있음
- `buildContext` 가 할당될 때 this.mounted 가 `true` 로 리턴
- `widget` 이 unmounted 일 때, setState()를 호출할 경우 에러가 발생할 수 있음

> setState() 함수 호출 시, 비동기로 시간이 지연될 경우, `widget` 이 unmounted 될 수 있음.
> → if(mounted) {…} 를 사용하여 setState() 하는 것을 추천
