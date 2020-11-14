﻿# Socket(소켓)

네트워크상에서 동작하는 프로그램 간 `통신의 종착점`(Endpoint), 소켓을 통해 클라이언트와 서버 프로그램 사이에 `데이터를 송수신` 할 수 있다.
<br>

## Socket 통신
<br>

### Server Socket (서버 소켓)
`서버 프로그램에서 사용하는 소켓`, 클라이언트로부터 연결요청이 오기를 기다렸다가 연결요청이 들어오면 클라이언트와 연결을 맺고 데이터를 주고 받는다.
<br>

### Client Socket (클라이언트 소켓)
`클라이언트 프로그램에서 사용하는 소켓`, 서버로 연결 요청 및 데이터를 주고 받는 역할을 한다.
<br>

### Flow

<img src="https://user-images.githubusercontent.com/46274903/99140129-3911bd80-2682-11eb-991b-91cf32588014.png " width="450"  height="450">

<br>

1. 서버 소켓과 클라이언트 소켓을 만듬. (***socket()***)

2. ip와 port 번호 설정. (***bind()***)
3. 클라이언트 연결을 기다림. (***listen()***)
4. 클라이언트 소켓은 설정된 ip와 port 번호에 통신 요청. (***connect()***)
5. 서버 소켓은 클라이언트 소켓의 연결을 수락. (***accept()***)
6. 포트를 통해 데이터를 주고 받음. (***read()*** / ***write()***)
7. 통신을 끝냄 (***close()***)