## Result 패턴
> Result 클래스는 성공시에는 데이터를, 실패시에는 Exception(또는 String)을 담는 객체를 정의한다

  1. 링크를 참고하여 라이브템플릿 설정을 해준다. <a href="https://gravel-pike-705.notion.site/Flutter-Live-Templeate-579bac3070754bdf8fa10afe4ebe8c92#8999896cfad04dd6a5d249f42f9503d4">여기</a>
  2. Result 클래스를 생성한다.
  3. Result 패턴을 도입하는 곳에서 응답 객체를 Result 클래스로 감싸준다.
  4. 예외를 처리해준다.

<img width="500" alt="image" src="https://github.com/Gunbam27/TIL/assets/95085649/7a1c2146-c054-48b9-bbd7-ec6255c64ad8" />

[result 클래스 예시]

<img width="500" alt="image" src="https://github.com/Gunbam27/TIL/assets/95085649/ec7a9ed5-c2e2-4668-8a52-fb2d88f793cd" />

[Repository 에서 Result 타입을 반환하도록 작성]

<img width="500" alt="image" src="https://github.com/Gunbam27/TIL/assets/95085649/027055d3-a5dc-4b1c-919e-f01aa05f8faf" />

[switch문으로 에러종류에 따른 print 출력]

### Enum class vs Sealed clas
👉🏻 둘다 타입을 제한적으로 사용하고자 할 때 많이 사용하게 됨.

`enum` 👉🏻 상수를 선언하고 묶어서 사용하는데에서 끝난다. 상수의 집합을 위해 지원되는 기능. <br/>
`sealed class` 👉🏻 하위 클래스를 종속시킬때 쓴다.(마치 num타입 하위에 int와 double이 있듯이) enum 과 동일하게 switch 문과 조합하여 모든 처리를 강제할 수 있다.
