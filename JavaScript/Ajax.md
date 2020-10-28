# 📚 Ajax(Asynchronous Javascript and XML)

## 🔍 Ajax 란?
- 자바스크립트를 사용하여 브라우저가 서버에게 비동기 방식으로 데이터를 요청하고, 서버가 응답한 데이터를 수신하여 웹페이지를 동적으로 갱신하는 프로그래밍 방식
- Ajax는 브라우저에서 제공하는 Web API인 XMLHttpRequest 객체(HTTP 비동기 통신을 위한 메서드와 프로퍼티 제공)를 기반으로 동작
- 전통적인 방식의 렌더링
    - HTML을 서버로부터 전송받아 웹페이지 전체를 다시 렌더링하는 방식
    - 이전 웹페이지와 차이가 없어서 변경할 필요가 없는 부분까지 포함된 완전한 HTML을 서버로부터 매번 다시 전송받기 때문에 불필요한 데이터 통신이 발생
    - 변경이 필요 없는 부분까지 처음부터 다시 렌더링하기 때문에 화면 전환이 일어나면 화면이 순간적으로 깜박이는 현상 발생
    - 클라이언트와 서버와의 통신이 동기 방식으로 동작하기 때문에 서버로부터 응답이 있을 때까지 다음 처리는 블로킹 됨
- Ajax는 전통적인 방식과 비교했을 때 많은 장점이 있음
    - 변경할 부분을 갱신하는 데 필요한 데이터만 서버로부터 전송받기 때문에 불필요한 데이터 통신이 발생하지 않음
    - 변경할 필요가 없는 부분은 다시 렌더링하지 않음. 따라서 화면이 순간적으로 깜박이는 현상이 발생하지 않음
    - 클라이언트와 서버와의 통신이 비동기 방식으로 동작하기 때문에 서버에게 요청을 보낸 이후 블로킹이 발생하지 않음


## 📙 JSON(Javascript Object Notation)
- 클라이언트와 서버간의 HTTP 통신을 위한 텍스트 데이터 포맷
- 자바스크립트에 종속되지 않는 언어 독립형 데이터 포맷으로, 대부분의 프로그래밍 언어에서 사용 가능
- ### **JSON 표기 방식**
    - JSON은 자바스크립트의 객체 리터럴과 유사하게 키와 값으로 구성된 순수한 텍스트
        ``` json
        {
            "name" : "Lee",
            "age" : 20,
            "alive" : true,
            "hobby" : ["traveling", "tennis"]
        }
        ```
    - JSON의 키는 반드시 큰따옴표(작은따옴표 사용불가)로 묶어야함
    - 값은 객체 리터럴과 같은 표기법을 그대로 사용할 수 있지만 문자열은 반드시 큰따옴표(작은따옴표 사용불가)로 묶어야함
- ### **JSON.stringify**
    - JSON.stringify 메서드는 객체를 JSON 포맷의 문자열로 변환
    - 클라이언트가 서버로 객체를 전송하려면 객체를 문자열화 해야하는데 이를 직렬화(serializing)라고 함
    - ### **CODE**
        ``` javascript
        const obj = {
            name: 'Lee',
            age: 20,
            alive: true,
            bobby: ['traveling', 'tennis']
        };

        // 객체를 JSON 포맷의 문자열로 변환
        const json = JSON.stringify(obj);
        console.log(typeof json, json); // String {"name":"Lee", "age":20, "alive":true, "hobby":["traveling", "tennis"]}

        // 객체를 JSON 포맷의 문자열로 변환하면서 들여쓰기 함
        const prettyJson = JSON.stringify(obj, null, 2);
        console.log(typeof prettyJson, prettyJson);
        /*
        String {
            "name" : "Lee",
            "age" : 20,
            "alive" : true,
            "hobby" : [
                "traveling", 
                "tennis"
            ]
        }
        */

        // replacer 함수. 값의 타입이 Number이면 필터링되어 반환되지 않음
        function filter(key, value) {
            // undefined : 반환하지 않음
            return typeof value === 'number' ? undefined : value;
        }

        // JSON.stringify 메서드에 두 번째 인수로 replacer 함수를 전달
        const strFilteredObject = JSON.stringify(obj, filter, 2);
        /*
        String {
            "name" : "Lee",
            "alive" : true,
            "hobby" : [
                "traveling", 
                "tennis"
            ]
        }
        */

        // JSON.stringify 메서드는 객체뿐만 아니라 배열도 JSON 포맷의 문자열로 반환
        const todos = [
            {id: 1, content: 'HTML', completed: false},
            {id: 2, content: 'CSS', completed: true},
            {id: 3, content: 'JavaScript', completed: false}
        ];

        // 배열을 JSON 포맷의 문자열로 변환
        const arrJson = JSON.stringify(todos, null, 2);
        console.log(typeof arrJson, arrJson);
        /*
        string [
            {
                "id": 1,
                "content": "HTML",
                "completed": false
            },
            {
                "id": 2,
                "content": "CSS",
                "completed": true
            },
            {
                "id": 3,
                "content": "JavaScript",
                "completed": false
            }
        ]
        */

        ```

- ### **JSON.parse**
    - JSON.parse 메서드는 JSON 포맷의 문자열을 객체로 변환
    - 서버로부터 클라이언트에게 전송된 JSON 데이터는 문자열임. 이 문자열을 객체로서 사용하려면 JSON 포맷의 문자열을 객체화해야 하는데 이를 역직렬화(deserializing)라고 함
    - ### **CODE**
        ``` javascript
        const obj = {
            name: 'Lee',
            age: 20,
            alive: true,
            bobby: ['traveling', 'tennis']
        };

        // 객체를 JSON 포맷의 문자열로 변환
        const json = JSON.stringify(obj);

        // JSON 포맷의 문자여을 객체로 변환
        const parsed = JSON.parse(json);
        console.log(typeof parsed, parsed);
        // object {name:"Lee", age:20, alive:true, hobby:["traveling","tennis"]}


        // 배열이 JSON 포맷의 문자열로 변환되어 있는 경우 JSON.parse는 문자열을 배열 객체로 변환.
        // 배열의 요소가 객체인 경우 배열의 요소까지 객체로 변환
        const todos = [
            {id: 1, content: 'HTML', completed: false},
            {id: 2, content: 'CSS', completed: true},
            {id: 3, content: 'JavaScript', completed: false}
        ];

        // 배열을 JSON 포맷의 문자열로 변환
        const arrJson = JSON.stringify(todos);

        //JSON 포맷의 문자열을 배열로 변환. 배열의 요소까지 객체로 변환
        const arrParsed = JSON.parse(arrJson);
        console.log(typeof arrParsed, arrParsed);
        /*
        Object [
            {id: 1, content: 'HTML', completed: false},
            {id: 2, content: 'CSS', completed: true},
            {id: 3, content: 'JavaScript', completed: false}
        ]
        */
        
        ```