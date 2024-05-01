## map과 foreach

map()과 foreach() 모두 함수형 프로그래밍을 위한 메서드이다.

<br />

---

### Array.prototype.forEach

내부에서 반복문을 통해 자신을 호출한 배열을 순회화면서 **수행해야할 처리를 콜백 함수로 전달**받아 반복 호출한다.

```
let answer = [];
numbers.forEach(v => answer.push(v**2));
return answer;
```

**forEach 메서드의 반환값은 언제나 undefined다.**

<br />

---

### Array.prototype.map

자신을 호출한 배열을 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다.

```
numbers.map(v => v**2);
```

**그리고 forEach()와 다르게 콜백 함수의 반환값들로 구성된 새로운 배열을 반환한다.**

<br />

---

### 정리

```
둘다 자신을 호출한 배열을 순회하면서 인수로 전달받은 콜백 함수를 반복 호출한다.
foreach()는 반환값이 언제나 undefined 반면, map()은 콜백 함수의 반환값들로 구성된 새로운 배열을 반환한다.
```
