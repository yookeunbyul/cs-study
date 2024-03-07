## CORS란

원래는 다른 출처의 리소스를 사용하는 것을 제안하는 보안 방식이 있다. => SOP(Same Origin Policy)

<img width="666" alt="image (4)" src="https://github.com/yookeunbyul/codingtest-kit/assets/91243651/abed3fe2-6131-46fc-9185-1898e43d28b6">

출처란, URL에서 Protocol, Host, Port를 합친 것을 말한다.

프로토콜의 HTTP는 80번, HTTPS는 443번 포트를 사용하는데, 80번과 443번 포트는 생략이 가능하다.

만약 현재 웹 페이지가 https://velog.io면

| URL                                | 같은출처 | 이유                      |
| ---------------------------------- | -------- | ------------------------- |
| https://velog.io/write             | O        | Protocal, Host, Port 동일 |
| https://velog.io/write?id=1561ea92 | O        | Protocal, Host, Port 동일 |
| https://velog.io/write#work        | O        | Protocal, Host, Port 동일 |
| http://velog.io/write              | X        | Protocal 다름             |
| https://velog.heroku.io/write      | X        | Host 다름                 |
| https://velog.io:81/write          | X        | Port 다름                 |

<br />

### 그래서 CORS란?

다른 출처의 자원을 공유할 수 있도록 즉 **외부 리소스를 안전하게 사용**할 수 있도록 해주는 체제이다.

브라우저는 SOP(동일 출처 정책)을 지키고 있기 때문에 다른 출처의 리소스 접근을 금지하고있다.

만약 아무데나 데이터를 요청할 수 있게 된다면, 다른 사이트에서 원래 사이트를 흉내낼 수 있게 된다. 세션 또는 토큰을 탈취해서 악의적으로 정보를 꺼내오거나 해킹을 할 수도 있다.

우리가 API를 요청할 때 보는 오류는 CORS 정책을 위반할 때 발생한다.

<br />

### CORS 동작 원리

기본적으로 다른 출처의 리소스를 요청할 때는 HTTP 프로토콜을 사용하여 요청을 보내게 되는데, 이때 브라우저는 요청 헤더에 Origin이라는 필드에 요청을 보내는 출처를 함께 담아보낸다.

```
Origin: https://velog.io
```

이후 서버가 이 요청에 대한 응답을 할 때 응답 헤더의 Access-Control-Allow-Origin이라는 값에 **이 리소스를 접근하는 것이 허용된 출처**를 내려주고 이후 응답을 받은 브라우저는 자신이 보냈던 요청의 Origin과 서버가 보내준 응답의 Access-Control-Allow-Origin을 비교해본 후 이 응답이 유효한 응답인지 아닌지를 결정한다.

- Simple Request

  단순 요청은 서버에 API를 요청하고, 서버는 Access-Control-Allow-Origin 헤더를 포함한 응답을 브라우저에 보낸다. 브라우저는 Access-Control-Allow-Origin 헤더를 확인해서 CORS 동작을 수행할지 판단한다.

  특정 조건을 만족하는 경우에만 예비 요청을 생략할 수 있다. **그러나 이 조건들이 까다로워서 일반적인 방법으로 웹 어플리케이션 아키텍처를 설계하게 되면 거의 충족시키기 어려운 조건들이다.**

  - 요청의 메소드는 GET, HEAD, POST 중 하나여야 한다.

  - Accept, Accept-Language, Content-Language, Content-Type, DPR, Downlink, Save-Data, Viewport-Width, Width를 제외한 헤더를 사용하면 안된다.

  - 만약 Content-Type를 사용하는 경우에는 application/x-www-form-urlencoded, multipart/form-data, text/plain만 허용된다.

<br />

