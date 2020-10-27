# 📚 this 키워드

## 🔎 this 란?
- 객체지향 프로그래밍에서 객체란 상태를 나타내는 프로퍼티와 동작을 나타내는 메서드를 하나의 논리적 단위로 묶는 복합적인 자료구조
- 동작을 나타내는 메서드는 자신이 속한 객체의 상태, 즉 프로퍼티를 참조하고 변경할 수 있어야 함
- 객체 리터럴 방식으로 생성한 객체의 경우 메서드 내부에서 메서드 자신이 속한 객체를 가리키는 식별자를 재귀적으로 참조 가능
    > ### 객체 리터럴 방식  
    > 
    >   ``` javascript
    >   var user = {
    >       name : 'kim',
    >       age : 17,
    >       showInfo : function() {
    >           console.log(`${this.name}/${this.age}`)
    >       },
    >       ...
    >   };
    >   
    >    ```
    > - 리터럴 방식은 객체 리터럴을 의미하는 {} 내부에 프로퍼티와 메서드를 정의하는 구조

- ### **CODE ⌨️**
    ``` javascript
    const circle = {
        // 프로퍼티 : 객체 고유의 상태 데이터
        radius : 5,
        // 메서드 : 상태 데이터를 참조하고 조작하는 동작
        getDiameter() {
            // 이 메서드가 자신이 속한 프로퍼티나 다른 메서드를 참조하려면 자신이 속한 객체인 circle을 참조할 수 있어야 함
            return 2 * circle.radius;
        }
    };

    console.log(circle.getDiameter()); // 10

    ```
    - getDiameter 메서드 내에서 메서드 자신이 속한 객체를 가리키는 식별자 circle을 참조하고 있음
    - 자기 자신이 속한 객체를 재귀적으로 참조하는 방식은 일반적이지 않음
    - 생성자 함수 방식으로 인스턴스를 생성하는 경우 생성자 함수를 정의하는 시점에는 아직 인스턴스를 생성하기 이전이므로 생성자 함수가 생설할 인스턴스를 가리키는 식별자를 알 수 없다는 문제점 발생 이때 자신이 속한 객체 또는 자신이 생성한 인스턴스를 가리키는 특수한 식별자가 this
- this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 참조 변수(self-referencing variable)임
- this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있음
- this가 가리키는 값, 즉 this 바인딩은 함수 호출 방식에 의해 종적으로 결정
    > ### this 바인딩 이란?
    > - 바인딩 이란 식별자와 값을 연결하는 과정을 의미
    > - 변수 선언은 변수 이름(식별자)과 확보된 메모리 공간의 주소를 바인딩 하는 것
    > - this 바인딩은 this(키워드로 분류되지만 식별자 역할을 함)와 this가 가리킬 객체를 바인딩 하는 것

- ### 1. 객체 리터럴에서의 this
    - ### **CODE ⌨️**
        ``` javascript
        const circle = {
            radius: 5,
            getDiameter() {
                return 2 * this.radius;
            }
        }

        console.log(circle.getDiameter()); // 10

        ```
        - 객체 리터럴의 메서드 내부에서의 this는 메서드를 호출한 객체, 즉 circle을 가리킴


- ### 2. 생성자 함수 내부에서의 this
    - ### **CODE ⌨️**
        ``` javascript
        // 생성자 함수
        function Circle(radius) {
            // this는 생성자 함수가 생성할 인스턴스를 가리킴
            this.radius = radius;
        }

        Circle.prototype.getDiameter = function() {
            // this는 생성자 함수가 생성할 인스턴스를 가리킴
            return 2 * this.radius;
        };

        // 인스턴스 생성
        const circle = new Circle(5);
        console.log(circle.getDiameter()); // 10
        
        ```
        - 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킴


