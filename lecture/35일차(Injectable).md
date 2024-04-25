# **Dependency Injection - Injectable**

**Injectable 패키지**

```dart
import 'package:get_it/get_it.dart';
import 'package:injectable/injectable.dart'; 
import 'di_setup.config.dart'; 
final getIt = GetIt.instance; 
@InjectableInit() 
Future<void> configureDependencies() => getIt.init();
```

이제 의존성 주입이 필요한 객체에 어노테이션을 달고 빌드하면 됨

- injectable
- singleton  (as 사용할시에 S는 대문자로 해야함)

Injectable을 사용하기 위해서는 생성자방식으로 작성되어야함

외부 라이블러리에 대해서 의존성 주입을  사용하기 위해서 getter를 사용하는데  그예시는 아래와 같다.

```dart
@module
abstract class AppModule {
	@singleton 
	PixabayApi get pixabayApi => PixabayApi(); 
} 
```

생성된 어노테이션을 활용하여 각 환경에 필요한 객체를 주입할 수 있음

여러 모듈에서 같은 타입을 정의할 때

꼭 lazySingleton으로 할 것

```dart
@module
abstract class AppModule {
@prod
@lazySingleton 
FirebaseAuth get firebaseAuth => FirebaseAuth.instance;
```

에자일 방법론

기존의 방법론

폭포수 모델 → 단계별로 하나가 끝나면 다음단계로 이어짐 

애자일 →작은 단위로 계속 수정하며 단계 반복되어 진행됨
