# 📚 Node Manipulation(Node 조작하기)
- innerHTML 프로퍼티와 insertAdjacentHTML 메서드는 HTML 마크업 문자열을 파싱하여 노드를 생성하고 DOM 반영하지만, DOM은 노드를 직접 생성/삽입/삭제/치환하는 메서드도 제공

## 📖 Node 조작 키워드
1. 노드 생성과 추가
1. 복수의 노드 생성과 추가
1. 노드 삽입/이동/복사/교체/삭제


## 1. 노드 생성과 추가
- ### 1. 요소 노드 생성(createElement)
    - Document.prototype.createElement(tagName) 메서드는 요소 노드를 생성하여 반환.
    - createElement 메서드의 매개변수 tagName에는 만들고자하는 태그의 이름을 문자열로 전달
    - ### **CODE ⌨️**
        ``` javascript
        // 1. 요소 노드 생성
        const $li = document.createElement('li');
        ```
        - 위 코드에서 createElement 메서드로 생성한 요소 노드는 기존 DOM에 추가되지 않고 홀로 존재하는 상태임
        - 그리고 createElement 메서드로 생성한 요소 노드는 아무런 자식 노드를 가지고 있지 않음

- ### 2. 텍스트 노드 생성(createTextNode)
    - Document.prototype.createTextNode(text) 메서드는 텍스트 노드를 생성하여 반환
    - createTextNode 메서드의 매개변수 text에는 텍스트 노드의 값으로 사용할 문자열을 인수로 전달
    - ### **CODE ⌨️**
        ```javascript
        // 2. 텍스트 노드 생성
        const textNode = document.createTextNode('Banana');
        ```
        - 텍스트 노드는 기본적으로 요소 노드의 자식 노드임. 하지만, createTextNode 메서드로 생성한 텍스트 노드는 요소 노드의 자식 노드로 추가되지 않고 홀로 존재하는 상태임

- ### 3. 텍스트 노드를 요소 노드의 자식 노드로 추가(appendChild)
    - Node.prototype.appendChild(childNode) 메서드는 매개변수 childNode에게 인수로 전달한 노드를 appendChild 메서드를 호출한 노드의 마지막 자식 노드로 추가
    - ### **CODE ⌨️**
        ``` javascript
        // 3. 텍스트 노드를 $li 요소 노드의 자식 노드로 추가
        $li.appendChild(textNode);

        
        // $li.textContent = "Banana";
        ```
        - 위 코드는 appendChild를 통해 요소 노드와 텍스트 노드는 부자 관계로 연결되었지만 아직 기존 DOM에는 추가되지 않은 상태임
        - 위 예제처럼 요소 노드에 자식 노드가 하나도 없는 경우에는 텍스트 노드를 생성하여 요소 노드의 자식 노드로 텍스트 노드를 추가하는 것보다 textContent 프로퍼티를 사용하는 편이 더 간편함

- ### 4. 요소 노드를 DOM에 추가
    - Node.prototype.appendChild 메서드를 사용하여 텍스트 노드와 부자관계로 연결한 요소 노드를 #fruits 요소 노드의 마지막 자식 요소로 추가
    - ### **CODE ⌨️**
        ``` javascript
        // 4. $li 요소 노드를 #fruits 요소 노드의 자식 노드로 추가
        $fruits.appendChild($li);
        ```
    - 위 코드는 요소 노드를 생성하여 DOM에 추가하므로 DOM은 변경됨. 이때 리플로우와 리페인트가 실행


