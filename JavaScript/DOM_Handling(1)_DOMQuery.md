# 📚 DOM Query (DOM 선택하기)

## 📖 DOM 선택 키워드
1. ID
1. Tag
1. Class
1. CSS선택자

## **1. ID를 이용한 요소 노드 취득**
- Document.prototype.get.ElementById 메서드는 인수로 전달한 id 속성 값을 갖는 **하나의 요소 노드를 탐색**하여 반환
    - `id` : HTML 문서 내에서 유일한 값이어야 하며, class 속성과는 달리 공백 문자로 구분하여 여러개의 값을 가질 수 없음. 단, 같은 id값이 HTML 요소들에게 존재 하더라도 에러가 발생하지않아 사용시 주의 해야함
    
- ### **CODE ⌨️**
    ```html

    <!DOCTYPE html>
    <html>
        <head></head>
        <body>
            <ul>
                <li id="apple">Apple</li>
                <li id="banana">Banana</li>
                <li id="orange">Orange</li>
            </ul>

            <script>
                const $elem = document.getElementById('banana'); // id값이 'banana'인 요소 노드를 탐색하여 반환(두번째 li 요소 노드 반환)

                console.log($elem);// <li id="banana">Banana</li>
            </script>
        </body>
    </html>

    ```
    - 위 코드에서는 getElementById 메서드의 인자로 'banana'를 입력받아 HTML 문서내에서 id속성값을 'banana'인 요소를 찾음

- ### **BAD CODE 👿**
    ```html
        
    <!DOCTYPE html>
    <html>
        <head></head>
        <body>
            <ul>
                <!-- 같은 id값이 중복되는 경우 -->
                <li id="banana">Apple</li>
                <li id="banana">Banana</li>
                <li id="banana">Orange</li>
            </ul>

            <script>
                const $elem = document.getElementById('banana'); // id값이 중복되는 경우 전달된 id값을 갖는 첫 번째 요소 노드만 반환(첫번째 li 요소 반환)

                console.log($elem);// <li id="banana">Apple</li>
            </script>
        </body>
    </html>

    ```
    - 위 코드는 좋지 않은 코드로 id 속성은 원칙상 HTML문서 내에서 같은 속성값을 한번 선언해야하지만
        여러번 선언함. 이 경우 getElementById 메서드에서는 가장 먼저 찾게되는 요소를 반환
- 만약 인수로 전달된 id 값을 갖는 HTML 요소가 존재하지 않는 경우 getElementById 메서드는 null을 반환
- ### **CODE ⌨️**
    ``` html

    <!DOCTYPE html>
    <html>
        <head></head>
        <body>
            <div id='test'></div>
            <script>
                console.log(test);// <div id="test"></div>
            </script>
        </body>
    </html>

    ```
    - HTML 요소에 id 속성값을 부여하면 id 값과 동일한 이름의 전역변수가 암묵적으로 선언되고 해당 노드 객체가 할당. 단, 이미 동일한 이름의 전역변수가 선언되어 있으면 노드 객체가 재할당되지 않음

## **2. Tag 이름을 이용한 요소 노드 취득**
- [Document 또는 Element].prototype.getElementsByTagName 메서드는 인수로 전달한 태그 이름을 갖는 모든 요소 노드들을 탐색하여 반환(여러 개의 요소 노드 객체를 DOM 컬렉션 객체인 HTMLCollection 객체를 반환)
    - `HTMLCollection` 객체 : 리턴 결과가 복수인 경우에 사용하는 객체. 유사배열로 배열과 비슷한 사용법을 가지고 있지만 배열은 아님
- getElementsByTagName 메서드는 Document.prototype에 정의된 메서드와 Element.prototype에 정의된 메서드가 있음
    - Document.prototype.getElementsByTagName : DOM의 루트 노드인 문서 노드 즉, document를 통해 호출하며 DOM 전체에서 요소 노드를 탐색하여 반환
    - Element.prototype.getElementsByTagName : 특정 요소 노드를 통해 호출하며, 특정 요소 노드의 자손 노드 중에서 요소 노드를 탐색하여 반환
