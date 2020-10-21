# 📚 Browser Rendering(브라우저 렌더링)

## 🛠 브라우저 기본 렌더링 과정
1. HTML 마크업을 처리하고 DOM 트리를 빌드(DOM 파싱)
1. CSS 마크업을 처리하고 CSSOM 트리를 빌드(CSS 파싱)
1. DOM 및 CSSOM을 결합하여 렌더 트리를 형성(Attachment)
1. 렌더 트리에서 레이아웃을 실행하여 각 노드의 기하학적 형태를 계산(Layout)
1. 개별 노드를 화면에 페인트(Painting)

<img src='https://beomy.github.io/assets/img/posts/browser/gecko_rendering_engine_process.png' width=80%>

## 1.Parser(파싱)
- 서버로부터 전송받은 문서의 문자열을 브라우저가 이해할 수 있는 구조로 변환하는 과정
- ### **DOM(Document Object Model) 파싱**
    <img src='https://beomy.github.io/assets/img/posts/browser/dom_parsing.png' width=80%>

    1. 변환(Conversion) : HTML의 원시 바이트를 읽어와 해당 파일에 지정된 인코딩(UTF-8 등)에 따라 문자열로 변환하는 과정
    1. 토큰화(Tokenizing) : 문자열을 W3C HTML 표준에 따라 고유 토큰(<html>, <body> 등)으로 변환. 각 토큰은 특별한 의미와 고유한 규칙을 가짐
    1. 렉싱(Lexing) : 토큰을 해당 속성 및 규칙을 정의한 객체(Nodes)로 변환
    1. DOM 생성(Dom Construction) : HTML은 상위-하위 관계로 정의할 수 있어, 트리 구조로 나타낼 수 있음. 렉싱 과정을 거쳐 생성된 노드들을 트리 구조로 변환

- ### **CSSOM(CSS Object Model) 파싱**
    <img src='https://beomy.github.io/assets/img/posts/browser/cssom_construction.png' width=80%>
    
    - 브라우저는 DOM을 생성하는 동안 외부 CSS를 참조하는 <link> 태그를 만나게 되면 브라우저에 리소스를 요청
    - 이후 DOM을 생성하는 과정 그대로 CSSOM라는 트리구조를 생성

    <img src='https://beomy.github.io/assets/img/posts/browser/cssom_tree.png' width=80%>


## 2. Attachment(부착)
- CSSOM 트리와 DOM 트리를 결합하여, 표시해야 할 순서로 내용을 그려낼 수 있도록 하기 위해 렌더 트리를 형성(Webkit : Attachment, Gecko : Frame Constructor)
- ### **렌더 트리 생성 과정**
    <img src='https://beomy.github.io/assets/img/posts/browser/render_tree_construction.png' width=80%>

    1. DOM트리의 루트에서 시작하여 화면에 표시되는 노드 각각을 탐색. 이 과정에서 화면에 표시되지 않는 일부 노드들(script, meta 태그 등)은 렌더 트리에 반영되지 않음
    1. 화면에 표시되는 각 노드에 대해 적절하게 일치하는 CSSOM 규칙을 찾아 적용.(display:none 이 설정된 노드는 렌더 트리에 반영되지 않음)
    1. 화면에 표시되는 노드를 콘텐츠 및 계산된 스타일과 함께 내보냄

## 3. Layout
- 렌더 트리가 생성되고, 기기의 뷰포트 내에서 렌더 트리의 노드가 정학한 위치와 크기를 계산하는 과정(= Reflow)
- 모든 상대적인 측정값은 화면에서 절대적인 px단위로 변환(% 단위(상대값) =[계산]=> px 단위(절대값))

## 4. Panting
- 렌더 트리의 각 노드를 화면에 실제 픽셀로 나타내는 과정(= rasterizing)
- 이 과정을 거쳐서 브라우저 화면에 UI가 나타나게 됨
- 처리해야 할 스타일(텍스트, 색, 이미지, 그림자 효과 등)이 복잡할 수록 소요시간은 늘어남


## ➕ Reflow & Repaint
- 위에서 언급된 렌더링 과정을 거친 뒤에 최종적으로 페이지가 그려진다고 해서 렌더링 과정이 끝난것이 아님

- ### **Reflow (Layout 다시 수행)**
    - 어떠한 액션이나 이벤트에 따라서 html 요소의 크기나 위치 등 레이아웃 수치를 수정하면 그에 영향을 받는 자식 노드나 부모 노드들을 포함하여 layout 과정이 다시 수행
    - Reflow 대상
        - 뷰포트 크기 변경
        - 노드 추가 또는 제거
        - 요소의 위치, 크기 변경
        - 폰트 변경과 이미지 크기 변경 등

- ### **Repaint (Panting 다시 수행)**
    - Reflow 만 수행되면 실제 화면에 반영되 않음. 렌더트리를 다시 화면에 그려주는 과정 필요한데 그 과정을 Repaint라고 함
    - background-color, visibility와 같이 레이아웃에는 영향을 주지 않는 스타일 속성이 변경되었을 때는 Reflow 단계를 수행하지 않고 Repaint만 수행