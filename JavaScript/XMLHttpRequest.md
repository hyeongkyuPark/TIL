# 📚 XMLHttpRequest 객체

## 🔍 XMLHttpRequest 란?
- 브라우저는 주소창이나 HTML의 form 태그 또는 a 태그를 통해 HTTP 요청 전송 기능을 기본 제공함
- 자바스크립트를 사용하여 HTTP 요청을 전송하기위해 사용하는 객체가 XMLHttpRequest 임
- Web API인 XMLHttpRequest 객체는 HTTP 요청 전송과 HTTP 응답 수신을 위한 다양한 메서드와 프로퍼티를 제공

## 📗 XMLHttpRequest 객체 생성
- XMLHttpRequest 객체는 XMLHttpRequest 생성자 함수를 호출하여 생성(XMLHttpRequest 객체는 브라우저에서 제공하는 Web API이므로 브라우저 환경에서만 정상작동)
- ### **CODE ⌨️**
    ``` javascript
    //XMLHttpRequest 객체 생성
    const xhr = new XMLHttpRequest();
    
    ```

## 📗 XMLHttpRequest 객체의 프로퍼티와 메서드
- XMLHttpRequest 객체의 프로토타입 프로퍼티
    - readyState : HTTP 요청의 현재 상태를 나타내는 정수.
        - UNSET : 0
        - OPEND : 1
        - HEADERS_RECEIVED : 2
        - LOADING : 3
        - DONE : 4
    - status : HTTP 요청에 대한 응답 상태(HTTP 상태 코드)를 나타내는 정수(200, 400, 500 등)
    - statusText : HTTP 요청에 대한 응답 메세지를 나타내는 문자열("OK" 등)
    - responseType : HTTP 응답 타입
    - response : HTTP 요청에 대한 응답 몸체(response body).
    - responseText : 서버가 전송한 HTTP 요청에 대한 응답 문자열

- XMLHttpRequest 객체의 이벤트 핸들러 프로퍼티
    - onreadystatechange : readyState 프로퍼티 값이 변경된 경우 발생
    - onloadstart : HTTP 요청에 대한 응답을 받기 시작한 경우 발생
    - onprogress : HTTP 요청에 대한 응답을 받는 도중 주기적으로 발생
    - onabort : abort 메서드에 의해 HTTP 요청이 중단된 경우 발생
    - onerror : HTTP 요청에 에러가 발생한 경우 발생
    - onload : HTTP 요청이 성공적으로 완료한 경우 발생
    - ontimeout : HTTP 요청 시간이 초과한 경우 발생
    - onloadend : HTTP 요청이 완료한 경우. HTTP 요청이 성공 또는 실패하면 발생

- XMLHttpRequest 객체의 메서드
    - open : HTTP 요청 초기화
    - send : HTTP 요청 전송
    - abort : 이미 전송된 HTTP 요청 중단
    - setRequestHeader : 특정 HTTP 요청 헤더의 값을 설정
    - getResponseHeader : 특정 HTTP 요청 헤더의 값을 문자열로 변환

- XMLHttpRequest 객체의 정적 프로퍼티
    - UNSET(0) : open 메서드 호출 이전
    - OPEND(1) : open 메서드 호출 이후
    - HEADERS_RECEIVED(2) : send 메서드 호출 이후
    - LOADING(3) : 서버 응답 중(응답 데이터 미완성 상태)
    - DONE(4) : 서버 응답 완료


## 📗 HTTP 요청 전송
1. XMLHttpRequest.prototype.open 메서드로 HTTP 요청을 초기화
1. 필요에 따라 XMLHttpRequest.prototype.setRequestHeader 메서드로 특정 HTTP 요청의 헤더 값을 설정
1. XMLHttpRequest.prototype.send 메서드로 HTTP 요청을 전송

