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
<details>
<summary><strong>웹접근성의 개념과 개선 방법은?</strong></summary>

웹 접근성은 장애인과 고령자 등 신체적 제약이 있는 사용자를 포함해, 모든 사용자가 웹 페이지를 동등하게 이용할 수 있도록 보장하는 개념이다. 네트워크 속도가 느리거나 밝은 햇빛 아래 화면을 보는 등 일상적인 제약 상황에서도, 모든 사용자가 제약 없이 웹을 사용할 수 있도록 하는 것이 웹 접근성의 궁극적인 목표이다.

웹 접근성 개선에는 다양한 방법이 있다.
1. 단순하고 명확한 구조의 HTML과 시맨틱 태그
: 시맨틱 태그는 웹 페이지의 구조와 의미를 명확하게 전달해 스크린 리더가 컨텐츠를 쉽게 이해하도록 도와준다,

2. ARIA 속성을 활용하여 스크린 리더가 동적 컨텐츠나 복잡한 UI 요소를 올바르게 인식할 수 있게 만들 수 있음

3. 키보드로도 페이지를 탐색할 수 있도록 포커스를 명확히 지정하여 키보드 사용자가 필요한 정보에 접근하기 쉽게 해야함

</details>
<details>
<summary><strong>SSR이란?</strong></summary>

SSR이란 서버에서 완성된 정적 HTML을 클라이언트에 내려주는 방식이다. 클라이언트 측에서는 해당 HTML을 파싱하여 화면을 그리게 된다.

반면, CSR 방식은 브라우저가 서버로부터 비어있는 HTML을 받아온 후, 필요한 자바스크립트 번들을 다운로드 하고 번들을 실행하여 동적으로 컨텐츠를 채우는 방식이다.

SSR은 다음과 같은 장점을 가지고 있다.
: 화면이 동적으로 그려지는 CSR에 비해 크롤러가 컨텐츠를 쉽게 인식하고, 초기 로드가 상대적으로 빨라 우선순위가 부여되어 상위에 노출될 가능성이 높아지기 때문에 SEO 측면에서 유리하다.
블로그나 커머스 등 SEO가 중요한 웹 애플리케이션에 적합하다.
뿐만 아니라, CSR과 달리 SSR에서는 번들을 다운로드 받거나 번들을 실행하여 동적으로 화면을 그려낼 필요가 없기 때문에 사용자가 빠른 초기 로딩 속도를 경험할 수 있다.

하지만 SSR은 이러한 한계점이 존재한다.
전통적인 SSR 방식은 클라이언트 사이드 라우팅이 불가능하기 때문에 빠르고 매끄러운 페이지 전환 경험을 제공하기 어렵다.
또한, 단순히 정적인 리소스를 내려주는 것이 아니라, 요청 시마다 페이지를 동적으로 구성해서 내려주어야 하는 경우에는 서버 비용이 증가할 수 있다는 단점이 있다.
</details>
<details>
<summary><strong>실행 컨텍스트란?</strong></summary>
실행 컨텍스트는 자스립트에서 코드가 실행되는 환경을 의미한다. 
자바스크립트 엔진이 코드를 실행할 때, 그 코드가 실행될 때의 환경을 정의하고, 관리하기 위해 존재한다.

실행 컨텍스트는 전역 실행 컨텍스트와 함수 실행 컨텍스트로 나눌 수 있다.

전역 실행 컨텍스트는 자바스크립트가 처음 실행될 때 생성되는 컨텍스트이다. 이 전역 컨텍스트는 프로그램이 종료될 때까지 유지되며, 전역에 선언된 변수나 함수가 모두 포함된다.
전역 컨텍스트에서 선언된 변수와 함수는 프로그램 내 어디서든 접근이 가능하다.

기본적으로 자바스크립트는 싱글 스레드이기 떄문에, 전역 실행 컨텍스트는 1개만 존재한다.

함수 실행 컨텍스트는 함수가 호출될 때마다 생성되는 컨텍스트를 의미한다. 각 함수는 자신만의 실행 컨텍스트를 가지며, 이 컨테스트 내에서 선언된 변수와 함수는 해당 함수 내에서만 유효하다.
함수가 종료되면 해당 함수의 컨텍스트도 함께 사라진다.

