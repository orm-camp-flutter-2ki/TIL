# 📖 VSC 오류
<br>

![image](https://github.com/hwangtaewook/TIL/assets/87569211/13748981-7198-4093-85fe-dfeee435afe7)

- 카스퍼스키에서 java를 트로이목마로 인식 빌드가 되지 않음

- 자바21 업그레이드 gradle 수준이 맞지 않음 gradle-warpper.properties에서 8.6으로 변환

- 그래도 해결되지 않음

- 자바 17로 다운그레이드


![스크린샷 2024-03-05 100516](https://github.com/hwangtaewook/TIL/assets/87569211/fc739804-81f0-4b1e-9b1b-5f0dd499b3c6)


- 인터넷 서칭 후 해결방법 발견

- C:\Users\heops\AppData\Roaming\Code\User\workspaceStorage 에 가서 폴더를 통째로 날려버린다.
- 안되면 C:\Users\heops\AppData\Roaming\Code\CachedData 이것도 날려 버린다.

- 해결 완료

출처 https://kogle.tistory.com/237

