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

```

import 'dart:io';
   /**
   * 문제
   *    숫자를 입력받아서 구구단을 출력한다.
   *    // 숫자를 입력하세요. 
   *     3입력시 아래와 같이 출력한다.
   *    // 3, 6, 9, 12, 15, 18, 21, 24, 27 
   * 
   **/

 
void main(){
    print('숫자를 입력하세요.');
    // Reading name of the Geek
    int num = int.parse(stdin.readLineSync()!); // null safety in name string
 
    print(solution(num));

}
solution(num){
    String result = '';
 
    for ( int j = 1; j < 10; j++){
        if(j != 1){
            result +=', ';
        }
        result += (num*j).toString();
    }

    return result;
}

```

```
List<String> results = List.generate(9, (index) => ((index + 1) * setNumber).toString()); print(results.join(', '));
```

비만도 계산기
```
 
import 'dart:io';
 
void main()
{
    // 숫자를 입력받아서 구구단을 출력한다.
    //숫자를 입력하세요.
    
    // 3입력시 아래와 같이 출력한다.
    // 3, 6, 9, 12, 15, 18, 21, 24, 27
    print('나이를 입력하세요.');
    // Reading name of the Geek
    int age = int.parse(stdin.readLineSync()!); // 
 
     print('성별을 입력하세요.');
    // Reading name of the Geek
    String? sex = stdin.readLineSync();// null safety in name string
 
     print('키를 입력하세요.');
    // Reading name of the Geek
    double height = double.parse(stdin.readLineSync()!); // 
    print('몸무게를 입력하세요.');
    // Reading name of the Geek
    double weight = double.parse(stdin.readLineSync()!); // 
    
    solution(height, weight);

}
solution(height, weight){
    double bmi = weight / (height*height) * 10000;
    print(bmi);
    print(bmi.toStringAsFixed(2));
        
    String category;
    if (bmi < 18.5){
        category = '저체중';
    } else if (bmi < 23) {
        category = '정상';
    } else if (bmi < 25) {
        category = '과체중';
    } else {
        category = '비만';
    }
    switch (category) {
        case '정상':
            print('당신은 정상입니다.');
            break;
        case '과체중':
            print('당신은 과체중입니다.');
            break;
        case '비만':
            print('당신은 비만입니다.');
            break;
        case '저체중':
            print('당신은 저체중입니다.');
            break;
        default:
            print('BMI 수치가 유효하지 않습니다.');
            break;
        }
}
```