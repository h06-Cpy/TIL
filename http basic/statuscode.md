# http 상태코드
상태코드: 클라이언트가 보낸 요청의 처리 상태를 응답에서 알려줌

100번대~ 500번대가 있음

백의 자리 숫자에 따라

- 1xx: 요청 받았는데 처리중 (Informational) ← 거의 사용 안됨
- 2xx: 요청 정상 처리됨 (Successful)
- 3xx: 추가 행동 필요 (Redirection)
- 4xx: 클라이언트가 잘못함, 문법 오류같은 것 (Client Error)
- 5xx: 서버 작동 안됨 (Server Error)

## 2xx

- 200 OK: 요청 성공함, 예) GET으로 조회 완료
- 201 Created: 새로운 리소스 생성됨, 예) POST로 리소스 생성
- 202 Accepted: 요청 접수됐는데 처리 완료 안됨, 예) 요청 접수 후 1시간 뒤에 배치 프로세스가 요청 처리
- 204 No Content: 요청 수행 완료했는데 응답 본문에 보낼 데이터가 없음, 예) 웹 문서 편집기에서 save 버튼 눌러도 딱히 응답으로 보낼 데이터는 없음, 걍 save 됐다는 것만 알려주면 됨

## 3xx

Redirection: 웹 브라우저가 3xx 응답 결과에서 Location 헤더가 있으면 그 위치로 자동 이동함

### 영구 리다이렉션

리소스 URI가 영구적으로 이동되 원래꺼 사용 안함, 검색 엔진 등에서도 변경 인지

- 301 Moved Permanently: 리다이렉트시 요청 메서드가 GET으로 변하고 본문 제거될 수 있음
- 308 Permanent Redirect: 301이랑 같지만 리다이렉트시 요청 메서드와 본문 유지

301이 더 나은 이유: URI가 바껴서 리다이렉트하는데 보내야할 데이터도 바뀌는 경우가 많음
### 일시적인 리다이렉션

리소스 URI가 일시적으로 변경되므로 검색 엔진 등에서 URL 변경하면 안됨

- 302 Found: 리다이렉트시 요청 메서드가 GET으로 변하고 본문이 제거될 수 있음
- 307 Temporary Redirect: 302랑 같은데 리다이렉트시 요청 메서드와 본문 유지
- 303 See Other: 302랑 같은데 리다이렉트시 요청 메서드가 GET로 무조건 바뀜

---

302가 확실하지 않아서 307, 303이 나왔고 이들이 권장됨

하지만 이미 많은 애플리케이션 라이브러리들이 302가 기본이라 302 사용해도 큰 문제 없음

### PRG: Post/Redirect/Get

POST로 주문 후에 웹 브라우저를 새로고침하면 중복 주문이 될 수 있음

이를 방지하기 위해 POST로 주문 후에 결과 화면을 GET으로 리다이렉트하면 됨

PRG 사용 전에는 POST 요청하면 응답이 200 OK로 오지만 PRG 사용 후에는 응답이 302 Found로 옴

### 기타 리다이렉션

304 Not Modified: 클라이언트보고 로컬 PC에 저장된 캐시를 재사용하라고 알려줌(캐시로 리다이렉트)

304 응답은 메시지 바디를 포함하면 안됨

조건부 GET, HEAD 요청시 사용

## 4xx

클라이언트 문제라서 똑같은 요청을 재시도해도 실패함

- 400 Bad Request: 요청 구문, 메시지 등 오류, 예) 요청 파라미터 잘못, API 스펙 안맞음
- 401 Unauthorized: 인증(Authentication), 즉 로그인같은 것이 되지 않음, 응답에 WWW-Authenticate 헤더와 함께 인증 방법 설명
- 403 Forbidden: 인증 자격은 되는데 권한이 불충분함, 예) 로그인된 사용자가 어드민 등급 리소스에 접근하는 경우
- 404 Not Found: 요청 리소스가 서버에 없거나 권한 부족한 클라이언트에게 리소스를 숨기고 싶을 때

## 5xx

서버 문제라서 똑같은 요청을 재시도하면 성공할 수 있음

- 500 Internal Server Error: 서버 내부 문제로 오류 발생, 애매하면 이걸 사용
- 503 Service Unavailable: 서버가 일시적인 과부하 또는 예정된 작업으로 잠시 요청을 처리할 수 없음, Retry-After 헤더 필드로 얼마뒤에 복구되는지 보낼 수도 있으나 대부분 언제 복구될지 모름

오직 서버에 문제가 생겼을 때만 사용할 것!!

---
출처: 모든 개발자를 위한 HTTP 웹 기본 지식 - 김영한님

https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/dashboard
