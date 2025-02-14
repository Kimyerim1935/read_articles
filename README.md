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
<summary><strong>이미지 크기가 클 경우 렌더링 속도가 느려질 텐데, 이를 개선하기 위한 방법이 있다면?</strong></summary>

1. 이미지 포맷 최적화: 전통적인 JPEG나 PNG 대신, WebP 또는 AVIF와 같은 최신 포맷으로 변환할 수 있다. 해당 포맷들은 이미지 품질을 유지하면서도 파일 크기를 크게 줄여준다. 하지만 일부 구버전의 브라우저에서는 최신 이미지 포맷을 지원하지 않으므로 호환성을 고려할 필요가 있다. WebP나 AVIF의 호환성 문제에 대비하기 위해 HTML의 `<picture>` 요소를 통해 fallback 이미지를 적용할 수 있다.
`<picture>` 요소 내부에 WebP나 AVIF와 같은 고효율 포맷을 우선 설정하고, 브라우저가 이를 지원하지 않을 경우 JPEG나 PNG와 같은 기본 포맷을 로드하도록 할 수 있다.

2. 이미지 사이즈 조정: 화면에 노출되는 크기에 비해 이미지가 과도하게 큰 경우 이미지를 작게 리사이징할 수 있다. 필요한 크기에 맞게 잘라 서버에서 내려줄 수 있으며 다양한 디바이스 해상도에 대응하기 위해 Responsive Images 기술 `srcset`과 `sizes` 속성을 활용할 수 있다.
: `srcset`과 `sizes` 속성을 활용할 수 있다. 이 경우, 브라우저가 현재 화면 크기에 최적화된 이미지를 선택하여 로드할 수 있다.

3. 지연 로딩: 사용자가 화면에 스크롤할 때 해당 위치가 도달하는 이미지가 로드되도록 설정하는 방법. 지연 로딩을 통해 초기 로딩 속도를 개선할 수 있다. `HTML loading="lazy"` 속성을 통해 구현할 수 있으며, 이를 통해 불필요한 이미지의 로드를 방지할 수 있다.

4. CDN(Content Delivery Network): CDN을 적용하면 사용자가 지리적으로 가까운 서버에서 이미지를 다운로드하게 되어 로딩 속도를 단축 시킬 수 있다.

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
<details>
<summary><strong>자바스크립트는 싱글 스레드 언어인데, 어떻게 동시에 여러 작업들을 수행할까?</strong></summary>
자바스크립트는 한 번에 하나의 작업을 처리할 수 있는 단일 콜스택을 가지지만 브라우저나 node.js 환경이 제공하는 비동기 처리 메커니즘 덕분에 여러 작업을 동시에 수행할 수 있다.

자바스크립트는 브라우저의 Wev API나 libuv, 이벤트 루프, 태스크 큐를 이용하여 비동기 작업을 동시에 처리한다.
비동기 작업이 발생하면, 해당 작업은 브라우저의 Wev API에 위임된다.
예를 들어 `setTimeout`이나 `fetch`와 같은 작업이 수행되면 자바스크립트 엔진은 이 작업들을 Web API에 넘기고 다른 코드 실행을 이어간다. Web API에서 비동기 작업이 완료되면, 그 작업은 태스크 큐에 들어가 대기한다.

이후 이벤트 루프가 콜 스택이 비어있는지 확인한 뒤 태스크 큐에서 대기 중인 작업을 콜 스택으로 가져와 실행한다. 이러한 구조 덕분에 자바스크립트는 싱글 스레드임에도 비동기적으로 작업을 처리하여 다양한 작업을 효율적으로 관리할 수 있다. 해당 메커니즘 덕분에 UI 인터랙션이 끊기지 않으며, 대기 시간이 필요한 작업도 동시에 실행되는 것과 같이 동작하게 된다.

자바스크립트의 태스크 큐는 매크로태스크 큐와 마이크로태스크 큐로 나뉜다. 이런 큐는 비동기 작업의 우선순위를 관리하고, 이벤트 루프가 적절한 시점에 콜백을 실행하기 위해 사용된다.

1. 매크로태스크 큐는 일반적인 비동기 작업의 콜백이 저장되는 큐이다. `setTimeout`, `setInterval`, `I/O 작업`, 이벤트 핸들러 등은 작업 완료 후 매크로태스크 큐에 콜백을 대기시킨다. 매크로태스크 큐는 이벤트 루프의 한 번의 반복마다 하나의 태스크만 처리되므로, UI 업데이트나 다른 작업과 균형 있게 진행된다.

2. 마이크로태스크 큐는 더 높은 우선순위가 필요한 비동기 작업들이 대기하는 큐이다. `Promise.then`, `MutationObserver` 등의 비동기 콜백이 여기에 저장된다. 이벤트 루프는 매크로태스크를 실행하기 전에 항상 마이크로태스크 큐를 먼저 확인하고, 모든 마이크로태스크를 처리한 후 매크로태스크로 넘어간다. 이 방식으로 마이크로태스크 큐의 작업은 높은 우선순위로 처리된다.
</details>
<details>
<summary><strong>시맨틱 마크업이란 무엇이며, 왜 중요한가?</strong></summary>
시맨틱 마크업은 HTML 요소를 사용하는 방식으로, 단순히 시각적 목적이 아닌 요소의 의미를 잘 나타내도록 작성하는 방식을 말한다. 
`div`와 `span` 같은 비 시맨틱 태그가 아닌 `header,footer,article,section` 같은 시맨틱 태그를 사용하여 문서 구조와 컨텐츠의 역할을 명확하게 하는 것이다.

시맨틱 마크업이 중요한 이유는 다음과 같다.
1. 접근성을 개선하기 위함
: 시맨틱 요소들은 스크린 리더와 같은 접근성 도구에서 컨텐츠의 구조를 더욱 잘 해석할 수 있게 해주어 시각 장애인이나 노인 등 다양한 사용자 층이 사이트를 효과적으로 탐색할 수 있게 한다.
해당 요소를 올바르게 사용하면, 더 많은 사람들에게 접근 가능한 웹 환경을 제공할 수 있다.

2, SEO에 유리함
: 검색 엔진은 HTML의 시멘틱 구조를 통해 페이지 구성을 파악하기 때문에 시맨틱 마크업을 적절히 적용하면, 검색 엔진이 페이지를 올바르게 파악할 수 있고, 그에 따라 검색 결과에서 더 잘 노출될 가능성이 높아진다. 

따라서 시맨틱 마크업은 단순한 코드 작성 컨벤션을 넘어, 웹 접근성과 SEO를 위한 중요한 요소로 웹 개발에서 필수적인 요소이다.

그렇다면 CSR에서도 시맨틱 마크업이 SEO에 영향을 미칠까?

CSR 환경에서 대부분의 컨텐츠가 클라이언트에서 렌더링 되기 때문에 검색 엔진이 페이지를 크롤링 할 때 페이지의 초기 컨텐츠만 인식할 가능성이 크다. 하지만 최근 검색 엔진들은 javascript 렌더링을 지원하는 방향으로 진화하고 있으며, 페이지의 시맨틱 구조를 어느정도 파악할 수 있기 때문에 시맨틱 마크업을 제대로 적용하면 CSR에서도 검색 엔진이 컨텐츠의 중요한 부분을 더 쉽게 인식하게 되어 검색 결과에 긍정적인 영향을 미칠 수 있다.

</details>

<details>
<summary><strong>CommonJS와 ES Module의 차이점은?</strong></summary>
CommonJS와 ES Module(ESM) 은 자바스크립트에서 모듈을 관리하고 불러오는 두 가지 주요 방식이다.

