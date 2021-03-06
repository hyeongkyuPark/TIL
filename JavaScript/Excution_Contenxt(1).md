# 📚 Excution Context(실행 컨텍스트)
- 실행 컨텍스트는 자바스크립트 동작 원리를 담고 있는 핵심 개념

## 📕 소스코드의 타입
### 1. 전역 코드(global code)
- 전역 코드는 전역 변수를 관리하기 위해 최상위 스코프인 전역 스코프를 생성해야 함
- var 키워드로 선언된 전역 변수와 함수 선언문으로 정의된 전역 함수를 전역 객체의 프로퍼티와 메서드로 바인딩하고 참조하기 위해 전역 객체와 연결되어야 함. 이를 위해 전역코드가 평가되면 전역 실행 컨텍스트가 생성됨

### 2. 함수 코드(function code)
- 함수 코드는 지역 스코프를 생성하고 지역 변수, 매개변수, arguments 객체를 관리해야 함
- 생성한 지역 스코프를 전역 스코프에서 시작하는 스코프 체인의 일원으로 연결. 이를 위해 함수 코드가 평가되면 함수 실행 컨텍스트가 생성됨

### 3. eval 코드
- eval 코드는 strict mode(엄격모드)에서 자신만의 독자적인 스코프를 생성함. 이를 위해 eval 코드가 평가되면 eval 실행 컨텍스트가 생성됨

### 4. 모듈 코드(module code)
- 모듈 코드는 모듈별로 독립적인 모듈 스코프를 생성함. 이를 위해 모듈 코드가 평가되면 모듈 실행 컨텍스트가 생성됨


## 📕 소스코드의 평가와 실행
- 모든 소스코드는 실행에 앞서 평가 과정을 거치며 코드를 실행하기 위한 준비를 함
- 자바스크립트 엔진은 소스코드를 2개의 과정, 즉 소스코드의 평가와 소스코드의 실행으로 나누어 처리
    - 소스코드 평가 : 실행 컨텍스트를 생성하고 변수, 함수 등의 선언문만 먼저 실행하여 생성된 변수나 함수 식별자를 키로 실행 컨텍스트가 관리하는 스코프(렉시컬 환경의 환경 레코드)에 등록
    - 소스코드 실행 : 소스코드 평가가 끝나면 선언문을 제외한 소스코드가 순차적으로 실행되기 시작함(런타임이 시작됨). 이때 소스코드 실행에 필요한 정보, 즉 변수나 함수의 참조를 실행 컨텍스트가 관리하는 스코프에서 검색해서 취득하고 변수 값의 변경 등 소스코드의 실행 결과는 다시 실행 컨텍스트가 관리하는 스코프에 등록됨


## 📕 실행 컨텍스트의 역할
- ### **CODE**
    ``` javascript
    // 전역 변수 선언
    const x = 1;
    const y = 2;

    // 함수 정의
    function test(a) {
        //지역 변수 선언
        const x = 10;
        const y = 20;

        // 메서드 호출
        console.log(a + x + y); // 130
    }

    // 함수 호출
    test(100);
    
    // 메서드 호출
    console.log(x + y); // 3

    ```
    - ### 1. 전역 코드 평가
        - 전역 코드를 실행하기에 앞서 먼저 전역 코드 평가 과정을 거치며 전역 코드를 실행하기 위한 준비를 함.
        - 소스 코드 평가 과정에서는 선언문만 먼저 실행
        - 전역 코드의 변수 선언문과 함수 선언문이 먼저 실행되고, 그 결과 생성된 전역 변수와 전역 함수가 실행 컨텍스트가 관리하는 전역 스코프에 등록됨
        - 이때 var 키워드로 선언된 전역 변수와 함수 선언문으로 정의된 전역 함수는 전역 객체의 프로퍼티와 메서드가 됨

    - ### 2. 전역 코드 실행
        - 전역 코드 평가 과정이 끝나면 런타임이 시작되어 전역 코드가 순차적으로 실행되기 시작
        - 이때 전역 변수에 값이 할당되고 함수가 호출됨
        - 함수가 호출되면 순차적으로 실행되던 전역 코드의 실행을 일시 중단하고 코드 실행 순서를 변경하여 함수 내부로 진입
    
    - ### 3. 함수 코드 평가
        - 함수 호출에 의해 코드 실행 순서가 변경되어 함수 내부로 진입하면 함수 내부의 문들을 실행하기에 앞서 함수 코드 평가 과정을 거치며 함수 코드를 실행하기 위한 준비를 함
        - 이때 매개변수와 지역 변수 선언문이 먼저 실행되고, 그 결과 생성된 매개변수와 지역 변수가 실행 컨텍스트가 관리하는 지역 스코프에 등록됨
        - 또한 함수 내부에서 지역 변수처럼 사용할 수 있는 arguments 객체가 생성되어 지역 스코프에 등록되고 this 바인딩도 결정됨

    - ### 4. 함수 코드 실행
        - 함수코드 평가 과정이 끝나면 런타임이 시작되어 함수 코드가 순차적으로 실행됨
        - 이때 매개변수와 지역 변수에 값이 할당되고 console.log 메서드가 호출됨

- 이처럼 코드가 실행되려면 다음과 같이 스코프, 식별자, 코드 실행 순서 등의 관리가 필요
    1. 선언에 의해 생성된 모든 식별자(변수, 함수, 클래스 등)를 스코프를 구분하여 등록하고 상태 변화(식별자에 바인딩된 값의 변화)를 지속적으로 관리할 수 있어야 함
    1. 스코프는 중첩 관계에 의해 스코프 체인을 형성해야함. 즉, 스코프 체인을 통해 상위 스코프로 이동하며 식별자를 검색할 수 있어야 함
    1. 현재 실행중인 코드의 실행 순서를 변경(예를들어 함수 호출에 의한 실행 순서 변경)할 수 있어야 하며 다시 되돌아갈 수도 있어야 함
