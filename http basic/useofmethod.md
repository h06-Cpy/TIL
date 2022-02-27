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
## HTTP API 설계 예시

- 컬렉션
    - POST 기반 등록
    - 예) 회원 관리 API 제공
- 스토어
    - PUT 기반 등록
    - 예) 정적 컨텐츠 관리 ,원격 파일 관리
- HTML FORM 사용
    - 웹 페이지 회원 관리
    - GET, POST만 지원

### POST 기반 등록

회원 관리 시스템 api 설계해보자

- 회원 목록: /members → GET
- 회원 등록: /members → POST
- 회원 조회: /members/{id} → GET
- 회원 수정: /members/{id} → PATCH, PUT, POST
- 회원 삭제: /members/{id} → DELETE

---

POST 기반 등록 특징

- 클라이언트는 등록될 리소스 URI를 모른다(어느 폴더에 있는지만 알듯)
    - 위의 예시에서 /members 폴더까지는 안다
- **서버가 새로 등록된 리소스 URI를 생성해준다**
    - HTTP/1.1 201 Created
        
        Location: /members/100
        

리소스 식별자 100이 생김! 클라이언트가 아니라 서버가 생성해준 것임

- 컬렉션
    - 서버가 관리하는 리소스 디렉토리
    - 서버가 리소스의 URI를 생성하고 관리
    - 여기서 컬렉션은 /members

대부분 POST 기반 collection을 씀!

### PUT 기반 등록

파일 관리 시스템 api를 설계해보자

- 파일 목록: /files → GET
- 파일 조회: /files/{filename} → GET
- 파일 등록: /files/{filename} → PUT
- 파일 삭제: files/{filename} → DELETE
- 파일 대량 등록: /files → POST

---

PUT 기반 등록 특징

- 클라이언트가 리소스 URI를 알아야 함(서버가 식별자 생성 안함)
- **클라이언트가 직접 리소스의 URI를 지정함**
- 스토어
    - 클라이언트가 관리하는 리소스 저장소
    - 클라이언트가 리소스의 URI를 알고 관리
    - 여기서 스토어는 /files

스토어는 거의 안씀, 파일 관리나 게시판 관리에서는 쓰일 수 있음

### HTML FORM 사용

위의 2개 예시는 여러 메서드 사용 가능했지만 여기서는 GET, POST만 사용 가능!

어케 설계할까?

- 회원 목록 /members -> GET
- 회원 등록 폼 /members/new -> GET
- 회원 등록 /members/new, /members -> POST
- 회원 조회 /members/{id} -> GET
- 회원 수정 폼 /members/{id}/edit -> GET
- 회원 수정 /members/{id}/edit, /members/{id} -> POST
- 회원 삭제 /members/{id}/delete -> POST

---

리소스 기반으로만 URI를 설계하면 좋지만 그게 힘듦

그러므로 컨트롤 URI 사용!

컨트롤 URI 복습

- 동사로 된 리소스 경로
- 위의 예시에서 /new, /edit, /delete
- HTTP 메서드로 해결하기 애매한 경우에 사용할 수 있음

---

uri 설계 개념 참고(무조건 이걸 따르는 건 아님 걍 이렇게 하면 좋다)

- 문서(document)
    - 단일 개념(파일 하나, 객체 인스턴스, 데이터베이스 row)
- 컬렉션(collection)
- 스토어(store)
- 컨트롤러(controller), 컨트롤 URI
    - 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행

---
출처: 모든 개발자를 위한 HTTP 웹 기본 지식 - 김영한님

https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/dashboard
