# JS로 다루는 CSS, CSS-in-JS (feat. CSSOM)

**자바스크립트를 통해 동적인 CSS를 생성**할 수 있는 CSS-in-JS는 개발자 경험(DX)를 만족스럽게 한다.

### 1. CSS-in-JS

- Sass, Less, Stylus 등의 CSS 전처리기 방식
- JSS, styled-components, emotion 등의 CSS-in-JS 방식

CSS-in-JS는 말 그대로 JS로 작성한 CSS이다.

런타임에서 시트가 생성, 관리되며 프로그래밍 언어의 동적 특징을 이용할 수 있다.

<br />

### 2. CSSOM, CSSStyleSheet

**생성된 html 태그와 CSSOM 객체에 정의된 스타일 시트를 확인**

- react-jss의 createUseStyles를 이용

  ```
  const useStyles = createUseStyles(() => ({
      root: {
          width: 500,
          display: "inline-block",
      },
      rootChecked: {
          color: "grey",
          textDecoration: "line-through",
      },
  }));
  ```

  객체 형식으로 CSS를 작성.

  <img width="631" alt="react-jss-html" src="https://github.com/yookeunbyul/RisingTest_wanted/assets/91243651/20537f96-0728-4674-9499-8ac22d4ade69">

  head 태그 안에 style 태그가 생성된다.

  <img width="615" alt="react-jss-cssom" src="https://github.com/yookeunbyul/RisingTest_wanted/assets/91243651/296e5d03-2508-4f31-9690-11cb163c5e4d">

  CSSOM 객체에도 1개의 CSSSyleSheet가 생성되고 2개의 CSSStyleRule이 생성된다.

  ```
  const Task = (props) => {
      const cls = useStyles(props);
      const { title, done, onDoneChange } = props;
      return (
          // 완료 여부에 따라 조건부 클래스 적용
          <li className={[cls.root, done ? cls.rootChecked : ""].join(" ")}>
          <input type="checkbox" checked={done} onChange={onDoneChange} />
          {title}
          </li>
      );
  };
  ```

  <img width="828" alt="react-jss-condition-1-html" src="https://github.com/yookeunbyul/RisingTest_wanted/assets/91243651/ddea076e-56fb-4e38-a930-adc270b85e7c">

  체크박스를 통해 조건부 스타일을 적용시키면 element에 class가 추가되어서 스타일이 적용된다.

  **style 태그의 내용이나 CSSStyleSheet의 변경은 없다.**

<br />

### 3. Props 기반 스타일 적용(react-jss)

위의 예제는 done의 값을 통해 클래스명을 추가해서 스타일을 적용하는 방식.

이 방식은 미리 스타일 시트를 작성해두고, 조건적으로 적용할 것에 대해서만 결정할 수 있다.

```
const useStyles = createUseStyles(() => ({
  root: (props) => ({
    width: 500,
    display: "inline-block",
    //조건부 적용
    color: props.done ? "gray" : "inherit",
    textDecoration: props.done ? "line-through" : "inherit",
  }),
}));

const Task = (props) => {
  const cls = useStyles(props);
  const { title, done, onDoneChange } = props;
  return (
    <li className={cls.root}>
      <input type="checkbox" checked={done} onChange={onDoneChange} />
      {title}
    </li>
  );
};
```

useStyles의 인자로 넘겨준 props를 스타일 시트 객체에서 함수의 파라미터로 가져와 참조할 수 있다.

clssName을 건드려서 스타일을 적용하는게 아닌..

<img width="839" alt="react-jss-props-html" src="https://github.com/yookeunbyul/RisingTest_wanted/assets/91243651/15be1d12-2c7a-4df2-a9fe-238cde91b440">

이전과는 다르게 style 태그에 css는 작성되어 있지 않다.

**그리고 Task 컴포넌트에서 각 항목의 클래스를 다르게 주입**

root-0-2-1과 root-d?-0-2-?처럼 두 개씩 주입되어 있고 그중 하나는 각각 다른 클래스가 입력

<img width="818" alt="react-jss-props-condition-cssom" src="https://github.com/yookeunbyul/RisingTest_wanted/assets/91243651/8c0c08b1-ca63-45cb-8503-df73a5daa0ac">

CSSStyleSheet를 확인해보면 각 항목마다 **다르게 주입된 클래스별로 CSSStyleRule이 생성.**

조건부 스타일을 할 경우,

