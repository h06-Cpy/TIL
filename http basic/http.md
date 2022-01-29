# HTTP
HTTP 메시지가 전송하는 것: HTML, TEXT, 이미지, 음성, 영상, 파일, JSON, XML(API) 등

거의 모든 형태의 데이터 전송 가능

서버간에 데이터를 주고 받을 때도 사용

**지금은 HTTP 시대!**

**HTTP/1.1 (1997년)의 스펙을 가장 많이 사용한다**

HTTP/2(TCP)랑 HTTP/3(UDP)은 1.1에서 성능 개선을 한 것임 

HTTP 특징

- 클라이언트 서버 구조
- 무상태 프로토콜, 비연결성
- HTTP 메시지
- 단순함, 확장 가능

## 클라이언트 서버 구조

클라가 요청 보내면 응답 대기

서버가 요청에 대한 결과 만들어서 응답

**중요한 건 클라 역할(UX/UI)과 서버 역할(비즈니스 로직)이 분리되어 있다는 것!**

각자 독립적으로 진화하기 좋다

## Stateful, Stateless

무상태 프로토콜(stateless) 특징

- 서버가 클라이언트의 상태를 보존하지 않음
- 장점: 서버 확장성 높음(스케일 아웃)
- 단점: 클라가 추가 데이터 전송해야 함

stateful

- 클라랑 통신하던 서버가 항상 유지되어야 함
- 중간에 서버 장애나면 클라는 다른 서버랑 처음부터 다시 작업 시작해야 함

stateless는 stateful 단점 커버!

그러나 한계는 있다

stateless로 설계 못하는 경우도 있다 ex) 로그인은 상태 유지 필요

이는 쿠키와 서버 세션을 이용하여 해결 가능

상태 유지는 최소한만 사용

## 비 연결성

서바 하나와 클라 여러개가 연결을 유지하면 서버 자원 소모가 심함

그래서 하나 연결하고 데이터 전송하고 끊고 하는 비 연결성 사용

응답 속도가 초 단위 이하로 매우 빠르며 서버에서 동시에 처리하는 요청 수는 생각보다 작음

결국 서버 자원을 효율적으로 사용 가능

한계점

- TCP/IP 연결을 계속 새로 맺어야 함-3 way handshake 시간 추가
- HTML, CSS, JS, 이미지 등 수많은 자원이 함께 다운로드되므로 시간 추가

해결방안: HTTP 지속 연결(Persistent Connections) 사용 → HTML, CSS, JS, 이미지 등을 다 받을 때까지 연결 안 끊음

HTTP/2, 3에서 더 많은 최적화가 이루어짐(연결 속도 자체를 빠르게)

서버 개발자들이 어려워 하는 업무

같은 시간에 딱 맞추어 발생하는 대용량 트래픽 ex) 선착순 이벤트, 명절 KTX 예약, 대학 수강 신청

이런 상황에서도 stateless를 생각해야 함

트래픽을 분산시키는 방법들을 생각해보자

## HTTP 메시지

HTTP 요청 메시지 예시

GET /search?q=hello&hl=ko HTTP/1.1
Host: [www.google.com](http://www.google.com/)

HTTP 응답 메시지 예시

HTTP/1.1 200 OK Content-Type: text/html;charset=UTF-8 Content-Length: 3423


<html>
	<body>...</body>
</html>


HTTP 메시지 구조

1. start-line(시작 라인)
2. header
3. empty line (CRLF): 무조건 있어야 함
4. message body  

하나하나 보자

### 시작 라인

요청 메시지에서)

- HTTP 메서드: GET, POST, DELETE... → 서버가 수행해야 할 동작 지정
- 요청 대상: 절대경로와 쿼리
- HTTP 버전

응답 메시지에서)

- HTTP 버전
- 상태 코드: 200(성공), 400(클라 요청 오류), 500(서버 내부 오류)
- 이유 문고: 사람이 이해라 수 있는 짧은 설명글 ex) OK

### 헤더

header-field = field-name: OWS field-value OWS 형태

OWS는 띄어쓰기 허용

field-name은 대소문자 구분 없고 field-value는 구분함

헤더 특징

- HTTP 전송에 필요한 모든 부가정보(메시지 바디의 내용, 크기 ,압축 ,인증, 요청 클라 정보 등)
- 표준 헤더가 너무 많음
- 필요시 임의의 헤더 추가 가능(약속된 클라와 서버만 이해)

### 메시지 바디

실제 전송할 데이터

HTML, 이미지, 영상, JSON 등등 byte로 표현할 수 있는 모든 데이터 전송 가능

---
출처: 모든 개발자를 위한 HTTP 웹 기본 지식 - 김영한님

https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/dashboard
