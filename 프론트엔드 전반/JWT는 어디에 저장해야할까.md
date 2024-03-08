## JWT는 어디에 저장해야할까

로컬 스토리지(웹 스토리지)냐 쿠키냐..

### 사전 지식

- XSS(Cross Site Scripting)

  : 공격자가 의도한 악의적인 js 코드를 피해자 웹 브라우저에서 실행시키는 것

  이 방법으로 피해자 브라우저에 저장된 중요 정보들을 탈취 가능하다.

  ```
  Js 코드로 의도하지 않은 request를 날린다던가
  localStorage, 변수 값 등 모든 것이 탈취 가능하기 때문이다.

  XSS 공격 방지는 웹 보안의 뿌리라고 할 수 있다.
  ```

- CSRF(Cross Site Request Forgery)

  : 정상적인 request를 가로채 백엔드 서버에 변조된 request를 보내 악의적인 동작을 수행하는 공격을 의미한다.

<br />

토큰에는 payload에 암호화되지않은 채 클라이언트에 저장되기때문에 탈취 당하면 안된다.

그럼 어디에 저장되는 것이 좋을까..

### localStorage(웹 스토리지)에 저장

쿠키는 클라이언트가 **매 HTTP Request시 HTTP Header에 쿠키를 담아서 전송**

- 장점

  그래서 쿠키와는 다르게 **CSRF 공격에 안전하다.**

- 단점

  하지만 **XSS에 취약하다.**

  localStorage에 접근하는 js코드 한줄만 주입하면 localStorage에 공격자가 내 집처럼 드나들 수 있다.

### cookie에 저장

- 장점

  **XSS 공격으로부터 localStorage에 비해 안전하다.**

  **쿠키의 httpOnly 옵션을 사용하면 Js에서 쿠키에 접근 자체가 불가능하다.(그럼 XSS 공격을 방어할 수 있겠네)**

  하지만 XSS 공격으로부터 완전히 안전한 것은 아니다.

  js로 request를 보낼 수 있으므로 자동으로 request에 실리는 쿠키의 특성 상 사용자의 컴퓨터에서 요청을 위조할 수 있기 때문. 공격자가 귀찮을 뿐이지 XSS가 뚫린다면 httpOnly cookie도 안전하진 않다.

- 단점

  **자동으로 http request에 담아서 보내기 때문에 CSRF 공격에 취약하다.**

### 정리

```
나는.. 어디에다 저장할까하아....

로컬스토리지에 저장하면 CSRF 공격에 안전하고 XSS에 취약하다.

쿠키는 httpOnly 옵션을 사용해 js 접근을 막을 수 있기 때문에 XSS 공격에 안전하다. 하지만 자동으로 request에 담겨서 보내기 때문에 CSRF 공격에 취약하다.

결국 js로 request를 보낼 수 있기 때문에 httpOnly가 완전히 안전한 건 아니다.. 그럼 쿠키는 xss에도 csrf에도 안전하지않을 수 있다?
```

```
best option은 refesh token을 httpOnly 쿠키로 설정해서 js가 접근 못하도록하고 클라이언트에 저장.

그리고 새로고침 될 때마다 refresh token을 request에 담아 새로운 accessToken을 발급받는다.

발급받은 accessToken은 js private variable에 저장한다.

이러면 refresh token이 CSRF(requset 갈취)에 의해 사용된다 하더라도 공격자는 accessToken을 알수없다.

따라서 쿠키를 사용하여 XSS를 막고(refresh token 접근 X)

refresh token을 request에 담아 accessToken을 받기때문에 CSRF도 막을 수 있다.
```

<br />

### 참고

https://velog.io/@0307kwon/JWT%EB%8A%94-%EC%96%B4%EB%94%94%EC%97%90-%EC%A0%80%EC%9E%A5%ED%95%B4%EC%95%BC%ED%95%A0%EA%B9%8C-localStorage-vs-cookie
