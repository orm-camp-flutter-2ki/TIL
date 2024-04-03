### 1. 커밋 이름 확인
커밋 이름은 github에서 "<>code" 아래의 시계모양 누르면 commits 볼 수 있음
그 중에서 지우고 싶은 커밋 바로 전의 커밋의 이름을 아래에 넣으면 됨<hr>
### 2. reset 커밋
```
git reset --hard "커밋이름"
```
위 커밋 이름 이후의 커밋은 지우겠다는 것<hr>
### 3. push로 강제로 덮어씌우기
git push -f origin master

참고 https://panython.tistory.com/24
