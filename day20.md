# 이상적인 설계 - 도서 대출 관리 프로그램  적용

###  데이터 소스부분 . ( 라이브러리 소스 ) 
1. 실질적으로 데이터를 가져오는 부분 (하드코딩을 해서 데이터를 집어넣었음.  bookList = [ ] ; bookList.add(Book(데이터) )
2. CRUD만 구현하는 부분
   
예시 
```dart
// Creat 구현 부분 , book을 book 리스트에 저장합니다.               
bool createBook(Book book) {
    bookList.add(book);
    return true;
  } 
```
### 레파지토리 ( 라이브러리 레파지토리 소스 )     final BookDataSource _bookDataSource; 
1. 라이브러리 데이터로 부터 받은 값을 레파지토리에서 구현함.  
2. 데이터 액세스 레이어를 추상화합니다.
3. 비즈니스 로직과 데이터 액세스 로직의 분리
4. 도메인 객체와 데이터베이스 스키마의 매핑을 담당합니다.

예시
```dart
// 데이터 소스의 createBook 부분을 가져와서 유저 저장을 하는 부분 ( 매핑 + 추상화 )     , 데이터 소스에게만 요청
bool saveUser(User user) {
    return _bookDataSource.createUser(user);
  }
```

###  도메인 레이어 ( 라이브러리 클래스 )         final Repository repository;  LibrarySystem(this.repository);  
1. 비지니스 로직
2. 어플의 핵심적인 정책 

예시 
```dart
//  레파지토리의 saveUser 부분을 가져와서 유저저장을 하는 부분           , 레파지토리에게만 요청
 bool signUpUser(User user) {
    if (repository.getUserByNameAndPhoneNum(user.name, user.phoneNum).isEmpty) {
      return repository.saveUser(user);
    } else {
      return false;
    }
  }
```

### UI 레이어 ( 콘솔 앱 함수 부분 )                 final librarySystem = LibrarySystem(LibraryRepositoryImpl(bookDataSource: BookDataSourceImpl()));
1. 도메인에 데이터를 표시하고 사용자에 이벤트를 처리해서 데이터를 표시

예시
```dart
// 라이브러리 클래스의  signUpUser를 가져와서 유저저장을 하는 부분       ,비즈니스 로직에게만 요청
User signUpData = User(
          name: name,
          phoneNum: phoneNum,
          signUpDate: DateTime.now(),
          address: address,
          birthDay: birthDay,
          history: {});
      bool isSuccess = librarySystem.signUpUser(signUpData);
      if (isSuccess) {
        print('회원 가입 성공!');
        return;
      } else {
        print('이미 존재하는 회원입니다.');
        return;
      }
```

## 데이터의 흐름 
도메인레이어.signUpUser -> 레파지토리.getUserByNameAndPhoneNum 레파지토리.saveUser -> 데이터소스.createUser

### 설계적 로직 특징
UI Layer는 변경되기 쉽다.
Data sources 변경되기 쉽다. 
Domain Layer 변경이 잘 안되는 부분, 다른 레이어의 변경으로 인해서 변경이 되면안됨.
Repository 데이터소스만큼은 아니지만 변경되기 쉽다.

->입력과 출력에 가까울 수록 저수준이다.
->도메인 레이어는 고수준이다.
-> 변경되기 쉬운걸 고려하여 도메인 레이어를 작성한다.



