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
    - Transfer-Enconding 사용 시 Content-Length 사용 불가

표현 헤더는 전송, 응답 모두 사용됨

## 협상(콘텐츠 네고시에이션)
