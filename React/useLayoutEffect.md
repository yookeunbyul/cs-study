## useLayoutEffect

렌더링 과정에서

- render : **DOM Tree를 구성**하기 위해 각 엘리먼트의 스타일 속성을 **계산하는 과정**

- paint : **실제 스크린에 Layout을 표시하고 업데이트** 하는 과정

이 있는데, render => paint 순으로 진행된다.

---

<br />

### useEffect

<img src="https://github.com/yookeunbyul/cs-study/assets/91243651/9dac5b88-d0da-45ed-a13f-28d1829747aa" />

useEffect는 위 그림과 같이

render => paint => useEffect 순으로 실행된다.

이미 초기 렌더링이 되어있고 state가 변경되서 재렌더링이 되면 useEffect 내에 작업이 호출되기 때문에 기존 값이 paint 된 후(사용자에게 보여진 후)에 업데이트가 되는 것이다.

그래서 우리 눈에는 무언가 깜빡이는 것처럼 보이는 것이다.

<br />

### useLayoutEffect

<img src="https://github.com/yookeunbyul/cs-study/assets/91243651/e4ac615c-ec7e-49a6-9a3f-8052a56603db" />

render => useLayoutEffect => paint 순으로 실행되기 때문에 업데이트가 되고 나서 화면에 보여지는 것이다.

그래서 자연스럽게 바로 값이 반영된다.

<br />

### 결론

그러나 useLayoutEffect는 동기식이므로 성능이 저하될 수 있어 사용할 때 주의해야한다.

**이 메서드 실행이 완료될 때까지 UI가 업데이트 되지 않기 때문이다.**

이러한 사항을 고려해서 선택 사용하면 좋다.

<br />

### 출처

https://jaddong.tistory.com/entry/useEffect%EC%99%80-useLayoutEffect%EC%9D%98-%EC%B0%A8%EC%9D%B4-%EC%98%88%EC%A0%9C%EB%A1%9C-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0
