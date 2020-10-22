# 📚 DOM Traversing(DOM 탐색하기)
- 요소 노드를 찾고, 찾은 요소 노드를 기점으로 DOM 트리의 노드를 옮겨 다니며 부모, 형제, 자식 노드 등을 탐색(Traversing, node wolking)해야 할 때 사용


## 📖 DOM 탐색 키워드
1. 공백 텍스트 노드
1. 자식 노드
1. 부모 노드
1. 형제 노드

## 1. 공백 텍스트 노드
- 공백 텍스트 노드 : HTML 요소 사이의 스페이스, 탭, 줄바꿈(개행) 등의 공백 문자가 생성한 텍스트 노드
- 텍스트 에디터에서 HTML 문서에 스페이스 키, 탭 키, 엔터 키 등을 입력하면 공백 문자가 추가
- ### **CODE ⌨️**
    ``` html
    <body>
        <ul id='fruits'>
            <li class='apple'>Apple</li>
            <li class='banana'>Banana</li>
            <li class='orange'>Orange</li>
        </ul>
    </body>
    ```
- ### **DOM 트리**
    ```
    body
      ㄴ(white space)
      |
      ㄴ ul - [id = 'fruits']
      |  |
      |  ㄴ(white space)
      |  |
      |  ㄴ li - [class = 'apple']
      |  |   |
      |  |   ㄴ "Apple"
      |  |
      |  ㄴ(white space)
      |  |
      |  ㄴ li - [class = 'banana']
      |  |   |
      |  |   ㄴ "Banana"
      |  |
      |  ㄴ(white space)
      |  |
      |  ㄴ li - [class = 'orange']
      |  |   |
      |  |   ㄴ "Orange"
      |  |
      |  ㄴ(white space)
      |
      ㄴ(white space)
    ```

## 2. 자식 노드 탐색
- Node.prototype.childNodes
    - 자식 노드를 모두 탐색하여 DOM 컬렉션 객체인 NodeList에 담아 반환
    - childNodes 프로퍼티가 반환한 NodeList에는 요소 노드 뿐만 아니라 텍스트 노드도 포함되어 있을 수 있음

- Element.prototype.children
    - 자식 노드 중에서 요소 노드만 모두 탐색하여 DOM 컬렉션 객체인 HTMLCollection에 담아 반환
    - children 프로퍼티가 반환한 HTMLCollection에는 텍스트 노드가 포함되지 않음

- Node.prototype.firstChild
    - 첫 번째 자식 노드를 반환
    - 텍스트 노드이거나 요소 노드 반환

- Node.prototype.lastChild
    - 마지막 자식 노드를 반환
    - 텍스트 노드이거나 요소 노드 반환

- Element.prototype.firstElementChild
    - 첫 번째 자식 요소 노드를 반환
    - 요소 노드만 반환

- Element.prototype.lastElementChild
    - 마지막 자식 요소 노드를 반환
    - 요소 노드만 반환

- ### **CODE ⌨️**
    ``` html

    <!DOCTYPE html>
    <html>
    <body>
        <ul id="fruits">
            <li class="apple">Apple</li>
            <li class="banana">Banana</li>
            <li class="orange">Orange</li>
        </ul>

        <script>
            const $fruits = document.getElementById('fruits');

            // #fruits 요소의 모든 자식 노트 탐색
            // childNodes가 반환하는 NodeList에는 요소 노드뿐만 아니라 텍스트 노드도 포함
            console.log($fruits.childNodes);
            
            // #fruits 요소의 모든 자식 노트 탐색
            // children이 반환하는 HTMLCollection에는 요소 노드만 포함
            console.log($fruits.children);

            // #fruits 요소의 첫번째 자식 노드 탐색
            // 텍스트 노드도 반환 할 수 있음
            console.log($fruits.firstChild);

            // #fruits 요소의 마지막 자식 노드 탐색
            // 텍스트 노드도 반환 할 수 있음
            console.log($fruits.lastChild);

            // #fruits 요소의 첫번째 자식 노드 탐색
            // 요소 노드만 반환
            console.log($fruits.firstElementChild);

            // #fruits 요소의 마지막 자식 노드 탐색
            // 요소 노드만 반환
            console.log($fruits.lastElementChild);
        </script>
    </body>
    </html>

    ```
    ### **➕ 자식 노드 존재 학인**
    - Node.prototype.hasChildNodes : 자식 노드가 존재하는 확인하는 메서드
        - 자식 노드가 존재하면 true 반환
        - 자식 노드가 존재하지 않으면 false 반환
        - 텍스트 노드를 포함하여 자식 노드의 존재를 확인
        - ### **CODE ⌨️**
            ``` html

            <!DOCTYPE html>
            <html>
            <body>
                <ul id="fruits">
                </ul>

                <script>
                    const $fruits = document.getElementById('fruits');

                    // #fruits 요소에 자식 노드가 존재하는 지 확인
                    // 텍스트 노드를 포함하여 자식 노드 존재 확인
                    console.log($fruits.hasChildNodes()); // true
                </script>
            </body>
            </html>

            ```
    - 자식 노드 중에 텍스트가 노드가 아닌 요소 노드가 존재하는지 확인하기 위해서는 children.length 또는 Element 인터페이스의 childElementCount 프로퍼티 사용
        - ### **CODE ⌨️**
            ``` html

            <!DOCTYPE html>
            <html>
            <body>
                <ul id="fruits">
                </ul>

                <script>
                    const $fruits = document.getElementById('fruits');

                    // #fruits 요소에 자식 노드 중 텍스트 노드가 아닌 요소노드가 존재하는 확인
                    console.log(!!$fruits.children.length);  // 0 -> false

                    // #fruits 요소에 자식 노드 중 텍스트 노드가 아닌 요소노드가 존재하는 확인
                    console.log(!!$fruits.childrenElementCount);  // 0 -> false

                </script>
            </body>
            </html>

            ```