먼저 CommonJS는 주로 Node.js 환경에서 사용되며, 모듈을 동기적으로 불러옵니다. 모듈이 로드될 때까지 다음 코드가 실행되지 않는 방식입니다. 

CommonJS는 require 키워드를 사용해 모듈을 가져오고, module.exports를 통해 내보낸다. 이 방식은 주로 서버측에서 사용 됐지만, 클라이언트 환경에서도 번들러를 통해 사용할 수 있다.

ES Module은 자바스크립트의 공식 표준 모듈 시스템으로, ECMAScript 2015(ES6)부터 도입되었다. ESM은 브라우저와 Node.js 환경에서 모두 사용할 수 있으며, 모듈을 비동기적으로 로드한다. 
모듈을 가져올 때는 import 키워드를 사용하고, 내보낼 때는 export를 사용한다. ESM은 정적 분석이 가능해, 트리 쉐이킹과 같은 최적화 작업에도 유리하다.

정리하자면, CommonJS는 주로 동기적이고 서버 측에서 많이 사용되며,ESM은 비동기적이고 브라우저와 서버 모두에서 사용할 수 있다는 차이점을 가지고 있다.

하지만 Node.js에서도 최근에는 ESM 사용이 증가하고 있는 추세이며, Node.js는 버전 12부터 네이티브로 ESM을 지원하기 시작했다. 
브라우저와 서버 간의 모듈 호환성을 위해 풀스택 애플리케이션 개발에서도 ESM이 많이 사용되고 있다. 특히 ESM은 비동기적 로딩과 트리 쉐이킹 같은 최적화 작업에 유리하다는 점에서 점점 더 선호되고 있다.
</details>

<details>
<summary><strong>자바스크립트 배열에 대해 설명하시오</strong></summary>
자바스크립트의 배열은 순서가 있는 리스트형 객체로, 여러 값을 하나의 자료구조에 저장할 수 있다.

배열은 제로 인덱스 기반으로, 배열의 각 값은 인덱스를 통해 접근할 수 있다. 배열 내부에는 다양한 데이터 타입을 함께 저장할 수 있다.

```javascript
const array = [1, 'apple', true, { key: 'value' }];
```

자바스크립트 배열의 중요한 특징 중 하나는 동적 배열이라는 점이다. 배열의 크기를 미리 지정하지 않아도 요소를 추가할 때마다 배열의 크기가 자동으로 조정된다는 특징이 있다.
요소를 추가하거나 특정 인덱스에 값을 할당하면 배열은 자동으로 확장된다.

자바스크립트의 length 속성은 배열의 크기를 나타내며, 배열에 요소가 추가되거나 제거될 때 자동으로 변경된다.

배열은 자바스크립트의 객체와 유사한 방식으로 관리되며, 해시 테이블과 같은 자료구조로 구현되어 있다. 
이로 인해 배열 요소들은 메모리 상에서 연속적이지 않아도 되며 배열의 크기를 미리 지정하지 않고도 유연하게 사용 가능하다는 특징이 있다.

</details>
<details>
<summary><strong>undefined와 null의 차이점</strong></summary>
`undefined`와 `null` 둘 다 값이 없다는 의미를 갖고 있지만, 이러한 차이점을 가지고 있다.

`undefined`는 자바스크립트에서 자동으로 할당되는 값이다.
변수는 선언했지만, 아직 아무 값도 할당하지 않았을 때, 자바스크립트는 해당 변수에 `undefined`라는 값을 자동으로 할당한다.

반면에 `null`은 개발자가 의도적으로 할당하는 값으로 특정 변수에 값이 없음을 명확하게 표현하기 위해 `null`을 할당할 수 잇다.

==에서는 `null`과 `undefined`가 동일하다고 처리되지만 ===에서는 다르게 취겁된다.

메모리 관련 차이점은 다음과 같다.
`null`은 개발자가 명시적으로 메모리를 해제하고자 할 때 사용하는 방법이다. 객체를 참조하던 변수를 `null`로 설정하면, 해당 변수는 더이상 그 객체를 가리키지 않으므로 참조가 끊어진다. 참조가 끊기면 javascript의 가비지컬렉터는 해당 객체가 더이상 사용되지 않는다고 판단하여 메모리에서 제거할 수 있다.

`undefined`는 자바스크립트 엔진이 자동으로 할당하는 값으로, 메모리 해제와 직접적인 관련은 없다. 변수가 `undefined` 상태라고 해서 가비지 컬렉션 대상이 되는 것은 아니며, 이 값 자체가 메모리 해제를 유도하는 것은 아니다. `undefined`는 값이 정의되지 않음을 나타낼 뿐이며 변수 값이 `undefined`라고 해서 자바스크립트가 해당 변수를 메모리 해제 대상으로 인식하지는 않는다.
</details>
<details>
<summary><strong>Javascript ES6에 대하여</strong></summary>

ES6는 자바스크립트의 최신 버전으로 코드의 가독성과 유지보수셩을 높이고 현대 웹 애플리케이션의 요구를 반영하기 위한 여러 기능들을 제공한다.

다음과 같은 변경사항들이 있다.

1. let과 const 키워드의 추가: let은 변수 선언, const는 상수 선언에 사용된다. var과 달리 let과 const는 블록 스코프를 가지므로 코드의 안정성이 더 높다. 또한 변수 선언 이전에 접근했을 때 undefined가 할당되징 낳고, ReferenceError가 발생한다는 점에서도 차이가 있다.

2. 화살표 함수의 도입: 기존 함수의 정의 방식보다 간결하고 가독성이 좋다. this의 바인딩을 호출 문맥과 일치시키기 때문에 함수 내부에서의 혼란이 줄었다.

3. class 문법의 추가: 객체 지향 프로그래밍의 핵심 개념인 생성자, 상속, 메서드 오버라이딩 등을 자바스크립트에서 활용할 수 있게 되었다.

4. 템플릿 리터럴의 추가: 문자열 내에 변수를 쉽게 삽입할 수 있어 기존의 문자열 연결 방식보다 가독성과 유연성이 향상되었다.

이외에도 구조 분해 할당, Spread Operator과 Rest Parameter, Promise 등 중요한 기능들이 추가되었다.
</details>

<details>
<summary><strong>함수 선언식과 함수 표현식의 차이점</strong></summary>
함수 선언식과 함수 표현식은 자바스크립트에서 함수를 정의하는 방법으로 다음과 같은 차이졈을 갖고 있다.

- 함수 선언식은 이름이 있는 함수이다. 자바스크리븥 엔진이 코드를 실행하기 전에 메모리에 로드하기 때문에 호이스팅이 발생한다.<br/>
=> 함수 선언식으로 정의된 함수는 코드 내 어디서든 호출이 가능하다.

```javascript
console.log(add(2, 3)); // 5

function add(a, b) {
    return a + b;
}
```
`add` 함수는 선언된 위치보다 앞에서 호출해도 정상 작동한다. 자바스크립트 엔진이 실행 전에 함수 선언을 미리 메모리에 로드했기 때문이다.

- 함수 표현식은 변수에 익명 함수를 할당하는 방식으로, 할당된 변수명으로 호출할 수 있다.<br/>
함수 표현식은 호이스팅이 되지 않으며, 변수에 할당된 이후에만 호출할 수 있다. 코드의 흐름 상 변수가 선언된 후에만 해당 함수를 사용할 수 있다.

```javascript
console.log(multiply(2, 3)); // not defined 에러 발생

const multiply = function (a, b) {
    return a * b;
};
```

