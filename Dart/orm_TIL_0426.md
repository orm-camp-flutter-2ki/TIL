240426 (Fri)

플러터 과정 34일차 

알리미 프로 Mock-data 분석
========


main.dart
-

**import 불러오기**

firebase_core 는 firebase 클라우드 서비스를 사용하기위해

cloud_firestore 는 데이터베이스에 접근하기 위해

**final FirebaseFirestore db;** 

코드는 Dart 프로그래밍 언어에서 Firebase Firestore 데이터베이스를 사용하기 위한 변수 선언입니다.

**academyRepository 변수:**

- 이 변수는 `FirebaseAcademyRepositoryImpl` 클래스의 인스턴스를 담고 있습니다.
  
- `FirebaseAcademyRepositoryImpl` 클래스는 학원 정보와 학생 정보를 관리하는 기능을 제공하는 클래스입니다.

**`FirebaseAcademyRepositoryImpl` 생성자:**

- `academyRepository` 변수에 할당된 `FirebaseAcademyRepositoryImpl` 클래스의 생성자에는 두 개의 인수가 전달됩니다.

- `uid`: "KSm9vmT57KNDRb0QFWlZ0W416qs1" 이라는 문자열 값입니다. 이 값은 아마도 현재 사용자의 ID 함수이다.
  
- `firebaseFirestore`: `db` 변수에 저장된 `FirebaseFirestore` 인스턴스입니다. 이 인스턴스는 데이터베이스에 접근하는데 사용됩니다.


academy_repository.dart
-

- `package:alimipro_mock_data/domain/model/academy.dart` 에서 `Academy` 클래스를 불러옵니다.
- `../model/student.dart` 에서 `Student` 클래스를 불러옵니다.
두 클래스는 학원 정보와 학생 정보를 담는 데이터 모델 클래스이다.

**`AcademyRepository` 인터페이스:**
  
    - `abstract` 키워드는 이 클래스가 추상 클래스임을 의미합니다. 즉, 직접 객체를 생성할 수 없고, 상속받아 구현해야 하는 클래스입니다.

    - 인터페이스 내부에는 학원 정보와 학생 정보를 관리하는데 필요한 메서드들이 선언되어 있습니다.
    
        - `getAcademyStream`: 학원 정보를 실시간 스트림(Stream) 형태로 반환하는 메서드입니다. 데이터베이스의 변경 사항을 실시간으로 받아보는 데 사용될 수 있습니다.
        
        - `getAcademy`: 학원 정보를 단일 객체(Future<Academy>) 형태로 반환하는 메서드입니다.
        
        - `getStudents`: 학생 정보 목록을 리스트(Future<List<Student>>) 형태로 반환하는 메서드입니다.


academy.dart
-

**라이브러리 불러오기:**
    - `package:alimipro_mock_data/data/mapper/date_time_converter.dart` 에서 `DateTimeConverter` 클래스를 불러옵니다. (추측컨데 날짜와 시간 데이터를 변환하는 기능을 제공하는 클래스)
    
    - `package:cloud_firestore/cloud_firestore.dart` 에서 Cloud Firestore 관련 기능을 사용합니다.

    - `package:freezed_annotation/freezed_annotation.dart` 라이브러리와 함께 사용되는 코드입니다. (freezed 패키지 이용)


**`Academy` 클래스:**
    
    - `@freezed` 는 freezed 패키지를 이용하여 데이터 클래스를 생성하는 데 사용하는 어노테이션입니다.
    
    - 이 클래스에는 학원 정보를 나타내는 필드들이 정의되어 있습니다.
        
        - `countryCode`: 학원 국가 코드 (문자열)
        
        - `createdTime`: 학원 생성 시간 (날짜와 시간 정보, `DateTimeConverter` 사용)
        
        - `master`: 학원장 이름 (문자열)
        
        - `name`: 학원 이름 (문자열)
    
        - `phone`: 학원 전화번호 (문자열)
**생성자:**

    - 기본 생성자는 `_Academy` 입니다. 각 필드에 대한 값을 매개변수로 받아 객체를 생성합니다.

**fromJson 생성자:**
   
    - `fromJson` 생성자는 JSON 데이터를 파싱하여 `Academy` 객체를 생성하는 역할을 합니다. freezed 패키지가 자동으로 생성하는 부분입니다.

student.dart
-
`package:freezed_annotation/freezed_annotation.dart` 라이브러리만 불러옵니다.
**`Student` 클래스:**

    - `@freezed` 는 앞 코드와 동일하게 freezed 패키지를 이용하여 데이터 클래스를 생성하는 데 사용하는 어노테이션입니다.
    
    - 이 클래스에는 학생 정보를 나타내는 필드들이 정의되어 있습니다.
    
        - `id`: 학생 고유 식별 번호 (문자열, JSON에서는 'uid' 키 사용)
        
        - `name`: 학생 이름 (문자열)
        
        - `parentsPhone1`: 학부모 전화번호 1 (문자열)
        
        - `parentsPhone2`: 학부모 전화번호 2 (문자열, 선택적)
        
        - `parentsPhone3`: 학부모 전화번호 3 (문자열, 선택적)
**생성자:**
  
    - 기본 생성자는 `_Student` 입니다. 각 필드에 대한 값을 매개변수로 받아 객체를 생성합니다.
**fromJson 생성자:**

    - `fromJson` 생성자는 JSON 데이터를 파싱하여 `Student` 객체를 생성하는 역할을 합니다. freezed 패키지가 자동으로 생성하는 부분입니다.
    
    - JSON 데이터에서 'uid' 키로 id 값을 가져오도록 `@JsonKey(name: 'uid')` 어노테이션을 사용했습니다.

