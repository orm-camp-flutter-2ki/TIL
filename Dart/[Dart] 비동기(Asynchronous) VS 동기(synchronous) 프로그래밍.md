> 비동기식 프로그래밍(Asynchronous Programming):
- 작업들이 `동시에 실행`되거나, 한 작업의 완료를 기다리지 않고 다음 작업을 실행할 수 있습니다.<br>
- 작업 간의 의존성이 낮고, 한 작업이 완료될 때까지 다른 작업을 실행할 수 있습니다.<br>
ex) 네트워크 요청을 보내고 응답을 기다리는 동안에도 다른 작업을 수행가능<br>

> 동기식 프로그래밍(Synchronous Programming):<br>
- 작업들이 `순차적으로 실행`<br>
되며, 한 작업이 완료될 때까지 다음 작업이 실행되지 않습니다.<br>
- 작업 간의 의존성이 높고, 한 작업의 완료를 기다려야 다음 작업을 실행할 수 있습니다.<br>
ex)함수를 호출하고 반환값을 기다리는 동안 다른 작업을 수행 않음<br>

![](https://velog.velcdn.com/images/hee462/post/d07bc032-46f5-48ec-b3a4-6a0f26b95243/image.png)
 단계적으로 진행되는 동기식이 더 편해보이지만, <br>
 효율성은 비동기식이 더 좋음 <br>
 왜？ <br>
 작업이 완료될때까지 대기하지 않고 다른작업 수행 가능 <br>
 ex) 로딩중 화면 띄우기 , 선택한 값 가져오기 를 동시에 작업하여 <br>
 사용자에게 더 나은 경험 제공<br>
 또한 [병렬식 처리 ](https://velog.io/@hee462/Dart%EB%B3%91%EB%A0%AC%EC%8B%9D-%EA%B5%AC%EC%A1%B0)가능해서 시스템 확장 용이 하여
 전체적인 성능이 향상됨

비동기시 프로그램 처리방법<br>
- 콜백(Callbacks): 콜동기는 현재 코드의 `실행 결과를 받지 않고` 이후 코드를 수행하는 기법이다.<br>
컴퓨팅 자원을 효율적으로 사용하는 기법이지만 `정확한 순서`를 지켜 수행해야 하는지를 고려해야 한다.<br>
비동기 코드를 순서대로 실행하는 가장 일반적인 방안은 [콜백 지옥(callback hell)](https://www.google.com/search?sca_esv=cdc18846ebd0314a&rlz=1C5CHFA_enKR1063KR1063&sxsrf=ACQVn08NekmZ5K1k6DpusTkbmLO8uCy0GQ:1711022744098&q=%EC%BD%9C%EB%B0%B1%EC%A7%80%EC%98%A5&tbm=isch&source=lnms&prmd=ivsnbmz&sa=X&ved=2ahUKEwjn9_S2qIWFAxU9klYBHdmVBdoQ0pQJegQIERAB&biw=1366&bih=912&dpr=2#imgrc=syffojJwpvr5DM&imgdii=fSfipgiF6I9-iM)이라고 불리는 복잡성이 발생할 수 있습니다.<br>
_ex)<br>
음식을 주문하고 진동벨을 가지고 기다리면 음식이 준비되면 손님을 호출(Callback)하는 상황_

- `Future`를 사용할 때 `async/await`를 함께 사용하여 관리 <br>
이유는 코드를 더 읽기 쉽고 관리하기 쉽게 만들기 위해서입니다.<br>
이를 이해하기 위해 우선 두 가지 개념에 대해 알아야 합니다.<br>
Future: 비동기 작업의 결과를 나타내는 `객체`입니다.<br>
Future를 사용하면 비동기 작업이 완료되면 그 결과를 처리하거나 `반환`할 수 있습니다.<br>
async/await: async 키워드는 함수가 비동기적임을 나타내고, await 키워드는 비동기 작업의 완료를 기다립니다. <br>
이를 통해 비동기 코드를 동기식처럼 작성할 수 있습니다.<br>
_ex<br>
주문 처리 (Future) - 음식 준비 시간 (await) -결제 처리 (Future)_

> ⭐️ 사용법 TIP)<br>
Future를 사용할때 then() 사용가능하지만 지양함<br>
- 확실히 콜백 보다는 편하지만 동기식 코드 보다는 `결과 예측이 어렵다`.<br>
- 단계가 많아지면 then() 을 연결하는 체이닝 방식을 사용하는 것이 만만치 않다.<br>
- 로직이 복잡해 지면 적절한 예외처리하기에 용이하지 않다.<br>

> ⭐️한장정리![](https://velog.velcdn.com/images/hee462/post/a9d77192-415f-4349-8f49-c799cdc92014/image.png)




