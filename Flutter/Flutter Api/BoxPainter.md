# BoxPainter (absract)
[공식문서](https://api.flutter.dev/flutter/painting/BoxPainter-class.html) 

특정 Decoration을 paint할 수 있는 stateful한 클래스

Boxpainter 객체는 resource를 캐싱하여 resource를 재사용할 수 있다.

BoxPainter에의해 사용되는 몇몇 resource들은 비동기적으로 로드된다. 로드가 완료되면, onChanged 콜백이 실행된다. 호출부에서 이 콜백을 멈추기 위해서는 painter의 discarded가 호출된 이후에 dispose를 호출하면 된다.

>dispose(): 객체가 들고있는 resource들을 폐기(해제)한다.  
> => dispose가 호출되고 나면, onChanged 콜백은 더 이상 실행되지 않는다.
