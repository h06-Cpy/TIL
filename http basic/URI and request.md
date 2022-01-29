# URI와 브라우저 요청 흐름
## URI(Uniform Resource Identifier)

Uniform: 리소스를 식별하는 통일된 방식

Resource: URI로 식별할 수 있는 모든 것

Identifier: 다른 항목과 구분하는데 필요한 정보

URI에 해당하는 두가지

- URL(Uniform Resource Locator): 대부분 이걸 쓰고 리소스가 어느 위치에 있는지 알려줌
- URN(Uniform Resource Name): 리소스에 이름 자체를 부여하는 것으로 위치를 찾기는 어려움 그래서 잘 안쓰임 책의 ISBN 방식 같은 거랑 비슷함

URL 문법

scheme://[userinfo@]host[:port][/path][?query][#fragment]

ex) https://www.google.com:443/search?q=hello&hl=ko

하나하나 뜯어서 보자

1. scheme
    - 주로 프로토콜(어떤 방식으로 자원에 접근할 것인가 하는 약속) 사용
    - 앞서 배운 포트 번호 http 80 https 443 생략 가능
2. userinfo
    - URL에 사용자 정보를 포함해서 인증할 때 쓰이지만 거의 안쓰임
3. host
    - 도메인명 또는 ip 주소 직접 사용 가능
4. port
    - 접속 포트, scheme에서 언급했듯이 일반적으로 생략
5. path
    - 리소스 경로, 폴더나 디렉토리처럼 게층적 구조
6. query
    - key=value 형태
    - ?로 시작, &로 추가
    - query parameter, query string으로 불림 다 string 타입으로 보내져서, 웹서버에 제공되는 정보
7. fragment
    - html 내부 북마크 등에 사용(html 내부에서 다른 페이지로 이동할 때)
    - 서버에 전송하는 정보는 아님

## 웹 브라우저 요청 흐름

브라우저(클라이언트)랑 구글 서버가 통신한다고 생각

[https://www.google.com:443/search?q=hello&hl=ko](https://www.google.com:443/search?q=hello&hl=ko를) 주소창에 입력해보면?

1. 브라우저가 DNS 조회해서 ip를 알아내고 HTTP 요청 메시지 생성
2. socket 라이브러리로 OS에 메시지를 넘겨줌
    - TCP/IP 연결, 데이터 전달
3. TCP/IP 패킷 생성하고 내트워크 인터페이스에서 서버로 전달!
4. 요청 패킷을 전달해서 인터넷 망을 거쳐 서버에게 전달
5. 서버가 받고 HTTP 응답 메시지(OK, 텍스트, UTF-8, html 문서 등) 다시 보냄(과정 1,2,3,4)
6. 응답 패킷이 인터넷 망을 거쳐 브라우저에게 전달
7. 웹 브라우저 HTML 렌더링을 통해 화면에 페이지가 보인다!
---
출처: 모든 개발자를 위한 HTTP 웹 기본 지식 - 김영한님

https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/dashboard
