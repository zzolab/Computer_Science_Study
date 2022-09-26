# 2.2.2 PDU(Protocol Data Unit)

## 1. PDU란?
__Brief__
- 동일한 계층 사이에서 처리하는 한 덩어리의 데이터 단위

__Specific__
- `TCP/IP 4계층` or `OSI 7계층` 등 계층화된 구조에서
- 1가지의 `프로토콜`과 관련되어
   - 같은 계층에 존재하는 두 통신 개체 간에(Peer-to-Peer) 서로 주고 받게 되는
   - *헤더(제어정보) 및 데이터(SDU, Payload)가 합쳐진 캡슐화된 운반체(패킷, 프레임 등)
      * 해당 계층에서만 처리되는 특정한 *헤더를 붙이게 됨

## 2. PDU 구성
- 제어 관련 정보들이 포함된 `헤더` + 데이터를 의미하는 `페이로드`

   - PCI (Protocol Control Unit)  :  헤더 정보
      - 발신지 주소, 수신지 주소, 순서 번호, 오류검출용 FCS 등
   - SDU (Service Data Unit)      :  실제 사용자 정보

- PCI + SDU -> PDU : `캡슐화(Encapsulation)`
- PDU -> PCI + SDU : `비캡슐화(Decapsulation)`

![image](https://user-images.githubusercontent.com/89024993/192349010-254f9eca-608d-4049-91e9-733512e2dbe4.png)

![image](https://user-images.githubusercontent.com/89024993/192349027-9871f9ef-cb9e-4d1a-a3b3-c8633825804d.png)
Protocol Header Processing for Transmission by Layer N

![image](https://user-images.githubusercontent.com/89024993/192349099-a4ce004d-b657-41ad-9c69-639280905c2f.png)
Protocol Header Processing on Reception by Layer N


### (참고) PDU vs. SDU

   ㅇ PDU (Protocol Data Unit)
     - 동일 통신계층(즉, Peer-to-Peer) 간에 운반(교환)되는 전체 데이터량 (실제데이터 + 운반수단)

  ㅇ SDU (Service Data Unit)
     - 상향/하향 두 통신 계층 간에 전달되는 실제 정보 (실제 데이터 단위량)
        
     * SDU가 PDU화 하기 위해, 쪼개지거나(Fragment) 합쳐질 수(Aggregation) 있음

## 3. 계층별 PDU 명칭

계층마다 부르는 명칭이 다름
- 애플리케이션 계층 : `메시지` / `데이터`
- 전송 계층 : `세그먼트`(TCP), `데이터그램`(UDP)
- 인터넷 계층 : `패킷`
- 링크 계층 : `프레임`(데이터 링크 계층), `비트`(물리 계층)


ex1. 데이터링크 계층의 이더넷 = 이더넷 프레임

ex2. 네트워크 계층의 IP = IP 패킷


![image](https://user-images.githubusercontent.com/89024993/192349360-9fa24bf4-a9aa-4192-88e2-341082816862.png)


## 4. 기타 특징

- PDU 제일 아래 계층인 비트로 송수신 하는 것이 모든 PDU 중 가장 빠르고 효율적


- 애플리케이션 계층은 문자열 기반으로 송수신
   - 헤더에 authorization 값 등 다른 값들을 넣는 확장 용이


## 5. 실습

- curl 명령을 통한 PDU 테스팅 : https://reqbin.com/curl
- curl www.googl.com
![image](https://user-images.githubusercontent.com/89024993/192350628-9993c5b4-f110-49bd-8903-387d6767e755.png)