- 이 모든것을 관리하는 것이 바로 실행 컨텍스트임
- 실행 컨텍스트는 소스코드를 실행하는 데 필요한 환경을 제공하고 코드의 실행 결과를 실제로 관리하는 영역(모든 코드는 실행 컨텍스트를 통해 실행되고 관리됨)
- 식별자와 스코프는 렉시컬 환경으로 관리하고 코드 실행 순서는 실행 컨텍스트 스택으로 관리함


## 📕 실행 컨텍스트 스택
- 자바스크립트 엔진은 먼저 전역 코드를 평가하여 전역 실행 컨텍스트를 생성하고 함수가 호출되면 함수 코드를 평가하여 함수 실행 컨텍스트를 생성함
- ### **CODE**
    ``` javascript
    const x = 1;

    function test() {
        const y = 2;

        function inner() {
            const z = 3;

            console.log(x + y + z);
        }

        inner();
    }

    test(); // 6
    
    ```
    - 위의 코드 순서는 다음과 같음
        1. 전역 코드의 평가와 실행
            - 자바스크립트 엔진은 먼저 전역 코드를 평가하여 전역 실행 컨텍스트를 생성하고 실행 컨텍스트 스택에 푸시(push)함
            - 이때 전역 변수 x와 전역 함수 test는 전역 실행 컨텍스트에 등록됨(전역 코드 평가)
            - 이후 전역 코드가 실행되기 시작하여 전역 변수 x에 값이 할당되고 전역 함수 test가 호출되면서 전역코드 실행이 잠시 중단됨(전역 코드 실행)
        1. test 함수 코드의 평가와 실행
            - 전역 함수 test가 호출되면 전역 코드의 실행이 일시 중단되고 코드의 제언권이 test 함수 내부로 이동
            - 자바스크립트 엔진은 test 함수 내부의 함수 코드를 평가하여 test 함수 실행 컨텍스트를 생성하고 실행 컨텍스트 스택에 푸시(push)함
            - 이때 test 함수의 지역 변수 y와 중첩 함수 inner가 test 함수 실행 컨텍스트에 등록됨(test 함수 코드 평가)
            - 이후 test 함수 코드가 실행되기 시작하여 지역 변수 y에 값이 할당되고 중첩 함수 inner가 호출됨(test 함수 코드 실행)
        1. inner 함수 코드의 평가와 실행
            - 중첩 함수 inner가 호출되면 test 함수 코드의 실행은 일시 중단되고 제어권이 inner 함수 내부로 이동
            - 자바스크립트 엔진은 inner 함수 내부의 함수 코드를 평가하여 inner 함수 실행 컨텍스트를 생성하고 실행 컨텍스트에 푸시(push)함
            - 이때 inner 함수의 지역 변수 z가 inner 함수 실행 컨텍스트에 등록됨(inner 함수 평가)
            - 이후 inner 함수 코드가 실행되기 시작하여 지역 변수 z에 값이 할당되고 console.log 메서드를 호출한 이후 inner 함수가 종료됨(inner 함수 실행)
        1. test 함수 코드로 복귀
            - inner 함수가 종료되면 코드의 제어권은 다시 test 함수로 이동
            - 이때 자바스크립트 엔진은 inner 함수 실행 컨텍스트를 실행 컨텍스 스택에서 팝(pop)하여 제거
            - 그리고 test 함수는 더 이상 실행할 코드가 없으므로 종료됨
        1. 전역 코드로 복귀
            - test 함수가 종료되면 코드의 제어권은 다시 전역 코드로 이동
            - 이때 자바스크립트 엔진은 test 함수 실행 컨텍스트를 스택에서 팝(pop)하여 제거
            - 그리고 더 이상 실행할 전역 코드가 남아 있지 않으므로 전역 실행 컨텍스트도 실행 컨텍스트 스택에서 팝(pop)되어 실행 컨텍스트 스택에는 아무것도 남지 않게 됨
    - 이처럼 실행 컨텍스트 스택은 코드의 실행 순서를 관리함
    - 실행 컨텍스트 스택의 최상위에 존재하는 실행 컨텍스트는 언제나 현재 실행중인 코드의 실행 컨택스트임


## 렉시컬 환경(Lexical Environment)
- 렉시컬 환경은 식별자에 바인딩된 값, 그리고 상위 스코프에 대한 참조를 기록하는 자료구조로 실행 컨텍스트를 구성하는 컴포너트임
- 실행 컨텍스트 스택이 코드의 실행 순서를 관리한다면 렉시컬 환경은 스코프와 식별자를 관리함
- 렉시컬 환경은 두 개의 컴포넌트로 구성됨
    - 환경 레코드(Environment Record) : 스코프에 포함된 식별자를 등록하고 등록된 식별자에 바인됭된 값을 관리하는 저장소임. 환경 레코드는 소스코드의 타입에 따라 관리하는 내용에 차이가 있음
    - 외부 렉시컬 환경에 대한 참조(Outer Lexical Environment Reference) : 외부 렉시컬 환경에 대한 참조는 상위 스코프를 가리킨다. 이때 상위 스코프란 외부 렉시컬 환경, 즉 해당 실행 컨텍스트를 생선한 소스코드를 포함하는 상위 코드의 렉시컬 환경을 말함. 외부 렉시컬 환경에 대한 참조를 통해 단방향 링크드 리스트인 스코프 체인을 구현함