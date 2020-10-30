# 📚 Prototype-based(3)_`__proto__`(프로토타입 접근자 프로퍼티)
## 🔍 프로토타입 이란?
- 객체지향 프로그래밍의 근간을 이루는 객체 상속을 구현하기 위해 사용됨
- 프로토타입은 어떤 객체의 상위(부모) 객체의 역할을 하는 객체로서 다른 객체에 공유 프로퍼티(메서드 포함)를 제공함
- 프로토타입을 상속받은 하위(자식) 객체는 상위 객체의 프로퍼티를 자신의 프로퍼티처럼 자유롭게 사용할 수 있음
- 모든 객체는 [[prototype]]이라는 내부 슬롯을 가지며, 이 내부 슬롯의 값은 프로토타입의 참조임(null인 경우도 있음)
- 객체가 생성될때 객체 생성 방식에 따라 프로토타입이 결정되고 [[Prototype]]에 저장됨(객체 리터럴에 의해 생성된 객체의 프로토타입은 object.prototype이고 생성자 함수에 의해 생성된 객체의 프로토타입은 생성자 함수의 prototype 프로퍼티에 바인딩 됨)


## 📁 `__proto__` 접근자 프로퍼티
- 모든 객체는 `__proto__` 접근자 프로퍼티를 통해 자신의 프로토타입, 즉 [[Prototype]] 내부 슬롯에 간접적으로 접근할 수 있음
- ### **CODE ⌨️**
    ``` javascript
    const person = {name: 'Lee'};

    console.log(person);
    /*
    ▼{name: "Lee"}
        name: "Lee" // person 객체의 프로퍼티
        ▶ __proto__ // person 객체의 프로토타입(Object.prototype)
    */

    ```
    - 위 코드처럼 모든 객체는 `__proto__` 접근자 프로퍼티를 통해 프로토타입을 가리키는 [[Prototype]] 내부 슬롯에 접근할 수 있음

- ### 📘  **`__proto__`는 접근자 프로퍼티**
    - 접근자 프로퍼티 : 자체적으로 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수([[GET]], [[SET]] 프로퍼티 어트리뷰트)로 구성된 프로퍼티
    - 자바스크립트는 원치적으로 내부 슬롯과 내부 메서드에 직접적으로 접근하거나 호출할 수 있는 방법을 제공하지 않음
    - 단, 일부 내부 슬롯과 내부 메서드에 한하여 간접적으로 접근할 수 있는 수단을 제공
    - [[Prototype]] 내부 슬롯에도 직접 접근할 수 없으며 `__proto__` 접근자 프로퍼티를 통해 간접적으로 [[Prototype]] 내부 슬롯의 값, 즉 프로토타입에 접근할 수 있음
    - ### **CODE ⌨️**
        ``` javascript
        const obj = {};
        const parent = {x:1};

        // getter 함수인 get __proto__가 호출되어 obj 객체의 프로토타입을 취득
        obj.__proto__;

        // setter 함수인 set __proto__가 호출되어 obj 객체의 프로토타입을 교체
        obj.__proto__ = parent;

        console.log(obj.x); // 1
        
        ```

- ### 📘 **`__proto__` 접근자 프로퍼티는 상속을 통해 사용됨**
    - `__proto__` 접근자 프로퍼티는 객체가 직접 소유하는 프로퍼티가 아니라 Object.prototype의 프로퍼티임
    - 모든 객체는 상속을 통해 Object.prototype.`__proto__` 접근자 프로퍼티를 사용할 수 있음
    - ### **CODE ⌨️**
        ``` javascript
        const person = { name : "Lee" };

        // persont 객체는 __proto__ 프로퍼티를 소유하지 않음
        console.log(person.hasOwnProperty('__proto__'));
        
        // __proto__ 프로퍼티는 모든 객체의 포로토타입 객체인 Object.prototype의 접근자 프로퍼티임
        console.log(Object.getOwnPropertyDescriptor(Object.prototype, '__proto__')); // {get : f, set : f, enumerable : false, configurable : true}


        ```


