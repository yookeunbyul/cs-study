## 클래스형 컴포넌트의 LifeCycle(생명주기)

리액트는 컴포넌트를 기반으로 UI를 만드는 라이브러리이다.

그러다보니 각각의 컴포넌트는 수명 주기, 즉 라이프사이클이 존재한다.

컴포넌트의 수명은 보통 페이지에서 **렌더링되기 전인 준비 과정에서 시작하여 페이지에서 사라질 때 끝이 난다.**

생성자를 통해서 필요한 메모리를 할당하고, 소멸자를 통하여 메모리를 반환한다.

컴퓨터의 자원은 한정적이기 때문에 역할이 끝나면 모든 메모리를 반환해야 메모리 누수에 대한 문제가 생기지 않고, 더 좋은 성능을 발휘할 수 있다.

라이프사이클이 있는 이유는 **메모리 비우기**가 가장 큰 이유이다.

---

### 라이프 사이클의 분류

<img src="https://github.com/yookeunbyul/cs-study/assets/91243651/c0fae20c-bca9-4fa1-a180-69c762870ec5" />

크게 세가지 유형이 있는데

- 컴포넌트가 생성될때(마운팅)
- 업데이트 될 때(업데이팅)
- 제거할 때(언마운팅)

또 단계 별로 필요한 순간에 필요한 작업들을 끼워넣을 수 있는 메서드들이 존재한다.

---

## 라이프 사이클 메서드

1. 컴포넌트가 로딩되기 시작하는 Mount (생성)

   DOM이 생성되고 웹 브라우저 상에서 나타나는 것을 뜻한다.(렌더링)

   1-1. constructor (클래스 생성자)

   클래스 인스턴스 객체를 생성하고 초기화하는 메서드로 리액트에서 **컴포넌트를 만들 때 처음으로 실행**된다.

   이 메서드에서는 **초기 state를 정할 수 있다.**

   ```
   //class
    class Example extends React.Component {
        constructor(props) {
            super(props); //super 함수를 호출해야 React.Component class의 method가 호출된다.
            this.state = { count: 0 } ;
        }
    }
   ```

   1-2. static getDerivedStateFromProp

   **props로 받아온 값을 state에 동기화 시키는 용도로 사용한다.**

   컴포넌트가 마운트 될 때와 업데이트 될때 호출된다.

   ```
   //Class
    class Example extends React.Component {
        static getDerivedStateFromProps(nextProps, prevState) {
            if (nextProps.value !== prevState.value) {
                return { value: nextProps.value}
            }
            return null
        }
    }
   ```

   이 메서드는 이유와 상관없이 렌더링 때마다 매번 실행되므로 주의해야한다.

   최초 마운트 시와 갱신 시 모두에서 render 메서드를 호출하기 직전에 호출된다.

   1-3. shouldComponentUpdate

   **props나 state를 변경했을 때, 리렌더링을 할지 말지 결정하는 메서드**이다.

   반드시 true나 false를 반환한다. 기본적으로 true를 반환한다.

   오직 성능 최적화만을 위한 것이며 렌더링 방지 목적으로 사용하게 된다면 버그가 생길 수 있다.

   ```
   //Class
   class Example extends React.Component {
       shouldComponentUpdate(nextProps) {
           return nextProps.value !== this.props.value
       }
   }
   ```

   1-4. 실제 로딩이 이루어지는 render

   컴포넌트 렌더링 할때 필요한 메서드 중 유일한 필수 메서드이다.

   **최종적으로 component에서 작업한 결과물을 return 하는 메서드이다.**

   render 메소드가 실행되면서 JSX가 HTML로 변환되어 우리가 보는 웹 브라우저에 나타나게 된다.

   render 메서드는 순수 함수여야 한다. 이것은 input에 대해서 같은 output이 나와야한다.

   ```
   // Class
    class Example extends React.Component {
        render() {
            return <div>컴포넌트</div>
        }
    }
   ```

   결과물로 나온 Element들이 Virtual DOM에 mount되고 실제 DOM에 업데이트 된다.

   1-5. **처음 로딩이 끝난 뒤에 수행되는 ComponentDidMount**

   **이 메서드는 컴포넌트를 만들고 첫 렌더링을 마친 후 실행한다.**

   **초기 컴포넌트의 로딩 이후에 한번만 실행**되는 라이프사이클 메소드이다.

   여기서 **DOM을 직접 조작**할 수 있다. => **일반적으로 비동기 API 사용**

   ```
   componentDidMount() {
       fetch("https://jsonplaceholder.typicode.com/users")
       .then((response) => response.json())
       .then((users) => this.setState({ users, loading: false }));
   }
   ```

