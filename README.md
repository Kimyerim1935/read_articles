# Frontend 

<details>

<summary><strong>debounce &#x26; throttle에 대한 설명</strong></summary>

**debounce**와 **throttle**은 이벤트 핸들러 너무 자주 실행되지 않도록 조절하는 기법이다.&#x20;

debounce는 이벤트가 연속적으로 발생할 때, 마지막 이벤트가 발생한 후 일정 시간이 지나야 이벤트 핸들러가 실행되는 방식이다.

Searchbar에서 사용자가 키를 입력할 때마다 검색 요청을 보내면 부하가 지나치게 커지기 때문에, 사용자가 입력을 멈춘 후 일정 시간이 지나면 검색 요청을 보내는 방식으로 디바운스를 적용할 수 있다.&#x20;

throttle은 일정 시간 간격 동안 발생한 이벤트 중 첫 번째 또는 마지막 이벤트만 처리하는 방식이다. 이벤트가 계속해서 발생하더라도 설정된 시간 동안 한 번만 이벤트 핸들러가 실행된다.&#x20;

무한 스크롤은 스크롤이 하단에 위치하게 된 순간 즉시 추가 데이터 요청을 수행하므로, 사용자에게 더 자연스러운 스크롤 경험을 제공할 수 있기 때문에 throttle을 사용하는 것이 더 적합하다.

</details>

<details>

<summary>React에서 index를 key 값으로 사용하면 안되는 이유?</summary>

배열의 요소들이 추가되거나 삭제될 때, 배열의 순서가 바뀌는 경우 문제가 발생할 수 있기 때문이다.

리액트는 key를 통해 리스트에서 어떤 요소가 변경, 추가, 삭제되었는지 추적하며, index를 key로 사용하면 배열의 순서가 변경될 때 리액트가 요소들을 잘못 인식할 수 있기 때문이다. 리액트는 이를 새로운 요소로 인식해 불필요하게 재렌더링을 하거나, 요소의 상태를 잘못 처리할 수 있다.

따라서 데이터의 유일성을 보장하고 변하지 않는 값을 사용해야하며, 데이터베이스에서 제공하는 고유 ID를 사용하는 것이 일반적이다.

</details>

<details>

<summary><strong>인터프리터 언어인 자바스크립트에서 어떻게 호이스팅이 가능할까?</strong></summary>

자바스크립트에서 호이스팅이 가능한 이유는 자바스크립트 엔진이 코드를 실행하기 전에 컴파일 단계와 실행 단계를 거치기 때문이다.

컴파일 단계에서 함수 및 변수 선언을 한 부분이 메모리에 할당되며 undefined로 초기화된다. 이후 실행 단계에서 코드가 진행되면서 실제 할당된 값이 대입된다.
실행 단계란 실제 코드가 실행되는 과정으로, 컴파일 단계에서 메모리에 할당된 변수와 함수가 실행된다. 여기서 변수가 할당된 값을 가지게 되고, 함수가 호출되면 그 안의 코드가 수행된다.

</details>

<details>
<summary><strong>클로저란?</strong></summary>

클로저는 함수가 선언될 때의 스코프를 기억하여, 함수가 생성된 이후에도 그 스코프에 접근할 수 있는 기능을 말한다.

클로저는 자바스크립트의 함수가 일급 객체라는 특성과 렉시컬 스코프의 조합으로 만들어진다. 

```
function outerFunction(outerVariable) {
  return function innerFunction(innerVariable) {
    console.log('Outer Variable: ' + outerVariable);
    console.log('Inner Variable: ' + innerVariable);
  };
}

const newFunction = outerFunction('outside');
newFunction('inside'); 
```

`innerFunction`은 `outerFunction`의 내부에 정의되어 있다. `innerFunction`은 자신이 생성된 스코프(`outerFunction`의 스코프)를 기억하고 `outerFunction`의 호출이 완료된 이후에도 그 스코프에 접근할 수 있다.
이것이 클로저가 동작하는 방식이다.

클로저는 다음과 같은 상황에서 활용할 수 있다.

1. 외부에서 접근할 수 없는 비공개 변수와 함수를 만들 수 있으므로 데이터를 은닉하여 외부 접근을 막고 무결성을 유지할 수 있다.
2. 비동기 작업에서 이전의 실행 컨텍스트를 유지해야 할 때 유용하다. 콜백 함수가 비동기적으로 실행될 때, 클로저를 사용하면 함수 실행 시점의 변수를 참조할 수 있다.

```
function createLogger(name) {
  return function() {
    console.log(`Logger: ${name}`);
  };
}

const logger = createLogger('MyApp');
setTimeout(logger, 1000); // 1초 후에 'Logger: MyApp' 출력
```

3. 모듈 패턴은 특정 기능을 캡슐화하고, 외부에 공개하고자 하는 부분만 선택적으로 노출하여 코드의 응집력을 높이고, 유지보수성을 향상시키는 패턴이다.
클로저를 활용하면 필요한 함수와 데이터만 외부로 노출함으로써 모듈 패턴을 쉽게 구현할 수 있다.

</details>