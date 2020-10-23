# 📚 Text Manipulation(Text 조작하기)



## **📖 Text 조작 키워드**
    1. nodeValue
    2. textContent
    3. innerHTML
    4. insertAdjacentHTML

1. ## **nodeValue**
    - Node.prototype.nodeValue 프로퍼티는 setter와 getter 모두 존재하는 접근자 프로퍼티로 참조와 할동 모두 가능

    - 텍스트 노드가 아닌 노드, 즉 문서 노드나 요소 노드의 nodeValue 프로퍼티를 참조하면 null 반환
        - ### **CODE ⌨️**
            ``` html

            <!DOCTYPE html>
            <html>
                <body>
                    <div id="foo">Hello</div>
                </body>

                <script>
                    //문서 노드의 nodeValue 참조
                    console.log(document.nodeValue); // null

                    //요소 노드의 nodeValue 참조
                    const $foo = document.getElementById('foo');
                    console.log($foo.nodeValue); // null

                    //텍스트 노드의 nodeValue 참조
                    const $textNode = $foo.firstChild;
                    console.log($textNode.nodeValue); // Hello
                </script>
            </html>

            ```
            - 위 코드 처럼 텍스트 노드의 nodeValue를 참조할 때만 텍스트 노드의 값을 반환

    - 텍스트 노드의 nodeValue 프로퍼티의 값을 할당하면 텍스트 노드의 값, 즉 텍스트를 변경할 수 있음
        - ### **CODE ⌨️**
            ``` html

            <!DOCTYPE html>
            <html>
                <body>
                    <div id="foo">Hello</div>
                </body>

                <script>
                    // 1. #foo 요소 노드의 자식 노드인 텍스트 노드 취득
                    const $textNode = document.getElementById('foo').firstChild;

                    // 2. nodeValue 프로퍼티를 사용하여 텍스트 노드의 값을 변경
                    $textNode.nodeValue = 'World';

                    console.log($textNode.nodeValue); // World
                </script>
            </html>

            ```

1. ## **textContent**
    - Node.prototype.textContent 프로퍼티는 setter와 getter 모두 존재하는 접근자 프로퍼티로서 요소 노드의 텍스트와 모든 자손 노드의 텍스를 모두 취득하거나 변경 가능

    - 요소 노드의 textContent 프로퍼티를 참조하면 요소 노드의 콘텐츠 영역(시작 태그와 종료 태그 사이) 내의 텍스트를 모두 반환. 이때 HTML 마크업은 무시
        - ### **CODE ⌨️**
            ``` html

            <!DOCTYPE html>
            <html>
                <body>
                    <div id="foo">Hello <span>World</span></div>
                </body>

                <script>
                    const $foo = document.getElementById('foo');

                    console.log($foo.textContent); // Hello World
                </script>
            </html>

            ``` 
    - 만얀 요소 노드의 콘텐츠 영역에 자식 요소 노드가 없고 텍스트만 존재한다면 firstChild.nodeValue와 textContent 프로퍼티는 같은 결과를 반환

    - 요소 노드의 textContent 프로퍼티에 문자열을 할당하면 요소 노드의 모든 자식 노드가 제거되고 할당한 문자열이 텍스트로 추가. 이때 할당한 문자열에 HTML 마크업이 포함되어 있더라도 문자열 그대로 인식되어 텍스트로 취급(HTML 마크업이 파싱되지 않음)
        - ### **CODE ⌨️**
            ``` html

            <!DOCTYPE html>
            <html>
                <body>
                    <div id="foo">Hello <span>World</span></div>
                </body>

                <script>
                    const $foo = document.getElementById('foo');

                    $foo.textContent = 'Hi <span>there</sapn>'; // 텍스트 자체로 입력됨(HTML 파싱 X)

                    console.log($foo.textContent); // Hi <span>there</sapn>
                </script>
            </html>

            ``` 

    - ### **➕ innerText**
        - textContent와 유사하게 동작하지만 잘 사용하지 않음
            - innerText 프로퍼티는 CSS에 순종적(예시 : CSS에 의해 비표시(visibility : hidden;)로 지정된 요소 노드의 텍스트를 반환하지 않음)

            - innerText 프로퍼티는 CSS를 고려해야 하므로 textContent 프로퍼티보다 느림