## 3. 부모 노드 탐색
- 부모 노드를 탐색하려면 Node.prototype.parentNode 프로퍼티 사용
- 텍스트 노드는 DOM 트리의 최종단 노드인 리프 노드 이므로 부모 노드가 텍스트 노드인 경우는 없음
- ### **CODE ⌨️**
    ``` html
    
    <!DOCTYPE html>
    <html>
        <body>
            <ul id="fruits">
                <li class="apple">Apple</li>
                <li class="banana">Banana</li>
                <li class="orange">Orange</li>
            </ul>

            <script>
                const $banana = document.querySelector('.banana');

                // .banan 요소 노드의 부모 노드 탐색
                console.log($banana);  // <ul id="fruits">...</ul>
            </script>
        </body>
    </html>
    
    ```


## 4. 형제 노드 탐색
- Node.prototype.previousSibiling
    - 부모 노드가 같은 형제 노드 중에서 자신의 이전 형제 노드를 탐색하여 반환
    - 요소 노드뿐만 아니라 텍스트 노드일 수도 있음

- Node.prototype.nextSibiling
    - 부모 노드가 같은 형제 노드 중에서 자신의 다음 형제 노드를 탐색하여 반환
    - 요소 노드뿐만 아니라 텍스트 노드일 수도 있음

- Element.prototype.previousElementSibiling
    - 부모 노드가 같은 형제 노드 중에서 자신의 이전 형제 요소 노드를 탐색하여 반환
    - 요소 노드만 반환

- Element.prototype.nextElementSibiling
    - 부모 노드가 같은 형제 노드 중에서 자신의 다음 형제 요소 노드를 탐색하여 반환
    - 요소 노드만 반환

- ### **CODE ⌨️**
    ``` html

    <!DOCTYPE html>
    <html>
        <body>
            <ul id="fruits">
                <li class="apple">Apple</li>
                <li class="banana">Banana</li>
                <li class="orange">Orange</li>
            </ul>

            <script>
                const $fruits = document.getElementById('fruits');

                // #fruits 요소의 첫 번째 자식 노드 탐색
                // firstChild 프로퍼티는 요소 노드뿐만 아니라 텍스트 노드도 반환 할 수 있음
                const firstChild = $fruits.firstChild;
                console.log(firstChild); // #text

                // #fruits 요소의 첫 번째 자식 노드의 다음 형제 노드를 탐색
                const nextSibling = firstChild.nextSibling;
                console.log(nextSibling); // <li class="apple">...</li>

                // li.apple 요소의 이전 형제 노드 탐색
                const previousSibling = nextSibling.previousSibling;
                console.log(previousSibling); // #text

                // #fruits 요소의 첫 번째 자식 요소 노드를 탐색
                // firstElementChild 프로퍼티는 요소 노드만 반환
                const firstElementChild = $fruits.firstElementChild;
                console.log(firstElementChild); // <li class="apple">...</li>

                // li.apple 요소의 다음 형제 요소 노드 탐색
                const nextElementSibling = firstElementChild.nextElementSibling;
                console.log(nextElementSibling); // <li class="banana">...</li>

                // li.banana 요소의 이전 형제 요소 노드 탐색
                const previousElementSibling = nextElementSibling.previousElementSibling;
                console.log(previousElementSibling); // <li class="apple">...</li>
            </script>
        </body>
    </html>

    ```


## ➕ 노드 정보 탐색
- Node.prototype.nodeType
    - 노드 객체의 종류, 즉 노드 타입을 나타내는 상수를 반환
    - 노드 타입 상수는 Node에 정의 되어 있음

- Node.prototype.nodeName
    - 노드의 이름을 문자열로 반환
    - 요소 노드 : 대문자 문자열로 태그 이름("UL", "LI" 등) 반환
    - 텍스트 노드 : 문자열 "#text" 반환
    - 문서 노드 : 문자열 "#document" 반환