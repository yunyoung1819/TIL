# :book: 스프링부트

## :pushpin: 스프링부트 CRUD 만들기

### :seedling: 통신이란?

- Socket 통신
    - 접속을 계속 유지하여, 데이터를 전달 한다.
    - 서버의 자원에 따라서 연결될 수 있는 클라이언트의 숫자가 한정된다.
    - 실시간 정보 교환에 사용하며 HTTP보다 속도가 빠르다.

- HTTP 통신
    - 클라이언트의 요청이 있을 때만 데이터 응답을 전달한다.
    - 불필요한 자원의 점유를 없애 다른 접속을 원활하게 하여 많은 데이터를 처리한다.
    - 데이터 요청 후 응답이 오면 연결은 끊어진다. 
    
    
### 통신

![통신](./image/통신.png)


### :seedling: HTTP Method

### Rest API

#### HTTP - GET Method 
- 주소 창에 파라미터가 노출 된다.
- Example

````
www.localhost:8080/search?id=account&password=1234
www.google.com/search?id=abcd
````

- 브라우저에서 주소에 대한 캐시가 이루어 지므로, 정보를 얻을 때 사용한다.


#### HTTP - POST Method
- 주소 창에 파라미터가 노출 되지 않는다.

- Example
````
www.localhost:8080/search
www.google.com/search
````

- 주소 창에 사용자의 요청 사항이 노출되지 않는다.
- Get 방식에서는 주소 길이 제한이 있지만 POST는 그보다 길게 사용 가능(제한 존재)
- 브라우저가 주소 캐시를 하지 못하는 특성이 있다.


#### HTTP - PUT/PATCH Method

- POST와 마찬가지로 BODY에 데이터가 들어 있으며, 주로 업데이트에 사용한다.


#### HTTP - DELETE Method

- Get과 마찬가지로 주소에 파라미터가 들어가며, 데이터를 삭제할 때 사용한다.


### REST의 개념

- HTTP 프로토콜에 있는 Method를 활용한 아키텍처 스타일이다.
- HTTP Method를 통해서 Resource를 처리한다.
- CRUD를 통한 Resource 조작을 할 때 사용한다.

HTTP Method | 동작 | URL 형태
-----------| ------| ------
GET | 조회 (SELECT * READ) | /user/{id}
POST | 생성 (CREATE) | /user
PUT/PATCH | 수정 (UPDATE) * CREATE | /user
DELETE | 삭제(DELETE) | /user/{1}


