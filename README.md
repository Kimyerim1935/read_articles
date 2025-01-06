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
<details>
<summary><strong>reflow와 repaint의 차이점은?</strong></summary>

`reflow`는 브라우저가 페이지의 레이아웃을 다시 계산하는 과정을 말한다. 

DOM의 구조가 변경되거나 CSS 스타일이 변경되면, 브라우저는 각 요소가 화면에 어떻게 배치될지 다시 계산해야 한다. 이 과정은 모든 자식 요소와 관련된 부모 요소까지 영향을 주기 때문에 비용이 많이 드는 작업이다. 

예를 들어, CSS에서 요소의 width나 height 속성을 변경하면, 브라우저는 해당 요소뿐만 아니라 연관된 모든 요소의 배치를 다시 계산해야 한다.

반면에, `repaint`는 요소의 모양이나 스타일이 변경될 때 발생한다. 요소의 레이아웃은 그대로이고, 색상이나 배경 등의 스타일만 변경되는 경우를 말합니다. 

`background-color` 같은 속성을 예로 들면, 브라우저는 요소의 모양만 다시 그리면 되기 때문에 `reflow`보다는 비용이 덜 들지만, 여전히 성능에 영향을 줄 수 있다.

`reflow`는 레이아웃을 다시 계산하는 과정이고, `repaint`는 그 계산 결과를 화면에 다시 그리는 과정이다. 이 둘을 잘 이해하고 관리한다면 성능 최적화에 큰 도움이 됩니다.

1. reflow를 유발하는 CSS 속성 사용을 최소화: width, height, margin, padding, border 등의 속성은 요소의 레이아웃을 다시 계산하게 하므로 reflow를 일으킵니다. 가능한 한 미리 CSS에서 스타일을 설정해 초기 로드 시에만 계산이 이루어지도록 하고, 이후에는 가능한 변경을 지양한다.

2. CSS 애니메이션 최적화: 애니메이션에 transform과 opacity 속성만을 사용하는 것이 성능에 유리하다. 이 두 속성은 GPU 가속을 사용할 수 있어 reflow를 일으키지 않고 repaint만 발생시키므로 CPU 자원을 적게 사용한다.

3. `will-change`: CSS의 `will-change` 속성을 사용하여 브라우저에 특정 요소가 변경될 것이라고 미리 알려줄 수 있다. 예를 들어, `will-change: transform`으로 미리 GPU에서 요소를 준비하게 하여 `reflow` 및 `repaint`에 미치는 영향을 줄일 수 있다. 하지만 `will-change` 속성은 너무 자주 사용하면 메모리 낭비가 발생하므로 필요한 요소에만 적용해야 한다.
</details>

<h2>React</h2>

<details>

<summary><strong>React에서 index를 key 값으로 사용하면 안되는 이유?</strong></summary>

배열의 요소들이 추가되거나 삭제될 때, 배열의 순서가 바뀌는 경우 문제가 발생할 수 있기 때문이다.

리액트는 key를 통해 리스트에서 어떤 요소가 변경, 추가, 삭제되었는지 추적하며, index를 key로 사용하면 배열의 순서가 변경될 때 리액트가 요소들을 잘못 인식할 수 있기 때문이다. 리액트는 이를 새로운 요소로 인식해 불필요하게 재렌더링을 하거나, 요소의 상태를 잘못 처리할 수 있다.

따라서 데이터의 유일성을 보장하고 변하지 않는 값을 사용해야하며, 데이터베이스에서 제공하는 고유 ID를 사용하는 것이 일반적이다.

</details>

<details>
<summary><strong>useEffect와 useLayoutEffect의 차이점은?</strong></summary>

`useEffect`와 `useLayout` 모두 렌더링 후에 특정 작업을 수행하기 위해 사용되지만 실행되는 타이밍과 용도가 다르다.

`useEffect`는 렌더링이 완료되는 시점에 비동기적으로 실행된다. 화면이 실제로 사용자에게 그려진 후에 `useEffect`가 실행되는 방식이다. 보통 데이터를 가져오는 작업이나 이벤트 리스너 추가 등 렌더링 후에 화면에 직접적인 영향을 주지 않는 작업에 주로 사용된다.

`useLayoutEffect`는 렌더링 후 DOM이 업데이트 되기 직전 시점에 동기적(화면에 내용이 그려지기 전에 모든 레이아웃 관련 작업이 완료됨)으로 실행된다. DOM의 크기를 측정하거나 위치를 조정해야할 때 `useLayoutEffect`를 사용하면 즉각적으로 그 변경사항이 반영되어 화면 깜빡임이나 불필요한 재렌더링을 방지할 수 있다.

렌더링 후 실행되는 비동기 작업에는 `useEffect`가 적합하고 레이아웃 작업이나 DOM 조작과 같이 화면에 그려지기 전에 완료되어야 하는 작업에는 `useLayoutEffect`가 적합하다.

`useLayoutEffect`는 동기적으로 실행되기 때문에 너무 많은 작업이 실행되면 렌더링이 느려질 수 있다. 보통은 `useEffect`를 사용하고 화면에 영향을 주는 작업만 `useLayoutEffect`로 처리하는 것이 좋다.
</details>