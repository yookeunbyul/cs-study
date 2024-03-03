## DOM이란 무엇일까

브라우저가 서버에서 파일 및 데이터를 받아 화면에 표시 즉, **렌더링** 전에는 많은 단계를 거쳐야 하는데 우리는 그 과정을, **Critical Rendering Path 'CRP'라고 한다.**

- 파싱

  소스코드 자체는 텍스트 문서다. 파싱이라는 과정을 거쳐서 문법적인 의미와 구조를 부여해야 컴퓨터가 언어를 해석할 수 있다. 한마디로 컴퓨터가 이해할 수 있도록 바꿔주는 과정.

<br />

주소창에 url을 입력하면 브라우저는 HTML,CSS,JS 등 렌더링에 필요한 파일 및 데이터를 서버에 요청한다.

그리고 브라우저가 이해할 수 있도록 **파싱을 통해 자료구조 형태로 만들어준다.**

HTML을 파싱하면 **DOM tree**, 즉. DOM(Document Object)는 HTML 요소들을 파싱해서 (객체 기반 노드 트리 구조로) 구조화된 표현이다.

CSS를 파싱하면 **CSSOM tree**, CCSOM(Cascading Style Sheets Object Model)은 스타일 정보를 파싱해서 구조화된 표현이다.

JS를 파싱하면 **AST(Abstract Syntax Tree)** 가 된다.

![rendering](https://github.com/yookeunbyul/cs-study/assets/91243651/727fcc72-c284-4749-b403-f404d3f419d7)

그래서 이렇게 생성된 DOM과 CSSOM으로 렌더링 트리를 형성한다.

**렌더링 트리는 렌더링을 위한 트리 자료구조로, 렌더트리를 통해 렌더링이 실행된다.**

<br />

### 그래서 요약은

```
DOM이란,

브라우저는 렌더링을 하는 과정에서 서버에 필요한 파일과 데이터를 요청해 받는다. 그리고 이 파일은 단순히 소스코드에 불과하기 때문에 컴퓨터가 이해할 수 있도록 파싱을 해줘야한다.

그 때 HTML을 파싱하면 노드 트리 구조로 구조화된 객체모델이 되는데 이것이 DOM이다.

HTML 문서의 계층적 구조와 정보를 표현한다.

뿐만 아니라 DOM을 제어할 수 있는 API, 즉 프로퍼티와 메소드를 제공한다.
```

<br />

### 참조

https://velog.io/@zaman17/%EA%B8%B0%EC%88%A0%EB%A9%B4%EC%A0%91%EB%8C%80%EB%B9%84-%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EB%A0%8C%EB%8D%94%EB%A7%81-%EC%88%9C%EC%84%9C%EC%99%80-%EC%9B%90%EB%A6%AC

https://velog.io/@sj_dev_js/HTML-DOM%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C