- ### **CODE ⌨️**
    ``` javascript
    // XMLHttpRequest 객체 생성
    const xhr = new XMLHttpRequest();

    // HTTP 요청 초기화(요청메서드, url주소)
    xhr.open("GET", "https://jsonplaceholder.typicode.com/todos");

    // HTTP 요청 헤더 설정
    // 클라이언트가 서버로 전송할 데이터의 MIME 타입 지정: json
    xhr.setRequestHeader('content-type', 'application/json');

    // HTTP 요청 전송
    xhr.send();
    
    ```
    - ### **XMLHttpRequest.prototype.open**
        - 기본형태 : xhr.open(method, url[, async])
            - method : HTTP 요청 메서드("GET", "POST", "PUT", "DELETE" 등)
            - url : HTTP 요청을 전송할 URL
            - async : 비동기 요청 여부. 옵션으로 기본값은 true이며, 비동기 방식으로 동작
        - HTTP 요청 메서드는 클라이언트가 서버에게 요청의 종류와 목적(리소스에 대한 행위)을 알리는 방법. 주로 5가지 요청 메서드를 사용해 CRUD(Create, Read, Update, Delete)를 구현
            - GET : 모든/특정 리소스 취득
            - POST : 리소스 생성
            - PUT : 리소스 전체 교체
            - PATCH : 리소스 일부 수정
            - DELETE : 모든/특정 리소스 삭제

    - ### **XMLHttpRequest.prototype.send**
        - open 메서드로 초기화된 HTTP 요청을 서버에 전송
        - 기본적으로 서버로 전송하는 데이터는 GET, POST 요청 메서드에 따라 전송 방식에 차이가 있음
            - GET : 데이터를 URL 일부분인 쿼리 문자열로 서버에 전송
            - POST : 데이터(페이로드)를 요청 몸체(request body)에 담아 전송
        - send 메서드에는 요청 몸체에 담아 전송할 데이터(페이로드)를 인수로 전달할 수 있음. 페이로드가 객체인 경우 반드시 JSON.stringify 메서드를 사용해 직력화한 다음 전달해야 함
            ``` javascript
            xhr.send(JSON.stringify({id : 1, content : 'HTML', completed : false}));
            ```
            - HTTP 요청 메서드가 GET인 경우 send 메서드에 페이로드로 전달한 인수는 무시되고 요청 몸체는 null로 설정됨


    - ### **XMLHttpRequest.prototype.setRequestHeader**
        - setRequestHeader 메서드는 특정 HTTP 요청의 헤더 값을 설정함
        - setRequestHeader 메서드는 반드시 open 메서드를 호출한 이후에 호출해야함
        - content-type : 요청 몸체에 담아 전송할 데이터의 MIME 타입의 정보를 표현
            - text : text/plain, text/html, text/css, text/javascript
            - application : application/json, application/x-wwwform-urlencode
            - multipart : multipart/formed-data
        - ### **CODE ⌨️**
            ``` javascript
            const xhr = new XMLHttpRequest();

            xhr.open('POST', 'https://jsonplaceholder.typicode.com/todos');

            xhr.setRequestHeader('content-type', 'application/json');

            xhr.send(JSON.stringify(
                {
                    "userId": 1,
                    "title": "delectus aut autem",
                    "completed": false
                }
            ));
            
            ```
        - Accept : HTTP 클라이언트가 서버에 요청할 때 서버가 응답할 데이터의 MIME 타입을 지정할 수 있음
        - ### **CODE ⌨️**
            ``` javascript
            xhr.setRequestHeader('accept', 'application/json');
            ```


## 📗 HTTP 응답 처리
- 서버가 전송한 응답을 처리하려면 XMLHttpRequest 객체가 발생시키는 이벤트를 캐치해야 함
- XMLHttpRequest 객체는 onreadystatechange, onload, onerror 같은 이벤트 핸들러 프로퍼티를 가짐
- HTTP 요청의 현재 상태를 나타내는 readyState 프로퍼티 값이 변경된 경우 발생하는 onreadystatechange 이벤트를 캐치하여 다음과 같이 HTTP 응답을 처리할 수 있음
    - ### **CODE ⌨️**
        ``` javascript
        const xhr = new XMLHttpRequest();

        xhr.open('GET', 'https://jsonplaceholder.typicode.com/todos/1');

        xhr.send();

        xhr.onreadystatechange = () => {
            // readyState 프로퍼티는 HTTP 요청의 현재 상태를 나타냄
            // readyState 프로퍼티 값이 4(XMLHttpRequest.DONE)가 아니면 서버 응답이 완료되지 않은 상태
            // 만약 서버 응답이 아직 완료되지 않았다면 아무런 처리를 하지 않음
            if(xhr.readyState !== XMLHttpRequest.DONE) return;

            // status 프로퍼티는 응답 상태 코드
            // status 프로퍼티 값이 200이면 정상적으로 응답된 상태
            // status 프로퍼티 값이 200이 아니면 에러 발생
            // 정상적으로 응답된 상태라면 reponse 프로퍼티에 서버의 응답 결과가 담겨있음
            if(xhr.status === 200) {
                console.log(JSON.parse(xhr.response));
                // {userId: 1, id: 1, title: "delectus aut autem", completed: false}
            } else {
                console.error('Error', xhr.status, xhr.statusText);
            }
        };
        
        ```
        - send 메서드를 통해 HTTP 요청을 서버에 전송하면 서버는 응답을 반환하지만 언제 응답이 클라이언트에 도달할지는 알 수 없음
        - 따라서 onreadystatechange(HTTP 요청의 현재 상태를 나타내는 readyState 프로퍼티가 변경될 때마다 발생) 이벤트를 통해 HTTP 요청의 현재 상태를 확인해야함

    - ### **CODE ⌨️**
        ``` javascript
        const xhr = new XMLHttpRequest();

        xhr.open('GET', 'https://jsonplaceholder.typicode.com/todos/1');

        xhr.send();

        // onload 이벤트는 HTTP 요청이 성공적으로 완료된 경우 발생
        xhr.onload = () => {
            // status 프로퍼티는 응답 상태 코드
            // status 프로퍼티 값이 200이면 정상적으로 응답된 상태
            // status 프로퍼티 값이 200이 아니면 에러 발생
            // 정상적으로 응답된 상태라면 reponse 프로퍼티에 서버의 응답 결과가 담겨있음
            if(xhr.status === 200) {
                console.log(JSON.parse(xhr.response));
                // {userId: 1, id: 1, title: "delectus aut autem", completed: false}
            } else {
                console.error('Error', xhr.status, xhr.statusText);
            }
        };
        
        ```
        - onreadystatechange 이벤트 대신 load 이벤트를 캐치하면 HTTP 요청이 성공적으로 완료된 경우 발생하기 때문에 xhr.readyState가 XMLHttpRequest.DONE인지 확인할 필요가 없음