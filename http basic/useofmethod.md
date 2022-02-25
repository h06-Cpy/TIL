# http 메서드 활용
## 클라이언트에서 서버로 데이터 전송 예시

데이터 전달 방식 2가지

- 쿼리 파라미터 이용
    - GET을 이용하여 정렬필터(검색어)
- 메시지 바디 이용
    - POST, PUT, PATCH 등
    - 회원 가입, 상품 주문, 리소스 등록 및 변경

4가지 상황

- 정적 데이터 조회
    - 이미지, 정적 텍스트 문서
- 동적 데이터 조회
    - 주로 검색, 게시판 목록 정렬 필터(검색어)
- HTML Form을 통한 전송
    - 회원 가입, 상품 주문, 데이터 변경
- HTML API를 통한 전송
    - 회원 가입, 상품 주문, 데이터 변경
    - 서버 to 서버, 앱 클라이언트, 웹 클라이언트(AJAX)

### 정적 데이터 조회

쿼리 파라미터 미사용

GET을 이용해서 리소스 경로를 통해 이미지나 정적 텍스트를 요청함

### 동적 데이터 조회

쿼리 파라미터 사용

서버에서 쿼리 파라미터 기반으로 결과를 동적으로 생성

주로 검색, 게시판 목록 정렬 필터 등에 쓰임

**GET은 쿼리 파라미터를 사용함** 메시지 바디는 잘 안쓰임!

### HTML Form 데이터 전송

POST 전송을 통해 데이터를 서버에 저장

html form 태그 속성에 method=”post” 일케 되어 있음

만약 username=kim, age=20을 보낸다고 가정

그렇다면 웹 브라우저가 생성한 요청 http 메시지는?

---

POST /save HTTP/1.1

Host: [localhost:8080](http://localhost:8080) Content-Type: application/x-www-form-urlencoded

username=kim&age=20

---

쿼리 파라미터랑 비슷하게 생김!

method=”get”으로 바꾸면? 메시지 바디 부분이 url 경로의 쿼리 파라미터로 들어감!

위의 content type에서 urlencoded가 있는데 만약 데이터가 한글이면 utf-8로 인코딩 해야 돼서 그럼

---

파일(바이너리 데이터)도 전송하고 싶을 떄? —> multipart form-data 이용

form 태그 속성 enctype=”multipart form-data”

http 요청 메시지에서 브라우저가 자동으로 전송될 데이터들을 구분해줌

username, age, file 등...

---

정리!

- HTML Form submit 시 POST 전송
    - 회원 가입, 상품 주문, 데이터 변경
- Content-Type: application/x-www-form-urlencoded 사용
    - form 내용을 메시지 바디를 통해 전송
    - 전송 데이터를 url encoding 처리
- Content-Type: multipart/form-data
    - 파일 업로드같이 바이너리 데이터 전송에 사용
    - 다른 종류의 여러 파일과 폼 내용 전송 가능
- HTML Form 전송은 GET, POST만 지원

### HTML API 데이터 전송

클라→서버로 키 밸류 형태로 데이터 바로 전송할 때! api 방식이라고 함

- 서버 to 서버
    - 백엔드 시스템 통신
- 앱 클라이언트
    - 아이폰, 안드로이드
- 웹 클라이언트
    - HTML에서 Form 전송 대신 자바스크립트 통한 통신에 사용(AJAX)
    - 예) React, Vue 같은 웹 클라이언트와 API 통신
- POST, PUT, PATCH: 메시지 바디를 통해 데이터 전송
- GET: 조회, 쿼리 파라미터로 데이터 전달
- Content-Type: application/json을 주로 사용(예전엔 XML이 표준 지금은 JSON 표준)
    - TEXT, XML, JSON 등