실행 컨텍스트는 `변수 객체`, `스코프 체인`, `this`로 이루어져 있다.

1. 변수 객체
: 실행 컨텍스트 내에서 사용되는 변수와 함수 선언을 저장하는 공간이다. 전역 컨텍스트에서는 전역 객체가 변수 객체의 역할을 하고, 함수 컨텍스트에서는 활성화 객체가 변수와 매개변수를 관리한다.
2. 스코프 체인
: 현재 실행 중인 컨텍스트와 외부 렉시컬 환경의 연결을 유지한다. 변수를 참조할 때 현재 컨텍스트에서 찾지 못하면 외부 환경으로 범위를 넓혀가며 변수를 찾는다.
3. this
: this는 실행 컨텍스트에 따라 참조하는 객체가 달라진다. 전역 컨텍스트에서는 this가 전역 객체를 가리키며, 함수 컨테스트에서는 함수 호출 방법에 따라 달라진다.

실행 컨텍스트는 이러한 구성요소를 바탕으로 자바스크립트가 실행되는 동안의 환경을 관리하고, 코드 실행 시 변수의 유효 범위나 함수 호출의 맥락을 결정짓는다.
</details>
<details>
<summary><strong>이미지 크기가 클 경우 렌더링 속도가 느려질 텐데, 이를 개선하기 위한 방법이 있다면?</strong></summary>

1. 이미지 포맷 최적화: 전통적인 JPEG나 PNG 대신, WebP 또는 AVIF와 같은 최신 포맷으로 변환할 수 있다. 해당 포맷들은 이미지 품질을 유지하면서도 파일 크기를 크게 줄여준다. 하지만 일부 구버전의 브라우저에서는 최신 이미지 포맷을 지원하지 않으므로 호환성을 고려할 필요가 있다. WebP나 AVIF의 호환성 문제에 대비하기 위해 HTML의 <picture> 요소를 통해 fallback 이미지를 적용할 수 있다. <picture> 요소 내부에 WebP나 AVIF와 같은 고효율 포맷을 우선 설정하고, 브라우저가 이를 지원하지 않을 경우 JPEG나 PNG와 같은 기본 포맷을 로드하도록 할 수 있다.

2. 이미지 사이즈 조정: 화면에 노출되는 크기에 비해 이미지가 과도하게 큰 경우 이미지를 작게 리사이징할 수 있다. 필요한 크기에 맞게 잘라 서버에서 내려줄 수 있으며 다양한 디바이스 해상도에 대응하기 위해 Responsive Images 기술 srcset과 sizes 속성을 활용할 수 있다.
: srcset과 sizes 속성을 활용할 수 있다. 이 경우, 브라우저가 현재 화면 크기에 최적화된 이미지를 선택하여 로드할 수 있다.

3. 지연 로딩: 사용자가 화면에 스크롤할 때 해당 위치가 도달하는 이미지가 로드되도록 설정하는 방법. 지연 로딩을 통해 초기 로딩 속도를 개선할 수 있다. HTML loading="lazy" 속성을 통해 구현할 수 있으며, 이를 통해 불필요한 이미지의 로드를 방지할 수 있다.

4. CDN(Content Delivery Network): CDN을 적용하면 사용자가 지리적으로 가까운 서버에서 이미지를 다운로드하게 되어 로딩 속도를 단축 시킬 수 있다.

</details>

<details>
<summary><strong>낙관적 업데이트란?</strong></summary>
  
낙관적 업데이트는 성공적인 상태 업데이트가 이뤄질거라는 가정 하에 서버 응답 이전에 UI를 미리 업데이트하는 방법이다. 사용자 요청을 서버가 성공적으로 처리할 거라고 미리 예상하고, UI를 즉각적으로 변경해서 사용자에게 빠른 반응을 보여준다.

낙관적 업데이트의 대표적인 예시는 좋아요 기능이다. 사용자가 좋아요 버튼을 클릭하면 서버 응답을 기다리지 않고, 화면에 바로 좋아요 클릭에 대한 상태를 보여주는 것이다. 서버 응답이 성공적으로 돌아오면 그대로 두고, 실패하면 UI에서 해당 좋아요 상태를 해제하거나, 오류 메시지를 보여주는 방식이다.

