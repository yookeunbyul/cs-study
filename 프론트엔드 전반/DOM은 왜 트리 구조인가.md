## DOM은 왜 트리 구조인가.md

### DOM이란

```
HTML이나 XML같은 마크업 언어로 작성된 문서를 자바스크립트와 같은 프로그래밍 언어가 조작할 수 있도록 변환한 객체 트리다.
```

<br />

---

### DOM은 왜 필요한가?

동적인 웹 페이지를 만드려면 자바스크립트와 같은 프로그래밍 언어가 **문서에 접근하고, 제어할 수 있는 수단**이 있어야 한다.

그러나 마크업 언어로 작성된 문서에는 이러한 수단이 없다. 따라서, 문서에 접근하고 제어할 수 있는 수단인 DOM이 필요한 것이다.

<br />

---

### DOM을 통해 어떤 동작을 할 수 있는가

button element가 클릭되었을 때, **특정 함수를 호출하도록 Event handler를 추가**할 수 있고, 웹 페이지 내에서 **새로운 요소를 추가하거나 삭제, 수정**할 수 있다.

<br />

---

### DOM은 왜 계층적 구조인 트리로 표현하는가

우선 **트리는 계층 관계가 있는 데이터들을 표현하기에 가장 적합한 자료구조**이다.

마크업 언어인 HTML가 상위 태그가 하위 태그를 감싸는 형태로 이루어져있고, 이 관계를 계층 관계로 볼 수 있다.

또한 이런 관계가 노드의 추가, 이동, 제거 작업을 쉽게 할 수 있도록 도와준다.

그리고 이벤트가 발생한 요소로부터 이벤트가 올라가는 이벤트 버블링, 반대로 이벤트가 내려가는 이벤트 캡쳐링 동작은 계층적 구조에서 효과적으로 동작하기 때문에, DOM을 계층적 구조로 표현하는 것이다.

<br />

---

### 그래서 가상 DOM은?

우선 DOM은 렌더링 과정에서 마크업 언어로 만든 문서를 프로그래밍 언어가 조작할 수 있도록 변환된 객체 트리이다.

동적인 웹 페이지를 만들면서 수많은 DOM 수정이 필요했고 수정할 때마다 발생하는 리플로우와 리페인트는 너무나 많은 비용이 들었다.

그래서 이러한 DOM 수정을 최소화하기 위해 **DOM의 사본을 저장하는 자바스크립트 객체인 가상 DOM**이 등장했고, 동시에 발생하는 업데이트를 모아 가상 DOM을 기존의 DOM이나 이전에 만든 가상 DOM과 비교해서 변경된 요소들만 한번에 업데이트 하는 것이다.

### 출처

https://velog.io/@haizel/DOM%EC%9D%80-%EC%99%9C-%ED%8A%B8%EB%A6%AC-%EA%B5%AC%EC%A1%B0-%EC%9D%BC%EA%B9%8C

https://www.youtube.com/watch?v=pYHgo5mEcYE&list=PLBh_4TgylO6CI4Ezq3OLRRzg2NAn3FLPB&index=2
