Git commands (mac)
=============
### 변경사항 확인
```
$ git status
```

### 저장소 생성(초기화)
```
$ git init
```

### 원격 저장소를 복제
```
$ git clone {url}
```

### 파일 스테이징
```
$ git add [파일명] // 특정 파일 add
$ git add . // 변경된 모든 파일 add
```

### 현재 상태 기록(commit)
```
$ git commit -m "{변경 내용}"
```

### 원격으로 커밋 보내기
```
$ git push
```

### 원격으로 커밋 당겨오기
```
$ git pull
```

### 원격저장소 추가
```
$ git remote add origin {원격서버주소}
```

### 파일 삭제
```
git rm --cached --ignore-unmatch [삭제할 파일명]
```