## 2. 복수의 노드 생성과 추가
- DOM을 변경하는 것은 높은 비용이 드는 처리이므로 가급적 횟수를 줄이는 편이 성능에 유리
    - ### **CODE ⌨️**
        ``` html
        <!DOCTYPE html>
        <html>
            <body>
                <ul id='fruits'></ul>
            </body>

            <script>
                const $fruits = document.getElementById('fruits');

                ['Apple', 'Banana', 'Orange'].forEach(text => {
                    // 1. 요소 노드 생성
                    const $li = document.createElement('li');

                    // 2. 텍스트 노드 생성
                    const textNode = document.createTextNode(text);

                    // 3. 텍스트 노드를 $li 요소 노드의 자식 노드로 추가
                    $li.appendChild(textNode);

                    // 4. $li 요소 노드를 #fruits 요소 노드의 마지막 자식 노드로 추가(DOM 변경)
                    $fruits.appendChild($li);
                });
            </script>
        </html>

        ```
        - 위의 코드에서는 DOM 변경이 3번 발생하므로 비효율적임
- DOM을 여러 번 변경하는 문제를 회피하기 위해 컨테이너 요소를 사용
    - ### **CODE ⌨️**
        ``` html
        <!DOCTYPE html>
        <html>
            <body>
                <ul id='fruits'></ul>
            </body>

            <script>
                const $fruits = document.getElementById('fruits');

                const $container = document.createElement('div');

                // 컨테이너 요소 노드 생성
                ['Apple', 'Banana', 'Orange'].forEach(text => {
                    // 1. 요소 노드 생성
                    const $li = document.createElement('li');

                    // 2. 텍스트 노드 생성
                    const textNode = document.createTextNode(text);

                    // 3. 텍스트 노드를 $li 요소 노드의 자식 노드로 추가
                    $li.appendChild(textNode);

                    // 4. $li 요소 노드를 컨테이너 요소 의 마지막 자식 노드로 추가(DOM 변경 X)
                    $container.appendChild($li);
                });

                $fruits.appendChild($container);
            </script>
        </html>

        ```
        - 위 코드는 DOM을 한 번만 변경하므로 성능에 유리하기는 하지만 불필요한 컨테이너 요소(div)가 DOM에 추가되는 부작용이 있음
- 불필요한 컨테이너 요소가 추가되는 것을 해결하기위해 DocumentFragment 노드 사용
- DocumentFragment : 노드 객체의 일종으로, 부모 노드가 없어서 기존 DOM과는 별도로 존재하며, DocumentFragment 노드를 DOM에 추가하면 자신은 제거되고 자신의 자식 노드만 DOM에 추가됨
    - ### **CODE ⌨️**
        ``` html
        <!DOCTYPE html>
        <html>
            <body>
                <ul id='fruits'></ul>
            </body>

            <script>
                const $fruits = document.getElementById('fruits');

                const $fragment = document.createDocumentFragment();

                // 컨테이너 요소 노드 생성
                ['Apple', 'Banana', 'Orange'].forEach(text => {
                    // 1. 요소 노드 생성
                    const $li = document.createElement('li');

                    // 2. 텍스트 노드 생성
                    const textNode = document.createTextNode(text);

                    // 3. 텍스트 노드를 $li 요소 노드의 자식 노드로 추가
                    $li.appendChild(textNode);

                    // 4. $li 요소 노드를 컨테이너 요소 의 마지막 자식 노드로 추가(DOM 변경 X)
                    $fragment.appendChild($li);
                });

                $fruits.appendChild($fragment);
            </script>
        </html>
        
        ```
        - 위의 소스는 DOM을 한 번만 변경하고, 불필요한 요소도 생성하지 않으므로 여러개의 요소 노드를 DOM에 추가하는 경우 DocumentFragment 노드를 사용하는 것이 더 효율적임


## 3.노드 삽입
1. 마지막 노드로 추가(appendChild)
    - Node.prototype.appendChild 메서드는 인수로 전달받은 노드를 자신을 호출한 노드의 마지막 노드로 DOM에 추가
    - 노드를 추가할 위치를 지정할 수 없고 언제나 마지막 자식 노드로 추가
