## OAuth

- OAuth란?

  - Google 로그인 기능을 떠올리면 간단하다.

  - SNS 간편 로그인 기능을 제공한다. => 예를 들어, Google 비밀번호를 제공하지 않고도 나의 서비스가 사용자로부터 어떠한 **토큰 정보**만을 받아서 그것을 구글에 보내주면 계정에 대한 일부 정보를 알아낼 수 있도록 해주는 방식이다.

- Access Token 이용하기

  - Access Token을 이용하여 사용자가 설정한 권한에 대해서만 Google 정보에 접근할 수 있도록 하자.

  - 모든 정보가 아니라 필요한 일부 정보만 넘겨준다는 점에서 보안이 좋다.

<br />

- OAuth 2.0 동작 예시 (개발자 = Client 입장에서)

    <img width="829" alt="스크린샷 2024-03-01 161512" src="https://github.com/yookeunbyul/cs-study/assets/91243651/5e6cd5bb-b9ab-4d7e-9d02-58b582284560">

  1. 사용자가 sns 로그인 기능 호출

  2. 개발자인 client가 바로 client id와 Redirect URI를 보내준다.

  3. 그럼 사용자가 이 정보를 가지고 sns api 제공자에게 sns 로그인 페이지를 요청

  4. sns 로그인 페이지를 제공

  5. 기존에 회원가입했던 아이디와 패스워드를 입력해 로그인 수행

  6. 인증 서버가 회원정보를 찾으면 Authorization Code를 사용자에게 전달

  7. 그럼 사용자는 client에게 redirect uri로 Authorization Code 전달

  8. client는 이 코드를 가지고 인증 서버에게 토큰 요청

  9. 토큰을 발급해주면 또 이 토큰을 가지고 resource sever에 회원 정보 요청

  10. 요청된 자원 전달

  11. 해당 회원 정보를 받아서 회원가입, 로그인 기능을 수행하여 실질적인 서비스를 제공한다.
