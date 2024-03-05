# 프로젝트 만들기

  New Flutter Project
  
  ![생성1](https://github.com/philiplee25/TIL/assets/76925432/1de2644f-7441-4dc5-b58e-7d4287098ce3)


  Dart tab -> Dart SDK path
  
  ![생성2](https://github.com/philiplee25/TIL/assets/76925432/c67eff56-1de5-423c-84e5-e72e057a87b6)
  
  ![생성3](https://github.com/philiplee25/TIL/assets/76925432/3142628a-e5ee-4959-827b-163618745f36)


  title 작성
  
  ![생성4](https://github.com/philiplee25/TIL/assets/76925432/40a02e7f-e440-4887-8034-575274871cdf)

  
  Next -> 끝!
  

  ## trouble shooting
  1. dart SDK 위치를 몰랐다.
   ![sdk 위치](https://github.com/philiplee25/TIL/assets/76925432/75e3df1d-4162-4cf0-bb2e-6b2281d14bcf)
  => cmd / powershell 에서 flutter doctor -v 로 flutter 가 설치된 위치를 찾고 그 안에서 dart SDK 를 찾아냈다!

    
  3. title을 정할 때 대문자를 쓰니 lib, bin 폴더는 물론 pubspec.yaml 파일 등도 생성되지 않았다. ㅠ
    ![프로젝트 생성 에러](https://github.com/philiplee25/TIL/assets/76925432/8904dcc6-21a0-4034-b62a-6d25958468fb)
  => 프로젝트 title 은 소문자로 쓰자!
