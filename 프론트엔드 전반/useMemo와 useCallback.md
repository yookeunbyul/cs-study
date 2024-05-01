## useMemo와 useCallback

### 메모이제이션

메모이제이션(memoization)은 값비싼 함수 호출의 결과를 **캐싱하고 동일한 입력이 다시 발생할 때 캐싱된 결과를 반환**하는 프로그래밍 기술이다.

메모이제이션를 사용하면 동일한 결과를 불필요하게 **다시 계산하지 않고, 캐시된 결과를 반환**할 수 있다.

따라서, useCallback, useMemo와 같은 **메모이제이션 훅**을 통해 성능을 향상시키고 코드의 복잡성을 줄일 수 있다.

<br />

---

### useMemo

**useMemo는 메모이제이션된 값(캐싱한 값)을 반환하는 함수입니다.**

```
useMemo(() => fn, [deps])
```

이미 함수가 실행되어 연산된 값이 있다면, **함수를 다시 호출하지 않고 기존에 연산된 값을 재활용하는 방식**이다.

근데 만약 두번째 인자인 의존성 배열에 있는 값이 변하게 되면 **() => fn 함수를 실행하고, 그 함수의 반환 값을 반환**해준다.

```
import { useState } from "react";

export default function App() {
  const [val1, setVal1] = useState(0);
  const [val2, setVal2] = useState(0);

  const handleAdd1 = () => {
    setVal1((prev) => prev + 1);
  };

  const handleAdd2 = () => {
    setVal2((prev) => prev + 1);
  };

  const computedVal = val1 * val1;
  console.log("computedValue", computedVal);

  return (
    <>
      <div>val1: {val1}</div>
      <div>val2: {val2}</div>
      <div>val3: {computedVal}</div>
      <br />
      <button type="button" onClick={handleAdd1}>
        Add val1
      </button>
      <button type="button" onClick={handleAdd2}>
        Add val2
      </button>
    </>
  );
}
```

val2의 값을 증가시키면, val2 상태가 변화되기 때문에 val1의 값이 같아도 리액트가 상태 변화를 화면에 표시하기 위해 컴포넌트를 리렌더링 시킨다.

따라서 의존하지 않는 val2값이 변해도 computedVal의 연산이 계속 재실행된다.

```
import { useState, useMemo } from 'react'

...

const computedVal = useMemo(() => {
  console.log(val1 * val1)
  return val1 * val1;
}, [val1]);
```

근데 useMemo()를 사용하면 va2가 변할때는 이미 val1 \* val1 값을 메모이제이션 해놨기 때문에 그 연산값을 계속 반환해주는거다. 다시 계산하는 게 아니라..

<br />

---

### useCallback

useCallback은 **메모이제이션된 함수(캐싱된 함수)를 반환**하는 함수다.

```
useCallback(fn, [deps])
```

useCallback 또한 콜백 함수의 의존성이 변경되었을 때에만 새로 fn에 등록한 함수를 반환한다.

만약 useCallback을 사용하지 않는다면, 함수는 컴포넌트가 렌더링 될 때마다 새롭게 생성된다.

하지만, useCallback을 사용하면 컴포넌트가 다시 렌더링 되더라도, 해당 함수가 의존하고 있는 값들이 바뀌지 않는다면 함수를 새로 생성하지 않고 기존 함수를 계속 반환한다.

```
const memoizedCallback = useCallback(() => console.log(), [test])
```

함수를 반환하기 때문에 그 함수를 가지는 const 상수에 초기화하는 것이 일반적이다.

useCallback을 사용할 때는,

- **자식 컴포넌트에 props로 함수를 전달할 경우**

  ```
  const functionOne = function() {
      return 5;
  };
  const functionTwo = function() {
      return 5;
  };
  // 서로의 참조가 다르기 때문에 false
  console.log(functionOne === functionTwo);
  ```

  **우선 함수는 값이 아니라 참조로 비교된다.**

  컴포넌트에서 특정 함수를 정의할 경우 각각의 함수들은 모두 고유한 함수가 된다.

  ```
  function App() {
  const [name, setName] = useState('');
  const onSave = () => {};

    return (
        <div className="App">
        <input
            type="text"
            value={name}
            onChange={(e) => setName(e.target.value)}
        />
        <Profile onSave={onSave} />
        </div>
    );
  }
  ```

  useCallback을 사용하지 않을 경우, name이 변경되어 리렌더링이 발생하면 onSave()도 다시 만들어지고 props로 onSave()가 새로 전달되게 된다.

  그럼 Profile 컴포넌트도 리렌더링이 일어난다.

  ```
  import React, { useCallback, useState } from 'react';
  import Profile from './Profile';


    function App() {
    const [name, setName] = useState('');
    const onSave = useCallback(() => {
        //  작업
    }, [deps]);

    return (
            <div className="App">
            <input
                type="text"
                value={name}
                onChange={(e) => setName(e.target.value)}
            />
            <Profile onSave={onSave} />
            </div>
        );
    }
  ```

  useCallback을 사용하면 의존성있는 값이 변하지않는 한 onSave()를 재사용해서 함수의 참조값이 변하지않기 때문에 Profile 컴포넌트의 리렌더링을 방지할 수 있다.

- **외부에서 값을 가져오는 api를 호출하는 경우**

  ```
    import React, { useState, useEffect } from "react";

    function Profile({ id }) {
    const [data, setData] = useState(null);

    const fetchData = () =>
        fetch(`https://test-api.com/data/${id}`)
        .then((response) => response.json())
        .then(({ data }) => data);

    useEffect(() => {
        fetchData().then((data) => setData(data));
    }, [fetchData]);

    // ...
    }
  ```

  fetchData는 함수이기 때문에 id 값에 관계없이 컴포넌트가 렌더링 될 때마다 새로운 참조값으로 변경이 된다. 함수가 변경되었으므로, 매번 useEffect가 실행되어 다시 렌더링이 되고 무한루프에 빠지게 된다.

  ```
  import React, { useState, useEffect } from "react";

    function Profile({ id }) {
    const [data, setData] = useState(null);

    const fetchData = useCallback(
        () =>
        fetch(`https://test-api.com/data/${id}`)
            .then((response) => response.json())
            .then(({ data }) => data),
        [id]
    );

    useEffect(() => {
        fetchData().then((data) => setData(data));
    }, [fetchData]);

    // ...
    }
  ```

  이렇게 useCallback 훅을 사용하면, 컴포넌트가 다시 렌더링 되더라도 fetchData 함수의 참조값을 동일하게 유지시킨다.

  따라서, useEffect에 의존성 배열 값에 있는 fetchData 함수는 id 값이 변경되지 않는 한, 재호출되지 않는다.

<br />

### 출처

https://narup.tistory.com/273

https://velog.io/@khy226/useMemo%EC%99%80-useCallback-%ED%9B%91%EC%96%B4%EB%B3%B4%EA%B8%B0#usecallback

https://velog.io/@khy226/useMemo%EC%99%80-useCallback-%ED%9B%91%EC%96%B4%EB%B3%B4%EA%B8%B0
