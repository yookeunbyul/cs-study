## React.js의 렌더링 방식 살펴보기

1. 웹 브라우저는 어떻게 동작할까?

- 브라우저는 HTML, CSS로 작성한 웹 페이지를 어떤 과정을 거쳐 화면에 렌더링 하는걸까?

  - **Critical Rendering Path** 과정을 통해서 렌더링을 한다.

  1. HTML, CSS를 DOM, CCSOM로 변환한다.

     - DOM(Document Object Model) - 문서 객체 모델

       HTML을 브라우저가 해석하기 편한 방식으로 변환한 객체 트리

  2. Render Tree 생성

     DOM과 CSSOM을 합쳐서 생성한다.

  3. Layout

     Render Tree를 기반으로 실제 웹 페이지에 요소들의 **배치를 결정**하는 작업

  4. Painting

     실제 요소들을 화면에 그려내는 과정

<br />

- 그렇다면 업데이트는 어떻게 이루어질까?

  - JavaScript가 DOM을 수정하면 업데이트가 발생 함

  - DOM이 수정되면 Critical Rendering Path가 다시 실행 됨

  - **하지만 Layout(Reflow), Painting(Repaint)을 다시 하는 건 비용이 많이 든다.(연산과 시간이 오래 걸린다.)**

  - 잦은 Reflow, Repaint는 웹 성능 악화의 주범.

- 결론

  - JS로 DOM을 직접 수정하려면, 동시에 발생한 업데이트를 모아서 다 모았다면 한번에 수정한다. 그래서 Reflow와 Repaint를 최소화한다.

  - 하지만 서비스의 규모가 커질 수록 점점 힘들어진다. DOM도 많아지고 업데이트도 많아지고 순수한 JS로 하기에는 무리무리.....

  - React JS에서는 이런 로직을 자동으로 해준다. => 렌더링 프로세스가 있다.

<br />

2. React의 렌더링 프로세스

- React는 2단계를 거쳐 화면에 UI를 렌더링 함

  ```
  컴포넌트를 계산하고 업데이트 사항을 파악하는 단계(Render Phase) -> 변경사항을 실제 DOM에 반영하는 단계(Commit Phase)
  ```

  - Render Phase

    1. 컴포넌트를 호출해서 계산 후 React Element라는 객체를 반환한다.

       **React Element, 컴포넌트가 렌더링하고자 하는 UI의 정보를 담고있는 객체.**

    2. React Element들을 모아 Virtual DOM을 생성

       **Virtual DOM, React Element라고 부르는 객체 값의 모임**

       실제 DOM은 아니고 **값으로 표현된 UI**라고 이해하는게 더 정확하다.

    - **React 컴포넌트가 호출해서 React Element 객체를 반환하고 이 객체들을 모아서 Virtual DOM을 만든다.**

  - Commit Phase

    **Virtual DOM을 Actual DOM에 반영함**

    반영하면 다시 DOM이 변경된 걸 감지하고 **Critical Rendering Path** 과정을 수행한다.

<br />

- 굳이 이렇게까지 복잡하게 하는 이유가 뭘까?

  ```
  DOM 수정을 최소화 하기 위해서..
  ```

  - 업데이트 발생 시

    1. Render Phase를 처음부터 다시 실행 -> **새로운 Virtual DOM 생성**

    2. 이전의 Virtual DOM과 차이점을 비교

    3. 계산된 차이점(변경된 부분만)을 Actual DOM에 한번에 업데이트

- 렌더링 프로세스 정리

  ```
  동시에 발생한 업데이트를 모아(이게 중요) 한번만 DOM을 수정
  대부분의 상황에 충분히 빠른 속도로 화면 업데이트가 이루어짐

  이 과정을 특별히 Reconciliation(재조정)이라고 부름.

  -> 항상 최고의 속도를 보장한다는 아님.
  ```

<br />

- 총정리

  - 순수한 JavaScript만을 이용해 DOM을 조작할 때에는 DOM 수정을 최소화 해야함

    - Reflow, Repaint를 최소한으로 발생시키기 위함

    - 동시에 발생하는 업데이트를 최대한 모아 한번만 DOM을 수정해야 함

    - 서비스 규모가 커질수록 쉽지 않음

  - React는 자체적인 렌더링 프로세스를 사용하므로 이런 걱정에서 자유로움

    - Render Phase와 Commit Phase로 나뉨

    - Render Phase에 Virtual DOM을 생성하여 동시에 발생하는 업데이트를 모음

    - Commit Phase에 Virtual DOM에 반영된 모든 업데이트를 Actual DOM에 한번만 반영함
