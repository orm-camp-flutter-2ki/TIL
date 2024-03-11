# 테스트 코드

1. 프로젝트 폴더 내에 test directory 에 test 파일 생성
   
     ![image](https://github.com/philiplee25/TIL/assets/76925432/7b809dba-cd41-44c5-a134-25a23e0c1911)


2. 같은 directory 경로에 넣되 이름에 _test로 끝나도록 명명한다.

     ![image](https://github.com/philiplee25/TIL/assets/76925432/391d53c0-372b-49c6-a6a8-364a0d49867d)


3. 형식은 아래와 같다.

```
  void main() {
    test('description', body() { });
  }
```


4. given - when - then 테스트

```
  void main() {
  // test('description', body() { });   <- test code 형식
  test('test', () {
    // given (준비)
    Cleric cleric = Cleric('홍길동');

    // when (실행)
    cleric.hp = 101;
    cleric.selfAid();

    // then (검증)
    expect(cleric.hp, Cleric.maxHp);
    expect(cleric.hp, 101);
  });
}
```