- ### **CODE ⌨️**
    ```html
    <!DOCTYPE html>
    <html>
        <head></head>
        <body>
            <ul id='fruits'>
                <li>Apple</li>
                <li>Banana</li>
                <li>Orange</li>
            </ul>
            <ul>
                <li>HTML</li>
            </ul>
            <script>
                //DOM 전체에서 태그 이름이 li인 요소 노드를탐색하여 반환
                const $lisFromDocument = document.getElementsByTagName('li');
                console.log($lisFromDocument); // HTMLCollection(4) [li, li, li, li]

                //ul#fruits 요소의 자손 노드 중에서 태그 이름이 li인 요소 노드들을 탐색하여 반환
                const $fruits = document.getElementById('fruits');
                const $lisFromFruits = $fruits.getElementsByTagName('li');
                console.log($lisFromFruits); // HTMLCollection(3) [li, li, li]
            </script>
        </body>
    </html>

    ```
- 만약 인수로 전달된 태그 이름을 갖는 요소가 존재하지 않는 경우 getElementsByTagName 메서드는 빈 HTMLCollection 객체를 반환


## **3. Class를 이용한 요소 노드 취득**
- [Document 또는 Element].prototype.getElementsByClassName 메서드는 인수로 전달한 class 속성값을 갖는 모든 요소 노드들을 탐색하여 반환
- 인수로 전달할 class 값은 공백으로 구분하여 여러개의 class를 지정할 수 있음
- getElementsByTagName 메서드와 마찬가지로 여러개의 요소 노드 객체를 갖는 DOM 컬렉션 객체인 HTMLCollection 객체를 반환
- ### **CODE ⌨️**
    ``` html
    
    <!DOCTYPE html>
    <html>
        <head></head>
        <body>
            <ul>
                <li class='fruit apple'>Apple</li>
                <li class='fruit banana'>Banana</li>
                <li class='fruit orange'>Orange</li>
            </ul>
            
            <script>
                // class 값이 'fruit'인 요소 노드를 모두 탐색하여 HTMLCollection 객체에 담아 반환
                const $elems = document.getElementsByClassName('fruit');

                console.log($elems); // HTMLCollection(3)[li.fruit.apple, li.fruit.banana, li.fruit.orange]

                // class 값이 'fruit apple'인 요소 노드를 탐색하여 HTMLCollection 객체에 담아 반환
                const $apples = document.getElementsByClassName('fruit apple');

                console.log($apples); // HTMLCollection [li.fruit.apple]
            </script>
        </body>
    </html>
    
    ```
- getElementsByClassName 메서드는 getElementsByTagName 메서드와 마찬가지로 Document.prototype에 정의된 메서드와 Element.prototype에 정의된 메서드가 있음
- 만약 인수로 전달된 class 값을 갖는 요소가 존재하지 않는 경우 빈 HTMLCollection 객체를 반환


## **3. CSS 선택자를 이용한 요소 노드 취득**
- CSS 선택자 : 스타일을 적용하고자 하는 HTML 요소를 특정할 때 사용하는 문법
    ``` css
    
    /*전체 선택자 : 모든 요소 선택*/
    * {...}

    /*태그 선택자 : 모든 p 태그 요소들 선택*/
    p {...}

    /*id 선택자 : id값이 'id-name'인 요소 선택*/
    #id-name {...}

    /*class 선택자 : class값이 'class-name'인 모든 요소들 선택*/
    .class-name {...}

    /*속성 선택자 : input 요소들 중에 type 속성값이 'text'인 모든 요소들 선택*/
    input[type=text] {...}

    /*후손 선택자 : div 요소의 후손 요소 중 모든 p 요소들 선택*/
    div p {...}

    /*자식 선택자 : div 요소의 자식 요소 중 모든 p 요소들 선택*/
    div > p {...}

    /*인접 형제 선택자 : p요소의 형제 요소 중 p요소 바로 뒤에 위치하는 ul요소 선택*/
    p + ul {...}

    /*일반 형제 선택자 : p요소의 형제 요소 중 p요소 뒤에 위치하는 모든 ul요소들 선택*/
    p ~ ul {...}

    /*가상 클래스 선택자 : hover 상태인 a요소를 모두 선택*/
    a:hover {...}

    /*가상 요소 선택자 : p요소의 콘텐츠 앞에 위치하는 공간을 선택. 일반적으로 content 프로퍼티와 함께 사용*/
    p::before {...}

    
    ```

