## Port Scanning 종류 및 설명



1. TCP Scan(Open Scanning)
   TCP 통신의 3 Way-Handshake을 정상적으로 이용하여 열려있는 포트번호를 알아내는 방법이다.
   Half Scan, Stealth Scan과 다르게 정상적인 방법을 사용하기 때문에 추적당하기 매우 쉽다.
   공격자는 해당서버의 포트번호를 알기 위해 TCP통신을 시도, SYN 메시지를 보내고 서버는 요청한 해당포트가 열려있으면 응답 메시지 SYN/ACK를 전송하며 3 Way Handshake을 수행하고, 열려있지 않다면 RST/ACK 메시지를 전송한다.
2. Syn Scan(Half Scaaning)
   Syn Scan은 3 Way-Handshake의 SYN메시지만 수행하여 열려있는 포트번호를 확인한다.
   공격자가 서버에 SYN 메시지를 보내어 연결 요청을 하면 서버는 해당 포트번호가 열려있을 경우 SYN/ACK를, 닫혀있을 경우 RST/ACK를 보낸다. 공격자는 열려있는 포트번호를 확인 할 수 있고, 3 Way-Handshake의 마지막 단계인 공격자가 서버에게 ACK메시지를 보내지 않고 RST을 보내면서 Scan은 종료된다.

### Stealth Scan

1. FIN Scan
   TCP 패킷의 Flag 정보를 FIN으로 설정하여 공격자는 서버에게 패킷을 전송한다. 서버는 FIN패킷을 받고 해당 포트가 열려있으면 패킷을 Drop시키고 닫혀있으면 RST 패킷을 보내므로 열려있는 포트번호를 확인한다.
2. Null Scan
   TCP 패킷의 Flag 정보에 아무것도 설정하지 않고 공격자는 서버에게 패킷을 전송한다. 서버는 포트번호가 열려있으면 아무응답하지 않고 패킷을 Drop하며, 포트번호가 닫혀있을 경우 RST 메시지를 보낸다.
3. X-Mas Scan
   TCP 패킷의 Flag 정보에 PSH, URG, FIN을 설정하여 서버에게 보낸다.
   다른 Stealth Scan과 마찬가지로 서버는 포트번호가 열려있으면 아무 응답하지 않고, 닫혀있으면 RST 패킷으로 응답한다.