2. 컴포넌트의 업데이트 Updating (업데이트)

   - props가 바뀔 때
   - state가 바뀔 때
   - 부모 컴포넌트가 리렌더링 될 때
     -this.forceUpdate로 강제로 렌더링을 trigger할 때

   업데이트가 발생된다.

   2-1. componentWillReceiveProps

   **컴포넌트가 새로운 속성을 전달받을 때 실행된다.**

   속성 값의 변경과 상관없이 재렌더링이 이루어질 때마다 실행한다.

   2-2. shouldComponentUpdate

   1-3과 동일.

   2-3. getSnapShotBeforeUpdate

   render에서 만들어진 결과가 브라우저에 실제로 반영되기 직전에 호출된다.

   컴포넌트에 변화가 일어나기 직전의 DOM 상태를 가져와서 특정 값을 반환하면 그 다음 발생하게 되는 componentDidUpdate함수에서 받아와서 사용한다.

   2-4. **componentWillUpdate**

   새로운 속성이나 상태를 받은 후에 렌더링 직전 호출한다.

   초기 렌더링 시에는 호출되지 않는다.

   **컴포넌트를 DOM에서 제거할 때 실행한다.**

   componentDidMount에서 등록한 이벤트, 타이머, 직접 생성한 DOM이 있다면 여기서 제거 작업을 해야한다.

   2-5. **componentDidUpdate**

   **컴포넌트의 변경이 완료되었을 때 수행되는 메소드이다.**

   처음 렌더링 될때는 실행되지 않고, 리 렌더링을 완료한 후 실행한다.

   state나 props가 변경되어 DOM 변화가 발생한 뒤 발생된다는 것.

   ```
   // Class
   class Example extends React.Component {
       componentDidUpdate(prevProps, prevState) {
           ...
       }
   }
   ```

   prevProps 또는 prevState를 사용하여 컴포넌트가 이전에 가졌던 데이터에 접근이 가능하다.

3. 컴포넌트의 삭제 Unmounting (제거)

   Unmounting은 **DOM에서 제거**되는 것을 뜻한다. => 컴포넌트가 사라질 때 수행되는 메소드이다.

   JSX에 포함되었다가 이후에 제거되는 경우에 발생한다.

   3-1. **ComponentWillUnmount**

   **컴포넌트를 DOM에서 제거할 때 실행한다.**

   componentDidMount에서 등록한 이벤트가 있다면 여기서 제거 작업을 해야한다.

   ```
   // Class
   class Example extends React.Component {
       coomponentWillUnmount() {
           ...
       }
   }
   ```

4. Error Handling

   4-1. componentDidCatch

   이 메서드는 컴포넌트 렌더링 도중에 에러가 발생했을 때 애플리케이션이 멈추지 않고 오류 UI를 보여줄 수 있게 한다.

<br />

### 출처

https://velog.io/@remon/React-%EB%A6%AC%EC%95%A1%ED%8A%B8-%EB%9D%BC%EC%9D%B4%ED%94%84-%EC%82%AC%EC%9D%B4%ED%81%B4#react-%EB%9D%BC%EC%9D%B4%ED%94%84-%EC%82%AC%EC%9D%B4%ED%81%B4%EC%9D%B4%EB%9E%80
