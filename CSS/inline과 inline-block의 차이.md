## inline과 inline-block의 차이

우선 dispaly 속성은 **요소들을 어떻게 배치하고 보여줄 것인지를 결정**한다.

자주 사용하는 속성은 none, block, inline, inline-block이 있다.

1. display : none

   UI 화면상에 보이지 않도록 숨기는 것이다.

   어떠한 영역을 가지지도 않고 완전히 삭제된 것처럼 보인다.

2. display : block

   화면의 가로 너비 기준으로 전체의 한 영역을 차지한다. (한 줄 쫘악)

   width, height을 통해 사이즈 조절할 수 있으며, 지정하지않으면 width는 화면의 가로너비

   height는 컨텐츠 만큼의 크기를 가진다.

3. display : inline

   컨텐츠 크기 만큼의 크기를 가지며 줄바꿈이 되지 않는다. (한 줄 차지 X)

   width, height을 지정할 수 없다.

4. display : inline-block

   inline + block

   컨텐츠만큼의 크기를 가지며 줄바꿈이 되지 않는다.(inline)

   대신 width, height을 지정할 수 있다.(block)

---

### 그래서 inline과 inline-block의 차이

```
둘다 컨텐츠 크기만큼의 크기를 가지고 줄바꿈이 되지 않는다. (한 줄 다 차지 X)

대신, inline은 크기 조절이 안되고 inline-block은 크기 조절을 할 수 있다.
```

### 출처

https://cceeun.tistory.com/261