## 📔 함수 호출 방식과 this 바인딩
- ### 1. 일반 함수 호출
    - 기본적으로 this에는 전역 객체(global object)가 바인딩
    - ### **CODE ⌨️**
        ```javascript
        function test() {
            console.log("test's this : ", this); // window

            function inner() {
                console.log("inner's this : ", this); // window
            }

            inner();
        }

        test();

        ```
        - 위의 코드에서는 전역 함수와 중첩 함수를 일반 함수로 호출하면 함수 내부의 this에는 전역객체가 바인딩 됨
        - this는 객체의 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수이므로 객체를 생성하지 않는 일반 함수에서 thi는 의미 없음

    - ### **CODE ⌨️**
        ``` javascript
        var value = 1;


        const obj = {
            value: 100,
            test() {
                console.log("test's this : ", this); // {value: 100, test: f}
                console.log("test's this.value : ", this.value); // 100


                function inner() {
                     console.log("inner's this : ", this); // window
                console.log("inner's this.value : ", this.value); // 1
                }

                inner();
            }
        }

        obj.test();
        
        ```
        - 메서드 내에서 정의한 중첩 함수도 일반 함수로 호출되면 중첩 함수 내부의 this에는 전역 객체가 바인딩 됨

    - ### **CODE ⌨️**
        ``` javascript
        var value = 1;


        const obj = {
            value: 100,
            test() {
                console.log("test's this : ", this); // {value: 100, test: f}
                console.log("test's this.value : ", this.value); // 100

                setTimeout(function() {
                    console.log("callback's this : ", this); // window
                    console.log("callback's this.value : ", this.value); // 1
                , 100});
            }
        }

        obj.test();
        
        ```
        - 콜백 함수가 일반 함수로 호출된다면 콜백 함수 내부의 this에도 전역 객체가 바인딩 됨
    - 이처럼 일반 함수로 호출된 모든 함수(중첩 함수, 콜백 함수 등) 내부의 this에는 전역객체가 바인딩 됨
    - 중첩 함수 또는 콜백 함수는 외부 함수를 돕는 헬퍼 함수의 역할을 하므로 외부 함수의 일부 로직을 대신하는 경우가 대부분이기 때문에 this가 전역객체를 바인딩하는 것은 문제가 있음
    - ### **CODE ⌨️**
        ``` javascript
        var value = 1;

        const obj = {
            value: 100,
            test() {
                //this 바인딩(obj)을 변수 that에 할당
                const that = this;

                // 콜백 함수 내부에서 this 대신 that 참조
                setTimeout(function() {
                    console.log(that.value); // 100
                }, 100);

            }
        }

        ```
        - 위 코드는 콜백 함수의 this 바인딩을 메서드 this 바인딩과 일치 시키기 위한 방법
        - 이외에도 Function.prototype.apply, Function.prototype.call, Function.prototype.bind 메서드를 이용해 this를 명시적으로 바인딩 가능
        - 화살표 함수 내부의 this는 상위 스코프의 this를 가리킴