함수 선언식은 호이스팅이 되어 코드의 어디서든 호출이 가능하지만, 함수 표현식은 변수에 할당된 후에만 사용 가능하다.

</details>

<details>
<summary><strong>자바스크립트 이벤트 루프란?</strong></summary>

자바스크립트의 이벤트 루프는 자바스크립트가 싱글 스레드 기반 언어임에도 불구하고 비동기 작업을 처리할 수 있게 해주는 중요한 메커니즘이다.

자바스크립트는 기본적으로 한 번에 한 가지의 작업만 수행할 수 있다. 하지만 이벤트 루프가 콜 스택과 태스크 큐를 관리하면서 비동기 작업이 완료되면 그 결과를 처리할 수 있게 도와준다.
콜 스택은 현재 실행 중인 코드가 쌓이는 곳이고, 태스크 큐는 비동기 작업이 완료되면 그 결과를 대기시키는 곳이다.

자바스크립트에서 `setTimeout(callback, 0)`을 호출하면, 이 콜백 함수는 바로 실행되는 것이 아니라 웹 API에 의해 타이머가 설정되고, 그 타이머가 0밀리초 후에 만료되면 콜백 함수가 태스크 큐에 추가된다. 그 후 콜스택이 비어있는 시점에 이벤트 루프가 태스크 큐에서 대기 중인 callback을 꺼내서 실행한다.

따라서 `setTimeout(callback, 0)`을 호출해도 현재 실행 중인 모든 동기 작업들이 완료된 후에야 그 콜백이 실행된다. 
</details>
<details>
<summary><strong>Promise의 resolve와 fulfilled에 대하여</strong></summary>

resolve는 Promise를 완료시키는 함수이고, fulfilled는 해당 Promise가 완료된 상태를 뜻한다.

resolve는 Promise가 성공적으로 끝났을 때 결과 값을 넘겨주는 함수이다.

어떤 비동기 작업이 잘 끝났을 때, resolve를 호출해서 '이 작업이 끝났고 결과는 이렇게 나왔다' 라고 전달하게 된다. 이렇게 resolve가 호출되면, Promise의 상태는
fulfilled로 바뀌게 된다.

resolve는 Promise를 성공적으로 마무리 짓는 행위라고 볼 수 있고, fulfilled는 그 결과로 발생하는 완료된 상태를 의미한다.

만약 비동기 작업에 오류나 실패가 발생하면 reject가 호출되어 reject 상태가 된다. 
then은 resolve 된 값을 처리하고 catch는 reject된 오류를 처리하는 식으로 Promise의 결과를 다루게 된다.
</details>

<details>
<summary><strong>인터넷 창에 www.google.com을 입력하면 일어나는 일은?</strong></summary>

1. DNS 조회: 사용자가 www.google.com을 입력하면 브라우저는 도메인 주소를 IP 주소로 변환(DNS 조회)한다. 브라우저는 캐시된 DNS 기록을 먼저 확인하고, 없으면 로컬 DNS 서버에 요청하여 해당 IP 주소를 얻는다. 
2. TCP 연결 수립: IP 주소가 확인되면, 브라우저는 서버와 TCP 연결을 수립한다. TCP는 데이터를 신뢰성 있게 전달하기 위한 프로토콜이다. 이 과정에서 브라우저는 서버와 3-way-handshake를 수행한다.<br/>
브라우저가 SYN 패킷을 보내고, 서버가 SYN-ACK 패킷을 보내며, 다시 브라우저가 ACK 패킷을 보내는 과정이다.
3. HTTP 요청:  TCP 연결이 수립되면, 브라우저는 HTTP/HTTPS 요청을 보낸다. 만약 HTTPS 를 사용할 경우, SSL/TLS 핸드셰이트도 수행한다. 이 과정에서 브라우저와 서버가 암호화된 연결을 설정하기 위한 보안 인증서를 교환하고, 암호화 키를 협상한다.
4. 서버의 응답: 서버는 요청을 받고 해당 리소스(HTML, CSS, Javascript)를 브라우저에게 응답으로 보낸다.
5. 브라우저 렌더링: 받은 리소스를 바탕으로 브라우저 렌더링 파이프라인을 진행한다. DOM과 CSSOM을 생성하고, 렌더 트리를 구성한 뒤, 레이아웃과 페인트 단계를 통해 웹 페이지가 화면에 표시된다.

</details>
<details>
<summary><strong>javascript Promise에 대한 설명</strong></summary>
자바스크립트는 비동기처리를 위한 콜백 함수를 많이 사용한다. 하지만 콜백 함수는 코드가 복잡해짐에 따라 중첩되는 콜백 지옥 문제를 야기할 수 있다. Promise는 이러한 비동기 처리의 가독성을 높이고, 코드의 흐름을 명확하게 관리하도록 도와주는 방식이다.

Promise는 다음과 같은 상태를 가진다.

1. Pending(비동기 작업이 아직 완료되징 않은 초기 상태)
2. Fulfilled(비동기 작업이 성공적으로 완료되어 값을 반환한 상태)
3. Rejected(비동기 작업이 실패하여 오류를 반환한 상태)

세 가지 상태 중 하나로 전환되면, 이후에는 다른 상태로 전환되지 않으며, `Fulfilled`나 `Rejected`상태가 되면 결과값을 통해 해당 작업의 성공 여부를 알 수 있다.

Promise 객체는 비동기 작업을 수행할 함수를 인자로 받아서 실행하며, 해당 함수는 resolve와 reject라는 두 가지 콜백을 받는다.

resolve는 비동기 작업이 성공했을 때 값을 전달하여 Promise를 fulfilled 상태로 전환하고, reject는 비동기 작업이 실패했을 때 오류를 전달하여 Promise를 Rejected 상태로 전환한다.

또한 try-catch-finally의 구조로 비동기 작업의 실패와 에러, 또 마지막 부분에 대한 처리를 명시적으로 나타내줄 수 있다.

Promise는 코드의 가독성을 높이고, 비동기 작업의 흐름을 제어하는 데 매우 유용하다. 여러 개의 Promise를 순차적으로 연결할 수도 있고, Promise.all이나 allSettled 같은 메서드를 통해 병렬로 비동기 작업을 처리해볼 수 있다.

하지만 다음과 같은 단점이 있다. 

1. 복잡한 에러처리: Promise는 단일 체인에서는 에러 처리가 간단하지만, 여러 Promise가 중첩되거나 서로 다른 비동기 흐름에서 에러가 발생할 경우 복잡도가 증가할 수 있다. 비동기 흐름에서 발생하는 다양한 에러를 모두 처리하려면 코드가 복잡해질 수 있다.

2. 콜백 지옥을 완전히 해결할 수 없음: Promis는 콜백 지옥 문제를 어느 정도 해결하지만, 비동기 작업이 복잡하게 중첩되면 여전히 콜백과 유사하게 여러 then 메서드가 연속해서 사용되며 가독성이 떨어질 수 있다. 여러 Promise를 순차적으로 실행해야 할 때 then 체인을 계속 사용하면 코드의 들여쓰기 구조가 복잡해지고 이해하기 어려워지는 문제점이 있다. 해당 문제점은 async/await를 통해 개선할 수 있다.
</details>
<details>
<summary><strong>이벤트 전파란?</strong><summary>

이벤트 전파는 DOM에서 이벤트가 발생했을 때, 그 이벤트가 어떤 방식으롷 전파되는지를 설명하는 개념이다.

이벤트 전파는 크게 세 단계로 나뉜다.