firebase_academy_repository_impl.dart
-

이 코드는 **Firebase Firestore를 이용하여 학원 정보와 학생 정보를 관리하는 클래스** (`FirebaseAcademyRepositoryImpl`) 를 구현하고 있으며,
앞선 `AcademyRepository` 인터페이스를 상속받아 정의된 메서드들을 구체적으로 구현하고 있습니다.

**코드 분석:**

**필드:**
    
    - `_uid`: 생성자로부터 받은 학원 고유 식별 번호 문자열을 저장합니다.

    - `_firebaseFirestore`: 생성자로부터 받은 FirebaseFirestore 인스턴스를 저장합니다.
**생성자:**
    
    - `uid`와 `firebaseFirestore` 를 매개변수로 받아 객체를 생성합니다.
    
    - 받은 `uid` 값을 `_uid` 필드에 저장합니다.
    
    - 받은 `firebaseFirestore` 인스턴스를 `_firebaseFirestore` 필드에 저장합니다.

**메서드 구현:**

    - **`getAcademyStream`**
    
        - 학원 정보 스트림을 반환하는 메서드입니다.
        
        - `_firebaseFirestore` 의 `Academies` 컬렉션에 `_uid` 문서에 대한 실시간 스냅샷(snapshots) 스트림을 생성합니다.
        
        - 스트림을 통해 받은 데이터(DocumentSnapshot)를 `Academy.fromJson` 메서드를 이용하여 `Academy` 객체로 변환하여 반환합니다.
    
    - **`getAcademy`**
    
        - 학원 정보를 단일 객체로 반환하는 메서드입니다.
        
        - `_firebaseFirestore` 의 `Academies` 컬렉션에 `_uid` 문서를 불러옵니다.
        
        - 문서가 존재하지 않으면 `Exception`을 발생시킵니다.
        
        - 존재하는 경우 문서 데이터(DocumentSnapshot)를 `Academy.fromJson` 메서드를 이용하여 `Academy` 객체로 변환하여 반환합니다.
    
    - **`getStudents`**
    
        - 학생 정보 목록을 반환하는 메서드입니다.
        
        - `_firebaseFirestore` 의 `Academies` 컬렉션에 `_uid` 문서의 하위 컬렉션인 `Students` 컬렉션을 불러옵니다.
        
        - 쿼리 결과(QuerySnapshot)의 문서(DocumentSnapshot) 목록을 가져와 각 문서 데이터를 `Student.fromJson` 메서드를 이용하여 `Student` 객체로 변환합니다.
        
        - 변환된 `Student` 객체 목록을 리스트로 반환합니다.

**전체적으로**

`FirebaseAcademyRepositoryImpl` 클래스는 `AcademyRepository` 인터페이스를 상속받아 구체적인 기능을 구현합니다.
이 클래스를 사용하면 Firebase Firestore를 통해 학원 정보를 실시간으로 받아보거나, 학원 정보와 학생 정보를 불러오는 등의 작업을 수행할 수 있습니다.

date_time_converter.dart
-

**설명:**

이 코드는 `DateTimeConverter` 라는 이름의 맞춤 변환기 클래스를 정의합니다. 이 클래스는 Dart의 `json_annotation` 라이브러리와 함께 사용되며, JSON 데이터의 직렬화 및 역직렬화 과정에서 Dart의 `DateTime` 객체와 Firebase Firestore의 `Timestamp` 객체 간의 변환을 담당합니다.

**코드 분석:**

1. **라이브러리 불러오기:**

    - `package:cloud_firestore/cloud_firestore.dart`: Cloud Firestore 관련 클래스 (예: `Timestamp`) 를 불러옵니다.

    - `package:json_annotation/json_annotation.dart`: JSON 어노테이션과 관련된 클래스들을 불러옵니다.

2. **`DateTimeConverter` 클래스:**
    
    - 이 클래스는 `json_annotation` 라이브러리가 제공하는 `JsonConverter` 인터페이스를 구현합니다.
    
    - 생성자 (`const DateTimeConverter()`) 는 간단하며 인수를 필요로 하지 않습니다.

3. **`fromJson` 메서드:**
 
    - `Timestamp` 객체를 입력값 (`timestamp`) 으로 받습니다.
    
    - `timestamp.toDate()` 메서드를 사용하여 `Timestamp` 객체를 `DateTime` 객체로 변환하고 반환합니다.
    
    - 이는 Firebase Firestore 타임스탬프 형식을 표준 Dart `DateTime` 객체로 변환하는 역할을 합니다.

5. **`toJson` 메서드:**

    - `DateTime` 객체를 입력값 (`date`) 으로 받습니다.
    
    - `Timestamp.fromDate(date)` 생성자를 사용하여 `DateTime` 객체를 `Timestamp` 객체로 변환하고 반환합니다.
    
    - 이는 표준 Dart `DateTime` 형식을 Firebase Firestore와 호환되는 `Timestamp` 객체로 변환하는 역할을 합니다.

**전반적인 기능:**

이 변환기 클래스를 사용하면 JSON 데이터를 처리할 때 `DateTime` 및 `Timestamp` 객체를 모두 손쉽게 사용할 수 있습니다. 
모델 클래스의 `DateTime` 필드에 `@JsonKey` 어노테이션과 함께 이 변환기를 사용하면 해당 필드의 직렬화 및 역직렬화가 자동으로 처리됩니다. 
이를 통해 두 데이터 유형 간의 수동 변환을 줄이고 일관성을 유지하는 데 도움이 됩니다.



