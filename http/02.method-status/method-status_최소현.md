# HTTP 메서드
### 메서드의 속성

### 안전 (safe)

- 서버의 상태가 변하지 않는 것
- 즉, read-only

### 멱등 (indempotent)

- 여러번 연속으로 보내어도 서버의 상태가 동일하게 남을때 멱등성이 있다고 함
- 판단할 때, 서버의 상태만 봄!! (응답 코드는 달라질 수 있음 — delete 200, 404)

### 캐시 가능 (cacheable)

- 응답 결과를 캐시해서 사용할 수 있는지
- GET, HAED는 아주 목적에 부합
- POST, PATCH는 가능은 하지만 사용X —> 본문 내용까지 캐시 키로 고려해야하는데 구현이 어려움
- PUT, DELETE는 캐시불가

### GET 메서드

- 리소스를 조회할 때 사용하는 메서드
    
    ```
    // 요청
    GET /search?q=hello&hl=ko HTTP/1.1
    HOST: www.google.com
    
    // 응답
    HTTP1.1 200 OK
    Content-Type: application/json
    Content-Length: 34
    
    {
       "useername" : "a"
       "age" : 20
    }
    ```
    
- 서버에 전달하고 싶은 데이터는 query를 통해 전달 (body 전달 가능. 하지만 권장하지 않음 — 금지x, 정의x)

### POST 메서드

- 요청 데이터 처리, 메시지 바디를 통해 서버로 요청 데이터 전달
    
    ```
    // 요청
    POST /member HTTP/1.1
    Content-Type: appliction/json
    
    {
       "useername" : "a"
       "age" : 20
    }
    ```
    

### PUT, PATCH 메서드

- PUT: 리소스 대체. 없으면 생성 —> 덮어씀
    
    ```
    // 요청
    PUT /members/100 HTTP/1.1
    Content-Type: appliction/json
    
    {
       "useername" : "a"
       "age" : 20
    }
    ```
    
- PATCH: 변경된 부분만 변경
    
    ```
    // 요청
    PATCH /member/100 HTTP/1.1
    Content-Type: appliction/json
    
    {
       "age" : 20
    }
    ```
    

### DELETE 메서드

- 리소스 제거
    
    ```
    // 요청
    DELETE /member/100 HTTP/1.1
    ```
    

### 클라이언트 → 서버 전송

1. 정적 데이터 조회
    - 쿼리 파라미터 미사용
    - 이미지, 정적 텍스트 문서
    
    ```
    GET /static/test.jpg HTTP/1.1
    Host: localhost:8080
    ```
    
2. 동적 데이터 조회
    - 쿼리 파라미터 사용
    - 정렬 필터 후 결과를 동적으로 생성
    
    ```
    GET /search?q=hello&hl=ko HTTP/1.1
    Host: localhost:8080
    ```
    
    - HTTP FORM 태그를 통한 방식
        
        * POST 메서드
        * GET 메서드

1. API 데이터 전송
    - 서버 to 서버
    - 웹 클라이언트
        - AJAX (React, View.js 등)
    
    ```
    POST /members HTTP/1.1
    Content-Type: application/json
    
    {
    	"username": "young",
    	"age": 20
    }
    ```
    

# HTTP 상태코드
### 요약

| 1XX | 요청이 수신되어 처리중 |
| --- | --- |
| 2XX | 요청 정상 처리 |
| 3XX | 요청을 완료하려면 추가 행동 필요 |
| 4XX | 클라이언트 오류 |
| 5XX | 서버 오류 |


## 2xx (Successful)

- **200 (OK)**
    
    결과를 정상적으로 응답하며 200 코드 반환
    
- **201 (Created)**
    
    요청 성공해서 새로운 리소스가 생성됨 (POST, PUT에 많이 사용)
    
- **202 (Accepted)**
    
    요청은 정상적이나, 서버가 아직 처리를 완료 못한 경우 (요청이 크고 무거워서)
    
    —> Callback (서버가 알려줌)
    
    —> Polling (클라이언트가 주기적으로 작업 상태 조회)
    
- **204 (No Content)**
    - 클라이언트의 요청은 정상. 하지만 제공할 컨텐츠가 없음
    - 같은 화면을 유지해야 함 (PATCH, DELETE에 사용 — 저장 후 편집 계속 등)
    - 캐시 사용 — 반응속도 증가