1. 캡처링: 이벤트가 DOM 트리의 최상위 요소에서 시작하여 이벤트가 발생한 요소로 향해 내려가는 단계로 상위 요소들에 이벤트 리스너가 있으면 그 순서대로 실행될 수 있다.
2. 타겟: 이벤트가 실제로 발생한 타겟 요소에 도달하는 단계로 타겟 요소에 등록된 이벤트 리스너가 이 시점에 실행된다.
3. 버블링: 타겟 요소에서 이벤트가 발생한 후, 다시 DOM 트리의 상위 요소들로 이벤트가 전파되어 올라가는 단계로, 이 과정에서 상위 요소들에 등록된 이벤트 리스너들이 실행될 수 있다.

기본적으로 대부분의 이벤트는 버블링을 통해 전파되지만, `addEventListnener()`의 세 번째 인자로 `{ capture: true }`를 전달하면, 캡처링 단계에서도 이벤트를 처리할 수 있다.

</details>
<details>
<summary><strong>localStorage와 sessionStorage의 차이점은?</strong><summary>

localStorage와 sessionStorage는 브라우저에서 제공하는 클라이언트 측 저장소 API로, 둘 다 데이터를 키-값 쌍 형태로 저장한다.

차이점은 데이터의 지속성과 범위이다.

localStorage는 데이터를 영구적으로 저장하여 브라우저를 닫거나 장치를 재부팅해도 데이터가 유지되며, 동일한 도메인 내의 모든 탭에서 데이터를 공유할 수 있다.

다크모드와 같은 테마 설정이나 장바구니 데이터와 같이 장기적으로 유지해야하는 데이터 저장에 적합하다.

sessionStorage는 데이터가 현재 브라우저 세션 동안만 유지되며, 브라우저 탭이나 창을 닫으면 데이터가 삭제된다. 같은 도메인이라도 탭 간에는 데이터를 공유하지 않는다.
로그인 후 인증 데이터를 일시적으로 저장하거나, 특정 탭에서만 사용할 데이터를 관리할 때 사용한다.

localStorage는 장기 데이터 저장에 유용하고, sessionStorage는 단기 데이터 저장에 적합하다.

localStorage와 sessionStorage를 사용했을 때 문제점은?

둘 다 보안 관점에서 주의가 필요하며 localStorage에 민감한 데이터를 저장하면 영구적으로 유지되므로 보안 위험이 크다.
sessionStorage에 데이터를 저장할 경우에도 보안적인 문제는 여전히 남아있다.

브라우저 저장소는 데이터를 암호화하거나 보호할 방법이 기본적으로 제공되지 않기 때문에 민감한 데이터를 직접 저장하지 않는 것이 가장 중요하다.

인증 토큰이나 사용자 비밀번호는 HTTP-Only 쿠키를 사용해야한다. 이렇게 하면 자바스크립트에서 접근할 수 없으므로 XSS 공격에 대한 위험을 줄일 수 있다.
</details>

<h2>Network</h2>

<details>
<summary><strong>CORS는 무엇이며 왜 필요할까?</strong><summary>

CORS는 서로 다른 출처(Origin)에서 제공되는 리소스에 접근할 수 있도록 허용하는 정책이다.

기본적으로 브라우저에는 보안 상의 이유로 동일 출처 정책이 적용되어 있다.

해당 리소스가 같은 출처에서 제공되는 것이 아니라면 브라우저가 이를 차단하도록 되어 있다. 다른 출처의 서버에 요청을 보낼 경우, 해당 요청에 대한 응답에 접근할 수 없도록 막는다.
이러한 정책은 보안을 강화하지만, 이로 인해 합법적인 요청까지 차단될 수 있다. 이런 상황을 해결하기 위해 CORS가 개발되었다.

CORS를 적용하는 방법은?

- 서버 측에서 `Access-Control-Allow-Origin` 헤더를 설정하면, 특정 출처에서의 접근을 허용할 수 있다. `Access-Contol-Allow-Origin: *`으로 모든 출처에 대해 허용하거나 특정 출처만 선택적으로 허용할 수 있다.
- `Access-Cotrol-Allow-Methods`와 `Access-Control-Allow-Headers` 헤더를 통해 HTTP 메서드나 특정 헤더를 허용할 수 있다.<br/>
이는 서버에서 수행되는 동작이다.

동일 출처 정책은 어떤 공격을 막기 위해 존재하는 것일까?

동일 출처 정책은 크로스사이트 요청 위조 공격의 위력을 낮추기 위해 존재한다.

CSRF 공격은 악성 웹사이트가 사용자의 요청을 도용하여, 의도치 않은 요청을 서버에 보내게 만드는 공격이다. 피해자가 공격자의 웹 사이트에 들어왔을 때, 해당 사용자의 요청인 것처럼
타 사이트에 GET 요청을 보내 사용자의 개인정보를 탈취할 수 있다. SOP는 악성 사이트에서 임의로 다른 출처의 서버로 요청을 보내거나, 응답에 접근하는 것을 막아, CSRF 공격의 효과를 줄여준다.
</details>
<details>
<summary><strong>Webpack, rollup과 같은 번들러가 필요한 이유는?</strong></summary>

번들러는 다양한 파일과 모듈을 하나의 배포 가능한 번들로 묶는 역할을 한다. 번들러가 필요한 주요 이유는 다음과 같다.

1. 네트워크 요청 성능을 개선하기 위해: 다수의 개별 파일에 대해 모두 네트워크 요청을 수행할 경우, 성능에 부정적인 영향이 있을 수 있다. 번들러는 다수의 파일을 하나 또는 소수의 파일로 묶어 네트워크 요청을 최적화함
2. 번들러는 트랜스파일링을 통해 더 효율적이고 호한성 있는 애플리케이션을 만드는데 기여한다: 트랜스파일링을 통해 코드를 최적화하고 `Dead Code Elimination`과 `Tree Shaking`과 같은 방법을 통해 사용되지 않는 코드와 불필요한 모듈을 제거해 번들 크기를 줄이고 로딩 성능을 개선한다.<br/>
번들러는 호환성을 높이기 위해 최신 Javascript 문법과 기능을 구형 브라우저에서도 실행 가능하도록 변환한다.
</details>
<details>
<summary><strong>브라우저 렌더링 파이프라인이란?</strong></summary>

브라우저가 웹 페이지를 화면에 표시하기 위해 거치는 과정을 브라우저 렌더링 파이프라인이라고 한다.

다음과 같은 단계로 나눌 수 있다.

1. DOM 생성: 브라우저가 HTML 파일을 받으면, 이 파일을 바이트 단위로 읽기 시작한다. 브라우저의 HTML 파서는 이 바이트들을 문자로 변환하고, 이 문자들을 다시 HTML 토큰으로 변환한다. 이 HTML 토큰들은 각각의 태그와 그 안에 포함된 텍스트, 속성 등을 의미하게 된다.<br/>
HTML 토큰이 생성되면, 브라우저는 이를 기반으로 DOM 트리를 생성한다. DOM 트리는 HTML 문서의 구조를 트리 형태로 표현한 것으로, 각 태그가 노드가 되어 부모-자식 관계를 형성한다.

2. CSSOM 생성: 브라우저는 CSS파일을 파싱한다. CSS 파일 역시 바이트로 전송되므로, 브라우저는 이를 문자로 변환한 뒤, CSS 규칙으로 나눈다. 각 CSS 규칙은 선택자(selector)와 선언(declaration)으로 구성되는데, 선택자는 스타일을 적용할 HTML 요소를 정의하고, 선언은 적용할 스타일을 정의한다.<br/>
브라우저는 이 CSS 규칙들을 기반으로 CSSOM 트리를 생성한다. CSSOM 트리는 DOM과 유사하게 트리 구조를 가지며, 각 노드는 해당 노드에 적용될 스타일 정보를 포함한다.

