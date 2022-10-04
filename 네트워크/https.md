# https

## 1. https란?

HTTPS (HTTP Secure) 는 HTTP protocol의 **암호화된 버전**이다.
HTTPS는 대개 클라이언트와 서버 간의 모든 커뮤니케이션을 암호화 하기 위하여
**SSL** 이나 **TLS**을 사용한다. 이는 클라이언트가 민감한 정보를 서버와
안전하게 주고받도록 해준다. 예를들면 금융 활동 이나 온라인 쇼핑이 있을 수 있다.

---

## 2. SSL(Secure Sockets Layer)

Secure Sockets Layer(SSL)는 클라이언트와 서버 간의 안전한 링크를 통해
송수신되는 모든 데이터를 안전하게 보장하는 과거의 보안 표준 기술이었다.
SSL 버전 3.0은 Netscape가 1999년에 발표했으며 현재에는
**Transport Layer Security (TLS)** 로 대체되었다.

---

## 3. TLS(Transport Layer Security)

TLS(Transport Layer Security)는 인터넷 상의 커뮤니케이션을 위한
개인 정보와 데이터 보안을 용이하게 하기 위해 설계되어 널리 채택된 **보안**
프로토콜이다. TLS는 웹 브라우저와 서버 간의 커뮤니케이션을 암호화한다.

TLS는 국제 표준 기구인 IETF(Internet Engineering Task Force)에
의해 제안되었으며 프로토콜의 첫 번째 버전은 1999년에 발표되었다.
가장 최신 버전은 2018년에 발표된 TLS 1.3이다.

TLS는 Netscape가 개발한 SSL(Secure Sockets Layer)이라고
불리는 이전의 암호화 프로토콜에서 발전한 것으로 TLS 버전 1.0은
SSL 버전 3.1로서 개발을 시작했지만 Netscape와 더 이상 연관이
없음을 명시하기 위해 발표 전에 프로토콜의 이름이 변경되었다.
이러한 역사 때문에 용어 TLS와 SSL은 가끔 서로 바꿔서 사용된다.

