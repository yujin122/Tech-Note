# 쿠키(cookie) / 세션(session)
<br>

## 쿠키와 세션을 사용하는 이유?
`HTTP 프로토콜`의 Connectionless 와  Staeless 특성 때문에 서버는 클라이언트가 누구인지 확인을 해야한다. 이러한 `문제점을 보완`하기 위해 사용한다.
<br>

**Connectionless**

클라이언트 요청 응답 후 연결을 끊어버리는 특성

**Stateless** 
연결이 끝나면 상태를 유지하지 않는 특성
<br>

## 쿠키(cookie)
브라우저를 사용하는 `클라이언트 환경`에 서버에서 받은 `데이터를 저장`한 파일

- 다시 서버에 request 할 필요가 없기 때문에 속도가 빠름.

- 클라이언트 PC에 저장되는 정보이기 때문에 다른 사용자에 의해 임의로 변경이 가능.
- 보안 문제를 신경써야함.
- 유효시간을 명시할 수 있고, 웹이 종료되어도 유효 시간까지 인증 유지.

### 동작순서

<img src="https://user-images.githubusercontent.com/46274903/98435553-41fd0f00-2117-11eb-9c47-6fa1a8edd310.png " width="600"  height="">

<br>

## 세션(session)
`서버`에서 유저의 인증상태를 임시로 `저장`한 파일

- 서버에 저장되어 있어 쿠키보다 다소 느리고 유저정보가 많을 경우 메모리 과부하가 생길 수 있음.

- 서버에 저장해두기 때문에 쿠키보다 보안이 우수함.
- 클라이언트를 종료할 때까지 인증상태 유지

### 동작순서
<img src="https://user-images.githubusercontent.com/46274903/98435556-4cb7a400-2117-11eb-8b35-0e0ddbe933ed.png" width="600"  height="">


##### [참고]
[1](https://noahlogs.tistory.com/38) [2](https://bangu4.tistory.com/29)