- ### 2. 메서드 호출
    - 메서드 내부의 this에는 메서드를 호출한 객체, 즉 메서드를 호출할 때 메서드 이름 앞의 마침표(.) 연산자 앞에 기술한 객체가 바인딩 됨
    - 주의할 것은 메서드 내부의 this는 메서드를 소유한 객체가 아닌 메서드를 호출한 객체에 바인딩된다는 것
    - ### **CODE ⌨️**
        ``` javascript
        const person = {
            name: 'Lee',
            getName() {
                // 메서드 내부의 this는 메서드를 호출한 객체에 바인딩
                return this.name;
            }
        }

        console.log(person.name); // Lee

        ```
        - 위 코드의 getName 메서드는 person 객체의 메서드로 정의
        - 메서드는 프로퍼티에 바인딩된 함수임 즉, person 객체의 getName 프로퍼티가 가리키는 함수 객체는 person 객체에 포함된 것이 아니라 독립적으로 존재하는 별도의 객체임. getName 프로퍼티가 함수 객체를 가리키고 있을 뿐
        - ### **CODE ⌨️**
            ```javascript
            const anotherPerson = {
                name: 'kim';
            }

            // getName 메서드를 anotherPerson 객체의 메서드로 할당
            anotherPerson.getName = person.getName;

            // getName 메서드를 호출한 객체는 anotherPerson
            console.log(anotherPerson.getName()); // Kim

            // getName 메서드를 변수에 할당
            const getName = person.getName;

            // getName 메서드를 일반 함수로 호출
            console.log(getName()); // ''
            // 일반 함수로 호출된 getName 함수 내부의 this.name은 브라우저 환경에서 window.name과 같음(Node.js 환경에서 this(전역객체).name은 undefined)

            ```
            - 위 코드 처럼 메서드 내부의 this는 프로퍼티로 메서드를 가리키고 있는 객체와는 관계가 없고 메서드를 호출한 객체에 바인딩 됨
    - 프로토타입 메서드 내부에서 사용된 this도 일반 메서드와 마찬가지로 해당 메서드를 호출한 객체에 바인딩 됨
    - ### **CODE ⌨️**
        ``` javascript
        function Person(name) {
            this.name = name;
        }

        Person.prototype.getName = function() {
            return this.name;
        }

        const me = new Person('Lee');

        // getName을 호출한 객체는 me
        console.log(me.getName()); // Lee

        Person.prototype.name = 'Kim';

        // getName 메서드를 호출한 객체는 Person.prototype
        console.log(Person.prototype.getName()); // Kim

        ```
    
- ### 3. 생성자 함수 호출
    - 생성자 함수 내부의 this에는 생성자 함수가 (미래에)생성할 인스턴스가 바인딩 됨
    - ### **CODE ⌨️**
        ``` javascript
        /*
         <생성자 함수>
         - 객체(인스턴스)를 생성하는 함수
         - 일반 함수와 동일한 방법으로 생성자 함수를 정의하고 new 연산자와 함께 호출하면 해당 함수는 생성자 함수로 동작. 만약 new 연산자와 함께 생성자 함숙를 호출하지 않으면 생성자 함수가 아니라 일반 함수로 동작
        */
        const Person(name) {
            this.name = name;
            this.getName = function() {
                return this.name;
            };
        }

        // 이름이 Kim인 Person 객체 생성
        const person1 = new Person('Kim');
        // 이름이 Lee인 Person 객체 생성
        const person2 = new Person('Lee');
        
        console.log(person1.getName()); // Kim
        console.log(person2.getName()); // Lee

        ```

