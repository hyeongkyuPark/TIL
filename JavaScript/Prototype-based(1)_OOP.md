# 📚 Prototype Based(1) OOP(객체지향 프로그래밍)

## 🔍 OOP(Object Oriented Programming) 이란?
- 객체지향 프로그래밍 : 프로그램을 명령어 또는 함수의 목록으로 보는 전통적인 명령형 프로그래밍의 절차지향적 관점에서 벗어나 여러 개의 독립적 단위, 즉 객체의 집합으로 프로그램을 표현하려는 프로그래밍 패러다임
- 객체지향 프로그래밍은 실세계의 실체(사물이나 개념)를 인식하는 철학적 사고를 프로그래밍에 접목하려는 시도에서 시작함
- 실체는 특징이나 성질을 나타내는 속성(attribute/property)을 가지고 있고, 이를 통해 실체를 인식하거나 구별할 수 있음\
- 예를 들어, 사람은 이름, 주소, 성별, 나이, 신장, 체중, 학력, 성격, 직업 등 다양한 속성을 갖는대, 이때 이름이 아무개이고 성별은 여성이며 나이는 20세인 사람과 같이 속성을 구체적으로 표현하면 특정한 사람을 다른 사람과 구별하여 인식 할 수 있음

- ### **CODE ⌨️**
    ``` javascript
    // 이름과 주소 속성을 갖는 객체
    const person = {
        name: 'Lee',
        address: 'seoul'
    };

    console.log(person); // {name:'Lee', address: 'Seoul'}
    
    ```
    - 위 코드에서는 프로그래머가 이름과 주소 속성으로 표현된 객체인 person을 다른 객체와 구별하여 인식할 수 있음
    - 이처럼 속성을 통해 여러 개의 값을 하나의 단위로 구성한 복합적인 자료구조를 객체라함
    - 객체지향 프로그래밍은 독립적인 객체의 집합으로 프로그램을 표현하려는 프로그래밍 패러다임임


- ### **CODE ⌨️**
    ``` javascript
    // 이름과 주소 속성을 갖는 객체
    const circle = {
        radius: 5,
        getDiametor() {
            return 2 * this.radius;
        },
        getPrimeter() {
            return 2 * Math.PI * this.radius;
        },
        getArea() {
            return Math.PI * this.radius ** 2;
        }
    };

    console.log(circle);

    console.log(circle.getDiametor());
    console.log(circle.getPerimeter());
    console.log(circle.getArea());

    console.log(person); // {name:'Lee', address: 'Seoul'}
    
    ```
    - 위 코드처럼 객체지향 프로그래밍은 객체의 상태(status)를 나타내는 데이터와 상태 데이터를 조작할 수 있는 동작(behavior)을 하나의 논리적인 단위로 묶어서 생각함
    - 따라서 객체는 상태 데이터와 동작을 하나의 논리적인 단위로 묶은 복합적인 자료구조임
        - 어떤 객체의 상태 데이터 : 프로퍼티(property)
        - 어떤 객체의 동작 : 메서드(method)
- 각 객체는 고유의 기능을 갖는 독립적인 부품으로 볼 수 있지만 자신의 고유한 기능을 수행하면서 다른 객체와 관계성을 가질 수 있음
- 다른 객체와 메세지를 주고 받거나 데이터를 처리할 수도 있고 다른 객체의 상태 데이터나 동작을 상속받아 사용하기도 함