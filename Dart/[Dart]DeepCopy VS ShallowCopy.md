> ### Deep Copy
다트에서 객체를 복사하는 두 가지 방법
+ 얕은 복사(Shallow Copy)
+ 깊은 복사(Deep Copy)


Dart의 깊은 복사는 객체의 내부에 포함된 모든 객체를 `재귀적`으로 복사하여 `새로운 객체`를 생성한다. 이는 객체의 모든 데이터를 완전히 복사하여 새로운 객체를 생성하기 때문에 객체의 `불변성`을 보장하고 객체를 안전하게 다룰 수 있게 해준다.

> 일반적인 DeepCopy 사용 상황
1. 객체를 변경할 때 원본 객체를 `보존`하고 싶을 때
2. 객체를 다른 곳에 전달하거나 공유할 때 원본 객체를 `보존`하고 싶을 때
3. 다른 스레드에서 `안전`하게 객체를 사용할 때

![](https://velog.velcdn.com/images/hee462/post/d018390e-7570-46f3-aebd-d4667ed69061/image.png)
![](https://velog.velcdn.com/images/hee462/post/f5976ba9-e348-4af9-b320-13d115188781/image.png)
![](https://velog.velcdn.com/images/hee462/post/c79ff0c6-0869-4d91-baee-6bbdddc9cd94/image.png)<br>
_주소값 비교)_<br>![](https://velog.velcdn.com/images/hee462/post/f0f7beb0-138d-4edd-8e17-e6d9875c341b/image.png)

> ####  ⭐️한장정리
깊은복사는 쌍둥이처럼 생각하면 편할것 같다!
![](https://velog.velcdn.com/images/hee462/post/018cda7e-a815-4ecd-b5cc-215262efe38f/image.png)



