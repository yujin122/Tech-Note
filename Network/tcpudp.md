# TCP / UDP
<br/>

# TCP (Transmission Control Protocol)
서버와 클라이언트 간에 데이터를 `신뢰성` 있게 전달하기 위해 만들어진 프로토콜
<br/><br/>

### 특징
1. **1:1 통신**

2. **신뢰성** <br/>
패킷이 전송된 것을 보장하기 위해 `확인응답(ACK)를 사용`하여 상대편에서 데이터를 받았다는 ACK를 보내지 않으면 다시 데이터를 보낸다.
3. **흐름제어 / 혼잡제어**
- 흐름제어
	-	송신측에서 데이터를 보내는 속도가 수신측에서 데이터를 받는 속도보다 빠를 때 처리하는 제어방법 <br/><br/>
Ⅰ. **stop and wait** 방식 : 확인 응답을 받아야 다음 데이터를 받는 방식 <br/><br/>
Ⅱ. **sliding window** 방식 : 수신측에서 설정한 윈도우 크기만큼 송신측에서 확인 응답 없이 세크먼트를 전송, 데이터 흐름을 동적으로 조절하는 방식 <br/>

- 혼잡제어
	- 송신측의 데이터 전달과 네트워크의 처리속도 차이를 해결하기 위한 기법 
	
  -	상대가 데이터를 받았을 경우 보내는 데이터의 양을 점차 늘려 보내다가 상대가 데이터를 받지 못한 경우 보내는 양을 확 줄인다.

4. **연결형 서비스** <br/>
데이터를 전송하기 전에 연결 설정을 해야한다.

5. **양방향 전송** <br/>
데이터를 동시에 양쪽 방향으로 전송할 수 있다.
6. **3 way handshake / 4 way handshake**
<br/>

## 3 way handshake / 4 way handshake

SYN(synchronize sequence numbers) , ACK(acknowledgements)
<br/><br/>

### 3 way handshake
#### <연결 설정>

<img src="https://user-images.githubusercontent.com/46274903/97772399-fb913880-1b89-11eb-9a55-bdffacec786f.png " width="400"  height="">

1. 클라이언트는 서버에 접속요청(SYN)을 전송
2. 서버는 요청 수락(SYN, ACK)을 전송
3. 클라이언트는 요청을 잘 받았다는 ACK를 서버에 전송, 서버의 상태는 ESTABLSHED(연결완료) 상태
<br/>

### 4 way handshake
#### <연결해제>

<img src="https://user-images.githubusercontent.com/46274903/97772451-b4577780-1b8a-11eb-8dc7-5bf4affec963.png " width="400"  height="">

1. 클라이언트가 연결을 종료하겠다는 [FIN,ACK]를 서버에 전송
2. 서버는 확인 메시지 ACK를 보내고 통신이 끝날때까지 TIME_WAIT상태
3. 서버통신이 끝났으면 연결이 종료되었다고 클라이언트에게 FIN 전송
4. 클라이언트는 확인 메시지 ACK 전송, 연결 해제.
<br/>

## TCP 헤더

<img src="https://user-images.githubusercontent.com/46274903/97772563-c259c800-1b8b-11eb-8669-4e0c0467f5fe.png " width="450"  height="">

- ***Source Port | Destination Port*** : 송신 포트 | 수신 포트
- ***Sequence Number*** :  데이터를 여러 개의 패킷으로 나누는데 이때 수신자가 데이터를 받고 순서대로 재조립 할 수 있도록 `데이터의 순서`를 알려줌 
- ***Acknowledgment Number*** : 수신자가 예상하는 다음 시퀀스 번호
- ***Window Size*** : 한번에 전송할 수 있는 데이터의 양
- ***Checksum*** : 데이터 송신 중 발생할 수 있는 오류 검출을 위한 값
<br/><br/>

# UDP (User Datagram Protocol)
비연결형, `신뢰성 없는` 전송 프로토콜
<br/>

### 장점
처리속도와 데이터 전송률이 빠름
- 온라인 게임, 실시간 방송, 스트리밍 서비스에 주로 이용
<br/>

## UDP 헤더

<img src="https://user-images.githubusercontent.com/46274903/97772711-ed90e700-1b8c-11eb-8f75-907447dc16ed.png " width="450"  height="">

- ***Source Port | Destination Port*** : 송신 포트 | 수신 포트
- ***Length*** : 헤더 + 데이터, 가변적
- ***Checksum*** : 데이터 송신 중 발생할 수 있는 오류 검출을 위한 값
