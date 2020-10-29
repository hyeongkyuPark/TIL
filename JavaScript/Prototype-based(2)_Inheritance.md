# 📚 Prototype-based(2)_Inheritance(상속과 프로토타입)

## 🔍 상속 이란?
- 상속은 객체지향 프로그래밍의 핵심 개념으로, 어떤 객체의 프로퍼티 또는 메서드를 다른 객체가 상속받아 그대로 사용할 수 있는 것을 말함
- 자바스크립트는 프로토타입을 기반으로 상속을 구현하여 불필요한 중복을 제거함(코드 재사용)
- ### **CODE ⌨️**
    ``` javascript
    // 생성자 함수
    const Circle(radius) {
        this.radius = radius;
        this.getArea = function() {
            // Math.PI는 원주율을 나타내는 상수
            return Math.PI * this.radius ** 2;
        }
    }


    // 반지름이 1인 인스턴스 생성
    const circle1 = new Circle(1);

    // 반지름이 2인 인스턴스 생성
    const circle2 = new Circle(2);

    /* 
    Circle 생성자 함수는 인스턴스를 생성할 때마다 동일한 동작을하는 getArea 메서드를 중복 생성하고 모든 인스턴스가 중복 소유함
    getArea 메서드는 하나만 생성하여 모든 인스턴스가 공유해서 사용하는 것이 바람직함
    */
    console.log(circle1.getArea = circle2.getArea); // false

    console.log(circle1.getArea()); // 3.141592653589793
    console.log(circle2.getArea()); // 12.566370614359172

    ```
    - 위 코드처럼 생성자 함수는 동일한 프로퍼티(메서드 포함) 구조를 갖는 객체를 여래 생성할 때 유용하지만 문제점을 가짐
        - radius 프로퍼티 값은 일반적으로 인스턴스마다 다름(같은 상태를 갖는 여러 개의 인스턴스가 필요하다면 radius 프로퍼티 값이 같을 수도 있음)
        - getArea 메서드는 모든 인스턴스가 동일한 내용의 메소드를 사용하므로 단 하나만 생성하여 모든 인스턴스가 공유해서 사용하는 것이 바람직함
        - 하지만 위의 Circle 생성자 함수는 인스턴스를 생성할 때마다 getArea 메서드를 중복 생성하고 모든 인스턴스가 중복 소유하는 문제가 있음(프로토타입 기반의 상속으로 해결)

    - ### **CODE ⌨️**
        ``` javascript
        // 생성자 함수
        const Circle(radius) {
            this.radius = radius;
        }

        // Circle 생성자 함수가 생성한 모든 인스턴스가 getArea 메서드를 공유해서 사용할 수 있도록 프로토타입에 추가
        // 프로토타입은 Circle 생성자 함수의 Prototype 프로퍼티에 바인딩되어 있음
        Circle.Prototype.getArea = function() {
            // Math.PI는 원주율을 나타내는 상수
            return Math.PI * this.radius ** 2;
        }


        // 반지름이 1인 인스턴스 생성
        const circle1 = new Circle(1);

        // 반지름이 2인 인스턴스 생성
        const circle2 = new Circle(2);

        /* 
        Circle 생성자 함수가 생성한 모든 인스턴스는 부모 객체의 역할을 하는 프로토타입 Circle.prototype으로부터 getArea 메서드를 상속 받음
        즉, Circle 생성자 함수가 생성하는 모든 인스턴스는 하나의 getArea 메서드를 공유함
        */
        console.log(circle1.getArea = circle2.getArea); // true

        console.log(circle1.getArea()); // 3.141592653589793
        console.log(circle2.getArea()); // 12.566370614359172

        ```
        - Circle 생성자 함수가 생성한 모든 인스턴스는 자신의 프로토타입, 즉 상위(부모) 객체 역할을 하는 Circle.prototype의 모든 프로퍼티와 메서드를 상속받음