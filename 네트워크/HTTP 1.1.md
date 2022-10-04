# HTTP 1.1 
HTTP 1.0에서 진화한 형태! 1997년 발표되었다.
<br/><br/>
## HTTP 1.0과 HTTP 1.1의 비교
HTTP는 Connectionless 방식으로 연결을 매번 끊고 새로 생성하는 구조이다.   
이는 Network 비용 측면에서 최초 연결을 하기 위해 많은 비용을 소비하는 구조이다.   
   
HTTP/1.1부터는 이미 연결되어 있는 TCP 연결을 재사용하는 Keep-Alive라는 기능을 Default로 지원한다.   
중간중간마다 거쳐야 하는 Handshake 과정이 생략되므로 성능 향상을 기대 할 수 있다.
   
하지만 문서 안에 포함된 다수의 리소스(이미지, CSS파일, SCRIPT파일)를 처리하려면 요청할 리소스 개수에 비례해서 대기 시간이 길어진다.
<br/><br/>

## HOL Blocking  
Head Of Line Blocking.   
네트워크에서 같은 큐에 있는 패킷이 그 첫번 째 패킷에 의해 지연될 때 발생하는 성능 저하 현상
![image](https://user-images.githubusercontent.com/59358570/193714281-ac1fb5a3-a5cb-4e78-8852-b0e6f2818433.png)

<br/><br/>

## 무거운 헤더 구조  
HTTP 1.1의 헤더에는 쿠키 등의 많은 메타데이터가 들어가 있고 압축이 되지 않아 무거웠다.

   
## 이러한 단점들을 해결하기 위한 노력
### 이미지 스프라이팅   
Image Spriting 아이콘을 하나의 큰 이미지 파일로 만들어, 아이콘 이미지 파일 요청 횟수 자체를 줄이는 방식이다. 
CSS에서 해당 이미지 파일의 아이콘 좌표 값을 이용하여 표현한다. 
   
### Domain Sharding 
다수의 Connection을 사용하여 병렬로 요청한다. 브라우저 별로 Connection 개수 제한이 존재한다. 
   
### Minify CSS/javascript
CSS, Javascript 소스코드를 축소하여 전달한다.
   
### Data URI Scheme 
Data URI Scheme은 HTML문서내 이미지 리소스를 Base64로 인코딩된 이미지 데이터로 직접 기술하는 방식이고 이를 통해 요청 수를 줄이기도 한다.
   
### Load Faster
스타일시트를 HTML 문서 상위에 배치 스크립트를 HTML문서 하단에 배치
   
      
## SPDY(speedy)의 등장   
Google은 Latency 관점에서 HTTP를 고속화한 SPDY라는 새로운 프로토콜을 구현했다.   
HTTP를 대치하는 프로토콜이 아닌, HTTP를 통한 전송을 재정의하는 방식으로 구현되었다.   
따라서 전송 계층의 구현만 변경하면 기존 HTTP 서버 프로그램을 그대로 SPDY에서 사용할 수 있다.   
HTTP2 초안은 Google의 SPDY를 참고하여 만들어지게 된다.   

SPDY는 웹 페이지의 로딩 시간을 줄이기 위한 목적으로 설계되었다.   
이를 위해 SPDY 클라이언트는 하나의 소켓 연결을 통해 페이지를 구성하는 여러개의 하위 요소를 한꺼번에 전송받을 수 있도록 만들어졌다.   
또한 항상 사람이 읽을 수 있는 형태의 헤더를 보내는 HTTP와 달리, SPDY 헤더는 gzip 또는 DEFLATE 알고리즘으로 압축되어 적은 용량을 차지한다.   
   
### 참고자료   
1. [MDN - Evolution of HTTP](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/Evolution_of_HTTP)   
2. [융복 - HTTP 1.1 vs HTTP 2.0](https://ybdeveloper.tistory.com/116#toc-HTTP%202%EC%9D%98%20%ED%83%84%EC%83%9D)
3. 