3. 렌더 트리 생성: 브라우저는 DOM과 CSSOM을 결합하여 렌더 트리를 생성한다. 렌더 트리는 화면에 실제로 표시될 요소들로만 구성된다. 렌더 트리의 각 노드는 DOM 트리의 요소와 연결되며, CSSOM 트리에서 해당 요소에 적용된 스타일 정보를 포함한다. 렌더 트리는 HTML 문서의 구조와 각 요소의 스타일 정보를 모두 포함한 트리이다.

4. 레이아웃: 렌더 트리가 생성된 후, 브라우저는 이 트리를 사용해 각 요소의 정확한 위치와 크기를 계산한다. 이 과정이 바로 레이아웃이다. 레이아웃 과정에서는 렌더 트리의 각 노드가 화면의 어디에 위치할 지, 그리고 얼마나 큰지를 계산하게 된다. 이 계산은 뷰포트 크기와 같은 정보에 의존하게 되며, 화면의 크기가 변경되면 브라우저는 레이아웃 과정을 다시 수행해야 한다.

5. 페인팅: 레이아웃이 완료되면, 브라우저는 각 요소를 실제로 화면에 그리는 작업을 시작한다. 이 과정을 페인팅이라고 하며, 텍스트, 색상, 그림자, 이미지 등 모든 시각적 요소가 화면에 그려진다. 복잡한 그래픽이나 애니메이션이 포함된 경우 페인트 작업이 많아져 성능이 저하될 수 있다.

6. 컴포지팅: 브라우저는 화면에 그려질 요소들을 각각의 레이어로 분리하고, 이 레이어들을 결합하여 최종 화면을 구성한다. 이 과정에서는 GPU를 활용하여 각 레이어를 빠르게 합성한다.

</details>
<details>
<summary><strong>HTTP란?</strong></summary>

HTTP는 웹 상에서 클라이언트와 서버 간 데이터를 주고 받는 데 사용되는 통신 규약으로, 클라이언트가 서버에 요청을 보내면 서버가 그 응답을 반환하는 방식으로 동작한다.
HTTP는 비연결성을 특징으로 하여 한 번의 요청-응답이 끝나면 연결이 종료된다. 그리고 통신이 안전하게 연결될 수 있도록 TCP 연결을 사용한다.

HTTP는 HTML, JSON 등을 비롯하여 다양한 데이터 포맷을 전달할 수 있다. 요청과 응답에는 URL 경로, 각종 메서드, 상태 코드와 헤더 등 정해진 몇 가지 정보를 포함한다.

HTTP의 보안을 강화한 버전인 HTTPSsms HTTP에 TLS/SSL 프로토콜에 따라 데이터를 암호화하여 전송한다. 이를 통해 보안 상 중요한 정보들을 안전하게 보호하여 통신을 주고 받는다.
</details>

## React

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
<details><summary><strong>useEffect가 호출되는 시점은?</strong></summary>

React의 useEffect는 컴포넌트의 특정 시점에 자동으로 호출되는 훅이다

컴포넌트가 

1. 마운트
2. 업데이트
3. 언마운트

되는 시점에 호출된다.

useEffect는 컴포넌트가 마운트될 때(처음 렌더링되고 나서) 호출된다. 이때 데이터 초기화나 외부 API 호출, 구독 설정 등의 작업을 실행할 수 있다. 이때 useEffect는 컴포넌트가 처음 마운트될 때 필요한 초기 작업을 수행할 수 있다.

useEffect는 의존성 배열에 지정된 값이 변경될 때마다 다시 호출된다. 두 번째 인자로 주어지는 의존성 배열은 useEffect가 어떤 상태나 props의 변화에 반응할지를 결정하는데, 예를 들어 

```javascript
useEffect(() => {...}, [count])
```

처럼 `count` 상태가 의존성 배열에 있을 경우, `count` 값이 변경될 때마다 useEffect가 호출된다. 

이를 통해 특정 상태나 props가 변경될 때마다 필요한 동작을 수행하도록 할 수 있으며, 컴포넌트의 변화에 따라 동적으로 실행되는 로직을 설정할 수 있다.
단, 의존성 배열을 넘기지 않을 경우에는 매 렌더링마다 호출된다.

마지막으로, 의존성 배열에 지정된 값이 변경될 때와, 컴포넌트가 언마운트될 때 useEffect의 return 값으로 지정된 클린업 함수가 호출된다. 

이 정리 함수를 이용하여 이벤트 리스너 제거, 타이머 해제, 구독 취소 등의 작업을 수행할 수 있다. 이를 통해 useEffect를 통해 발생한 부수효과를 정리하는 것이다.

useEffect는 컴포넌트가 처음 렌더링된 후, 의존성 배열의 값이 변경될 때, 그리고 컴포넌트가 언마운트될 때 호출된다.
</details>
<details>
<summary><strong>Error Boundary란?</strong></summary>
Error Boundary는 React 컴포넌트에서 발생하는 오류를 잡아내고, 전체 애플리케이션이 다운되는 것을 방지하기 위한 특수한 컴포넌트이다. 클라이언트에서 오류가 발생할 때 표시할 UI를 지공하여, 애플리케이션의 신뢰성과 사용자 경허을 높이는 데 활용된다.
클래스 형 컴포넌트의 `componentDidCatch`와 `getDerivedStateFromError` 두 가지 라이프 사이클 메서드를 사용하여 오류 발생 시의 행동을 정의할 수 있다.

`ErrorBoundary`는 클래스형 컴포넌트에서만 사용할 수 있다.

`ErrorBoundary`가 필요한 이유는?

React는 기본적으로 비동기 작업에서 발생하는 오류를 자동으로 처리하지 않으므로, 오류가 발생할 경우 페이지 전체가 하얗게 변하거나 사용자 입장에서 알 수 없는 화면이 표시되는 상황이 발생할 수 있다.
이는 사용자 경험을 크개 저해하고, 대규모 애플리케이션에서 신뢰성에 큰 문제가 된다. `ErrorBoundary`는 해당 문제를 해결하여 에러가 발생한 영역에서 대체 UI를 표시하고, 애플리케이션의 나머지 부분은 정상적으로 동작하도록 도와준다.

`ErrorBoundary`를 적절히 배치하면ㅡ 오류가 발생한 컴포넌트만 대체 UI로 전환되어 애플리케이션의 안정성을 유지하고, 사용자에게 오류 메시지나 대체 화면을 제공하여 더 나은 사용자 경험을 제공한다. 

더불어 `ErrorBoundary`는 오류 발생 시의 대체 UI 로직을 선언형으로 작성할 수 있게 하여 코드의 가독성과 유지 보수성을 높이는 데 도움이 된다.

선언형으로 처리하는 것의 의미와 유지 보수성에 왜 도움이 되는지?

선언형으로 처리한다는 의미는 개발자가 무엇을 해야하는지를 정의하는 방식으로, 어떻게 할지에 대한 세부적인 절차를 직접 작성하지 않아도 된다는 것을 뜻한다.

`ErrorBoundary`에서 이 컴포넌트가 오류를 감지하면 특정 대체 UI를 보여준다와 같은 목적을 코드 상에서 명시함으로써, 실제로 오류가 발생할 때 실행되는 세부적인 절차는 컴포넌트가 알아서 처리하게 된다.

