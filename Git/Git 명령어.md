# 📖 Git 명령어
<br>

## 📄 git 버전확인
![image](https://github.com/hwangtaewook/TIL/assets/87569211/5080ec26-81c7-4b4a-887a-dbff589468e5)
- git ---version
  <br>
  <br>
## 📄 글로벌 설정
![image](https://github.com/hwangtaewook/TIL/assets/87569211/d325b066-7033-483b-b0f0-fe41067f49dd)
- git config --global user.name "hwangtaewook"
- git config --global user.email "hwangxodnr@nate.com"
  
![image](https://github.com/hwangtaewook/TIL/assets/87569211/f8b97df1-f7e5-404b-997b-2af9812f6051)

- git config --list 로 설정 확인 가능
  <br>
  <br>
## 📄 현재 디렉토리를 로컬 저장소로 만들기
- git init 기본적으로 하나의 브랜치 생성 (main or master)
  <br>
  <br>
## 📄 브랜치란?
- 브랜치는 독립적으로 어떤 작업을 진행하기 위한 개념으로 여러 작업을 동시에 진행할 수 있다.
  <br>
  <br>
## 📄 인덱스 등록
- gitadd <파일명>
  <br>
  <br>
## 📄 변경 사항을 기록 (commit)
- git commit -m "커밋 메시지"
  <br>
  <br>
## 📄 로컬 저장소를 리모트 저장소에 origin 이라는 별칭으로 연결
- git remote add origin <git주소>
  <br>
  <br>
## 📄 로컬의 origin을 리모트 main 브랜치에 업로드
- git push -u origin main
