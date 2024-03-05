#### 수의 비교

```void main() {
  print(solution(10, 20));
  print(solution(3, 3));
}
  solution (a, b){
    String result = 'eq';
    
    if(a > b) {
      result = a.toString();    
    }else if(a < b) result = b.toString();
    
    return result;
  }
```
#### 문자열 결합  

```
void main() {
  int n1 = 2;
  int n2 = 5;
  List<String> s1 = ['Java', 'Gino'];
  List<String> s2 = ['Alice', 'Bob', 'Carol', 'Dave', 'Ellen'];
  print(solution(n2, s2));
}

solution(n, s) {
  String result = 'Hello';
  for (int i = 0; i < n; i++) {
    result += ' ';
    result += s[i];
    if (i != n - 1) {
      result += ',';
    }
  }
  result += '.';
  return result;
}
```

#### 등차수열

```
void main() {
 
  print(solution(3,3));
  print(solution(5,10));
  print(solution(1,3));
}

solution(int m, int n) {
  int num = m;
  List<String> result = ['$m'];

  for (int i = 0; i < 9; i++) {    
    num += n;
    result.add(num.toString());
  }
  
  return result;
}
```

#### 부족한 카드

```
void main() {
  List<int> input1 = [1, 3, 2, 5];
  List<int> input2 = [4, 3, 2, 1];
  print(solution(input1));
  print(solution(input2));
}

solution(cards) {
  int sum = 0;
  int result = 0;
  for (int card in cards) {
    sum += card;
  }
  result = 15 - sum;
  return result;
}
```
#### 숫자 판별
```
// 4자리 한정
void main() {
  int n1 = 4444;
  int n2 = 3335;  

  print(solution(n1));
  print(solution(n2));
}

solution(n) {
  int num = n%10;
  if(n/num == 1111){
    return n;
  }else{
    return 'No';
  }
}
// 4자리 한정 아닐 때
void main() {
  int n1 = 4444;
  int n2 = 3335;
  int n3 = 555559;
  int n4 = 77777777;

  print(solution(n1));
  print(solution(n2));
  print(solution(n3));
  print(solution(n4));
}

solution(n) {
  String nums = n.toString();
  int sum = 0;
  int num = n%10;
  for (int i = 0; i < nums.length; i++) {
    sum += int.parse(nums[i]);
  }  
 
  if (sum % num == 0) {
    return n;
  } else {
    return 'No';
  }
}
```

#### 태풍의 간격

```
void main() {
  List<int> day1 = [5, 8, 19, 25, 31];
  List<int> day2 = [2, 3, 7, 9, 28];
  print(solution(day1));
  print(solution(day2));
}

solution(day) {
  int num = 0;
  List<int> gan = [];
  for (int i = 0; i<(day.length-1); i++){
    num = day[i+1]-day[i];   
    gan.add(num);
  }
  return gan;
}

```

#### 빼빼로 파티

```
void main() {
  String ppae1 = '11111111111';
  String ppae2 = '1111';
  String ppae3 = '1111111111111111111';
  
  print(solution(ppae1));
  print(solution(ppae2));
  print(solution(ppae3));
}

solution(ppae) {
  int length = ppae.length;
  String result = 'OK';

  if(length < 11){
    result = (11 - length).toString();
  }
  return result;
}
```

#### 카드 정렬

```
void main() {
  List<int> nums1 = [2, 9, 3, 8];
  List<int> nums2 = [7, 8, 7, 7];
  
  print(solution(nums1));
  print(solution(nums2));

}

solution(nums) {
  int result = 0;
  int temp = 0;
  for(int i = 0; i < 3; i+=2){
    if (nums[i] < nums[i+1]){
      temp = nums[i+1];
      nums[i+1] = nums[i];
      nums[i] = temp;
    }
  }
  result = 10 * (nums[0]+nums[2]) + nums[1] + nums[3] as int;
  return result;
}
 
```
