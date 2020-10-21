# 📚 var & let & const
- ES6(ES2015)이전에는 변수를 선언할 수 있는 키워드가 `var` 뿐, 하지만 ES6에서는 `let` 과 `const` 키워드가 추가 되어 이를 이용해 변수를 선언할 수 있음

## var & let & const 비교 키워드
1. 변수 값의 할당과 변환
1. 변수의 유효범위
1. 호이스팅

## 1. 변수 값의 할당과 변환
- 기존 ES6 이전의 자바스크립트의 가장 큰 문제점은 변수 선언 방식이었음(`var`를 사용하면 변수 선언이 여러번 가능하여 값이 유동적으로 변경될 수 있는 단점을 가짐)

    ### **ES6 이전 CODE ⌨️**

    ``` javascript
    var name = "홍길동";
    console.log(name);

    var name = "김철수";
    console.log(name);

    /*
    <출력>
    "홍길동"
    "김철수"
    */

    ```

- 위 코드와 같이 name이라는 변수를 2번 선언했는데도 에러가 발생하지 않고 각기 다른 값이 출력되는 것이 문제(실수로 같은 변수명을 사용했을 때 원하지 않던 결과가 나올수 있음)
- 이러한 문제들을 해결하기 위해 ES6에서 새로 등장한 `let`과 `const`는 `var`와 같이 여러번 선언하는 방식을 막음

    ### **ES6 이후 CODE ⌨️**

    ``` javascript
    let name = "홍길동";
    console.log(name);

    let name = "김철수";
    console.log(name);

    /*
    <출력>
    Identifier 'name' has already been declared (에러 발생)
    */

    ```
- 위 코드와 같이 let을 사용했을 경우 name이 이미 선언되어 있다는 에러 메세지가 보여짐(`const`도 마찬가지)
- `let` 과 `const`의 차이
    - `let`과 `const`는 모두 변수를 다시 선언하는 것은 불가능.
    - 둘의 차이는 immutable(불변성).
    - `let`으로 선언한 변수는 값의 재할당이 가능한 반면, `const`로 선언한 변수는 값의 재할당이 불가능(`const` : immutable)

    ### **let vs const CODE ⌨️**
    ``` javascript
    /*let*/
    
    let letTest = 'letTest1'; // 출력 : letTest1
    let letTest = 'letTest2'; // 출력 : Uncaught SyntaxError: Identifier 'letTest' has already been declared(이미 선언되었다는 에러 발생)
    letTest = 'letTest3'; // 출력 : letTest3

    ```

    ``` javascript
    /*const*/

    const constTest = 'constTest1'; // 출력 : constTest1
    const constTest = 'constTest2'; // 출력 : Uncaught SyntaxError: Identifier 'letTest' has already been declared(이미 선언되었다는 에러 발생)
    constTest = 'constTest3'; // 출력 : Uncaught TypeError:Assignment to constant variable.(상수에 할당할수 없다는 에러 발생)

    ```

    ## 2. 변수의 유효범위(Scope)
    - `var` : 기본적으로 함수 범위를 가짐
    - `let`, `const` : 블록 범위를 가짐
    - 자바스크립트의 범위(scope)에 관해서는 [JavaScript_Scope](./JavaScript_Scope.md)에서 학습

    ## 3. 호이스팅(Hoisting)
    - 자바 스크립트에서 모든 변수는 호이스트 됨
    - 호이스트란, 변수의 정의가 그범위에 따라 선언(declaration)/초기화(initialization)/할당(assignment)으로 분리되는 것을 의미

        ### **작성 CODE ⌨️**
        ``` javascript
        function hoisting() {
            console.log('name :', name);
            var name = '홍길동';
            console.log('name :', name);
        }

        hoisting();
        /*
            <출력>
            name : undefined
            name : 홍길동
        */

        ```

        ### **호이스팅 CODE ⌨️**
        ```javascript
        function hoisting() {
            var name; // name 변수는 호이스트 되어 변수 선언부가 함수 최상단으로 이동, 이때 값은 아직 정의되지 않아 undefined
            console.log('name :', name); // name : undefined
            name = '홍길동'; // name에 값 할당
            console.log('name :', name); // name : 홍길동
        }

        hoisting();

        ```
    - `let` 과 `const` 도 호이스팅이 되는가??
        ``` javascript
        fonction hoisting() {
        console.log("name:", name);
        let name = "홍길동";
        }

        hoisting();
        // ReferenceError: name is not defined
        ```
        - 위 코드를 실행해보면 name in not defined라는 에러가 발생
        - `let`, `const` 선언은 기본적으로 실행중인 실행 컨텍스트의 어휘적 환경(Lexical Environment)으로 범위가 지정된 변수를 정의
        - 변수는 그들의 어휘적 환경에 포함될 때 생성되지만, 어휘적 바인딩이 실행되기 전까지는 엑세스할 수 없다.이러한 현상을 TDZ(Temporal Dead Zone)라고 함( 쉽게 말해서 스코프에 진입할 때 변수가 만들어지고 TDZ가 생성되지만, 코드 실행이 변수가 실제 있는 위치에 도달할 때까지 엑세스 할 수 없음)
        - 결국 `let` 과 `const`도 호이스트가 발생하지만, TDZ(선언은 되어있지만 아직 초기화가 되지않아 변수에 담길 값을 위한 공간이 메모리에 할당되지 않은 상태) 구간에 있어 실제 변수 할당 이전까지 해당 변수에 접근을 제한하는 것

## 📖 정리
키워드|재선언|재할당|범위(scope)|호이스팅
:---:|:---:|:---:|:---:|:---:
`var`|O|O|함수범위|발생
`let`|X|O|블록범위|발생(TDZ 생성 : 할당전 접근 불가)
`cont`|X|X|블록범위|발생(TDZ 생성 : 할당전 접근 불가)