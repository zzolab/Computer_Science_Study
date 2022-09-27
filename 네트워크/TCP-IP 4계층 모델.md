## 인터넷이란 무엇인가?
   
전 세계에 걸쳐 파일 전송 등의 데이터 통신 서비스를 받을 수 있는 컴퓨터 네트워크의 시스템
데이터를 막 주고 받는 게 아니라 어떤 규율을 따라야 한다. 이를 프로토콜이라고 한다.
ex) 전화를 받으면 “여보세요?” 하고 받는 게 규율이다.
   
인터넷은 너무도 복잡한 세계이다. 통신이 이루어지는 데 필요한 프로토콜은 매우 많다.
   
![image](https://user-images.githubusercontent.com/59358570/192132062-a2271420-b9e3-4980-a42c-16ba44190282.png)
   
   
## 프로토콜은 누가 규정하는가?
   
네트워크 프로토콜 = 다른 장치들끼리 주고받기 위해 설정된 공통된 인터페이스
IEEE라는 표준화 단체가 정함
   
ex) IEEE802.3 = 유선 LAN 프로토콜
    HTTP = 노드들이 웹 서비스를 기반으로 데이터를 주고 받음
   
   
## TCP/IP (Internet Protocol Suite, 인터넷 프로토콜 스위트)  
   
인터넷에서 컴퓨터들이 서로 정보를 주고 받는 데 쓰이는 프로토콜의 집합
TCP와 IP를 함께 지칭하는 말이니 풀어서 생각해보자.
   
TCP는 전송 제어 프로토콜이다. (Transmission Control Protocol) ⇒ 신뢰성 높은 데이터 송수신을 보장!  
   
IP는 인터넷 프로토콜이다. (Internet Protocol) ⇒ IP주소 체계   
- IPv4  
- IPv6  
   
TCP를 기반으로 한 수많은 애플리케이션이 IP위에서 동작한다. 그래서 TCP/IP를 묶어서 지칭하는 것이다.  
   
   
## TCP/IP의 4개의 계층
TCP/IP계층에는 4개의 추상화된 계층이 존재한다.
일단 무엇이 있는지만 간단히 살피고 가자.
    
   
### 애플리케이션 계층
![image](https://user-images.githubusercontent.com/59358570/192407373-fb6390ab-d0f2-4c83-b19b-72d7c473cd8e.png)

특정 서비스를 제공하기 위해 애플리케이션끼리 정보를 주고 받게 해줌.  
   
FTP, HTTP, SSH, Telnet, SMTP, DN
   
   
### 전송 계층
![image](https://user-images.githubusercontent.com/59358570/192132145-9b3917e7-40e9-448e-b434-c926bb347fcf.png)

송신된 데이터를 수신측 애플리케이션에 확실히 전달하게 해줌.  
   
TCP, UDP, RTP, RTCP, QIC
   
   
### 인터넷 계층
![image](https://user-images.githubusercontent.com/59358570/192132152-e33eedd9-ba7e-4515-8e1b-be098fafe9f6.png)

수신 측까지 데이터를 전달하기 위해 사용됨.  
   
IP, ARP, ICMP, RARP, OSPF
   
   
### 링크 계층

네트워크에 직접 연결된 기기 간 전송을 할 수 있도록 함.  
   
Ethernet, PPP, Token Ring
   
   
# 4계층 상세
![image](https://user-images.githubusercontent.com/59358570/192132174-e9584f7f-2083-4521-93ea-a6ef054012c5.png)

## TCP와 UDP
![image](https://user-images.githubusercontent.com/59358570/192132314-3f6d8191-4ddd-4b43-a969-5703e12e7681.png)
  
  
## 세그먼트란?
![image](https://user-images.githubusercontent.com/59358570/192132177-8a70cbf1-8cda-4b5d-ac7a-16a83910a02a.png)
  
  
## 3웨이 핸드셰이킹
![image](https://user-images.githubusercontent.com/59358570/192132184-37945e56-359e-4424-942b-940a16a9c733.png)
  
  
## 4웨이 핸드셰이킹
![image](https://user-images.githubusercontent.com/59358570/192132189-bb69c096-c869-4c24-8e33-546c45d1fae1.png)
  
## 패킷
![image](https://user-images.githubusercontent.com/59358570/192132195-68fdb34a-57d8-4f7b-a0f3-a892e0c9d10b.png)
  
## 프레임
![image](https://user-images.githubusercontent.com/59358570/192132204-f0e896e8-90e2-40b5-9386-1ade764a5fc3.png)
  
## 4계층 다시 보기
![image](https://user-images.githubusercontent.com/59358570/192132215-4ebcecf7-facc-4607-a2b4-d104db90753a.png)
  
   
## 데이터 통신이란
![image](https://user-images.githubusercontent.com/59358570/192132222-3b432fe7-c3e9-48c3-92a1-a0adcf2d32d1.png)
이 과정을 선을 통해서 하면 유선통신, 선이 없으면 무선통신
한 방향으로 이루어지면 단방향, 양방향인데 동시에 못하면 반이중, 동시에 가능하면 전이중
  
## 통신의 유형
![image](https://user-images.githubusercontent.com/59358570/192132236-e693f669-cefc-4293-a5dc-6f68bb47426d.png)
  
## CSMA/CA
반이중화 통신 중 하나로, 데이터 송/수신 간 충돌을 방지하는 방식을 사용한다.
1) 데이터 송신 전 무선 매체 살핌
2) 캐리어 감지 : 회선이 비어있는가?
3) IFS(Inter FrameSpcae) 랜덤한 시간만큼 기다림, 만약 무선 매체가 사용중이면 그 간격을 늘려가면서 기다림
4) 회선이 사용 가능하면 데이터 송신

## 무선 통신 기술
- wifi : 전자기기들이 무선 LAN 신호에 연결할 수 있게 하는 기술. 무선 접속 장치(AP, 공유기)가 있어야 함. 
- BSS(Basic Server Set) : 동일 BSS 내에 있는 AP 장치들이 서로 통신 가능한 구조. 근거리 무선 통신 제공, 하나의 AP만을 기반으로 구축 => 사용자 이동 제약
- ESS(Extended Service Set) : 하나 이상의 연결된 BSS그룹. 장거리 무선 통신 제공, 더 많은 가용성, 이동성 지원
