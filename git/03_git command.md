## Git command 

```
//이름 및 주소 설정
$ git config --global user.name "your_name"
$ git config --global user.email "your_email"

//정보 확인
$ git config --list

//새로운 Git 저장소(repository)를 생성
$ git init

//모든 파일 commit 준비
$ git add .

//변경될 commit 상태보기
$ git status

//메세지와 함께 변경파일 commit
$ git commit -m "메세지입력"

//주소의 가상 저장소와 연결
$ git remote add origin 주소

//가상 저장소에 git push
$ git push origin master

//가상 저장소에서 git pull
$ git pull origin master
```
