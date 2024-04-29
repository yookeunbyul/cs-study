## Element와 Component의 차이

- Element는 **React 앱의 가장 작은 단위**이다.

  ```
  const element = <h1>Hello, world</h1>;
  ```

  Element는 **화면에 표시할 내용**을 기술한다.

  Component에서 리턴받아 사용한다.

<br />

- Component는 **이러한 Element를 조합하여 형성한 재사용 가능한 코드 블록이다.**

  ```
  import ReactDOM from 'react-dom/client';

  function Hello() {
    return <h1>Hi React!</h1>;
  }

  const root = ReactDOM.createRoot(document.getElementById('root'));
  root.render(
    <>
        <Hello />
        <Hello />
        <Hello />
    </>
  );
  ```

  자바스크립트 함수를 사용하여 함수형 컴포넌트를 생성해 **리액트 엘리먼트를 반환**한다.

  **그럼 이 엘리먼트를 기반으로 Virtual DOM을 생성해서 효율적인 렌더링을 한다.**

<br />

- 컴포넌트를 사용하면,

  ```
  목적에 따라 코드를 세분화 가능.

  반복적인 개발이 줄어듦.

  재사용할 때도 유용하게 활용할 수 있기 때문에 유지보수가 용이.
  ```

<br />

### 출처

https://velog.io/@aksen5240/%EC%97%98%EB%A6%AC%EB%A8%BC%ED%8A%B8Element%EC%99%80-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8Component-%EB%A6%AC%EC%95%A1%ED%8A%B8-%EC%82%AC%EC%9A%A9%EC%9D%84-%EC%9C%84%ED%95%9C-%ED%95%B5%EC%8B%AC-%EA%B0%9C%EB%85%90