유지 보수성에 도움이 되는 이유는, 선언형 코드가 명령형 코드에 비해 직관적이고 간결하여 가독성이 높기 때문이다.<br/>
`ErrorBoundary` 같은 경우에 특정 `ErrorBoundary`로 감싼 영역이 어떤 방식으로 에러를 처리할 지 한 눈에 알 수 있다. 뿐만 아니라 비즈니스 로직과 에러 처리 로직이 명확하게 분리되어 코드의 복잡성이 낮아진다.
</details>
<details>
<summary><strong>리액트의 strict mode란?</strong></summary>

리액트의 strict mode는 주로 개발 중에 발생할 수 있는 잠재적인 문제를 사전에 감지하고 예방하기 위해 사용된다. 

몇 가지의 주요 목적이 있다.

1. 오래된 라이프 사이클 메서드와 비권장 API 사용을 감지
: componentWillMount, componentWillReceiveProps와 같은 메서드들은 더이상 사용이 권장되지 않은데, 해당 메서드들이 코드에 포함된 경우 경고를 표시해준다.

2. 의도치 않은 부수 효과 방지
: 컴포너트의 렌더링이 예측 가능하고 순수하게 이루어지기를 기대한다. 

</details>

<details>
<summary><strong>리액트에서 성능 최적화를 위해 적용할 수 있는 방법들</strong></summary>

리액트에서 성능 최적화를 위해 여러 가지 방법을 사용할 수 있는데, 대표적으로 메모이제이션이 있다.

리액트의 memo를 사용하여 컴포넌트를 메모이제이션 할 수 있다. 컴포넌트의 props가 변경되지 않았을 때, 리렌더링을 방지하여 성능을 최적화하는 기법이다.
특히 렌더링 비용이 큰 컴포넌트에서 유용하다.

useCallback과 useMemo를 활용할 수도 있다.

useCallback은 함소를 메모이제이션하여 불필요한 함수 재생성을 방지하고, useMemo는 값의 재계산을 방지하여 성능을 최적화한다.

마지막으로 코드 스플리팅이 있다. 코드 스플리팅은 큰 애플리케이션을 여러 개의 작은 청크로 나누어, 필요한 청크만 로드하게 하여 초기 로드 시간을 줄인다.

React.lazy와 Suspense를 사용하여 컴포넌트를 동적으로 로드할 수 있다.

코드 스플리팅은 다음과 같은 경우에 사용해야 한다.

- 초기 로딩 시간이 길어지는 경우: 애플리케이션이 커지면, 초기 로딩에 모든 코드를 로드하는 것이 비효율적일 수 있기 때문에 스플리팅을 사용해 초기 로드 시 필요한 핵심 코드만 로드하고, 이후 추가적인 기능은 필요할 때 로드하도록 하면 초기 로딩 속도를 크게 개선할 수 있다.
- 라우트 별 코드 분할이 필요한 경우: SPA에서는 각 페이지가 별도의 기능과 UI를 가지므로, 라우트 별로 필요한 코드만 분리하여 로드할 수 있다. 이 방식은 React.lazy와 Suspense를 사용하여 라우트 별 컴포넌트를 동적으로 불러올 때 유용하다.

</details>
<details>
<summary><strong>리액트 동시성 모드란?</strong></summary>

리액트의 동시성 모드는 여러 작업을 비동기적으로 동시에 처리하면서도 중간에 더 중요한 작업이 들어오면 우선순위를 바꿔서 그 작업을 먼저 처리하는 기능을 의미한다.

예전 리액트는 스택 구조로 이루어져, 한 번 렌더링을 시작하면 끝까지 멈추지 않고 다 처리했어야 했다. 하지만 동시성 모드에서는 중간에 멈추거나 작업을 잠시 뒤로 미뤄둘 수 있어서 중요한 작업을 먼저 끝낼 수 있게 되었다.

이 동시성 기능을 활용하여 리액트는 중요한 작업과 덜 중요한 작업을 나눠서 덜 중요한 작업은 백그라운드에서 진행하고 중요한 부분은 바로 사용자에게 보여준다.

검색창에 뭔가 입력하고 있을 때, 그에 맞춰 검색 결과가 업데이트 되더라도, 리액트가 해당 작업을 백그라운드에서 처리하게 하여 화면이 느려지지 않게 할 수 있다.

동시성을 활용한 기능은?

- startTrascistion이란 기능을 사용하면 특정 상태 업데이트를 덜 중요한 작업으로 분류하여 사용자가 클릭하거나 입력하는 반응 같은 중요한 업데이트가 우선적으로 처리된다.

- useDeferredValue라는 훅을 사용하면 값의 업데이트를 잠시 지연시킬 수 있어, 사용자가 빠르게 입력할 때마다 리렌더링 되지 않게 최적화할 수 있다.

동시성 모드의 장점은 사용자와 상호작용하는 부분이 훨씬 매끄럽게 느껴진다는 것이다.

동시성이 필요한 부분은?

주로 사용자와의 상호작용이 빈번하고 응답성이 중요한 경우이다.

1. 검색 필터링이나 자동 완성 같은 기능: 사용자가 검색어를 입력할 때마다 결과가 업데이트 되는 경우, 모든 입력마다 화면이 리렌더링 된다면 앱이 느려지고 끊김이 생길 수 있다.
이 때 동시성 모드를 사용하면 검색어 입력 자체가 더 중요한 작업이 되어 검색 결과 업데이트는 백그라운드에서 처리되므로, 입력이 빠르고 부드럽게 유지된다

2. 무거운 데이터나 리스트를 로딩하는 경우: 스크롤 목록을 보면서 네트워크를 통해 데이터를 로딩할 때, 새로운 항목을 추가로 불러오는 작업보다 사용자가 현재 보고 있는 화면이 더 중요한 작업이다. 이럴 경우에 동시성을 사용하면 로딩은 백그라운드로 넘기고, 스크롤을 최우선으로 부드럽게 렌더링 할 수 있다.

3. 애니메이션이 포함된 화면 전환이나 중요도가 높은 사용자 입력 작업: 사용자가 버튼을 클릭했을 때, UI가 즉각적으로 반응하고, 이후에 비동기 작업이 처리되도록 설정해주면 클릭 시의 지연 없이 상호작용이 자연스러워진다.

</details>
<details>
<summary><strong>useEffect를 이용하여 로딩 상태를 관리하는 방법과 Suspense를 활용하는 방법에 대한 차이점</strong></summary>

기존 로딩 상태 관리 방식인 useEffect는 로딩 상태를 관리하는 방식에서 근본적인 차이가 있다. 기존 방식에서는 데이터를 불러올 때 useEffect() 훅을 사용하고, 로딩 상태를 관리하기 위해 isLoading이라는 별도의 상태 변수를 만들어야 한다. 조건에 따라 로딩 UI를 보여주는 식으로 작동한다. 이런 방식은 간단한 상황에서는 충분히 유효하지만, 여러 개의 비동기 데이터를 다룰 때에는 조건부 렌더링 로직이 복잡해질 수 있다.

Suspense는 로딩 중인 컴포넌트를 직접 렌더링하지 않고, Suspense 컴포넌트의 fallback 속성으로 로딩 UI를 정의하게끔 한다. 데이터를 기다리는 동안에는 fallback으로 정의된 UI만 보여주고, 데이터가 모두 준비되면 Suspense에 감싸진 컴포넌트를 자연스럽게 표시한다. 이렇게 선언적으로 고나리할 수 있기 때문에 전체 코드가 단순해지고 유지 보수도 쉬워진다.