낙관적 업데이트의 장점은, 서버 응답 속도와 관계 없이 즉각적인 피드백을 제공해서 사용자들이 시스템을 빠르게 쓸 수 있다는 점이다. 
네트워크 상태가 좋지 않거나 응답 시간이 길어도 사용자 경험에는 영향을 덜 미치게 된다.
하지만, 서버에서 오류가 발생하면 잠시동안 화면에 잘못된 정보가 표시될 수 있기 때문에 이 경우를 대비하여 오류 핸들링 로직을 같이설계해야 한다는 주의점이 있다.

낙관적 업데이트는 요청이 성공할 가능성이 높고, 사용자 경험을 즉시 개선하는 데 큰 장점이 있을 때 사용하는 것이 적합하다.
결제나 거래 내역과 같이 중요한 데이터를 다루는 경우에는 낙관적 업데이트가 오히려 사용자 경험을 저해할 수 있다.

낙관적 업데이트를 적용했을 때, 요청에 실패한다면 민감도 높은 정보가 순간적으로 잘못 표시되면서 사용자 경험을 크게 저해할 수 있기 때문이다.

또한 네트워크 환경이 불안정한 경우에, 요청에 대한 실패율이 높아질 수 있으며 이로 인해 잦은 롤백이 발생할 수 있다. 이 경우에도 사용자 경험을 저해할 수 있기 때문에 서버 응답을 기다리는 것이 더 나은 판단일 수 있다.
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

## State
<details>
<summary><strong>tanstack-query에서 stale time과 gc time의 차이점은?</strong></summary>

`tanstack-query`에서 `staleTime`과 `gcTime`은 데이터를 캐싱하고 관리하는 데 중요한 두 가지 설정 값이다. 

staleTime은 데이터를 처음 가져온 후에 그 데이터를 신선한 상태로 간주하는 시간을 말한다. `staleTime` 내에는 같은 쿼리에 대한 새로운 네트워크 요청이 일어나지 않고, 캐시 데이터를 그대로 사용하게 된다.
`staleTime`을 5분으로 설정하면, 데이터를 가져오고 나서 5분 동안은 이 데이터가 신선하다고 판단해서 쿼리 호출 시 추가 네트워크 요청 없이 캐시 데이터를 계속 사용한다.
`staleTime`이 지난 후 해당 쿼리를 호출한다면 새로운 요청을 보내 데이터를 갱신하게 된다. `staleTime`의 기본 값은 0이다.

`gcTime`은 해당 쿼리가 더이상 사용되지 않을 때, 캐시 데이터가 메모리에 얼마나 더 남아 있을지 정하는 시간이다.
`staleTime`이 지나면 데이터는 오래된 상태가 되지만, 여전히 캐시된 데이터는 사용이 가능하다. 이 캐시 데이터는 새로운 요청을 보내 신선한 데이터를 받아오기 이전에 임시로 기존 데이터를 표시하는데 활용된다.
하지만, 해당 쿼리가 사용되지 않게 된 시점으로부터 `gcTime`으로 설정된 시간이 지나면 캐시에서 데이터가 삭제된다. `gcTime`의 기본 시간은 5분이다.

요약하자면, `staleTime`은 데이터를 처음 가져온 후 얼마동안 네트워크 요청 없이 캐시된 데이터를 사용할 지 정하는 시간이고, `gcTime`은 해당 쿼리가 사용되지 않게 된 후에도 캐시에 유지될 시간을 정하는 것이다.
이렇게 각각의 설정을 통해 데이터를 더 효율적으로 관리하고, 불필요한 네트워크 요청을 줄이면서도 최신 데이터를 가져올 수 있도록 할 수 있다.

</details>

## CSS

<details>
<summary><strong>CSS Flexbox와 Grid의 차이
</strong></summary>

`Flexbox`와 `Grid` 모두 화면 요소를 배치하고 정렬하는 데 사용된다.

