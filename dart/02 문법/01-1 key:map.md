# 키맵 (key-map)
- 키(key)와 값(value)의 쌍으로 이루어진 요소를 담는 자료 구조이다.
- 크기를 정해두지 않고 요소를 추가할 때마다 크기가 커진다.   
- 키의 중복은 허용되지 않는다.
- 순서를 보장하지 않는다.
<br/>

## 선언
```dart
// 이름(key)과 나이(value)를 매핑
Map<String, int> person = {
  'david han': 30,
  'amy kim': 25,
};
```
<br/>

## 수정 및 출력
```dart
// 요소 추가
person['Bob'] = 35; // 'Bob' 추가

// 요소 제거
person.remove('Alice'); // 'Alice' 삭제

// 맵의 모든 요소 제거
person.clear();

// 특정 키의 값
int johnAge = person['John'];

// 모든 키값
Set<String> keys = person.keys;
```
<br/>

## 저장된 값 하나씩 출력
```dart
// entries.forEach 사용
mapName.entries.forEach((element) {
print('Key: ${element.key}, Value: ${element.value}');
})
```

