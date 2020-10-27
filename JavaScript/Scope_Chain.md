# 📚 Scope Chain(스코프 체인)

## 📒 스코프 체인과 중첩 함수
- 함수는 전역에서 정의할 수도 있고 함수 몸체 내부에서 정의할 수도 있는데, 함수 몸체 내부에서 함수가 정의된 것을 '함수의 중첩'이라고 함
- 함수 몸체 내부에서 정의한 함수를  중첩함수(nested function), 중첩 함수를 포함하는 함수를 외부함수(outer function)라고 함
- 함수는 중첩될 수 있으므로 함수의 지역 스코프도 중첩될 수 있음. 이는 스코프가 함수의 중첩에 의해 계층적 구조를 갖는다는 것을 의미함
- 이때 외부 함수의 지역 스코프를 중첩 함수의 상위 스코프라고 함
- ### **CODE ⌨️**
    ``` javascript
    var x = "global x";
    var y = "global y";

    function outer() {
        var z = "outer's local z";

        console.log(x); // global x
        console.log(y); // global y
        console.log(z); // outer's local z

        function inner() {
            var x = "inner's local x";

            console.log(x); // inner's local x
            console.log(y); // global y
            console.log(z); // outer's local z
        }

        inner();
    }

    outer();

    console.log(x); // global x
    console.log(z); // ReferenceError : z is not defined

    ```
    - 위 코드에서 지역은 outer 함수의 지역과 inner 함수의 지역이 있음
    - inner 함수는 outer 함수의 중첩 함수임
    - outer 함수가 만든 지역 스코프는 inner 함수가 만든 지역 스코프의 상위 스코프임
    - outer 함수의 상위 스코프는 전역 스코프임
    - 이렇게 스코프가 계층적으로 연결된 것을 스코프 체인이라 함
    - 변수를 참조할 때 자바스크립트 엔진은 스코프 체인을 통해 변수를 참조하는 코드의 스코프에서 지가하여 상위 스코프 방향으로 이동하며 선언된 변수를 검색함. 이를 통해 상위 스코프에서 선언한 변수를 하위 스코프에서 참조할 수 있음

## 📒 스코프 체인에 의한 변수 검색
- ### **CODE ⌨️**
    ``` javascript
    var x = "global x";
    var y = "global y";

    function outer() {
        var z = "outer's local z";

        console.log(x); // global x
        console.log(y); // global y
        console.log(z); // outer's local z

        function inner() {
            var x = "inner's local x";

            console.log(x); // inner's local x
            console.log(y); // global y
            console.log(z); // outer's local z
        }

        inner();
    }

    outer();

    console.log(x); // global x
    console.log(z); // ReferenceError : z is not defined

    ```
    - 위의 코드에서 inner 함수의 내부를 살펴보면 console.log 메서드로 x, y, z를 각각 출력하고 있는데 스코프 체인에 의한 변수 검색이 이루어짐
        - `console.log(x)` : 우선 inner 함수 자신의 내부 스코프에서 식별자 x를 검색함. 존재하므로 inner 스코프의 x값(inner's local x)을 출력
        - `console.log(y)` : 우선 inner 함수 자신의 내부 스코프에서 식별자 y를 검색함. 존재하지 않으므로 상위 스코프인 outer 함수 내부에서 y를 검색함. 존재하지 않으므로 outer 함수의 상위 스코프인 전역 스코프에서 검색함. 존재하므로 전역 스코프의 y값(global y)을 출력
        - `console.log(z)` : 우선 inner 함수 자신의 내부 스코프에서 식별자 z를 검색함. 존재하지 않으므로 상위 스코프인 outer 함수 내부에서 z를 검색함. 존재하므로 outer 스코프의 z값(outer's local z)을 출력

## 📒 스코프 체인에 의한 함수 검색
- 스코프를 변수를 검색할 때 사용하는 규칙이 아니라 식별자를 검색할 때 사용하는 규칙으로 표현하는 것이 더 적합함(일반 함수를 검색할 때에도 일반 함수의 이름을 식별자로 스코프 검색을 하기 때문)
- ### **CODE ⌨️**
    ``` javascript
    function foo() {
        console.log('global');
    }

    function bar() {
        function foo() {
            console.log('local');
        }

        foo();
    }

    bar(); // local
    foo(); // foo

    ```
    - 변수 검색과 마찬가지로 bar 함수 안에서 foo 함수를 호출 하려면 우선 bar 함수의 스코프 내부에서 식별자 foo를 찾음. 존재하므로 bar 함수의 스코프 내부에 있는 foo 함수를 호출함
    