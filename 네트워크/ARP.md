# 용어 정리
- IP 주소 :인터넷에 연결된 기기를 식별하는 유일한 번호로, 다음과 같이 4개의 10진수 형태로 구성
- MAC 주소 : 네트워크에 사용되는 모든 기기의 고유 번호
- ARP(Address Resolution Protocol) : IP 주소로부터 MAC 주소를 구하는 IP와 MAC 주소의 다리 역할을 하는 프로토콜
- RARP(Reverse Address Resolution Protocol) : MAC 주소를 IP 주소로 변환하는 프로토콜
- 브로드캐스트 : 송신 호스트가 전송한 데이터가 네트워크에 연결된 모든 호스트에 전송되는 방식
- 유니캐스트 : 고유 주소로 식별된 네트워크 목적지에 1:1로 데이터를 전송하는 방식
![브로드캐스트_유니캐스트](https://user-images.githubusercontent.com/90097723/193454554-ddd8c322-7d21-446d-8a1e-e31ed2b62720.png)

## 게이트웨이 vs 라우터
- 라우터는 OSI 모델의 물리, 데이터링크, 네트워크 층의 기능 수행장치로 경로를 배정해주는 역할
- 게이트웨이는 OSI 모델의 모든 계층의 기능 수행(프로토콜 변환기)하는 장치. 네트워크 계층 이상에서 LAN간 접속 기능을 수행하는 장치. 라우터를 포괄함.

# 4.1 ARP
- ARP를 통해 가상 주소인 IP 주소를 실제 주소인 MAC 주소로 환, RARP를 통해 실제 주소인 MAC 주소를 가상 주소인 IP로 변환
- ARP Request 브로드캐스트를 보내서 IP에 해당하는 MAC 주소를 가진 기기를 찾고 주소가 일치하는 장치가 ARP Reply 유니캐스트로 반응하여 찾게 됨.
- 장점  
  네트워크의 단일 라우터에 추가할 수 있으며 네트워크에 있는 다른 라우터의 라우팅 테이블을 방해하지 않는다
- 단점
  세그먼트에서 ARP 트래픽의 양이 증가  
  보안 문제(ARP 스푸핑)-> NDP(주변(인접) 노드들을 발견/탐색/변경검출/유지하기 위한 정보를 요청하거나 제공)로 보안 문제 보완  
  (이것도 SEND 프로토콜로 추가 보완?)

## 참고자료
[APR_RARP](https://luckyking.tistory.com/entry/ARPRARP-%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9CTCPIP-%EC%9D%B8%ED%84%B0%EB%84%B7-%EA%B3%84%EC%B8%B5)  
[NDP_용어해설](http://www.ktword.co.kr/test/view/view.php?no=2954)
