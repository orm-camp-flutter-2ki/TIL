# Git Command

#### git push --force
- --force option을 사용하여 remote에 local branch 상태를 강제로 적용
- 동일한 branch에서 작업 중인 팀원이 있을 경우 미리 알리고 주의해서 신중히 사용

#### git commit --amend
- 최근 한 개의 commit message만 변경하고 싶을 경우 사용
- 변경된 commit을 remote에 강제로 push 가능

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
- 아직 commit하지 않은 변경 사항을 임시로 저장
- 작업 중이던 변경 사항을 임시로 보관하고 다른 작업을 수행할 때 유용

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