## 3xx (Redirection)

: 요청을 완료하려면 추가적인 작업이 필요함, 3xx 결과에 location 헤더가 있으면, 그 위치로 자동 이동


### 영구 리다이렉션 (Permanently Redirect)

- **301 (Moved Permanently)**
    
    리다이렉트시 요청 메서드가 GET으로 변하고 본문이 제거 될 수 있음
    
- **308 (Permanent Redirect)**
    
    301과 기능은 같으나, 요청 메서드와 본문 유지
    

### 일시 리다이렉션  (Moved Permanently)

- **302 (Found)**
    
    리다이렉트시 요청 메서드가 GET으로 변하고 본문 제거 될 수 있음
    
- **307 (Temporary Redirect)**
    
    302와 기능은 같으나, 요청 메서드와 본문 유지
    
- **303 (See Other)**
    
    302와 기능은 같으나, 리타이렉트시 요청 메서드가 GET으로 변경
    

### 영구냐 일시냐는 사실 검색 엔진을 위한 것

- **검색 엔진**
    
    검색 엔진은 페이지에 대한 정보를 수집하고 평가하여 우선순위에 따라 콘텐츠를 노출시킴
    
- **영구 리다이렉트**
    
    기존 URL에 대한 사이트 랭크와 평가 점수를 받지 않으며, 새로운 URL 페이지만 수집해라. 라는 의미
    
    - 사용 예시
        
        ```
        - 웹사이트의 `도메인`을 변경할 경우, 완전 영구 이동이 필요할때
        - 웹 사이트에서 사용되는 `URL 구조`를 영구적으로 변경하려는 경우.
        - 두 개의 웹사이트 또는 페이지를 `병합`할때
        - 웹사이트를 HTTP에서 HTTPS 로 전환하는 경우 
        ```
        
- **일시 리다이렉트**
    
    요청한 정보가 일시적으로 옮겨진 것이므로, 사이트 랭크와 평가 점수는 기존 URL로 수집해라. 라는 의미
    
    - 사용 예시
        
        ```
        - 페이지가 임시 점검 중일때 (일시적인 수정)
        - 이전 사이트 디자인에서 새 페이지 또는 디자인에 대한 피드백을 요청하고 싶을때 (A/B 테스팅)
        - en, ko, jp 과 같은 언어를 지원하는 페이지로 옮길때
        - 쇼핑몰 같은 경우 제품이 품절되서, 관련 제품 사이트로 안내할때 (만일 품절된 제품을 없애고 대체품으로 변경해버릴 경우 사이트 랭킹 점수에 영향이 감)
        - 주문 완료 페이지로 리다이렉션 할때 (결국 서비스 이용을 위해 이전 페이지를 다시 가져오게됨)
        - 모바일 사용자를 위해 간소화된 모바일 버전 웹사이트를 제공할때
        ```
        

[🌐 301 vs 302 상태 코드 차이점 (SEO)](https://inpa.tistory.com/entry/HTTP-🌐-301-vs-302-상태-코드-차이점-💯-완벽-정리)

## 4xx (Client Error)

- 400 (Bad Request)
    
    클라이언트가 잘못된 요청을 해서 서버가 요청을 처리할 수 없음 (요청 파라미터 잘못 됨, API 스펙이 안맞음)
    
- 401 (Unauthorized)
    
    인증 되지 않음 (로그인, ADMIN같은 권한)
    
- 403 (Forbidden)
    
    서버가 요청을 이해했지만 승인을 거부
    
- 404 (Not Found)
    
    요청 리소스를 찾을 수 없음
    

## 5xx (Server Error)

- 500 (Internal Server Error)
    
    애매하면 다 이거로 걍 ㄱㄱ
    
- 503 (Service Unavailable)
    
    일시적인 과부하 또는 예정된 작업으로 요청 처리 불가
    

### 상태 코드는 클라이언트와 서버간의 통신상태를 나타내는 약속

[데이터가 없을 때 200인가 404인가?](https://techblog.yogiyo.co.kr/데이터가-없을-때-200인가-404인가-f1c8c39ca9df)