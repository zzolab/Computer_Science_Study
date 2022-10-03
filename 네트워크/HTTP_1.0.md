# HTTP : HyperText Transfer Protocol

- 최상위 '애플리케이션 계층'에서 이뤄짐
- W3(World Wide Web)상에서 정보를 주고받는 프로토콜
- Client와 Server가 사이에서 이루어지는 요청/응답 프로토콜
- 연결 방식
    - HTTP/2 까지
        - TCP 연결 기반 위에서 동작
    - HTTP/3 이후
        - UDP 사용


## 그전에! HTTP/0.9
- From 1991
- GET 메소드만 가능
- HTTP Header가 없어서 HTML 문서만 전송 가능
    - 다른 유형의 문서 전송 불가
- 상태 or 오류 코드 없음
    - 문제 상황 시 해당 파일 내부에 문제에 대한 설명을 추가하여 보냄


![image](https://user-images.githubusercontent.com/89024993/193588221-c72e1159-8c43-45b5-8def-f20b0d82d5a9.png)

<br>

## 2.5.1 HTTP/1.0

- From 1996
- POST, HEAD 메소드 추가 됨
- 상태코드가 응답 첫 줄에 포함
    - 요청에 대한 성공/실패 여부를 바로 확인 가능
- HTTP Header 추가
    - Header의 'Content-Type' 기능으로 HTML 파일 이외의 다른 문서도 전송 가능
- 한 연결당 하나의 요청을 처리하도록 설계됨
    - TCP Connection당 하나의 URL만 fetch하며, 매번 request/response가 끝나면 연결이 끊김
    - 필요할 때마다 다시 연결해야하는 단점이 있어 속도가 현저히 느림

![image](https://user-images.githubusercontent.com/89024993/193588704-2bf41118-233f-4eaf-a449-b2abaa7a1c52.png)


### RTT 증가 이슈

- 서버로부터 파일을 가져올 때마다 TCP의 3-웨이 핸드세이크를 계속 열어야 함
- RTT가 증가하는 단점
    - 서버에 부담이 많이 감
    - 사용자 응담 시간이 길어짐

> `RTT` : 패킷이 목적지에 도달하고 나서 다시 출발지로 돌아오기까지 걸리는 시간, (Round Trip Time, 왕복 시간)

![image](https://user-images.githubusercontent.com/89024993/193589410-536a40d6-90c0-4339-abed-4d62ba3b3f1a.png)


### RTT 증가를 해결하기 위한 방법

- 스플리팅, 코드 압축, 이미지 Base64 인코딩 등등

#### 1. 이미지 스프라이트(Image Sprite)

- 여러 개의 이미지를 하나의 이미지로 합쳐서 관리하는 것
- 웹 페이지에 이미지가 사용된다?
    - 해당 이미지를 다운받기 위해 웹 브라우저는 서버에 이미지를 요청
    - 사용된 이미지가 많을 경우 웹 브라우저는 서버에 해당 이미지의 수만큼 요청해야 함
    - 웹 페이지의 로딩 시간이 오래 걸리는 단점

- 이미지를 다운받기 위한 서버 요청 줄일 수 있음
- 몇 개의 스프라이트 이미지(sprite image) 파일만을 관리하면 되는 장점


![image](https://user-images.githubusercontent.com/89024993/193591216-4728bf6c-83e0-417e-8c1f-f5c25e6dedbe.png)


#### 2. 코드 압축

- 소스 코드 양이 많아질수록 로딩이 점점 느려지는 단점 해결
- 개행 문자, 빈칸 등을 없애서 코드 용량을 최소화 하는 것
- 실습 사이트 : https://refresh-sf.com/

![image](https://user-images.githubusercontent.com/89024993/193591764-7915b36a-d914-4e6f-8625-af5c28697f63.png)
![image](https://user-images.githubusercontent.com/89024993/193591796-ec22a9f7-28eb-4c85-ba82-cb391e640050.png)


#### 3. 이미지 Base64 인코딩

- Base64
    - 이미지 파일을 64진법으로 이루어진 문자열로 인코딩하는 방법
    - 전자 메일(SMTP)을 통한 이진 데이터 전송 등에 많이 쓰임
- 원리
    - src에 url을 사용하면 그 url에서 이미지를 받아와야 해서 추가적인 http 요청이 필요
    - base64 인코딩을 해서 html 출력에 직접 '문자열'로 넣어서 추가적인 요청을 안하도록 함

- 장점
    - 서버와의 연결을 열고 이미지에 대해 서버에 HTTP 요청을 할 필요 없음
- 단점
    - 인코딩으로 33-36% 오버헤드(용량 증가) 발생 단점
- 실습 사이트 : https://www.base64-image.de/

> `인코딩` : 정보의 형태나 형식을 표준화, 보안, 처리 속도 향상, 저장 공간 절약 등을 위해 다른 형태나 형식으로 변환하는 것
