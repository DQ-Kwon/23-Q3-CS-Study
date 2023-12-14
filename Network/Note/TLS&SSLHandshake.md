# :books: TLS/SSL Handshake <sub>TLS/SSL 핸드셰이크</sub>

## :bookmark_tabs: 목차

[:arrow_up: **Network**](../README.md)

1. ### [TLS/SSL Handshake](#📕-tlsssl-handshake-tlsssl-핸드셰이크) <sub>TLS/SSL 핸드셰이크</sub>

# :closed_book: TLS/SSL Handshake <sub>TLS/SSL 핸드셰이크</sub>

## 정의

> 전송 계층 보안<sub>Transport Layer Security, TLS</sub> 또는 보안 소켓 레이어<sub>Secure Sockets Layer, SSL</sub>를 통한 안전한 인터넷 통신을 위한 암호화 및 인증 프로토콜

## 특징

![img:TSL](../img/tls-ssl-handshake_01.png)

- 보안 소켓 계층<sub>SSL</sub>은 HTTP용으로 개발된 암호화 프로토콜
- SSL은 전송 계층 보안<sub>TLS</sub>으로 대체
- SSL Handshake는 "SSL"이라는 이름이 사용되지만, TLS Handshake에 포함
- 사용자가 HTTPS를 통해 웹 사이트를 탐색하고 브라우저가 처음 해당 웹 사이트의 원본 서버를 쿼리하기 시작할 때마다 발생
- TLS 프로토콜은 기밀성<sub>Confidentiality</sub>과 인증<sub>Authentication</sub>, 무결성<sub>Integrity</sub>을 보장

## TLS의 동작 과정

### 요약

1. 사용할 TLS 버전(TLS 1.0, 1.2, 1.3 등)을 지정
2. 사용할 암호 제품군을 결정
3. 서버의 공개 키와 SSL 인증서 기관의 디지털 서명을 통해 서버의 ID를 인증
4. 핸드셰이크가 완료된 후에 대칭 암호화를 사용하기 위하여 세션 키를 생성

### 상세

1. Client Hello
   - 클라이언트가 서버로 "Hello" 메시지를 전송하면서 핸드셰이크를 개시
   - 메시지에는 클라이언트가 지원하는 TLS 버전과 지원되는 암호 제품군, 무작위 바이트 문자열이 포함함
2. Server Hello
   - 클라이언트 헬로 메시지에 대한 응답으로 서버가 서버의 SSL 인증서, 서버에서 선택한 암호 제품군, 그리고 서버에서 생성한 또 다른 무작위 바이트 문자열울 함하는 메시지를 전송
3. 인증
   - 클라이언트가 서버의 SSL 인증서를 인증서 발행 기관을 통해 검증
   - 서버가 인증서에 명시된 서버인지, 그리고 클라이언트가 상호작용 중인 서버가 실제 해당 도메인의 소유자인지를 확인
4. 예비 마스터 암호
   - 클라이언트가 "예비 마스터 암호"라고 하는 무작위 바이트 문자열을 하나 더 전송
   - 예비 마스터 암호는 공개 키로 암호화되어 있으며, 서버가 개인 키로만 해독 가능
   - 클라이언트는 서버의 SSL 인증서를 통해 공개 키를 받음
5. 개인 키 사용
   - 서버가 예비 마스터 암호를 해독
6. 세션 키 생성
   - 클라이언트와 서버가 모두 클라이언트 무작위, 서버 무작위, 예비 마스터 암호를 이용해 세션 키를 생성
   - 모두 같은 결과가 나와야 함
7. 클라이언트 준비 완료
   - 클라이언트가 세션 키로 암호화된 "완료" 메시지를 전송
8. 서버 준비 완료
   - 서버가 세션 키로 암호화된 "완료" 메시지를 전송
9. 안전한 대칭 암호화 성공
   - Handshaking이 완료되고, 세션 키를 이용해 통신이 계속 진행
