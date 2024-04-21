# Git Command

#### git push --force
- --force option을 사용하여 remote에 local branch 상태를 강제로 적용
- 동일한 branch에서 작업 중인 팀원이 있을 경우 미리 알리고 주의해서 신중히 사용

#### git commit --amend
- 최근 한 개의 commit message만 변경하고 싶을 경우 사용
- 변경된 commit을 remote에 강제로 push 가능

#### git rebase
- rebase를 사용하는 주된 이유는 git history를 선형으로 유지하기 위함
- history를 어떻게 유지하고 싶은지에 따라 rebase와 merge 중 하나를 선택하여 사용
1. 예를 들어, feature branch에서 작업을 진행하던 중 main branch에 최신 변경 사항 발생
2. feature branch에 main branch의 최신 변경 사항이 필요할 때 rebase를 하면 최신 main branch에서부터 작업이 시작된 것처럼 보이게 하여 git history를 선형으로 깨끗하게 유지(rebase 대신 merge를 할 경우 merge에 대한 새로운 commit이 생김)
```
git checkout feature
git rebase main
```
<img width="571" alt="스크린샷 2024-04-21 오후 1 48 49" src="https://github.com/leeseowoo/orm-camp-flutter-note/assets/76784643/613db6d8-f70a-49d3-a6bd-86f86386436e"></br>
> https://www.atlassian.com/ko/git/tutorials/merging-vs-rebasing

#### git merge
- 두 개의 branch를 병합
```
git checkout feature
git merge main
```
- 이렇게 하면 feature branch에 두 개의 branch에 대한 hitory를 연결하는 새로운 merge commit이 만들어져 다음과 같은 branch 구조를 얻게 됨
<img width="499" alt="스크린샷 2024-04-21 오후 1 47 12" src="https://github.com/leeseowoo/orm-camp-flutter-note/assets/76784643/08e09c55-ccd1-441e-903c-fd813baaeeed"></br>
> https://www.atlassian.com/ko/git/tutorials/merging-vs-rebasing


#### git rebase -i HEAD~n
- remote에 push된 commit message를 변경하고자 할 때, local에서 message를 수정하고, remote에 강제로 push하는 절차를 따르면 변경 가능

1. -i option을 사용하여 interactive rebase mode로 진입
2. HEAD\~n은 rebase를 시작할 기준이 되는 commit이나 branch  
  2-1. HEAD\~n는 현재 branch의 가장 최근 commit에서 n개의 commit을 거슬러 올라간 commit을 나타내는 방식  
  2-2. HEAD\~1은 현재 branch의 가장 최근 commit에서 바로 이전 commit, HEAD~2는 HEAD commit에서 두 번째 이전 commit을 의미
3. interactive rebase 편집기 화면이 나타나면 수정할 commit의 앞에 있는 pick을 reword로 변경 후 파일을 저장하고 종료
4. rebase가 완료되면 commit message 수정 완료
5. 수정된 commit을 remote에 강제로 push

#### git reset --hard \<commit_hash>
- local branch를 이전 상태로 재설정, commit을 완전히 제거하고 싶은 경우 --hard option 사용

1. \<commit_hash>는 해당 branch에서 재설정할 commit의 hash 값을 나타내며 재설정할 지점까지 commit을 삭제
2. --force option을 사용하여 remote에 local branch의 상태를 강제로 적용  

위 단계를 수행하면 remote에서 해당 commit이 삭제되고 local과 일치하게 되며, --hard option을 사용하면 commit뿐만 아니라 file 변경 사항도 함께 삭제되므로 주의 필요

#### git fetch
- remote의 최신 변경 사항을 local로 download할 때 사용

#### git stash
- 아직 commit하지 않은 변경 사항을 임시로 보관
- 작업 중이던 변경 사항을 임시로 보관하고 다른 branch로 이동해서 작업을 수행하고자 할 때 유용
```
git stash
git stash save
git stash list
git stash apply
git stash pop
git stash drop
```

#### git log --graph
- branch들의 commit history를 시각화
```
git log --graph --oneline --decorate --all
```

#### git diff
두 개의 commit, branch, 또는 file 사이 차이점을 표시하여 코드 변경 사항을 비교할 때 사용

#### git show
- commit의 변경 사항, 메시지, 날짜, 저자 등 세부 정보 확인


#


#### git init
- 현재 directory를 새로운 git 저장소로 사용할 수 있도록 초기화
- 해당 directory가 git 저장소로 변환되어 git 관련 작업 수행 가능

#### git config
- global 또는 local 수준에서 git 설정 확인 및 변경
```
git config --list
git config --global
git config --local
```

#### git clone
- remote 저장소 복사본을 local directory에 만듦

#### git status
- working directory와 staging area의 현재 상태 확인

#### git add
- working directory의 변경 사항을 staging area 추가
```
git add .
git add <file>
```

#### git restore --staged
- staging area에 올라간 파일을 unstage
```
git restore --staged <file>
```

#### git commit
- staging area에 올라간 변경 사항을 commit
- 커밋 메시지를 입력하여 변경 사항을 설명
```
git commit -m ""
```

#### git push
- local에 있는 commit을 remote로 전달하여 동기화

#### git pull
- remote의 변경 사항을 local로 가져와 remote의 최신 상태를 local에 적용

#### git log
- commit 이력 확인
```
git log
git log --oneline
git log --oneline -3
```

#### git branch
- branch 생성, 확인, 삭제 등 수행
```
git branch
git branch <branch>
git branch -d <branch>
```

#### git checkout
- branch 전환 또는 생성과 함께 전환
```
git checkout <branch>
git checkout -b <branch>
```