- [Document 또는 Element].prototype.querySelector 메서드는 인수로 전달한 CSS 선택자를 만족시키는 **하나의 요소 노드**를 탐색하여 반환
    - ### **CODE ⌨️**
        ``` html

        <!DOCTYPE html>
        <html>
            <head></head>
            <body>
                <ul>
                    <li class='apple'>Apple</li>
                    <li class='banana'>Banana</li>
                    <li class='orange'>Orange</li>
                </ul>
                 
                <script>
                    // class 속성값이 'banana'인 첫 번째 요소 노드를 탐색하여 반환
                    const $elem = document.querySelector('.banana');

                    console.log($elem); // <li class='banana'>Banana</li>
                </script>
            </body>
        </html>

        ```
        - 여러개 존재 : 첫 번째 요소 노드만 반환
        - 존재 X : null 반환
        - CSS 선택자 문법 오류 : DOMException 에러 발생
- [Document 또는 Element].prototype.querySelectorAll 메서드는 인수로 전달한 CSS 선택자를 만족시키는 모든 요소 노드를 탐색하여 반환. querySelectorAll 메서드는 여러개의 요소 노드 객체를 갖는 DOM 컬렉션 객체인 NodeList 객체(유사 배열)를 반환
    - ### **CODE ⌨️**
        ``` html

        <!DOCTYPE html>
        <html>
            <head></head>
            <body>
                <ul>
                    <li class='apple'>Apple</li>
                    <li class='banana'>Banana</li>
                    <li class='orange'>Orange</li>
                </ul>
                 
                <script>
                    // ul 요소의 자식 요소인 li 요소를 모두 탐색하여 반환
                    const $elems = document.querySelector('ul > li');

                    console.log($elems); // NodeList(3) [li.apple, li.banana, li.orange]
                </script>
            </body>
        </html>

        ```
        - 존재 X : 빈 NodeList 객체 반환
        - CSS 선택자 문법 오류 : DOMException 에러 발생
- querySelector, querySelectorAll 메서드 모두 getElementsByTagName, getElementsByClassName 메서드와 마찬가지로 Document.prototype에 정의된 메서드와 Element.prototype에 정의된 메서드가 있음
- 다른 요소 노드를 취득하는 메서드들 보다 느린 것으로 알려져 있지만, 좀 더 구체적인 조건으로 요소 노드를 취득할 수 있고 일관된 방식으로 요소 노드를 취득할 수 있다는 장점이 있음

## **➕ 특정 요소 노드를 취득할 수 있는지 확인**
- Element.prototype.mathes 메서드는 인수로 전달한 CSS 선택자를 통해 특정 요소 노드를 취득할 수 있는지 확인함

- ### **CODE ⌨️**
    ``` html

    <!DOCTYPE html>
    <html>
        <head></head>
        <body>
            <ul id='fruits'>
                <li class='apple'>Apple</li>
                <li class='banana'>Banana</li>
                <li class='orange'>Orange</li>
            </ul>
                 
            <script>
                const $apple = document.querySelector('.apple');

                console.log($apple.matches('#fruits > li.apple')); // true
                console.log($apple.matches('#fruits > li.banana')); // false
            </script>
        </body>
    </html>

    ```