- ### 3. Function.prototype.apply/call/bind 메서드에 의한 간접 호출
    - Function.prototype.apply, Function.prototype.call 메서드는 this로 사용할 객체와 인수 리스트를 인수로 전달 받아 함수를 호출함
    - ### **CODE ⌨️**
        ``` javascript
        function getThisBinding() {
            return this;
        }

        // this로 사용할 객체
        const thisArg = {a:1};

        console.log(getThisBinding()); // window

        console.log(getThisBinding.apply(thisArg)); // {a:1}
        console.log(getThisBinding.call(thisArg)); // {a:1}

        ```
        - apply와 call 메서드의 본질적인 기능은 함수를 호출하는 것
        - apply와 call 메서드는 함수를 호출하면서 첫 번째 인수로 전달한 특정 객체를 호출한 함수의 this에 바인딩함
        - apply와 call 메서드는 호출할 함수에 인수를 전달하는 방식만 다를 뿐 동일하게 동작함
    
    - ### **CODE ⌨️**
        ``` javascript
        function getThisBinding() {
            console.log(arguments);
            return this;
        }

        // this로 사용할 객체
        const thisArg = {a:1};

        // getThisBinding 함수를 호출하면서 인수로 전달한 객체를 getThisBinding 함수의 this에 바인딩
        // apply 메서드는 호출할 함수의 인수를 배열로 묶어 전달
        console.log(getThisBinding.apply(thisArg, [1, 2, 3]));
        // Arguments(3) [1, 2, 3, callee: f, Symbol(Symbol.iterator): f]
        // {a:1}

        // call 메서드는 호출할 함수의 인수를 쉼표로 구분한 리스트 형식으로 전달
        console.log(getThisBinding.call(thisArg, 1, 2, 3));
        // Arguments(3) [1, 2, 3, callee: f, Symbol(Symbol.iterator): f]
        // {a:1}

        ```
        - 위 코드처럼 apply와 call 메서드는 호출할 함수에 인수를 전달하는 방식만 다를 뿐 this로 사용할 객체를 전달하면서 함수를 호출하는 것은 동일함

    - ### **CODE ⌨️**
        ``` javascript
        function convertArgsToArray() {
            console.log(arguments);
            
            // arguments 객체를 배열로 변환
            // Array.prototype.slice를 인수 없이 호출하면 배열의 복사본을 생성
            const arr = Array.prototype.slice.call(arguments);

            console.log(arr);

            return arr;
        }

        convertArgsToArray(1, 2, 3); // [1, 2, 3]

        ```
        - 위 코드는 arguments 객체와 같은 유사 배열 객체에 배열 메서드를 사용하는 코드(arguments 객체는 배열이 아니기 때문에 Array.prototype.slice 같은 배열의 메서드를 사용할 수 없으나 apply와 call 메서드를 이용하면 가능)
    - Function.prototype.bind 메서드는 apply와 call 메서드와 달리 함수를 호출하지 않고 this로 사용할 객체만 전달
    - ### **CODE  ⌨️**
        ``` javascript
        function getThisBinding() {
            return this;
        }

        // this로 사용할 객체
        const thisArg = {a:1};

        // bind메서드는 함수에 this로 사용할 객체를 전달
        // bind메서드는 함수를 호출하지 않음
        console.log(getThisBinding.bind(thisArg)); // getThisBinding

        // bind 메서드는 함수를 호출하지 않으므로 명시적으로 호출해야 함
        console.log(getThisBinding.bind(thisArg)()); // {a:1}
        
        ```
    - bind 메서드는 메서드의 this와 메서드 내부의 중첩함수 또는 콜백함수의 this가 불일치하는 문제를 해결하기 위해 유용하게 사용됨
    - ### **CODE ⌨️**
        ``` javascript
        const person = {
            name: 'Lee',
            test(callback) {
                setTimeout(callback, 100);
            }
        };

        person.test(function() {
            console.log(`Hi! my name is ${this.name}.`); // Hi! my name is .
            // 일반 함수로 호출된 콜백함수 내부의 this.name은 브라우저 환경에서 window.name과 같음
            // 브라우저 환경에서 window.name은 브라우저 창의 이름을 나타내는 빌트인 프로퍼티이며 기본값은 ''

        });
        
        ```
        - 위와 같은 코드에서의 내부함수 또는 콜백함수 내부에서의 this사용 문제점은 bind 메서드를 통해 해결할 수 있음
        - ### **CODE**
            ``` javascript
            const person = {
                name: 'Lee',
                test(callback) {
                    // bind 메서드로 callback 함수 내부의 this바인딩을 전달
                    setTimeout(callback.bind(this), 100);
                    }
            };

            person.test(function() {
                console.log(`Hi! my name is ${this.name}.`); // Hi! my name is Lee.
            });
            
            ```

## 🗒 요약

함수 호출 방식|this 바인딩
:---|:---
일반 함수 호출|전역객체
메서드 호출|메서드를 호출한 객체
생성자 함수 호출|생성자 함수가 (미래에)생성할 인스턴스
Function.prototype.apply/call/bind 메서드에 의한 간접 호출| Function.prototype.apply/call/bind 메서드에 첫번째 인수로 전달한 객체