>[장표](https://docs.google.com/presentation/d/1VKiTrUwbq9XQP0YPfhBEmKNlqxcu802LVOkCDkEiVbc/edit#slide=id.g2ce3deb99ee_0_1)

#### 🙋🏻Get it이란?
- Flutter에서 자주 사용되는 `의존성 주입 라이브러리(Dependency Injection)` 중 하나.
- 서비스 로케이터 패턴을 기반으로 이루어져 있다.*(막쓰면 안티 패턴이되기때문에 잘 써야 함)*
- `View`, `Bloc`등 여러가지 객체에 접근해야 할 때 사용된다.

설치명령어
`flutter pub add get_it`


>#### 사용방법 
`Singleton Factory`: 하나의 인스턴스만 존재 <br>
(veiwModel 제외 다른곳에서 사용) <br>
`Factory`: 매번 새로운 인스턴스를 생성<br>
( viewModel 에서만 사용) <br>

>### 왜? <br>
Singleton Factory<br>
특징: 하나의 인스턴스만 생성되며, 앱 전체에서 공유하여 사용됩니다.<br>
적용 곳: 상태 관리가 필요하지 않거나, 앱 전역에서 동일한 인스턴스를 공유해야 하는 서비스나 리포지토리 등에서 사용됩니다.<br>
_예시: 데이터베이스 연결, API 클라이언트 등_<br>
viewModel에서의 사용: 주로 viewModel에서는 사용하지 않습니다. viewModel은 각각의 뷰에 대한 상태를 관리하므로 새로운 인스턴스가 필요할 수 있습니다.<br>
Factory<br>
특징: 요청마다 새로운 인스턴스를 생성합니다.<br>
적용 곳: viewModel 같은 경우에는 새로운 인스턴스가 필요할 수 있으므로 Factory를 사용하여 의존성을 주입합니다.<br>
_예시: viewModel, 화면 전환 시 새로운 인스턴스가 필요한 경우_<br>
viewModel에서의 사용: viewModel에서는 사용자의 상태를 관리하므로 각각의 뷰에 대한 새로운 인스턴스가 필요할 수 있습니다. <br>
따라서 Factory를 사용하여 새로운 인스턴스를 주입합니다.<br>

### 선생님 꿀조합 추천<br>
**go _router+provider+get it 조합**<br>
![](https://velog.velcdn.com/images/hee462/post/1743d57e-134e-4a82-a8a7-1b8f6927a1d8/image.png)
![](https://velog.velcdn.com/images/hee462/post/19bb4c3c-a270-4535-a474-ecd0e35c45a9/image.png)






