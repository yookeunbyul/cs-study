# 왜 Next.js는 tailwind를 추천할까

### CSS-in-JS

CSS의 문제점(전역에 선언되어 겹치지않는 classname, css가 js와 분리되어 있어서 상태 값을 공유하기 어려운 문제.... 등등)때문에 CSS-in-JS가 등장.

자바스크립트를 통해 CSS를 동적으로 생성하고 처리하면서 위 문제들을 커버했다.

- JS 내부에서 선언 : 수정과 상태 값 공유가 수월
- 컴포넌트 단위로 적용
- class name 자동 생성 : 빌드 타임에 짧고 유일한 이름을 지어줌

#### 구현 방식

대부분의 CSS-in-JS 라이브러리들이 쓰는 방식은 **Runtime CSS-in-JS** 또는 **Runtime stylesheets**라고 한다.

스타일을 정의하는 코드가 **클라이언트 런타임 때 실행되는 JS 번들에 포함**되는 방식인데 브라우저는 스타일 코드를 해석하지 못하므로 라이브러리 코드도 JS 번들에 포함되어야한다.

해석된 스타일 코드는 document의 head 태그에 style 태그를 추가하거나 CSSStyleSheet API로 직접 CSSSOM에 적용시켜서 사용한다.

```
CSS-in-JS는 스타일을 정의하는 코드를 클라이언트 런타임 때 JS 번들에 포함해서 브라우저가 해석하도록 한다.

그러면 style 태그를 추가하거나 CSSStyleSheet API로 CSSOM을 직접 조작하여 스타일을 적용한다.
```

하지만, 이러한 방식으로 단점이 존재하는데

- JS 번들 용량 증가 : 스타일 코드가 많을 수록 더 많은 코드가 클라이언트로 전달되어야한다.

- 페이지 렌더링 시간 증가 : JS에 작성된 CSS 코드를 구문 분석하고 동적으로 추가하면서 렌더링 시간이 증가한다.

하지만 장점이 커서 많이 사용되었고 CSR 환경을 바탕으로 두고 구상한 방법(JS의 동적인 처리가 같기 때문이겠지?)이었기 때문에 SSR 환경에서 문제가 나타났다.

<br />

### SSR에서의 CSS-in-JS

SSR에서 CSS-in-JS 라이브러리를 그대로 사용하면,

```
우선 서버 사이드 렌더링은 초기에 빠르게 브라우저에 화면을 렌더링할 수 있도록 이벤트와 핸들러는 뺀, 즉 js를 뺀 html 파일만 넘겨준다.

그 후에 hydrate로 뺀 이벤트와 핸들러를 붙이는 작업을 하는데 별도의 자바스크립트 코드를 모두 다운로드, 파싱, 실행하는 과정을 거쳐 브라우저에게 전달한다.
```

하튼 이런 과정이 있기 때문에 초기에 **HTML에 스타일이 전혀 적용되지 않아 잠깐 날 것의 HTML이 나타나는 문제가 있다.**

때문에 초기 HTML에 포함되는 요소에 대한 CSS인 Critical CSS를 서버쪽에서 사용할 수 있도록 하는 처리가 필요하다. 보통 SSR 과정에서 정적으로 생성되는 요소의 CSS만 추출해서 HTML에 적용하도록 설정한다. => 따로 처리가 필요.

하지만 이것도 클라이언트 쪽에서 실행될 JS에도 포함되어야해서 동일한 스타일에 대한 코드가 초기 HTML에 한번, JS 번들에서 두 번 클라이언트에게 전달된다.

<br />

### Tailwind CSS

```
React의 스타일 툴로 많이 사용되는 Styled-components나 Emotion은 CSS-in-JS로 CSS 코드처럼 보이지만, 사실 JavaScript 코드이고, 브라우저에서 JavaScript 파일이 읽혀야지만 CSS 적용이 된다.

서버사이드 렌더링을 하는 Next.js 경우 이러한 CSS-in-JS툴을 사용하려면 별도의 설정을 해주어야 사용이 가능한데, Tailwind CSS는 순수 CSS로 파일을 생성해주기 때문에 JavaScript에 의존하지 않아도 된다. (서버사이드 렌더링의 장점을 살릴 수 있다.)
```

=> 기존 CSR과 CSS-in-JS는 동적으로 처리하기위해 JS에 굉장히 의존적

=> 하지만 요즘은 초기 렌더링 속도 문제와 검색 엔진 최적화 문제 때문에 SSR이 뜨고있고,

=> SSR은 JS에 의존적이지않기에 CSS-in-JS와는 가는 길이 다르며 Tailwind는 스타일 코드가 html 안에 있고 순수 css 파일을 생성해주기 때문에 SSR과 적합하다.

<br />

Tailwind CSS는 **Utility CSS**로 class name을 컴포넌트가 아니라 기능에 붙임으로써 CSS의 문제를 해결하려 했다.

예전에 유명했던 Bootstrap과 유사하게 **미리 정의된 스타일 구성 요소**를 가져와서 사용하는 방식으로 동작한다.

빌드 시에 사용하지 않는 클래스는 제거되어 **번들 크기에 주는 영향도 줄일 수 있다.**

```
SSR 관점에서 중요한 건 런타임에 스타일시트를 생성하지 않고 빌드 타임에 스타일시트를 가져오는 방식이라는 점이다. 때문에 SSR에서도 추가적인 설정 없이 작동할 수 있다.
```

=> 그럼 js에 의존적이지도 않고 런타임에 생성하는 css-in-js와 다르게 빌드 타임에 스타일시트를 가져오는 방식이기 때문에

=> 결국 tailwind CSS가 SSR인 next.js와 궁합이 좋다?!

<br />

---

### 출처

https://babycoder05.tistory.com/entry/Nextjs-TypeScript-Tailwind-CSS-%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Tailwind-CSS-%EC%9E%A5%EB%8B%A8%EC%A0%90

https://velog.io/@shinhw371/CSS-why-Nextjs-recommand-Tailwind#ssr%EC%97%90%EC%84%9C%EC%9D%98-css-in-js
