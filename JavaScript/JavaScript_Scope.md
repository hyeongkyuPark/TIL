# 📚 JavaScript Scope(자바스크립트 범위)


## 🔍 자바스크립트 범위
- 범위(scope) : 자바스크립트 변수에 대한 접근 권한을 정의하는 것
- 자바스크립트에서 변수는 전역 범위 또는 지역 범위에 속할 수 있음


## 📢 전역 범위(Global Scope)
``` javascript
test = 'test';
console.log(test);
```
- 위 코드에서 test라는 이름의 전역변수를 생성
- 자바스크립트에서 가장 안좋은 사용법 중 하나
- 항상 var나 let을 사용해 변수를 선언하는 것을 권장(수정하지 않는 변수 즉, 상수를 선언할 떄는 const 사용)


## 🏠 지역 범위
- 함수 범위(Function Scope)
- 블록 범위(Block Scope)

- ### **🛸 var 사용하기(함수 범위 : Function Scope)**
    - 자바스크립트에서 var는 변수를 선언하는데 사용되는 키워드
    - 변수를 어디에 선언하든 변수 선언이 함수의 맨 앞으로 이동하는 특성을 가짐(변수 호이스팅 : variable hoisting)

        #### **작성 📝**
        ``` javascript
        function scope1() {
            var one = 1;
            two = 2;

            console.log(two);

            var two;
        }

        scope1(); // 2를 출력하며 오류가 발생하지 않음

        ```

        #### **동작 🏃‍♂️**
        ``` javascript
        function scope1() {
            var one = 1;
            var two;
            two = 2;
            
            console.log(two);

            /*var two; 변수 선언부분이 함수의 맨 앞으로 이동*/
        }

        scope1(); // 2를 출력하며 오류가 발생하지 않음

        ```
    - var 키워드의 핵심적인 사항은 해당 변수의 범위가 가장 가까운 함수범위 라는 것

        #### **작성 📝**
        ``` javascript
        function scope2(input) {
            if(input) {
                var result = 'input OK';
            }

            console.log(result);
        }

        scope2(true); // 'input OK'를 출력하며 오류가 발생하지 않음

        ```

        #### **동작 🏃‍♂️**
        ``` javascript
        function scope2(input) {
            var result;

            if(input) {
                result = 'input OK';// 가장가까운 함수 scope2의 맨 앞으로 변수 선언부 이동
            }

            console.log(result);
        }

        scope2(true); // 'input OK'를 출력하며 오류가 발생하지 않음

        ```
    - 자바에서는 위의 구문이 오류를 일으킴. if문 내에서 선언한 변수는 if 블록 내에서만 사용가능하고 외부에서는 사용할 수 없기 때문(자바는 기본적으로 호이스팅이 발생하지 않고, 변수들의 범위가 블록범위임)


- ### 🎲 let 사용하기(블록 범위 : Block Scope)
    - 자바크립트에서 let은 가장 가까운 블록 범위를 가짐(변수가 선언된 {} 내에서 유효)

        ```javascript
        function scope3(input) {

            if(input) {
            let result = 'input OK';
            }// 이 괄호를 기준으로 괄호 안에서만 사용가능한 변수의 범위를 블록 범위 변수라고 함

            console.log(result);
        }

        scope3(true); //"result is not defined" 에러 발생
        ```


        > **var 와 let의 차이점에 대해서는 좀 더 자세히 공부해보고 따로 올릴 예정**

