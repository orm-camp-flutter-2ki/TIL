# test 코드 작성 하는 방법

### 1. 테스트 하고싶은 파일 선택
ex) wizard.dart
### 2. test 디렉토리 아래 동일 위치에 _test를 붙인 파일 생성
ex) lib/test/wizard_test.dart

```
// 테스트 기법중 given > when > then 사용 : BDD(행위주도 개발)
// 주어진 상황(given)
// 언제( when) : 실행
// 그러면 (then) : 검증
import 'package:test/test.dart'

void main(){
    test('Wizard Test', (){
        //given(준비)
        final wizard = Wizard(name:'마법사', hp:100);
        final hero = Hero(name:'히어로', hp:10);
        
        //when(실행)
        wizard.heal(hero);
        
        //then(검증)
        expect(hero.hp, equals(20));
    })
}
```

### 터미널에 test pass 여부가 나옴