![SSL/TLS](https://www.lesstif.com/1stb/files/18219486/21561469/1/1406730379000/image2014-7-30+23%3A29%3A18.png)

---

## 4. https가 중요한 이유

### 4-1. 보안성

https가 아닌 http 위에서 네이버에 로그인을 한다고 생각해보자. 나의 비밀번호를 입력을 하게 되면 여러 경로를
거쳐 네이버의 서버에 도달한다. 이때 순간이동을 하여 바로 다이렉트로 네이버 서버로
이동하는 것이 아니라 아래의 사진과 같이 많은 경로를 거쳐 이동하게 된다.

![네이버까지의 통신 과정](https://2158680719-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FtlrW8c4MEVWoel5YVxSk%2Fuploads%2Fgit-blob-21354b7d178be98593e11dd2cf6855c0192da45e%2FHTTPS1.png?alt=media)

이때 문제가 발생한다.

- 중간에 해커가 나의 개인정보를 탈취할 수 있다.
- 나와 요청을 주고 받는 상대가 진짜 네이버인지 알 수 없다.
- 네이버 서버까지 가는 도중 중간에 요청에 대한 내용이 바꿀 수 있다.

![헤커로 부터의 위협](https://2158680719-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FtlrW8c4MEVWoel5YVxSk%2Fuploads%2Fgit-blob-a1e7eb49279c7b1ae01d36c8a1a6e90c5e837303%2Fhttps2.jpg?alt=media)

https는 위와 같은 보안상의 문제를 해결한다. 즉, 클라이언트와 서버 사이에서
주고 받는 요청을 암호화하기 때문에 해커는 암호화 된 요청을 해석할 수 없다.

---

### 4-2. SEO

우리가 흔히 사용하는 검색 엔진 중 하나인 구글은 https 웹 사이트에 가산점을 준다.
자신의 웹 사이트가 검색에 많이 노출되기 위해서는 https는 필수적이다.

---

## 5. 대칭키 VS 공개키/개인키(비대칭키)

SSL/TLS은 대칭키, 공개키/개인키 기반으로 사용된다. 대칭키와 공개키/개인키는 암호화,
복호화를
위해 사용되는 방법으로 SSL/TLS는 이 중 하나의 방법만 사용하는 것이 아니라
두 개의 방법을 모두 혼합하여 사용한다.

---

### 5-1. 대칭키

클라이언트와 서버가 같은 대칭키를 가지며 이 대칭키를 사용하여 데이터를 암호화하고
복화한다.

이런 대칭키 방법은 테이터를 암호화, 복호화하는 과정이 쉽다는 장점을 가지고 있지만
데이터와 함께 대칭키를 배송할 때 해커도 대칭키를 알 수 있기 때문에 해커 또한 데이터를
복호화할 수 있다는 단점을 가지고 있다.

![대칭키](https://2158680719-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FtlrW8c4MEVWoel5YVxSk%2Fuploads%2Fgit-blob-6a3fb4687bceaaa298cda0650a504fb44035dc9a%2F%EB%8C%80%EC%B9%AD%ED%82%A4.jpg?alt=media)

---

### 5-2. 공개키/개인키(비대칭키)

공개키는 헤커를 포함하여 모든 클라이언트가 가지고 있는 말 그대로 공개된 키이다. 하지만
개인키는 절대로 유출이 되서는 안되는 키이다. 공개키로 암호화 한 데이터는
비밀키로만 복호화를 할 수 있다. 그 반대도 가능하다.

이러한 방법으로 인해 개인키를 모르는 헤커는 암호화된 데이터를 복호화할 수 없다. 대치킹보다
보안성이 더 뛰어나지만 대칭키 방법보다 암호화 연산 시간이 더 소요되어 비용이 큰 단점이있다.

![공개키/개인키(비대칭키)](https://2158680719-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FtlrW8c4MEVWoel5YVxSk%2Fuploads%2Fgit-blob-a8c3b2fba7c6d32323af3411389e6123a8728ece%2F%EA%B3%B5%EA%B0%9C%ED%82%A4.jpg?alt=media)

비대칭키 실습은 아래의 웹사이트에서 할 수 있다.  
[www.devglan.com](https://www.devglan.com/online-tools/rsa-encryption-decryption)

---

## 6. CA(Certificate Authorities)

그렇다면 클라이언트와 통신을 하고 있는 서버가 안전하고 신뢰를 할 수 있다는 인증은 어떻게 이루어질까?
인증 메커니즘은 CA에서 발급한 인증서를 기반으로 이루어진다.

네이버를 예시로 든다면 url주소 옆 자물쇠 모양의 아이콘을 볼 수 있다. 자물쇠 모양의
아이콘이 CA에서 인증서를 발급을 했다는 의미이다. CA에서 발급한 인증서는 사용자가
접속한 서버가 신뢰할 수 있는 서버임을 보장한다.

이런 CA는 신뢰성이 엄격하게 공인된 기업들만 참여할 수 있다. 대표적인 기업으론
Comodo, GoDaddy, GlobalSign, 아마존 등이 있다.

![CA](https://2158680719-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FtlrW8c4MEVWoel5YVxSk%2Fuploads%2Fgit-blob-b7d9b0c88d2af2f712651125455ad75a7d2eb2c9%2FCA.png?alt=media)

아래는 CA 발급과정이다. 여러 사이트에서 발급된 CA는 이미 우리가 자주 사용하는
크롬, 사파리, 엣지 등 브라우저에 내장되어 있다.

![CA 발급과정](https://2158680719-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FtlrW8c4MEVWoel5YVxSk%2Fuploads%2Fgit-blob-e1554767542e5a0d1717f5ca4744d2f69e4bc488%2FCAIssued.jpg?alt=media)

---

## 7. https가 구현되는 과정

### 7-1. handshake

클라이언트는 아직 통신하고자 하는 서버를 신뢰하지 못하기 때문에 일종의 탐색과정을
거친다. 이를 `handshake`라 한다.

![handshake 과정](https://2158680719-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FtlrW8c4MEVWoel5YVxSk%2Fuploads%2Fgit-blob-60dfe295161431b3cc6e90d0d41b414c4ff51d36%2Fhadnshake.png?alt=media)

---

### 7-2. 사이트가 제공한 인증서가 정품인지 확인

사이트에서 제공한 인증서가 정품인지 즉, 클라이언트가 정말 사이트를 신뢰할 수 있는지
확인을 해야 한다.

이를 위해선 이미 브라우저에 내장된 인증기관의 공개키를 사용하여 사이트에서 제공한
인증서를 복호화하는 작업을 한다. 이 인증서는 인증기관에서 인증기관의 개인키로 서명(암호화)을
했기 때문에 인증기관의 공개키를 사용하여 복호화를 할 수 있다. 이는 비대칭키 방식을 활용한 것이다.

![CA 확인하기](https://2158680719-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FtlrW8c4MEVWoel5YVxSk%2Fuploads%2Fgit-blob-671c041a9b97969a4e46757fe370965b3816f5aa%2FhttpsCA.png?alt=media)

인증서 복호화를 성공하였다면 클라이언트는 해당 사이트를 신뢰를 할 수 있기 때문에
url 주소 옆 자물쇠 모양의 아이콘을 볼 수 있다.

![신뢰할 수 있는 사이트](https://2158680719-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FtlrW8c4MEVWoel5YVxSk%2Fuploads%2Fgit-blob-9c42bea0f78eb8604b94e9cfa59ec66658ecbd05%2FhttpsCA1.png?alt=media)

하지만 인증서 복호화를 실패하였다면 아래와 같은 경고 메시지를 볼 수 있다.

![신뢰할 수 없는 사이트](https://2158680719-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FtlrW8c4MEVWoel5YVxSk%2Fuploads%2Fgit-blob-2755310fddca68d62d6fa65f47b738d670b59a7e%2FhttpsCA2.png?alt=media)

---

### 7-3. 대칭키 공유하기

인증서를 복호화를 하게 되면 클라이언트는 통신하게 될 서버의 공개키를 사용할 수 있다.
그렇다면 클라이언트에선 서버의 공개키를 사용하여 암호화하고 서버에선 서버의 개인키를
사용하여 복호화하는 과정을 통해 통신을 하면 되지 않을까? 하는 생각을 할 수 있는데
결론적으론 대칭키 방식을 사용하게 된다.

하지만 대칭키로 데이터를 암호화하고 복호화하는 것은 위에서 살펴봤던 것과 같이 헤커에게
탈취당할 가능성이 있기 때문에 위험하다고 설명을 하였다.

이를 해결하기 위해 비대칭키 방식을 사용하여 같은 대칭키를 클라이언트와 서버가
공유할 수 있도록 한다.

`handshake` 과정에서 클라이언트와 서버는 랜덤 데이터를 서로 주고 받았다.
이 데이터를 사용하여 클라이언트는 `사용자 대칭키`를 만든 후 `서버의 공개키`로
암호화 하여 서버에 보낸다.

서버에서는 받은 암호화 된 `사용자 대칭키`를 `서버의 개인키`로 복호화하여
`사용자 대칭키`를 얻어낸다.

이제 클라이언트와 서버 양쪽 모두 `사용자 대칭키`를 알고 있으므로 이를 이용하여
대칭키 방식으로 통신을 하게 된다.

![대칭키 공유하기](https://2158680719-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FtlrW8c4MEVWoel5YVxSk%2Fuploads%2Fgit-blob-f92b0ff35d63727d13a8980562f9f2c3c45d8ddd%2FhttpsShared.jpeg?alt=media)

---

## 출처

[MDN - HTTPS](https://developer.mozilla.org/ko/docs/Glossary/https)  
[MDN - Secure Sockets Layer (SSL)](https://developer.mozilla.org/ko/docs/Glossary/SSL)  
[TLS(Transport Layer Security)는 무엇입니까?](https://www.cloudflare.com/ko-kr/learning/ssl/transport-layer-security-tls/)

도움이 많이 되었던 유튜브 🎬

- HTTPS가 뭐고 왜 쓰나요? (Feat. 대칭키 vs. 비대칭키)  
  [![HTTPS가 뭐고 왜 쓰나요? (Feat. 대칭키 vs. 비대칭키)](https://img.youtube.com/vi/H6lpFRpyl14/0.jpg)](https://youtu.be/H6lpFRpyl14)
- [10분 테코톡] 🍭 다니의 HTTPS  
  [![[10분 테코톡] 🍭 다니의 HTTPS](https://img.youtube.com/vi/wPdH7lJ8jf0/0.jpg)](https://youtu.be/wPdH7lJ8jf0)
- 암호학1 - 4.1. 양방향 암호화 - 비대칭키(공개키 방식) - 기밀성을 위해서 사용하기  
  [![암호학1 - 4.1. 양방향 암호화 - 비대칭키(공개키 방식) - 기밀성을 위해서 사용하기](https://img.youtube.com/vi/MR4sCU82tgo/0.jpg)](https://youtu.be/MR4sCU82tgo)
