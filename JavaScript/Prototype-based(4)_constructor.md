# 📚 Prototype-based(4)_constructor(생성자 함수와 프로토타입)

## 📔 함수 객체의 prototype 프로퍼티
- 함수 객체만이 소유하는 prototype 프로퍼티는 생성자 함수가 생성할 인스턴스의 프로토타입을 가리킴
- ### **CODE ⌨️**
    ``` javascript
    // 함수 객체는 prototype 프로퍼티를 소유함
    (function() {}).hasOwnProperty('prototype'); // true

    // 일반 객체는 prototype 프로퍼티를 소유하지 않음
    ({}).hasOwnProperty('prototype'); // false

    ```
- prototype 프로퍼티는 생성자 함수가 생성할 객체(인스턴스)의 프로토타입을 가리킴
- 화살표 함수와 ES6 메서드 축약 표현으로 정의한 메서드는 non-constructor 로서 prototype 프로퍼티를 소유하지 않으며 프로토타입도 생성하지 않음
- ### **CODE ⌨️**
    ``` javascript
    // 화살표 함수는 non-constructor임
    const Person = name => {
        this.name = name;
    }

    //non-constructor는 prototype 프로퍼티를 소유하지 않음
    console.log(Person.hasOwnProperty('prototype')); // false

    // non-constructor는 프로토타입을 생성하지 않음
    console.log(Person.prototype); // undefined

    // ES6의 메서드 축약 표현으로 정의한 메서드는 non-constructor임
    const obj = {
        test() {}
    };

    //non-constructor는 prototype 프로퍼티를 소유하지 않음
    console.log(obj.test.hasOwnProperty('prototype')); // false

    // non-constructor는 프로토타입을 생성하지 않음
    console.log(obj.test.prototype); // undefined
    
    ```
- 생성자 함수로 호출하기 위해 정의하지 않은 일반함수(함수 선언문, 함수 표현식)도 prototype 프로퍼티를 소유하지만 객체를 생성하지 않는 일반 함수의 prototype 프로퍼티는 아무런 의마가 없음
- 모든 객체가 가지고 있는(엄밀히 말하면 Object.prototype으로부터 상속 받은) `__proto__` 접근자 프로퍼티와 함수 객체만이 가지고 있는 prototype 프로퍼티는 결국 동일한 프로토타입을 가리킴. 하지만 이들 프로퍼티를 사용하는 주체가 다름

구분|소유|값|사용 주체|사용 목적
---|---|---|---|---
`__proto__` 접근자 프로퍼티|모든 객체|프로토타입의 참조|모든 객체|객체가 자신의 프로토타입에 접근 또는 교체하기 위해 사용
`prototype` 프로퍼티|constructor|프로토타입의 참조|생성자 함수|생성자 함수가 자신이 생성할 객체의 프로토타입을 할당하기 위해 사용

- ### **CODE ⌨️**
    ``` javascript
    // 생성자 함수
    function Person(name) {
        this.name = name;
    }

    const me = new Person('Park');

    // 결국 Person.prototype과 me.__proto__는 동일한 프로토타입을 가리킴
    console.log(Person.prototype === me.__proto__); // true
    
    ```

## 📔 프로토타입의 constructor 프로퍼티와 생성자 함수
- 모든 프로토타입은 constructor 프로퍼티를 가짐
- constructor 프로퍼티 : prototype 프로퍼티로 자신을 참조하고 있는 생성자 함수를 가리킴
- 이 연결은 생성자 함수가 생성될 때, 즉 함수 객체가 생성될 때 이루어짐
- ### **CODE ⌨️**
    ``` javascript
    // 생성자 함수
    function Person(name) {
        this.name = name;
    }

    const me = new Person('Park');

    // me 객체의 생성자 함수는 Person임
    console.log(me.constructor === Person); // true
    
    ```
    - 위의 코드에서 Person 생성자 함수는 me 객체를 생성함
    - 이때 me 객체는 프로토타입의 constructor 프로퍼티를 통해 생성자 함수와 연결됨
    - me 객체에는 constructor 프로퍼티가 없지만 me 객체의 프로토타입인 Person.prototype에는 constructor 프로퍼티가 있음
    - 따라서 me 객체는 프로토타입인 Person.prototype의 constructor 프로퍼티를 상속받아 사용가능

## 📔 리터럴 표기법에 의해 생성된 객체의 생성자 함수와 프로토타입
- 생성자 함수에 의해 생성된 인스턴스는 프로토타입의 constructor 프로퍼티에 의해 생성자 함수와 연결됨. 이때 constructor 프로퍼티가 가리키는 생성자 함수는 인스턴스를 생성한 생성자 함수임
- 하지만 리터럴 표기법에 의한 객체 생성 방식과 같이 명시적으로 new 연산자와 함께 생성자 함수를 호출하여 인스턴스를 생성하지 않는 객체 생성 방식도 있음
    ``` javascript
    // 객체 리터럴
    const obj = {};

    // 함수 리터럴
    const add = function (a, b) {return a + b};

    // 배열 리터럴
    const arr = [1, 2, 3];

    // 정규표현식 리터럴
    const regexp = /is/ig;

    ```
    - 리터럴 표기법에 의해 생성된 객체도 프로토타입이 존재함
    - 하지만 리터럴 표기법에 의해 생성된 객체의 경우 프로토타입의 constructor 프로퍼티가 가리키는 생성자 함수가 반드시 객체를 생성한 생성자 함수로 단정할 수는 없음
    - ### **CODE ⌨️**
        ``` javascript
        // obj 객체는 Object 생성자 함수로 생성한 객체가 아니라 객체 리터럴로 생성함
        const obj = {};

        // 하지만 obj 객체의 생성자 함수는 Object 생성자 함수임
        console.log(obj.constructor === Object); // true

        ```
        - 위 코드의 obj 객체는 Object 생성자 함수로 생성한 객체가 아니라 리터럴에 의해 생성된 객체지만 Object 생성자 함수와 constructor 프로퍼티로 연결되어 있음
        - Object 생성자 함수에 인수를 전달하지 않거나 undefined 또는 null을 인수로 전달하면서 호출하면 내부적으로 추상 연산 OrdinaryObjectCreate를 호출하여 object.prototype을 프로토타입으로 갖는 빈 객체를 생성함

        > 추상연산 : ECMAScript 사양에서 내부 동작의 구현 알고리즘을 표현한 것(함수와 유사한 의사 코드)

리터럴 표기법|생성자 함수|프로토타입
---|---|---
객체 리터럴|Object|Object.prototype
함수 리터럴|Function|Function.prototype
배열 리터럴|Array|Array.prototype
정규식 리터럴|RegExp|RegExp.prototype