Suspense의 단점은 무엇일까?
여러 개의 Suspense 컴포넌트를 중첩하거나 트리 구조로 사용할 경우, 각 Suspense가 독립적으로 로딩 상태를 관리하기 때문에 데이터 준비 시점이 다를 수 있다. 그 결과 로딩 화면이 여러 번 표시되거나 비일관적인 UI 경험이 발생할 수 있기 때문에 트리의 구조와 데이터 로딩 흐름을 신정하게 설계해야 한다.

또한 Suspense는 Promise 기반의 비동기 작업만 지원하기 때문에 fetch 요청에 바로 적용할 수 있는 것이 아니라, 이를 위해 추가적인 라이브러리를 사용하거나 Suspense와 호환되는 형태로 Promise를 관리해야 한다.

</details>
<details>
<summary><strong>리액트의 render phase와 commit phase에 대해서 설명하시오</strong></summary>

render phase는 리액트가 변화된 상태나 props에 따라 어떤 UI가 변경되어야 할지를 결정하는 단계이다. 이 과정에서는 실제로 DOM을 업데이트 하지 않고, 변경사항을 가상 DOM에서 계산하여 비교한다. 이 단계는 순수하게 계산하는 과정이기 때문에 성능에 영향을 주지 않도록 중단되거나 다시 실행될 수 있으며, Concurrent Mode를 통해 비동기적으로 처리될 수도 있다.

commit phase는 실제로 변환된 UI를 DOM에 반영하는 단계이다. 가상 DOM에서 계산된 결과를 실제 DOM에 적용하고, 변화된 UI를 브라우저에 렌더링한다. DOM 업데이트 이후에는 useEffect와 같은 사이드 이펙트를 발생시키는 훅들이 실행된다.

render phase와 commit phase가 동기화될 때의 특징은?

1. 단계적 진행: render phase가 완료되면 리액트는 commit phase를 실행하지 않고, 다른 높은 우선순위 작업이 있다면 먼저 처리한 후 나중에 commit phase를 실행할 수 있다. React는 동기화가 필요한 작업을 효율적으로 관리하여 사용자 경험을 개선한다.
2. 병목 관리: render phase에서 모든 변경 사항이 Fiber Tree에 준비된 상태에서 commit phase로 넘어가므로, Render와 commit단계의 일관성이 유지된다. 이 두 단계는 순차적으로 작동하여 UI가 정확하게 동기화되고 불필요한 재렌더링을 방지한다.

</details>
<details>
<summary><strong>react의 props와 state의 차이점?</strong></summary>

`props`는 부모 컴포넌트가 자식 컴포넌트에 전달하는 데이터로 읽기 전용이다. 자식 컴포넌트는 props를 수정할 수 없다.
이를 통해 컴포넌트 간의 데이터 흐름을 예측 가능하게 만들고, 컴포넌트의 재사용성을 높인다.

`state`는 컴포넌트 내부에서 관리되는 데이터로, state는 동적으로 변경될 수 있으며, 컴포넌트 렌더링에 영향을 미친다. state를 변경하면 컴포넌트는 다시 렌더링되며, UI가 업데이트 된다. state는 주로 사용자 입력이나 네트워크 요청의 응답에 따라 변하는 데이터를 관리할 때 사용된다.

props가 자식 컴포넌트에서 변하지 않는 이유는 리액트의 단방향 데이터 흐름 원칙 떄문이다. 리액트는 부모 컴포넌트가 자식 컴포넌트에게 데이터를 전달할 때 단방향으로 전달하도록 설계되었다. <br/>
이렇게 하면 컴포넌트 간의 데이터 흐름을 예측 가능하고 일관성 있게 만들 수 있어 애플리케이션 상태 관리가 간단해진다.

props는 읽기 전용이기 때문에 부모 컴포넌트에서 전달된 값이 자식 컴포넌트 내에서 임의로 변경되지 않는다. 특정 상태가 어디서 어떻게 변경되었는지 예측할 수 있어 버그 발생 가능성을 줄이고 디버깅을 쉽게 한다는 장점이 있다.
</details>
<details>
<summary><strong>리액트에서 컴포넌트란?</strong></summary>

리액트에서 컴포넌트는 UI를 구성하는 독립적이고 재사용 가능한 코드조각이라고 설명할 수 있다. 컴포넌트는 특정 기능이나 UI 요소를 캡슐화한다. 잘 만들어진 컴포넌트는 주로 단일 책임 원칙을 따른다.

리액트에서 컴포넌트는 클래스형과 함수형으로 나누는데 최근 Hooks의 도입으로 함수형 컴포넌트가 주로 사용되고 있다. 함수형 컴포넌트는 더 간결하고 이해하기 쉬운 코드를 작성할 수 있게 해준다. 컴포넌트의 주요 장점은 유지보수성과 재사용성이다.

컴포넌트를 설계할 때 다음과 같은 사항을 고려해야 한다.

1. 하나의 컴포넌트가 너무 많은 책임을 갖지 않도록 해야 한다. 컴포넌트의 역할이 명확하도록 설계해야한다. 비즈니스 로직과 UI로직을 철저히 분리하는 것을 예시로 들 수 있다.

2. 재사용성을 고려해야 한다. 특정 컴포넌트가 여러 상황에서 재사용될 가능성이 높다면 유연하게 설계해야 추후 재사용이 용이하다. props를 통해 필요한 데이터와 동작을 주입받아 다양한 상황에서 쉽게 재사용될 수 있도록 하는 것이 좋다.

3. 성능 최적화를 고려해야 한다. 불필요한 리렌더링을 방지하기 위해 메모이제이션을 적절히 활용하고, 컴포넌트 크기를 적절히 유지해야 하는 것이 좋다.
</details>

<details>
<summary><strong>서버컴포넌트란?</strong></summary>

서버 컴포넌트는 리액트 18버전에서 도입된 새로운 기능으로, 기본적으로 클라이언트에서 실행되는 기존의 리액트 컴포넌트와 다르게 서버에서만 렌더링되는 컴포넌트를 말한다. 서버에서만 실행되기 떄문에 브라우저 쪽 번들 크기를 줄이고, 초기 로딩 속도를 개선하는 데 큰 장점이 있다.

서버 컴포넌트는 데이터 베이스 연결 정보나 API 키와 같은 민감한 정보를 클라이언트로 보내지 않아도 되는 구조라서 안전하게 데이터를 다룰 수 있다.

리액트에서는 서버 컴포넌트를 클라이언트 컴포넌트와 함께 사용할 수 있도록 설계하였다. 클라이언트 컴포넌트는 인터렉션이 필요한 UI를 담당하고, 서버 컴포넌트는 데이터 중심의 UI를 담당하는 식으로 역할을 분리할 수 있다.

서버 컴포넌트는 성능 최적화와 보안 개선, 개발자 경험 측면에서 많은 이점을 가져다 줄 수 있는 기능으로 정리할 수 있다.

서버컴포넌트의 단점은 다음과 같다.

1. 서버 의존성 증가: 서버 컴포넌트는 이름 그대로 서버에서 실행되기 때문에 서버가 반드시 필요하다. 정적 사이트나 서버리스 환경에서 작업하려는 경우에는 사용할 수 없거나 제약이 있을 수 있다.
2. 사용자 경험과 인터렉션 문제: 서버 컾모넌트는 클라이언트 컴포넌트와 결합해서 사용해야 하는데, 이 과정에서 복잡한 사용자 인터랙션을 처리하기 어렵다. 서버 컴포넌트는 정적인 데이터나 렌더링에 적합하기 때문에 클라이언트 쪽에 인터렉션이 필요한 경우에는 한계가 있을 수 있다.
</details>

