240419 (Fri)

플러터 과정 29일차

오늘 과제
=> 영화 어플 만들기
=

### 과정
1. 어플의 UI 화면 구성
2. data_source 받아오기
3. 영화 정보 선별

 # 어플의 UI 화면 구성

영화 어플을 검색 했을 때의 여러 예시를 확인 후 기본적으로 모두 가지고 있는 화면을 구성했다.

#### EX)

![image](https://github.com/BAUu/TIL/assets/44741680/a022ec3f-f289-423e-82cd-fa9020266961)

![image](https://github.com/BAUu/TIL/assets/44741680/25054715-58d7-474e-9b37-29c8a25c2cc3)

![image](https://github.com/BAUu/TIL/assets/44741680/9fdfd97b-eb98-4efa-8cee-cb783ebf65ac)

### 우리 팀이 선택한 UI

![image](https://github.com/BAUu/TIL/assets/44741680/3edb579b-3fb3-4306-8351-6b018342d958)

# data_source 받아오기

이번 영화 앱을 사용하기 위한 API는 https://developer.themoviedb.org/reference/ 이다.

# 영화 정보 선별

그 중에서 앱에 필요한 구성을 메인 홈, 검색 창, 영화 세부 정보 창 이다.

그래서 메인 홈에서는 현재 상영 중인 영화인 Movie List Tab에 Now playing을 사용했고

검색 창은 search Tab의 movie를

세부 정보 창은 movie Tab의 detail을 가져오기로 하였다.

