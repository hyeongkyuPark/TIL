# 🎮 DOM(Document Object Model)

## 🔍 DOM(문서 객체 모델) 이란?
- 웹 페이지에 대한 프로그래밍 인터페이스
- 기본적으로 여러 프로그램들이 페이지의 콘텐츠 및 구조, 그리고 스타일을 읽고 조작할 수 있는 API를 제공
- DOM은 원본 HTML 문서의 객체 기반 표현 방식이며 DOM의 개체 구조는 노드 트리(하나의 부모 줄기가 여러개의 자식 나뭇가지, 나뭇잎들을 가질 수 있는 나무와 같은 구조)로 표현 됨

## ⚔️ DOM 과 HTML의 차이점
- DOM은 HTML 문서로부터 생성이 되지만 항상 동일하지는 않음
- `HTML` : 화면에 보이고자 하는 모양과 구조를 문서로 만든 것으로 단순 텍스트로 구성 (최초 화면을 그릴때 사용하는 설계도)
- `DOM` : HTML 문서의 내용과 구조가 객체 모델로 변화되어 다양한 프로그램에서 사용될 수 있음 (설계도를 이용하여 실제로 화면에 나타내지는 인터페이스)
- 작성된 HTML 문서가 유효하지 않을 때 DOM을 생성하는 동안, 브라우저는 유효한 코드로 교정  
    - ### **CODE ⌨️**
        ``` html

        <!doctype html>
        <html>
            Hello, world!
        </html>

        ```
        - 위의 코드는 HTML 규칙의 필수 사항인 `<head>` 와 `<body>` 요소가 빠져있지만 DOM 트리에는 올바르게 교정되어 나타남
        ``` 
        html
            ㄴhead
            ㄴbody
                ㄴHello, world!
        ```
- DOM은 HTML 문서의 내용을 볼 수 있는 인터페이스 역할을 하는 동시에 동적 자원이 되어 수정될 수 있음(JavaScript에 의해 수정될 수 있음)
    - ### **CODE ⌨️**
        ``` javascript

        var p = document.createElement('p');
        var pContent = document.createTextNode('I\'m new!');
        p.appendChild(pContent);
        document.body.appendChild(p);
        

        ```
        - 위 코드는 JavaScript를 사용하여 DOM에 새로운 노드를 추가하는 코드로 DOM을 업데이트하지만 HTML 문서의 내용을 변경하지는 않음

## 🔩  DOM 과 렌더트리
- 브라우저 뷰 포트에 보이는 것은 렌더 트리로 DOM 과 CSSOM의 조합임
- 렌더 트리는 오직 렌더링 되는 요소만 관련이 있고 스크린에 그려지는 것으로 구성되기 때문에 시각적으로 보이지 않는 요소들은 제외시켜 DOM과는 다름
    - ### **CODE ⌨️**
    ``` html
    <!doctype html>
    <html lang="en">
        <head></head>
        <body>
            <h1> Hello, world! </h1>
            <p style="display : none;"> display none </p>
        </body>
    </html>
    ```
    - ### **DOM트리 🌲**
    ```
        
        <DOM트리>
        html
            ㄴhead
            ㄴbody
                ㄴh1
                |  ㄴHello, world!
                ㄴp
                   ㄴdisplay none

    ```
    - ### **렌더트리 🌲**
    ```
        
        <렌더트리>
        html
            ㄴhead
            ㄴbody
                ㄴh1
                    ㄴHello, world!
            
    ```

## DOM 과 CSS가상요소
- `::before`, `::after` 선택자를 사용하여 갱신된 가상요소는 CSSOM과 렌더트리의 일부를 구성하지만 DOM은 오직 원본 HTML 문서로부터 빌드 되고, 요소에 적용되는 스타일을 포함하지 않기 때문에 기술적으로 DOM의 일부가 아님
- 기본적으로 CSS가상요소는 DOM의 일부가 아니기 때문에 JavaScript로 수정될 수 없음