<details>
<summary><strong>Streaming SSR이란?</strong></summary>

Streaming SSR은 서버에서 렌더링된 HTML을 한 번에 완성해서 보내는 방식이 아니라 준비된 부분부터 점진적으로 스트리밍해서 클라이언트에 전달하는 기술이다.

기존 SSR은 서버에서 모든 데이터를 처리한 뒤 완전한 HTML을 전송하는 반면, Streaming SSR은 서버가 데이터를 준비하는 즉시 HTML 조각을 스트림 형태로 보내고, 클라이언트는 이를 실시간으로 렌더링한다. React 18에서는 renderToPipeableStream API를 통해 구현할 수 있으며, 이 API는 서버에서 HTML을 조각 단위로 스트리밍할 수 있도록 지원한다.

이 방식의 가장 큰 장점은 초기 로딩 시간을 단축할 수 있다는 점이다. HTML의 일부라도 준비되는 즉시 클라이언트가 렌더링을 시작하므로 TTFB가 개선된다. 데이터가 많거나 복잡한 대규모 애플리케이션에서 효과적이며, 사용자가 중요한 컨텐츠를 먼저 확인할 수 있어 전반적인 사용자 경험도 향상된다.
하지만 클라이언트에서 부분적으로 전송된 HTML을 제대로 Hydration할 수 있도록 설계가 필요하며, SEO나 캐싱 정책과의 호환성도 신중히 고려해야 한다.

이러한 특징과 장점을 통해 Streaming SSR은 기존 SSR의 한계를 극복하며 더욱 빠르고 효율적인 웹 페이지 렌더링을 가능하게 한다.
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

<details>
<summary><strong>tanstack-query를 사용하는 이유는?</strong></summary>

Tanstack Query는 서버 상태 관리의 복잡성을 극복하기 위해 사용하는 라이브러리이다.

서버 상태란 서버에서 제공하는 데이터로, 클라이언트에서 직접 수정할 수 없고 네트워크 요청과 같은 비동기 작업을 통해 가져오거나 갱신해야 하는 데이터를 의미한다.

Tanstack Query를 사용하는 주요 이유는 다음과 같다.

1. 효율적인 캐싱 처리 기능: 동일한 데이터를 반복적으로 요청하지 않아 네트워크 비용을 절감하고 캐싱된 데이터를 즉시 제공해 더 나은 사용자 경험 제공
2. 비동기 데이터 관리의 복잡성 줄이기: 데이터 fetch, refetch, invalidate 등의 작업을 선언적으로 처리할 수 있어  코드가 간결해지고 유지보수가 용이해짐
3. 에러 및 로딩 상태 단순화: `useQuery()`와 `useMutation()` 훅을 사용하면 서버 데이터와 관련된 로딩, 성공, 실패 상태를 명확하고 직관적으로 처리할 수 있어 로직이 깔끔해짐


Tanstack Query의 한계점은?

Tanstack Query은 서버 상태 관리를 간편하게 해주지만, 사용 시 몇 가지 단점 및 한계가 있다.

1. 캐싱 전략 관리의 복잡성: 강력한 캐싱 기능을 제공하지만, stale time, gcTime과 같은 옵션을 잘못 설정할 경우, 데이터 갱신 타이밍이 적절하지 않아 최신 데이터가 사용자에게 노출되지 않거나 불필요한 요청이 발생할 수 있음
2. 초기 학습 곡선: Query Key 설계, 데이터 무효화 등 다양한 개념을 이해하고 적절히 활용해야 하므로 초기에 학습해야 하는 지식의 양이 많음
3. 별도의 라이브러리 필요 가능성: 클라이언트 상태와 서버 상태 간 의존 관계가 복잡한 경우 별도의 상태 관리 라이브러리가 필요할 수 있음

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

## Typescript

<details>
<summary><strong>타입스크립트의 타입과 인터페이스의 차이점은?</strong></summary>


`interface`는 객체의 형태를 확장하는 데 용이한 반면, `type`은 튜플, 인터섹션, 유니온 등을 이용하여 더 복잡한 타입 정의 및 조합을 표현하는 데 용이하다.

`interface`는 선언 병합을 지원해 여러 번 선언할 수 있어 주로 객체 타입을 확장할 때 유리하다. 동일한 이름을 가진 `interface`를 여러 번 선언하면, 이 속성들이 자동으로 합쳐진다.

```Typescript
interface Person {
  age: number;
  name: string;
  isBirthday: boolean;
}

interface Person {
  address: string;
}

const person1: Person = {
  age: 1,
  name: "abcd",
  isBirthday: false,
  address: "1010",
};
```

`type`으로 선언한 경우에는 동일한 이름을 중복 선언하면 에러가 발생한다. 대신 `type`은 튜플과 같은 복잡한 타입 표현이 가능하며, 복잡한 타입 조합을 위해 인터섹션과 유니온 연산자를 지원한다.

```Typescript
type BasicInfo = {
  name: string;
  age: number;
};

type ContactInfo = {
  email: string;
  phone: string;
};

// 인터섹션 타입 (&)을 사용해 두 타입을 결합하여 하나의 타입으로 생성
type PersonInfo = BasicInfo & ContactInfo;

const person2: PersonInfo = {
  name: "John",
  age: 30,
  email: "john@example.com",
  phone: "123-456-7890",
};
```

`interface`는 선언 병합을 통해 여러 번 선언이 가능하여 주로 객체의 타입을 확장하는 데 유리하며, `type`은 튜플 등 복잡한 타입을 사용하고 유연한 연산자를 통해 복잡한 타입 조합을 표현하는 데 적합하다.
</details>

<details>
<summary><strong>타입스크립트를 사용하는 이유?</strong></summary>

타입스크립트를 사용하는 주요 이유는 크게 세 가지로 들 수 있다.

1. 정적 타이핑을 통해 코드의 안정성을 크게 향상시킬 수 있음: 개발 시 타입 오류를 런타임으로 실행하기 전에 발견할 수 있어 에러를 줄이고, 코드의 품질 개선 가능. 주로 대규모 프로젝트에서 적합함

2. 개발자의 생산성을 높여줌: IDE의 자동완성 기능과 인텔리센스가 더 많은 정보를 제공할 수 있기 때문에 코드 작성 속도가 빨라지고, 리팩토링이 쉬워진다. 명시적인 타입 정의로 인해 코드의 가독성과 이해도가 높아짐

3. 객체지향 프로그래밍의 일부 기능을 자바스크립트에 추가: 인터페이스, 제네릭, 열거형 등 현대적인 프로그래밍 패러다임을 지원하여 더욱 구조화되고 확장 가능한 코드 작성 가능


타입스크립트를 도입하지 않는 것이 더 적합한 프로젝트는?

- 개발 속도와 간단함이 중요한 소규모 프로젝트이다. 프로토타입 제작이나 단순한 랜딩 페이지처럼 빠른 개발 주기가 요구되고 복잡한 로직이 없는 경우 타입스크립트를 설정하고 사용하는 것이 오히려 과도한 비용이 될 수 있다.
- 팀 내에 타입스크립트에 대한 경험이 부족하거나 러닝 커브를 극복할 시간이 없는 경우에도 도입을 신중히 고려해야 함
- 기존 자바스크립트 프로젝트가 매우 방대하고, 타입스크립트로 전환하는 데 드는 비용이나 리소스를 감당할 수 없는 경우에도 도입이 적합하지 않을 수 있음. ㄴ

</details>

## Test

<details>
<summary><strong>E2E 테스트란?</strong></summary>

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
