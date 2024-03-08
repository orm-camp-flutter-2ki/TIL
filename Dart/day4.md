# 배운 내용
- 클래스
  -   다트는 모든 타입이 레퍼런스 타입이다.
       

  -   클래스를 인스턴스화 할때 final을 사용하면 클래스타입을 생략할수있다. 타입을 추론한다.
   예시
   
   ```dart
   final hero = Hero(name: '홍길동', hp:100);
   ```

  -   named (옵셔널) 파라미터를 사용한 생성방법
   ```dart
   class Hero{
   String name;
   int hp;
   Sword? sword;

   Hero(this.name, this.hp, {this.sword});
   }

   final hero1 = Hero('전사',100, sword:sword);
   ```
  -  모든 클래스는 반드 1개 이상의 생성자를 가진다.
  -  필드를 공유하는 2가지 방법
     1. 스태틱 변수를 사용한다.
     2. Top level 변수를 사용한다.
   
  -  정적 메소드 안에서 액세스 할 수 있는 것은 정적 멤버만 가능

   

