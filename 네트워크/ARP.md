# 용어 정리
- IP 주소 :인터넷에 연결된 기기를 식별하는 유일한 번호로, 다음과 같이 4개의 10진수 형태로 구성
- MAC 주소 : 네트워크에 사용되는 모든 기기의 고유 번호
- ARP(Address Resolution Protocol) : IP 주소로부터 MAC 주소를 구하는 IP와 MAC 주소의 다리 역할을 하는 프로토콜
- RARP(Reverse Address Resolution Protocol) : MAC 주소를 IP 주소로 변환하는 프로토콜
- 브로드캐스트 : 송신 호스트가 전송한 데이터가 네트워크에 연결된 모든 호스트에 전송되는 방식
- 유니캐스트 : 고유 주소로 식별된 네트워크 목적지에 1:1로 데이터를 전송하는 방식
![브로드캐스트_유니캐스트](https://user-images.githubusercontent.com/90097723/193454554-ddd8c322-7d21-446d-8a1e-e31ed2b62720.png)
- 라우팅 : IP 주소를 찾아가는 과정
- 라우팅 테이블 : 게라우터에 들어가 있는 목적지 정보들과 그 목적지로 가기 위한 방법이 들어있는 리스트
- 게이트웨이 : 서로 다른 통신망, 포르토콜을 사용하는 네트워크 간의 통신을 가능하게 하는 관문 역할을 하는 컴퓨터나 **소프트웨어**를 두루 일컫는 용어
- 네트워크 마스크(=서브넷 마스크, 넷마스크) : IP 주소의 네트워크 부분을 가리거나 걸러서 호스트 컴퓨터의 주소 부분만이 남도록 하기 위해 0과 1이 조합되어 있는 문자열 
- 네트워크 메트릭 : 메트릭은 특정 네트워크 인터페이스에 대한 IP 경로에 할당되는 값 

## 게이트웨이 vs 라우터
- 라우터는 OSI 모델의 물리, 데이터링크, 네트워크 층의 기능 수행장치로 경로를 배정해주는 역할
- 게이트웨이는 OSI 모델의 모든 계층의 기능 수행(프로코톨 변환기)하는 장치. 네트워크 계층 이상에서 LAN간 접속 기능을 수행하는 장치. 라우터를 포괄함.

# 4.1 ARP
- ARP를 통해 가상 주소인 IP 주소를 실제 주소인 MAC 주소로 벼환, RARP를 통해 실제 주소인 MAC 주소를 가상 주소인 IP로 변환
- ARP Request 브로드캐스트를 보내서 IP에 해당하는 MAC 주소를 가진 기기를 찾고 주소가 일치하는 장치가 ARP Reply 유니캐스트로 반응하여 찾게 됨.
- 장점  
  네트워크의 단일 라우터에 추가할 수 있으며 네트워크에 있는 다른 라우터의 라우팅 테이블을 방해하지 않는다
- 단점
  세그먼트에서 ARP 트래픽의 양이 증가
  보안 문제(ARP 스푸핑)-> NDP(주변(인접) 노드들을 발견/탐색/변경검출/유지하기 위한 정보를 요청하거나 제공)로 보안 문제 보완 (이것도 SEND 프로토콜로 추가 보완?)

## 참고자료
[서브넷_마스크_설명_나무위키](https://namu.wiki/w/%EC%84%9C%EB%B8%8C%EB%84%B7%20%EB%A7%88%EC%8A%A4%ED%81%AC)  
[넷마스크_네이버](https://terms.naver.com/entry.naver?docId=830487&cid=42344&categoryId=42344)  
[게이트웨이_라우터_차이](https://puzzle-puzzle.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%9A%A9%EC%96%B4-%EA%B2%8C%EC%9D%B4%ED%8A%B8%EC%9B%A8%EC%9D%B4-Gateway-%EA%B2%8C%EC%9D%B4%ED%8A%B8%EC%9B%A8%EC%9D%B4%EC%99%80-%EB%9D%BC%EC%9A%B0%ED%84%B0-%EC%B0%A8%EC%9D%B4%EC%A0%90)
[APR_RARP](https://luckyking.tistory.com/entry/ARPRARP-%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9CTCPIP-%EC%9D%B8%ED%84%B0%EB%84%B7-%EA%B3%84%EC%B8%B5)  
[용어해설](http://www.ktword.co.kr/test/view/view.php?no=2954)
