## 19.1 네트워크 기초
- 네트워크: 여러 컴퓨터들을 통신 회선으로 연결한 것
- LAN(Local Area Network): 가정, 회사, 건물, 특정 영역에 존재하는 컴퓨터를 연결
- WAN(Wide Area Network): LAN을 연결한 것. 인터넷
- IP(Internet Protocol)
  - 컴퓨터의 고유한 주소
  - 네트워크 어댑터(LAN 카드)마다 할당
- Port 번호
  - 운영체제가 관리하는 서버 프로그램의 연결번호
    ![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/ba2e9757-dd84-4171-800b-c51eeaed1b02)

## 19.2 IP 주소 얻기
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/610a4db1-9f14-43b2-8596-8ac2fa621a52)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/6340e6da-b494-4036-9395-76b16a20d135)

## 19.3 TCP 네트워킹
IP 주소로 프로그램들이 통신할 때는 약속된 데이터 전송 규약이 있다.
- TCP(Transmission Control Protocol)
  - 연결형 프로토콜
  - 상대방이 연결된 상태에서 데이터를 주고 받는다.
  - 웹 브라우저가 웹 서버에 연결할 때 사용
  - TCP 네트워킹을 위해 java.net 패키지에서 ServerSocket과 Socket 클래스를 제공
  - ServerSocket: 클라이언트의 연결을 수락하는 서버 쪽 클래스
  - Socket: 클라이언트에서 연결 요청할 때 클라이언트와 서버 양쪽에서 데이터를 주고 받을 때 사용되는 클래  
- UDP(User Datagram Protocol)
