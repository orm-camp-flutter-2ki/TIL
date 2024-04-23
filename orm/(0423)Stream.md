## Stream
실시간으로 생성되고 전송되는 데이터의 흐름
실시간 분석, 예측, 알림, 감시, 로깅, 모니터링 등에 활용

## Stream 활용 방법
* StreamBuilder
* 구독/해지


* 하나의 listener를 두 번이상 시도하려고 하면 에러 발생
* => 이럴땐 broadcast 사용

### StreamBuilder
* FutureBuilder와 Future 조합과 비슷
* Stream을 위젯으로 표현하는 위젯
* Future는 단발성이라면 Streamd은 지속적인 변화에 따라 화면을 갱신한다.

### 구독과 해지
* Stream 데이터를 UI로 변환할 필요가 없는 경우에 활용
* listen()으로 구독, cancel()로 해지

