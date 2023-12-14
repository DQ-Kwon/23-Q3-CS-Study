# :books: HTTP & HTTPS <sub>HTTP와 HTTPS</sub>

## :bookmark_tabs: 목차

[:arrow_up: **Network**](../README.md)

1. ### [HTTP](#📕-http-하이퍼-텍스트-전송-프로토콜) <sub>하이퍼 텍스트 전송 프로토콜</sub>
2. ### [HTTPS](#📙-https-https-프로토콜) <sub>하이퍼 텍스트 전송 프로토콜 시큐어</sub>

# :closed_book: HTTP <sub>하이퍼 텍스트 전송 프로토콜</sub>

## 정의

> HTML과 같은 하이퍼미디어 문서를 전송하기 위한 애플리케이션 계층 프로토콜

## 특징

![img:HTTP의 사용](../img/http_01.png)

- Hypertext Transfer Protocol의 약어
- 웹에서 이루어지는 모든 데이터 교환의 기초
- 대표적인 클라이언트<sub>Client</sub>-서버<sub>Server</sub> 프로토콜
- 클라이언트에 의해 메시지가 요청<sub>Requests</sub>되면 서버에서 메시지를 응답<sub>Responses</sub>하는 구조
- 비연결<sub>Connectionless</sub>과 무상태성<sub>Stateless</sub>을 가짐
- 예약된 네트워크 포트 80번을 사용

> **Client-Server Protocol**
>
> - 수신자 측에 의해 요청이 초기화되는 프로토콜

> **비연결<sub>Connectionless</sub>**
>
> - 클라이언트가 요청을 서버로 보내고 서버가 적절한 응답을 보내면 연결이 끊어짐

> **무상태성<sub>Stateless</sub>**
>
> - 연결을 끊는 순간 클라이언트와 서버의 통신은 끝나며 상태 정보를 폐기
> - 이전에 요청한 결과를 갖고있지 않음

## HTTP의 동작 과정

> 서버 접속 -> 클라이언트 -> 요청 -> 서버 -> 응답 -> 클라이언트 -> 연결 종료

1. 사용자가 웹 브라우저에 URL 주소를 입력
2. DNS 서버에 웹 서버의 호스트 이름을 IP 주소로 변경 요청
3. 웹서버와 TCP 3 way-handshaking 연결을 시도
4. 클라이언트가 서버에게 요청한다.
   - **HTTP Request Message = `Request Header` + `Blank Line` + `Request Body`**
     - Request Header
       - 요청 메소드 + 요청 URI + HTTP 프로토콜 버전  
         `GET /background.png HTTP/1.0` `POST / HTTP 1.1`  
         Header 정보(key-value 구조)
     - Blank Line
       - 요청에 대한 모든 메타 정보가 전송되었음을 알리는 용도
     - Request Body
       - 데이터 업데이트 요청과 관련된 내용 (HTML 폼 콘텐츠 등)
       - GET, HEAD, DELETE, OPTIONS처럼 리소스를 가져오는 요청에는 없음
5. 서버가 클라이언트에게 데이터를 응답한다.
   - **HTTP Response Message = `Response Header` + `Blank Line` + `Response Body`**
     - Response Header
       - HTTP 프로토콜 버전 + 응답 코드 + 응답 메시지  
         `HTTP/1.1 404 Not Found.`  
          Header 정보(key-value 구조)
     - Blank Line
       - 요청에 대한 모든 메타 정보가 전송되었음을 알리는 용도
     - Request Body
       - 응답 리소스 데이터
       - 201, 204 상태 코드에는 없음
6. 4 way-handshaking를 사용해 서버 클라이언트 간 연결종료(무상태성)
7. 웹 브라우저가 웹 문서 출력

## HTTP의 요청 메소드

- `GET` : 정보를 요청하기 위해 사용(SELECT)
- `POST` : 정보를 밀어넣기 위해 사용(INSERT)
- `PUT` : 정보를 업데이트하기 위해서 사용(UPDATE)
- `DELETE` : 정보를 삭제하기 위해서 사용(DELETE)
- `HEAD` : (HTTP)헤더 정보만 요청. 해당 자원이 존재하는지 혹은 서버에 문제가 없는지를 확인하기 위해 사용
- `OPTIONS` : 웹 서버가 지원하는 메서드의 종류를 요청
- `TRACE` : 클라이언트의 요청을 그대로 반환. 주로 echo 서비스로 서버 상태를 확인하기 위한 목적으로 사용

# :orange_book: HTTPS <sub>하이퍼 텍스트 전송 프로토콜 시큐어</sub>

## 정의

> HTTP에 보안요소를 추가한 차세대 프로토콜

## 특징

- Hypertext Transfer Protocol Secure의 약어
- HTTP의 보안 취약점을 보완하기 위해 SSL을 적용한 보안 프로토콜
- 예약된 네트워크 포트 433번을 사용

> SSL<sub>Secure Sockets Layer</sub>
>
> - 웹사이트와 브라우저 사이(또는 두 서버 사이)에 전송되는 데이터를 암호화하여 인터넷 연결을 보호하기 위한 표준 기술

## HTTPS의 동작 과정

![HTTPS의 동작](../img/http_ssl_01.png)

1. Client Hello
   - 클라이언트가 서버에게 전송할 데이터
   - 클라이언트 측에서 생성한 랜덤 데이터
   - 클라이언트-서버 암호화 방식 통일을 위해 클라이언트가 사용할 수 있는 암호화 방식
   - 이전에 이미 Handshaking 기록이 있다면 자원 절약을 위해 기존 세션을 재활용하기 위한 세션 아이디
2. Server Hello
   - Client Hello에 대한 응답으로 전송할 데이터
   - 서버 측에서 생성한 랜덤 데이터
   - 서버가 선택한 클라이언트의 암호화 방식
   - SSL 인증서
3. Client 인증 확인
   - 서버로부터 받은 인증서가 CA에 의해 발급되었는지 본인이 가지고 있는 목록에서 확인하고, 목록에 있다면 CA 공개키로 인증서 복호화
   - 클-서 각각의 랜덤 데이터를 조합하여 pre master secret 값 생성(데이터 송수신 시 대칭키 암호화에 사용할 키)
   - pre master secret 값을 공개키 방식으로 서버 전달(공개키는 서버로부터 받은 인증서에 포함)
   - 일련의 과정을 거쳐 session key 생성
4. Server 인증 확인
   - 서버는 비공개키로 복호화하여 pre master secret 값 취득(대칭키 공유 완료)
   - 일련의 과정을 거쳐 session key 생성
5. Handshaking 종료
   - 데이터 전송
   - 서버와 클라이언트는 session key를 활용해 데이터를 암복호화하여 데이터 송수신
     연결 종료 및 session key 폐기

## HTTPS의 요청 메소드

- [HTTP](#http의-요청-메소드)와 동일
