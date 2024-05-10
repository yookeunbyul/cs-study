## attribute와 property의 차이

- Attribute

  **HTML 요소의 속성**으로 정의된다.

  ```
  <p style="background-color: rgb(000,000,000);">ddd</p>
  ```

  style처럼 **시각적이거나 기능적인 효과**를 나타내는데 사용된다.

---

<br />

- Property

  **javascript 객체의 속성**이다.

  ```
  let change = document.querySelector('p.coding');

  change.textContent = ".....";
  ```

  textContent처럼 **HTML 요소의 상태를 나타내거나 조작**하는데 사용된다.

---

<br />

```
Attribute 속성은 정적인 값으로 Html 문서가 로드 될 때 초기화 되고
Property는 동적인 값으로 Javascript에서 요소를 조작하고 업데이트 할 때 사용가능하다.
```
