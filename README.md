# Flutter TIL

240506_04_김윤아

알고리듬 책 추천 
초등학생이 읽은 거 같이 그림 많은 거
ex) 난생처음 컴퓨팅 사고 with 파이썬
https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=259540160

한국엔 다트책 없음 - 안팔려서

open source 기여
오탈자 수정해도 PR받아준다.

git clone 
지라(atlassian jira) : 일정관리, 프로젝트 관리 용으로 회사에서 사용 
SUN : github과 비슷, 버전관리하는 시스템, SI업체 등에서 사용.. github이 더 편하다. 

<Futter 를 위한 Dart 문법>

다트는 객체지향과 함수형 프로그래밍 모두를 지원한다.
( 객체만 하다 함수하면 어렵지만 둘다 처음이면 다행 )
https://velog.io/@majaeh43/%EC%A0%88%EC%B0%A8%EC%A7%80%ED%96%A5-%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5-%ED%95%A8%EC%88%98%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D

dartpad에서 간단한 연습할 수 있어. -> 아이패드로 공부한다면 좋을 거 같기도~?

디스코드 #학습자료 에 문법 관련 강의와 자료 있음! 공부해라 
https://docs.google.com/presentation/d/1waYD61tUlg5Y1JdpfwfN7ULWioQQA-x7WAIhZNSGGcY/edit#slide=id.g1221ceda84c_0_1197

int 정수
double 실수
String 문자열 
bool 참 거짓 

변수 앞에 $붙여서 print 가능 

형변환 자료형 
int/double/String 간 변환가능

일반적으로는 계산 따로 출력 따로 한다. 

num++
num=num+1
num+=1 

모두 동일한데 1씩 더할때 첫번째꺼 제일 많이 쓴다 . 2씩 더하려면 세번째 사용 

초보라면 (나 ) as, var 사용 금지 ! (단점이 더 많아)

<헷갈리는 개념들> 

컴파일 vs 런타임
https://spaghetti-code.tistory.com/35

final vs const 

final 은 컴파일 할 때 실행되고 const 는 런타임에 실행된다. 
const가 비효율적! 그냥 final 써라 

컴파일언어 vs 인터프리터언어
컴파일이 안정성이 높고 디버깅도 쉽다.
인터프리터 언어로는 자바스크립트가 있다.
사전에 에러 캐치가 되지않고 런타임에 모든 에러들이 터지기 때문에 쓰레기다. 
그 점을 보완하기위해 나온 것이 타입스크립트!
https://velog.io/@congaweb/compiler-interpreter


매개변수 vs 인자 vs 인수 


맥 단축키 
[opt+cmd_l] 누르면 코드 정리 가능 (reformat code)

안드로이드 스큐디오 lib 폴더에 날짜별로 폴더 만들어서 코드 정리하기

import dart : io 
input 받기 위해 사용하는 라이브러리 
(dart keyboard input 구글 검색) 

<for 문> 

for(;;) 무한루프 

for(변수초기화;조건;변수조작){}
ex. for(i=0;i<3,i++){} 



<hw> 
stdout.write 한줄로 출력되는 함수
  
if문 안에서 변수 설정을 하면 적용이 안된다.
if문 밖에서 설정해야한다! 
