## [Git & GitHub]

### 1. Git 설치
  ```shell
winget install -e --id Git.Git
  ```

### 2. Git 명령어  
  - [깃 명령어 모음집 : 코딩알려주는누나](https://hackmd.io/@oW_dDxdsRoSpl0M64Tfg2g/ByfwpNJ-K)

### 3. MarkDown(.md) 작성 문법
   - [*Markdown 작성법 (영어)* ](https://www.markdownguide.org/cheat-sheet/)
   - [*Markdown 작성법 (한글)* ](https://gist.github.com/ihoneymon/652be052a0727ad59601)

### 4. **Fork** repository
   - 상대 Repository를 본인 계정의 Repository로 복사하여 저장하기 위해 사용함.
   - 본인 계정에 Fork된 Repository는 수정해도 상대 Repository에 영향을 주지 않음.

### 5. **Clone, Add, Commit, Push**
  - Clone : 원격 저장소(repository) -> 로컬 저장소(작업 디렉터리)로 복사.
  - Add : Commit하기 원하는 파일(ex. 수정된 코드)을 스테이지(커밋 준비공간)에 올림. 실제 변경은 Commit 단계에서 수행됨.
  - Commit : **로컬에** 실제 변경된 사항을 저장. 이때, 수행한 변경 사항에 대한 메시지를 함께 설정한다. (ex. first commit)
  - Push : 커밋한 내용을 **원격 저장소**에 저장

### 6. **Pull** requests (PR)
   - 본인 repository 내용을 상대 repository에 보내서 합치기 위해 사용함.
   - Pull Request시, 상대 repository의 알맞은 master(main)이 아닌 branch에 맞게 해당 branch에 pull할 수 있도록 할 것.
   - master 권한을 가진 상대가 PR을 승인하면 상대 repository에 merge됨.