하지만 다음과 같은 차이점을 가지고 있다.
- `Flexbox`는 1차원 레이아웃 속성으로 row 또는 cloumn 중 하나를 기준으로 요소를 정렬하고 배치하는 데 최적화되어 있다.
주로 행이나 열 중 하나의 방향으로 정렬해야 할 때 유용하며, 복잡한 행과 열을 모두 포함하는 레이아웃에서는 다소 한계가 있다.

- `Grid`는 2차원 레이아웃 속성으로, 행과 열을 모두 사용해 요소를 배치할 수 있다. 따라서 복잡한 레이아웃을 구성하거나, 웹페이지의 전체적인 구조를 잡는 데 적합하다.

기본 동작에 대한 차이는 다음과 같다.

- `Flexbox`에서는 주로 요소가 컨테이너의 크기나 위치에 맞춰 자동으로 정렬된다. Flexbox의 `justify-content`,`align-items` 속성을 사용해, 주 축 방향으로 요소들을 배치하고 여백을 조절할 수 있다.
- `Grid`는 행과 열을 사전에 정의하고 그 격자에 요소를 배치하는 방식이다. `grid-template-rows`, `grid-template-columns`와 같은 속성으로 행과 열의 크기를 정의하고, 각 요소의 위치를 세밀하게 설정할 수 있다.

사용 목적의 차이는 다음과 같다.

- `Flexbox`는 컨텐츠 중심으로, 컨텐츠가 추가되거나 줄어들 때 유연하게 대처하기 좋다. 버튼 그룹, 내비게이션 바 등 한 줄의 컨텐츠가 주가 되는 구성에 적합하다.
- `Grid`는 레이아웃 중심으로 페이지 구조를 구성하는 데 최적화되어 있다. 카드 레이아웃, 갤러리 형식 등 명확하게 구분된 영역을 기반으로 레이아웃을 구성할 때 `Grid`가 효과적이다.

</details>

## Test

<details><summary><strong>E2E 테스트란?</strong></summary>

프론트엔드에서 E2E 테스트는 애플리케이션의 사용자 경험을 처음부터 끝까지 시뮬레이션하여 테스트하는 방식이다.
단위 테스트나 통합 테스트와 달리, E2E 테스트는 사용자 관점에서 전체 애플리케이션이 의도한 대로 작동하는지 검증한다.
브라우저 환경에서 실제 사용자 동작을 흉내내어 다양한 시나리오를 테스트 하며, 버튼 클릭, 페이지 이동, 데이터 입력 등을 포함한다.

E2E 테스트를 진행하면 사용자와 동일한 방식으로 애플리케이션을 테스트하므로, 사용자에게 직접적인 영향을 미치는 오류를 조기에 발견할 수 있다. 
: E2E 테스트는 중요한 사용자 흐름이나 비즈니스 로직이 포함된 페이지에 적용하면 효과적이다.

유닛 테스트로도 충분히 안정성을 높일 수 있지 않을까?

유닛 테스트는 개별적인 코드 조각이 제대로 작동하는지 확인하지만, 전체 시스템의 흐름과 사용자가 실제로 겪는 경험을 확인 하지 않는다.

반면, E2E테스트는 애플리케이션을 사용자 관점에서 처음부터 끝까지 검사하여, 모든 시스템이 통합적으로 잘 작동하는지 확인한다. UI 상호작용, API 호출, 화면 전환 등 여러 구성 요소가 함께 작동하는
과정에서 발생할 수 있는 문제를 탐지할 수 있다. E2E 테스트를 통해 사용자가 실제로 겪게 될 시나리오를 점검함으로써, 전체 시스템 관점에서의 오류를 조기에 발견할 수 있다.

따라서 유닛 테스트와 E2E 테스트를 상호 보완적으로 함께 활용하는 것이 좋다. 유닛 테스트는 개별 컴포넌트를 신속하고 정확하게 검사하여 디버깅 시간을 줄이고, 코드의 작은 변화가 의도한 대로 작동하는지 확인한다.
E2E테스트는 애풀리케이션의 중요한 사용자 흐름을 점검하여 배포 후 발생할 수 있는 치명적인 문제를 예방한다.

두 테스트를 함께 활용하면 애플리케이션의 안정성과 신뢰성을 극대화 할 수 있다.
</details>