- Preflight request

  프리플라이트 방식은 서버에 예비 요청을 보내서 안전한지 판단한 후 본 요청을 보내는 방법이다. 브라우저는 예비 요청과 본 요청으로 나누어서 서버로 전송한다.

  예비요청을 preflight라고 부르는 것이며, 이 예비 요청에는 **HTTP 메소드 중 OPTIONS 메소드가 사용된다.**

  우리가 자바스크립트의 fetch API를 사용하여 브라우저에게 리소스를 받아오라는 명령을 내리면 브라우저는 서버에게 예비 요청을 먼저 보내고, 서버는 이 예비 요청에 대한 응답으로 현재 자신이 어떤 것들을 허용하고, 어떤 것들을 금지하고 있는지에 대한 정보를 응답 헤더(Access-Control-Allow-Origin)에 담아서 브라우저에게 다시 보내주게 된다.

  이후 브라우저는 자신이 보낸 예비 요청과 서버가 응답에 담아준 허용 정책을 비교한 후, 이 요청을 보내는 것이 안전하다고 판단되면 같은 엔드포인트로 다시 본 요청을 보내게 된다. 이후 서버가 이 본 요청에 대한 응답을 하면 브라우저는 최종적으로 이 응답 데이터를 자바스크립트에게 넘겨준다.

<br />

- Credentialed Request

  인증된 요청을 사용하는 방법이다. 다른 출처 간 통신에서 좀 더 보안을 강화하고 싶을 때 사용하는 방법이다. 브라우저의 쿠키 정보나 인증과 관련된 정보를 요청에 담을 수 있게 해주는 옵션이 바로 credentials 옵션이다.

  | 옵션 값              | 설명                                           |
  | -------------------- | ---------------------------------------------- |
  | same-origin (기본값) | 같은 출처 간 요청에만 인증 정보를 담을 수 있다 |
  | include              | 모든 요청에 인증 정보를 담을 수 있다           |
  | omit                 | 모든 요청에 인증 정보를 담지 않는다            |

  만약 same-origin이나 include 와 같은 옵션을 사용하여 리소스 요청에 인증 정보가 포함된다면, 이제 브라우저는 다른 출처의 리소스를 요청할 때 단순히 Access-Control-Allow-Origin 만 확인하는 것이 아니라 좀 더 빡빡한 검사 조건을 추가하게 된다.

<br />

### CORS 에러 해결 방법

에러가 나는 건 CORS를 사용할 수 있도록 서버가 응답 헤더에 필요한 값을 넣어서 보내지 않았기 때문이다.

그렇기에 서버에서 Access-Control-Allow-Origin 헤더를 포함한 응답을 브라우저에 보내는 방식으로 CORS 에러를 해결할 수 있다.

#### HTTP 응답 헤더

- Access-Control-Allow-Origin

  Access-Control-Allow-Origin 헤더에 작성된 출처에서만 브라우저가 리소스를 접근할 수 있도록 허용한다.

  - 사용 방법

  아래와 같이 응답 헤더가 작성되었다면 https://velog.io 페이지에서 브라우저는 서버 응답으로 온 리소스를 접근할 수 있다.

  ```
  Access-Control-Allow-Origin: https://velog.io
  ```

  아래와 같이 \*(와일드 카드)가 작성되었다면, 브라우저는 출처에 상관없이 모든 리소스에 접근할 수 있다.

  ```
  Access-Control-Allow-Origin: *
  ```

이 외에도 다양한 응답 헤더가 있고..

#### 또다른 방법 : Proxy

프론트엔드와 백엔드 사이에 대신 통신을 받아 주는 프록시 서버를 둬서 CORS를 해결할 수도 있다.

```
module.exports = {
  devServer: {
    proxy: {
      '/api': {
        target: 'https://api.hoo00nn.com',
        changeOrigin: true,
        pathRewrite: { '^/api': '' },
      },
    }
  }
}
```

/api 로 시작하는 URL로 보내는 요청에 대해 브라우저는 localhost:8000/api 로 요청을 보낸 것으로 알고 있지만, 사실 뒤에서 웹팩이 https://api.hoo00nn.com 으로 요청을 프록싱해주기 때문에 마치 CORS 정책을 지킨 것처럼 브라우저를 속이면서도 우리는 원하는 서버와 자유롭게 통신을 할 수 있다.

<br />

### 참조

https://velog.io/@hoo00nn/CORSCross-Origin-Resource-Sharing-%EB%9E%80

https://velog.io/@pwk921110/CORS%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80
