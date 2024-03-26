```dart
Hero({
required this. name,
required int hp, 
this. sword,
}) : _hp = hp t
// print('1. Hero 생성자') ;
}
// factory 기워드를 붙인다
// named 생성자 가능 (이름 없는 생성자 가능하지만 전체 · 1개만 • 가능)
factory Hero. fromJson (Map<String, dynamic> json) t
// 인스턴스 생성 후  리턴
return Hero(name: json[ 'name'], hp: json['hp']);
}
```
[생성자 공식문서](https://dart.dev/language/constructors#factory-constructors) 에 있는 예시는 보지 말것!

생성자를 재활용 가능하기 때문에 예시문제로만 본다면, 오해에 소지가 다분하다.

> **Factory 패턴**
공장 : 물건을 만드는 곳
factory 패턴 : 인스턴스를 만드는 패턴<br>
![](https://velog.velcdn.com/images/hee462/post/7c9da197-0143-4221-b47f-c8c22544d7d3/image.png)<br>
트럭 벤 세단 처럼 공장에서 다양하게 만들어 낼 수 있음<br>

> **Singleton 패턴**
`1개의 인스턴스`만 생성되는 것을 보증하기 위한 패턴<br>
인스턴스 생성을 여러번 시도해도 1개의 인스턴스가 `공유`됨<br>
캐시나 공유 데이터, 처리의 효율화 등에 사용되는 테크닉![](https://velog.velcdn.com/images/hee462/post/bb9f74f9-ef31-447c-91fb-f8efe1aa3e94/image.png)
```dart
class RentCar {
•// static 인스턴스를 미리 생성
static final RentCar _instance = RentCar._internal();
int _count = 0;
// factory 생성자
factory RentCar() {
return _instance;
}
// 내부에서만 사용할 named 생성자. (기본 생성자 금지 효과)
RentCar._internal();
int increment) {
return ++_count;
｝
void main() {
final instance1 = RentCar();
final instance2 = RentCar);
print(instance1 == instance2);      // true
｝

```


