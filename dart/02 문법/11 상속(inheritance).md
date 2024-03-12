# 상속 (inheritance)
- 이전에 만든 클래스와 닮았지만 일부 다른 클래스를 만들 필요가 있을 경우에 사용한다.
- 기반이 되는 클래스를 `extends`로 ... **기능을 확장하는 것**이다.
- 다중상속은 Dart에서 사용하지 않는다.  
<br/>

### is - a 원칙
- 올바른 상속은 'is-a 원칙' 규칙에 따른 상속을 말한다.  
- SuperHero is a Hero : SuperHero는 Hero의 한 종류이다.  
<br/>

### 잘못된 상속  
- 현실 세계의 등장인물 사이에 개념적으로 'is-a' 관계가 되지 못함에도 상속을 사용한 경우를 말한다.
- 클래스를 확장할 때 현실 세계와의 모순이 생긴다.
- 객체 지향의 3대 특징 중 '다향성'을 이용할 수 없게 된다.
<br/>

### 구체화와 일반화의 관계
- 자식클래스일 수록 구체화되고, 부모 클래스일 수록 추상적인 것으로 일반화된다.  
<br/>

## extends
### constructor
- 기반 되는 클래스의 생성자를 그대로 가져온다.
<img width="1011" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/f37ef85f-71c5-4084-8d9e-271d638ded79">

### super  
- 생성자에 `super.`는 기반이 된 클래스를 나타낸다.

![image](https://github.com/yujiyeong/TIL/assets/149862753/b9056203-abb0-4c4e-8d19-399322defa64)

<br/>

## override (@override)    
<img width="730" alt="image" src="https://github.com/yujiyeong/TIL/assets/149862753/4b50f238-f59a-46c0-9a19-2d4e2c716f6f">

- @ : annotation, 일종의 주석     
- 기존 기능을 재정의 하는 것이다.   

