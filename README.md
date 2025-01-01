# Frontend

<details>

<summary><strong>debounce &#x26; throttle에 대한 설명</strong></summary>

**debounce**와 **throttle**은 이벤트 핸들러 너무 자주 실행되지 않도록 조절하는 기법이다.&#x20;

debounce는 이벤트가 연속적으로 발생할 때, 마지막 이벤트가 발생한 후 일정 시간이 지나야 이벤트 핸들러가 실행되는 방식이다.

Searchbar에서 사용자가 키를 입력할 때마다 검색 요청을 보내면 부하가 지나치게 커지기 때문에, 사용자가 입력을 멈춘 후 일정 시간이 지나면 검색 요청을 보내는 방식으로 디바운스를 적용할 수 있다.&#x20;

throttle은 일정 시간 간격 동안 발생한 이벤트 중 첫 번째 또는 마지막 이벤트만 처리하는 방식이다. 이벤트가 계속해서 발생하더라도 설정된 시간 동안 한 번만 이벤트 핸들러가 실행된다.&#x20;



무한 스크롤은 스크롤이 하단에 위치하게 된 순간 즉시 추가 데이터 요청을 수행하므로, 사용자에게 더 자연스러운 스크롤 경험을 제공할 수 있기 때문에 throttle을 사용하는 것이 더 적합하다.

</details>

***
