## 자료구조 Collection

### 데이터 구조에 따른 대표적인 컬렉션
1) List : 순서대로 쌓여있는 구조. 아이템의 중복 허용
2) Map : 키(key)와 값(value)의 쌍으로 저장 (키의 중복 불가).순서를 보장하지 않음.
3) Set : 순서가 없는 집합 (중복 불가).속도가 빠름

#### List의 탐색 방법
```
for반복문,for-in,forEach()
```
#### Map의 탐색 방법
```
for-in,forEach()
```
#### Set의 탐색 방법
```
반복이 필요하면 Iterator를 사용하거나 forEach()를 사용
```
<br/>

#### 컬렉션 선택
- key, value 쌍 : Map
- 중복 가능 : List
- 중복 불가 : Set
- 순서 중요 : List
- 순서 안 중요 : Set
- 검색 속도 중요 : Set