<img width="823" alt="react-jss-props-cssom" src="https://github.com/yookeunbyul/RisingTest_wanted/assets/91243651/8d541499-9617-4115-8a78-0556990ded40">

**li 태그의 클래스는 변경된 것이 없고**, props.done으로 지정된 컴포넌트는 **CSSStyleRule이 변경**된다.

**각 항목마다 다른 class와 CSSStyleRule를 생성하여 적용한다.**

<br />

### 4. styled-components

styled-components는 **html 태그에 css를 결합하여 리액트 컴포넌트**로 만들어 사용.

=> 말그대로 스타일 된 컴포넌트를 만드는...

만들어진 리액트 컴포넌트의 props를 이용해 동적인 스타일을 적용.

```
import styled from "styled-components";

const ListItem = styled.li`
  width: 500px;
  display: inline-block;
  color: ${({ done }) => (done ? "gray" : "inherit")};
  text-decoration: ${({ done }) => (done ? "line-through" : "inherit")};
`;

const Task = (props) => {
  const { title, done, onDoneChange } = props;
  return (
    <ListItem done={done}>
      <input type="checkbox" checked={done} onChange={onDoneChange} />
      {title}
    </ListItem>
  );
};

export default Task;
```

<img width="838" alt="sc-html" src="https://github.com/yookeunbyul/RisingTest_wanted/assets/91243651/4206cebe-cd93-4874-b1c3-9991c02a02fc">

<img width="837" alt="sc-cssom" src="https://github.com/yookeunbyul/RisingTest_wanted/assets/91243651/bb057903-f628-4157-acf9-f78a6dd5f718">

html head에 style 태그 안에 css 작성, 하나의 CSSStyleRule이 생성되고 그것이 각 li 태그에 같게 적용되어 있다.

<img width="840" alt="sc-condition-html" src="https://github.com/yookeunbyul/RisingTest_wanted/assets/91243651/9c37a964-64b6-426b-8f47-32ddd038f604">

<img width="840" alt="sc-condition-cssom" src="https://github.com/yookeunbyul/RisingTest_wanted/assets/91243651/d5afdc60-19f2-4907-8257-c092be172fe4">

**조건부 스타일을 적용하자 html에서의 css가 생성되고 li 태그의 클래스 변경되고,**

**CSSStyleRule이 추가로 생성된다.**

styled-components는 필요한 css를 생성해서 사용하고, props에 의한 동적인 스타일에서는 런타임에서 css(CSSStyleRule)을 생성하여 사용한다.

props가 추가된다면 더 많은 CSSStlyeRule이 생성될 것이다.

<br />

### 5.@emotion/css

```
import { css } from "@emotion/css";

const Task = (props) => {
  const { title, done, onDoneChange } = props;
  return (
    <div
      className={css`
        width: 500px;
        display: inline-block;
        color: ${done ? "gray" : "inherit"};
        text-decoration: ${done ? "line-through" : "inherit"};
      `}
    >
      <input type="checkbox" checked={done} onChange={onDoneChange} />
      {title}
    </div>
  );
};

export default Task;
```

<img width="839" alt="emotion-html" src="https://github.com/yookeunbyul/RisingTest_wanted/assets/91243651/e850fe36-bd88-4ee3-9764-ff3ac522c7f0">

<img width="836" alt="emotion-cssom" src="https://github.com/yookeunbyul/RisingTest_wanted/assets/91243651/3aaeb7b5-0a74-4a14-9a6b-0c70477cd72a">

styled-components와 같이 style 태그 안에 css가 작성되고 하나의 CSSStyleRule 생성.

각 div 태그에 같게 적용.

<img width="842" alt="emotion-props-html" src="https://github.com/yookeunbyul/RisingTest_wanted/assets/91243651/7345dde2-d893-4ecc-86c2-980efac0697b">

<img width="842" alt="emotion-props-cssom" src="https://github.com/yookeunbyul/RisingTest_wanted/assets/91243651/238c3dfc-2f7a-45b6-876e-88a892e1d77a">

다른 라이브러리와 다르게 style 태그가 2개가 되고 CSSStyleRule이 추가된 것이 아닌 CSSStyleSheet가 추가된다.

<br />

### 6. 마무리

각 라이브러리들은 cssom을 조작하여 스타일을 적용하는데, 라이브러리마다 조작하는 방식이 다 다르다.

### 출처

https://hoontae24.github.io/16