- ### 📘 **`__proto__` 접근자 프로퍼티를 통해 프로토타입에 접근하는 이유**
    - [[prototype]] 내부 슬롯의 값, 즉 프로토타입에 접근하기 위해 접근자 프로퍼티를 사용하는 이유는 상호 참조에 의해 프로토타입 체인이 생성되는 것을 방지하기 위해서임
    - ### **CODE ⌨️**
        ``` javascript
        const parent = {};
        const child = {};

        // child의 프로토 타입을 parent로 설정
        child.__proto__ = parent;

        // parent의 프로토 타입을 child로 설정
        parent.__proto__ = child; // typeError: Cyclic __proto__ value
        
        ```
        - 위 코드에서는 parent 객체를 child 객체의 프로토타입으로 설정한 후, child 객체를 parent 객체의 프로토타입으로 설정함
        - 이러한 코드가 에러 없이 정상적으로 처리된다면 서로가 자신의 프로토타입이 되는 비정상적인 프로토타입 체인이 만들어지기 때문에 `__proto__` 접근자 프로퍼티는 에러를 발생시킴
    - 프로토타입 체인은 단방향 링크드 리스크로 구현되어야 함(프로퍼티 검색 방향이 한쪽 방향으로만 흘러가야 함)
    - 아무런 체크 없이 무조건적으로 프로토타입을 교체할 수 없도록 `__proto__` 접근자 프로퍼티를 통해 프로토타입에 접근하고 교체 하도록 구현 됨


- ### 📘 **`__proto__` 접근자 프로퍼티를 코드 내에서 직접 사용하는 것은 권장하지 않음**
    - `__proto__` 접근자 프로퍼티는 ES5까지 ECMAScript 사양에 포함되지 않은 비표준이었음. 하지만 일부 브라우저에서 `__proto__`를 지원하고 있었기 때문에 브라우저 호환성을 고려하여 ES6에서 `__proto__`를 표준으로 채택함
    - 하지만 코드 내에서 `__proto__` 접근자 프로퍼티를 직접 사용하는 것은 권장하지 않음
    - 모든 객체가 `__proto__` 접근자 프로퍼티를 사용할 수 있는 것은 아니기 때문(직접상속 등)
    - ### **CODE ⌨️**
        ``` javascript
        // Object.prototype을 상속받지 않는 객체를 생성
        const obj = Object.create(null); 

        // obj객체는 Object.__proto__를 상속 받을 수 없음
        console.log(obj.__proto__); // undefined

        // 따라서 __proto__ 보다 Object.getPrototypeOf 메서드를 사용하는 것이 좋음
        console.log(Object.getPrototypeOf(obj)); // null

        ```
        - 따라서 `__proto__` 접근자 프로퍼티 대신 프로토타입의 참조를 취득하고 싶은 경우에는 Object.getPrototypeOf 메서드를 사용하고, 프로토타입을 교체하고 싶은 경우 Object.setPrototypeOf 메서드를 사용할 것을 권장
        - ### **CODE ⌨️**
            ``` javascript
            const obj = {};
            const parent = { x : 1 };

            console.log(Object.getPrototypeOf(obj)); // {constructor: ƒ, __defineGetter__: ƒ, __defineSetter__: ƒ, hasOwnProperty: ƒ, __lookupGetter__: ƒ, …}

            Object.setPrototypeOf(obj, parent); // obj.__proto__ = parent

            console.log(obj);
            /*
                ▼ {}
                    ▼ __proto__:
                          x: 1
                        ▶ __proto__ : Object
            */
            
            ```
            - Object.getPrototypeOf 메서드와 Object.setPrototypeOf 메서드는 get Object.prototype.`__proto__` 와 set Object.prototype.`__proto__` 의 처리 내용과 정화히 일치함