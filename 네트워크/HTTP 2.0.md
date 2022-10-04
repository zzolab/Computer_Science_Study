# HTTP 2.0
![image](https://user-images.githubusercontent.com/59358570/193717342-5d449640-646a-4f77-9c07-3ae1895a0b94.png)   
SPDY 프로토콜에서 파생된 HTTP/1.x보다 지연시간을 줄이고 응답시간을 더 빨리 할 수 있다.

<br/><br/>
## 멀티플렉싱
여러 개의 스트림을 이용하여 송수신하는 것 => HOL Blocking 해결
HTTP/1.1의 Connection Keep-Alive, Pipelining의 개선했다.

## Stream Prioritization   
클라이언트가 요청한 HTML문서 안에 CSS파일 1개와 Image파일 2개가 존재하고   
이를 클라이언트가 각각 요청하고 난 후 Image파일보다 CSS파일의 수신이 늦어지는 경우   
브라우저의 렌더링이 늦어지는 문제가 발생하는데   
HTTP/2의 경우 리소스간 의존관계(우선순위)를 설정하여 이런 문제를 해결했다.   

<br/><br/>
## 헤더 압축
허프만 코딩 압축 알고리즘을 삭용하여 HPACK으로 헤더를 압축
<br/><br/>
### 허프만 코딩(Huffman coding)
![image](https://user-images.githubusercontent.com/59358570/193718307-738c273f-0d42-43ee-809f-1c1ba4f90534.png)   
(... 중략 ...)
![image](https://user-images.githubusercontent.com/59358570/193718204-eaa0d97b-fe9a-4239-b068-2fbcfdc70103.png)   
문자열을 문자 단위로 쪼개 빈도수를 세어 빈도가 높은 정보는 적은 비트 수를 사용하여 표현하고 빈도가 낮은 정보는 비트 수를 많이 사용하여 표현해서 전체 데이터의 표현에 필요한 비트 양을 줄이는 원리
<br/><br/>

## 서버 푸시 
Server Push 서버는 클라이언트의 요청에 대해 요청하지도 않은 리소스를 보내줄 수 있게 되었다.   
클라이언트(브라우저)가 HTML문서를 요청하고 해당 HTML에 여러 개의 리소스(CSS, Image...) 가 포함되어 있는 경우   
HTTP/1.1에서 클라이언트는 요청한 HTML문서를 수신한 후 HTML문서를 해석하면서 필요한 리소스를 재 요청하는 반면   
HTTP/2에서는 Server Push기법을 통해서 클라이언트가 요청하지 않은 (HTML문서에 포함된 리소스) 리소스를 Push 해주는 방법으로   
클라이언트의 요청을 최소화 해서 성능 향상을 이끌어 냈다.   
PUSH_PROMISE 라고 부르며 PUSH_PROMISE를 통해서 서버가 전송한 리소스에 대해선 클라이언트는 요청을 않는다.   
 
[참고자료]
1. [ziyoonee - HTTP/1부터 HTTP/3까지 알아보기](https://velog.io/@ziyoonee/HTTP1-%EB%B6%80%ED%84%B0-HTTP3-%EA%B9%8C%EC%A7%80-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0)
2. [동빈나 - 허프만 코드](https://www.youtube.com/watch?v=haXz9MEOGbo)
