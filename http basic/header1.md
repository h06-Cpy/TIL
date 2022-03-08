# http 헤더1
용도: HTTP 전송에 필요한 모든 부가정보 

예) 메시지 바다 내용, 크기, 압축, 인증, 요청 클라, 서버 정보, 캐시 관리 정보 등...

필요시 임의의헤더 추가 기능

## 표현

- Content-Type: 표현 데이터의 형식, 예) text/html; charset=utf-8, application/json, image/png
- Content-Encoding: 표현 데이터의 압축 방식
    - 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가
    - 읽는 쪽에서는 인코딩 헤더의 정보로 압축 해제
    - 예) gzip, deflate, identity(이건 압축 안했다는 거)
- Content-Language: 표현 데이터의 자연 언어, 예) ko, en, en-US
- Content-Length: 표현 데이터의 길이
    - 바이트 단위
    - Transfer-Encoding 사용 시 Content-Length 사용 불가

표현 헤더는 전송, 응답 모두 사용됨

## 협상(콘텐츠 네고시에이션)

클라이언트가 선호하는 표현을 요청하는 것

- Accept: 클라가 선호하는 미디어 타입 전달
- Accept-Charset: 클라가 선호하는 문자 인코딩
- Accept-Encoding: 클라가 선호하는 압축 인코딩
- Accept-Language: 클라가 선호하는 자연 연어

협상 헤더는 요청 때 사용

---

Accept-Language에서 선호하는 언어 보내줬는데 서버에서 지원 안해주면 어캄?

### 우선순위

- Quality Values(q) 값을 사용
    - 0~1, 클 수록 높은 우선순위이고 생략하면 1임
    - 일케 해서 여러 언어에 대한 선호도를 서버에게 보낼 수 있음
- 구체적인 것이 우선함, Accept에서 미디어 타입에 대한 정보가 구체적일 수록 우선순위 높음
- 구체적인 것을 기준으로 미디어 타입을 맞춤

## 전송 방식

- 단순 전송: Content-Length
- 압축 전송: Content-Encoding
- 분할 전송: Transfer-Encoding: chunked, 작은 바이트 단위로 쪼개서 보냄
- 범위 전송: Content-Range, ex) 리소스 절반 받았으니 나머지 주세요 요청받으면 나머지 보냄

## 일반 정보

- From: 유저 에이전트의 이메일 정보
- **Referer**: 이전 웹페이지 주소
    - 유입 경로 분석 가능, 요청에서 사용
- User-Agent: 유저 에이전트 애플리케이션 정보(브라우저 정보 등)
    - 어떤 종류 브라우저에서 장애가 발생하는지 파악 가능, 요청에서 사용
- Server: 요청을 처리하는 origin 서버 소프트웨어 정보, 응답에서 사용
- Date: 메시지가 발생한 날짜와 시간, 응답에서 사용

## 특별한 정보

- **Host**: 요청한 호스트 정보, 필수값임!
    - 서버에서 애플리케이션이 여러개 구동될 때 어느 클라가 애플리케이션에 접근하는지 알려줌
- Location: 3xx 응답 결과에서 Location 헤더가 있을 때 그 위치로 리다이렉트함
    - 2xx에서는 요청에 의해 생성된 리소스 URI
- Allow: 허용 가능한 HTTP 메서드를 클라에게 알려줌, 405 Method Not Allowed 응답에서 포함
- Retry-After: 503 Service Unavailable에서  클라에게 언제까지 서비스 불능인지 알려줌

## 인증

- Authorization: 클라이언트 인증 정보를 서버에 전달
- WWW-Authenticate: 리소스 접근 시 필요한 인증 방법 정의
    - 401 Unauthorized 응답과 함께 사용

## 쿠키

이걸로 나를 인식해달라고 서버에 알려줌

- Set-Cookie: 서버에서 클라로 쿠키 전달(응답)
- Cookie: 클라가 서버에서 받은 쿠키를 저장하고, http 요청시 서버로 전달

HTTP가 Stateless 프로토콜이므로 아무것도 안하면 서버가 날 못알아 봄

---

쿠키 대신 모든 요청에 내 정보를 포함하면 어떤가?

보안 문제도 있으면서 개발이 힘들어짐

---

쿠키는 자동으로 내 정보를 보내므로 편함

사용처: 사용자 로그인 세션 관리, 광고 정보 트래킹

쿠키는 ‘항상’ 서버에 전송됨 → 네트워크 트래픽 추가 유발

그러므로 최소한의 정보만 사용(세션 id, 인증 토큰)

서버 전송 싫으면 웹 스토리지(locaStorage, sessionStorage) 참고

---

예) set-cookie: **sessionid**=abcd1234; **expires**=Sat, 26-Dec-2020 00:00:00 GMT; **path**=/; **domain**=google.com; **Secure**

### 생명주기

- expires: 만료일 지정, 만료일이 되면 쿠키 삭제
- max-age: 초 단위 세팅, 0이나 음수를 지정하면 쿠키 삭제

세션 쿠키: 만료 날짜를 생략하면 브라우저 종료까지만 유지

영속 쿠키: 만료 날짜를 입력하면 해당 날짜까지 유지

### 도메인

예) domain=example.org

서브 도메인 dev.example.org

도메인 명시했을 경우: 명시한 문서 기준 도메인과 서브 도메인까지 다 쿠키 접근 가능

생략했을 경우: 서브 도메인은 쿠키 접근 불가능

### 경로

경로를 포함한 하위 경로 페이지만 쿠키 접근

일반적으로 path=/루트로 해서 하위 파일 다 접근하게 함

### 보안

- Secure: https인 경우만 전송, 원래 쿠키는 http도 전송
- HttpOnly: XSS 공격 방지, 자바스크립트 접근 불가, HTTP 전송에서만 사용
- SameSite: XSRF 공격 방지, 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송

samesite는 지원된지 몇년 안돼서 브라우저 확인 후 사용해야 함

---
출처: 모든 개발자를 위한 HTTP 웹 기본 지식 - 김영한님

https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/dashboard
