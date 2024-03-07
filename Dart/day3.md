1. null
   String name;           틀린 표현
   String name = null;    틀린 표현
   String? name = null    맞는 표현

   int? i = null;
   int j = 0;
   j = i ?? 0
   ?? ( 두 항중 null이 아닌것을 반환 )

   name?.length
   name객체가 null일 경우 null을 반환

2. 네이밍 컨벤션
   클래스 이름 UpperCamelCase                                     예시 Children
   변수 이름 lowerCamelCase                                       예시 age
   파일, 디렉토리, 패키지 이름 lowercase_with_underscores         예시 my_package

   
3. 커밋 컨벤션
   feat : 새로운 기능 추가
   fix : 버그 수정
   docs : 문서 수정
   style : 코드 포맷팅, 세미콜론 누락, 코드 변경이 없는 경우
   refactor : 코드 리펙토링
   test : 테스트 코드, 리펙토링 테스트 코드 추가
   chore : 빌드 업무 수정, 패키지 매니저 수정

   TIL 작성에 있어서 docs사용 할 예정