1. ## **innerHTML**
    - Element.prototype.innerHTML 프로퍼티는 setter와 getter 모두 존재하는 접근자 프로퍼티로서 요소 노드의 HTML 마크업을 취득하거나 변경

    - 요소 노드의 innerHTML 프로퍼티를 참조하면 요소 노드의 콘텐츠 영역(시작 태그와 종료 태그 사이) 내에 포함된 모든 HTML 마크업을 문자열로 반환
        - ### **CODE ⌨️**
            ``` html

            <!DOCTYPE html>
            <html>
                <body>
                    <div id="foo">Hello <span>World</span></div>
                </body>

                <script>
                    const $foo = document.getElementById('foo');

                    console.log($foo.innerHTML); // "Hello <span>World</span>"
                </script>
            </html>

            ```
            - textContent 프로퍼티를 참조하면 HTML 마크업을 무시하고 텍스트만 반환하지만 innerHTML 프로퍼티는 HTML 마크업이 포함된 문자열을 그대로 반환

    - 요소 노드의 innerHTML 프로퍼티에 문자열을 할당하면 요소 노드의 모든 자식 노드가 제거되고 할당한 문자열에 포함된 HTML 마크업이 파싱되어 요소 노드의 자식 노드로 DOM에 반영
        - ### **CODE ⌨️**
            ``` html

            <!DOCTYPE html>
            <html>
                <body>
                    <div id="foo">Hello <span>World</span></div>
                </body>

                <script>
                    const $foo = document.getElementById('foo');

                    // HTML 마크업이 파싱되어 요소 노드의 자식 노드로 DOM에 반영
                    $foo.innerHTML = 'Hi <span>there</span>'

                    console.log($foo.innerHTML); // "Hi <span>there</span>"

                    // textContent 프로퍼티로 HTML 파싱여부 확인
                    console.log($foo.textContent); // Hi there
                </script>
            </html>

            ```
            - 이처럼 innerHTML 프로퍼티를 사용하면 HTML 마크업 문자열로 간단히 DOM조작이 가능

    - 사용자로부터 입력받은 데이터를 그대로 innerHTML 프로퍼티로 할당하는 것은 크로스 사이트 스트립팅 공격(XSS : Corss-Site Scripting Atacks)에 취약하므로 위험. HTML 마크업 내에 자바스크립트 악성 코드가 포함되어 있다면 파싱 과정에서 그대로 실행될 가능성이 있기 때문
        - ### **CODE ⌨️**
            ``` html

            <!DOCTYPE html>
            <html>
                <body>
                    <div id="foo">Hello</div>
                </body>

                <script>
                    const $foo = document.getElementById('foo');

                    // innerHTML 프로퍼티로 스크립트 태그를 삽입하여 자바스크립트가 실행되도록 함
                    // HTML5는 innerHTML 프로퍼티로 삽입된 script 요소 내의 자바스크립트 코드를 실행하지 않음
                    $foo.innerHTML = `<script>alert(document.cookie)</script>`;
                </script>
            </html>

            ```
            - HTML5 에서는 직접 script를 삽입하면 동작하지 않지만 이벤트를 에러 이벤트를 강제로 발생시켜 script코드를 실행 할 수 있음
            ``` html
            
            <!DOCTYPE html>
            <html>
                <body>
                    <div id="foo">Hello</div>
                </body>

                <script>
                    const $foo = document.getElementById('foo');

                    // innerHTML 프로퍼티로 스크립트 태그를 삽입하여 자바스크립트가 실행되도록 함
                    // HTML5는 innerHTML 프로퍼티로 삽입된 script 요소 내의 자바스크립트 코드를 실행하지 않음
                    $foo.innerHTML = `<img src='x' onerror='alert(document.cookie)'>`>;
                </script>
            </html>

            ```
            - 위 예제처럼 innerHTML 프로퍼티를 사용하면 DOM 조작 구현이 간단하고 직관적이라는 장점이 있지만 크로스 사이트 스크립팅 공격에 취약한 단점이 있음

    - innerHTML 프로퍼티의 또 다른 단점은 요소 노드의 innerHTML 프로퍼티에 HTML 마크업 문자열을 할당하는 경우 요소 노드의 모든 자식 노드를 제거하고 할당한 HTML 마크업 문자열을 파싱하여 DOM을 변경한다는 점
        - 예를들어 `li` 항목을 1가지 추가하는 작업을 할때 원래 있던 요소들을 전부 지우고 다시 새로 `li` 항목들을 만들어야 한다는 것(불필요한 재생성)
        - 만약 요소와 요소 사이에 삽입하고 싶을 경우에는 innerHTML 프로퍼티를 사용하지 않는 것이 좋음


1. ## **insertAdjacentHTML**
    - Element.prototype.insertAdjacentHTML(position, DOMString) 메서드는 기존 요소를 제거하지 않으면서 위치를 지정해 새로운 요소를 삽입
    - insertAdjacentHTML 메서드는 두 번째 인수로 전달한 HTML 마크업 문자열(DOMString)을 파싱하고 그 결과로 생성된 노드를 첫 번째 인수로 전달한 위치(position)에 삽입하여 DOM에 반영
    - 첫 번째 인수로 전달할 수 있는 문자열 4가지
        - `'beforebegin'` : 시작 태그 앞
        - `'afterbegin'` : 시작 태그 뒤
        - `'beforeend'` : 종료 태그 앞
        - `'afterend'` : 종료 태그 뒤
        - ### **CODE ⌨️**
            ``` html

            <!DOCTYPE html>
            <html>
                <body>
                    <!-- <p>beforebegin</p> -->
                    <div id="foo">
                        <!-- <p>afterbegin</p> -->
                        Hello
                        <!-- <p>beforeend</p> -->
                    </div>
                    <!-- <p>afterend</p> -->
                </body>
                <script>
                    const $foo = document.getElementById('foo');

                    $foo.insertAdjacentHTML('beforebegin', '<p>beforebegin</p>');
                    $foo.insertAdjacentHTML('afterbegin', '<p>afterbegin</p>');
                    $foo.insertAdjacentHTML('beforeend', '<p>beforeend</p>');
                    $foo.insertAdjacentHTML('afterend', '<p>afterend</p>');
                </script>
            </html>

            ```
        - insertAdjacentHTML 메서드는 기존 요소에는 영향을 주지 않고 새롭게 삽입될 요소만을 파싱하여 자식 요소로 추가하므로 innerHTML 프로퍼티보다 효율적이고 빠름
        - 단, innerHTML 프로퍼티와 마찬가지로 HTML 마크업 문자열을 파싱하므로 크로스 사이트 스크립팅 공격에 취약