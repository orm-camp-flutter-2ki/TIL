
git 명령어 

# git 버전 확인

* git --versiion

# 글로벌 설정

* git config --global user.name "내이름"
* git config --global user.email"사용할 이메일"

# 현재 디렉토리 로컬 저장소 만들기

* git init

# 최초 push
* git remote add origin "git address"
* git push -u origin main or master

# 수정 후 push 
* git add .
* git commit -m "메세지"
* git push

  # branch?
  독립적으로 어떤 작업을 하기 위한 개념 -> 여러작업을 동시에 할 수 있음

  # fork 와 clone 차이점
* fork : 나의 remote에 저장하여 의존성 있음 -> 최초의파일 삭제시 작업내용사라짐
* clone : 단순히 파일 복사하여 내가 재편집 할수 있음
