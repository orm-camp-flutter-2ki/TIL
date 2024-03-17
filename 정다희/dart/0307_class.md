# class

## 용어정리
- 오브젝트: 현실세계의 모든 객체
- 클래스 : 오브젝트를 가상세계용으로 구체화 한것
- 인스턴스 : 클래스를 활용해 메모리상에 만들어낸것

클래스의 속성은 필드로, 동작을 메소드로 선언한다.
new 키워드를 사용하여 클래스로부터 인스턴스를 생성. Dart에서 new 키워드는 생략가능
```
class Hero {
    String name;
    int hp;
    //final 키워드로 상수 선언 가능
    Hero(this.name, this.hp);
    
    void attack(){}
    void run(){}
    void sleep(){
        hp = 100
        print('$name 은 잠을 자고 회복했다');
    }
 
```

### 클래스 멤버 변수의 네이밍 컨벤션
클래스명 : 명사, pascal(단어의 맨 처음은 대문자)
필드명 : 명사, camel(최초 이외의 단어의 맨처음은 대문자)
메소드명 : 동사, camel

### 클래스 로 뭘하는건데 ?
- 정의한 클래스로 인스턴스 생성 가능
- 새로운 변수 타입 가능
```
Hero hero = Hero('hero', 100);
```


