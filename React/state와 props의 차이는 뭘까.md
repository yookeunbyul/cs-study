## state와 props의 차이는 뭘까

React에서 state와 props는 모두 컴포넌트의 데이터를 다루는데 사용된다.

- props

  **컴포넌트가 외부에서 받는 데이터**

  즉, 부모 컴포넌트로부터 자식 컴포넌트로 전달되는 데이터이다.

  props는 **읽기 전용**이므로 내부에서 직접 수정할 수 없다.

  **컴포넌트 간에 데이터를 전달하는데 사용된다.**

- state

  **컴포넌트 내부에서 관리되는 데이터**

  즉, 컴포넌트 자체가 가지고 있는 데이터이다.

  **state는 컴포넌트의 상태를 변경하거나 업데이트할 때 사용된다.**

  state는 읽기와 쓰기 모두가 가능하다.

<br />

```
props는 외부에서 받는 데이터로, 컴포넌트 간에 데이터를 전달할 때 사용.
state는 컴포넌트 내부에서 관리하는 데이터로, 컴포넌트의 상태를 변경하거나 업데이트 할때 사용.
```

## 출처

https://kindjjee.tistory.com/102
