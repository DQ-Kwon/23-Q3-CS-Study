# :books: Cookie & Session <sub>쿠키와 세션</sub>

## :bookmark_tabs: 목차

[:arrow_up: **Network**](../README.md)

1. ### [Cookie](#📕-cookie-쿠키)
2. ### [Session](#📙-session-세션)

# :closed_book: Cookie <sub>쿠키</sub>

## 정의

> 웹 서버에 접속할 때 생성되는 정보를 담은 임시 파일

## 특징

- HTTP의 데이터의 일종
- 사용자가 어떠한 웹 사이트를 방문할 경우, 해당 웹 서버에서 사용자의 컴퓨터에 사용자 상태 정보를 저장하는 기록 파일
- 클라이언트의 PC에 상태 정보를 저장했다가 필요시 정보를 참조하거나 재사용 함
- 이름, 값, 만료일(저장 기간 설정), 경로 정보로 구성
- 데이터 형태는 키-값쌍으로 이루어진 String으로 저장하며 `;`를 기준으로 구분
  `document.cookie = 'userId=adjh54; path=/; max-age=3600;';`
- 브라우져별로 저장가능한 쿠키의 수가 다르며, 하나의 쿠키는 약 4KB까지 저장함

## 쿠키의 동작 순서

1. 클라이언트가 페이지를 요청 (사용자가 웹사이트 접근)
2. 웹 서버는 쿠키를 생성
3. 웹 서버는 HTTP 화면을 응답할 때 생성한 쿠키에 정보를 클라이언트에게 전송
4. 쿠키는 클라이언트가 가지고 있다가 서버에 요청할 때 요청과 함께 쿠키를 전송
   - 동일 사이트 재방문시 해당 쿠키가 있는 경우, 요청 페이지와 함께 쿠키를 전송

## 쿠키의 사용처

- **세션관리(Session Management)**
  - 로그인 인증, 사용자 닉네임, 접속시간, 장바구니 등의 서버가 알아야 할 정보들을 저장
- **개인화(Personalization)**
  - 사용자마다 다르게 각자에 맞는 적절한 정보나 광고를 보여줌
- **트래킹(Tracking)**
  - 사용자의 행동과 패턴을 분석하고 기록

## VanillaJS에서 쿠키 다루기

### 쿠키 등록 / 수정

- 쿠키에서 Cookie-name을 맞추게 된다면 수정 및 쿠키의 시간을 연장이 가능

```js
/**
 * Cookie의 값을 세팅해주는 함수
 * @param {string} cookieName : 쿠키의 이름
 * @param {string} cookieValue : 쿠키의 값
 * @param {number} expiresHour : 쿠키의 만료일
 * @return {void}
 */

const setCookie = (
  cookieName: string,
  cookieValue: string,
  expiresHour: number
): void => {
  const expired = new Date();
  expired.setTime(expired.getTime() + expiresHour * 24 * 60 * 60 * 1000);
  document.cookie = `${cookieName}=${cookieValue}; path=/; Expires=${expired}`;
};
```

### 쿠키 조회

```js
/**
 * Cookie의 값을 반환해주는 함수
 * @param cookieName
 * @returns {string} cookie value
 */

const getCookie = (cookieName: string): string => {
  let result = "";
  // 1. 모든 쿠키를 가져와서 분리 함
  document.cookie.split(";").map((item) => {
    // 2. 분리한 값의 앞뒤 공백 제거
    const cookieItem = item.trim();
    // 3. 키 값과 매칭이 되는 값을 반환
    if (item.includes(cookieName)) {
      result = cookieItem.split("=")[1];
    }
  });
  return result; // 존재하면 값을 반환, 미 존재하면 빈값 반환
};
```

### 쿠키 삭제

```js
/**
 * Cookie의 값을 삭제 해주는 함수
 * @param {string} cookieName : 쿠키의 이름
 * @return {void}
 */

const deleteCookie = (cookieName: string): void => {
  document.cookie = `${cookieName}=0; max-age=0`;
};
```

# :orange_book: Session <sub>세션</sub>

## 특징

- 웹 서버에 웹 컨테이너의 상태를 유지하기 위한 정보를 저장
- 웹 서버의 저장되는 쿠키또는 토큰으로 취급(=세션 쿠키, 세션 토큰)
- 사용자가 브라우저를 닫거나 서버가 세션을 만료시켰을때만 삭제됨
- 서버측에서 데이터를 다루므로 쿠키보다 보안이 비교적 좋음
- 저장 데이터에 규격과 용량의 제한이 없음
- 각 클라이언트마다 고유의 Session ID를 부여해 관리함
  - Session ID로 클라이언트를 구분하여 각 클라이언트 요구에 맞는 서비스 제공

## 세션의 동작 순서

1. 클라이언트가 페이지를 요청(사용자가 웹사이트 접근)
2. 서버는 클라이언트의 Request-Header 필드의 Cookie를 확인
   1. 클라이언트의 session-id가 존재하면
      - 서버에서 session-id가 일치하는 세션에 접근해 상태 정보를 저장/수정
   2. 클라이언트의 session-id가 존재하지 않으면
      - 서버는 session-id를 생성해 클라이언트에게 반환하고 새로운 세션을 생성
3. 웹 서버는 HTTP 화면을 응답할 때 session-id를 기록한 쿠키를 클라이언트에게 전송
   - 클라이언트는 재접속 시, 쿠키를 이용하여 session-id 값을 서버에 전달

## 세션의 사용처

- 쿠키와 사용 목적이 대부분 일치
- **세션관리(Session Management)**
  - 로그인 인증, 사용자 닉네임, 접속시간, 장바구니 등의 서버가 알아야 할 정보들을 저장
- **개인화(Personalization)**
  - 사용자마다 다르게 각자에 맞는 적절한 정보나 광고를 보여줌
- **트래킹(Tracking)**
  - 사용자의 행동과 패턴을 분석하고 기록