1. 지정한 위치에 노드 삽입
    - Node.prototype.insertBefore(newNode, childNode) 메서드는 첫 번째 인수로 전달받은 노드를 두 번째 인수로 전달 받은 노드 앞에 삽입
    - ### **CODE ⌨️**
        ``` html
        <!DOCTYPE html>
        <html>
            <body>
                <ul id='fruits'>
                    <li>Apple</li>
                    <li>Banana</li>
                </ul>
            </body>

            <script>
                const $fruits = document.getElementById('fruits');

                const $li = document.createElement('li');

                $li.appendChild(document.createTextNode('Orange'));

                $fruits.insertBefore($li, $fruits.lastElementChild);
            </script>
        </html>

        ```
        - 두 번째 인수로 전달받은 노드는 반드시 insertBefore 메서드를 호출한 노드의 자식 노드이어야 함. 그렇지 않으면 DOMExeption 에러 발생
    - 두 번째 인수로 전달받은 노드가 null이면 첫 번째 인수로 전달받은 노드를 insertBefore를 호출한 노드의 마지막 자식 노드로 추가(appendChild와 동일하게 작동)


## 4. 노드 복사(cloneNode)
- Node.prototype.cloneNode([deep: true | false]) 메서드는 노드의 사본을 생성하여 반환
- 매개변수 deep에 true를 인수로 전달하면 노드를 깊은 복사(deep clone)하여 모든 자손 노드가 포함된 사본을 생성
- 매개변수 deep에 false를 인수로 전달하면 노드를 얕은 복사(shallow clone)하여 노드 자신만의 사본을 생성
- 얕은 복사로 생성된 요소 노드는 자손 노드를 복사하지 않으므로 텍스트 노드도 없음
    - ### **CODE ⌨️**
        ``` html
        <!DOCTYPE html>
        <html>
            <body>
                <ul id='fruits'>
                    <li>Apple</li>
                </ul>
            </body>

            <script>
                const $fruits = document.getElementById('fruits');

                const $apple = $fruits.firstElementChild;

                // $apple 요소를 얕은 복사하여 사본 생성(textNode 없음)
                const $shallowClone = $apple.cloneNode();
                // 사본 요소 노드에 텍스트 추가
                $shallowClone.textContent = 'Banana';

                $fruits.appendChild($shallowClone);

                // #fruits 요소를 깊은 복사하여 모든 자손 노드가 포함된 사본 생성
                const $deepClone = $fruits.cloneNode(true);

                $fruits.appendChild($deepClone);
            </script>
        </html>

        ```
    - ### **결과**
        ``` 
        ● Apple
        ● Banana
            ○ Apple
            ○ Banana
        ```


## 5. 노드 교체(replaceChild)
- Node.prototype.replaceChild(newChild, oldChild) 메서드는 자신을 호출한 노드의 자식 노드를 다른 노드로 교체함
- 첫 번째 매개변수 newChild에는 교체할 새로운 노드를 인수로 전달하고, 두 번째 매개변수 oldChild에는 이미 존재하는 교체될 노드를 인수로 전달
- oldChild 매개변수에 인수로 전달한 노드는 replaceChild 메서드를 호출한 노드의 자식 노드이어야 함
- oldChild 노드는 DOM에서 제거됨
    - ### **CODE ⌨️**
        ``` html
        <!DOCTYPE html>
        <html>
            <body>
                <ul id='fruits'>
                    <li>Apple</li>
                </ul>
            </body>

            <script>
                const $fruits = document.getElementById('fruits');

                const $newChild = document.createElement('li');
                $newChild.textContent = 'Banana';

                $fruits.replaceChild($newChild, $fruits.firstElementChild);
            </script>
        </html>

        ```


## 6. 노드 삭제(removeChild)
- Node.prototype.removeChild(child) 메서드는 child 매개변수에 인수로 전달한 노드를 DOM에서 삭제함
- 인수로 전달한 노드는 removeChild 메서드를 호출한 노드의 자식 노드이어야 함
    - ### **CODE ⌨️**
        ``` html
        <!DOCTYPE html>
        <html>
            <body>
                <ul id='fruits'>
                    <li>Apple</li>
                    <li>Banana</li>
                </ul>
            </body>

            <script>
                const $fruits = document.getElementById('fruits');

                $fruits.removeChild($fruits.lastElementChild);
            </script>
        </html>

        ```