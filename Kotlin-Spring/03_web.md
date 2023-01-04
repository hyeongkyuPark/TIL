# Web 이란?
World Wide Web, WWW, W3 는 인터넷에 연결된 컴퓨터를 통해 사람들이 정보를 공유할 수 있는 전 세계적인 정보 공간을 말함

## Web의 용도

### Web Site

google, naver, facebook 등 HTML로 구성된 사이트들

### API(Application Programing Interface) Web Service

카카오 open API, 구글 open API, 등

### User Interface

크롬, 사파리, 익스플로러, 스마트 워치, IP TV 등

## Web의 기본 3가지 요소

### URI(Uniform Resource Identifier)

리소스 식별자

모든 정보에 접근 할 수 있는 정보

### HTTP(Hypertext Transfer Protocol)

어플리케이션 컨트롤

Get, Post, Put, Delete, Options, Head, Trace, Connect 등의 메서드를 활용

### HTML(Hypertext Markup Language)

하이퍼 미디어 포맷

XML기반 Web 범용 문서 포맷

브라우저에 사용자가 알아보기 쉬운 형태로 표현됨

# REST
## REST 란?

자원의 상태 전달 - 네트워크 아키텍처

1. Client, Server : 클라이언트와 서버가 서로 독립적으로 분리 되어 있어야 함
2. Stateless : 요청에 대해서 클라이언트의 상태를 서버에 저장하지 않음
3. Cache : 클라이언트는 서버의 응답을 Cache(임시저장) 할 수 있어야 하며, 클라이언트가 Cache를 통해서 응답을 재사용할 수 있어야 함(서버의 부하를 낮춤)
4. 계층화(Layer System) : 서버와 클라이언트 사이에 방화벽, 게이트웨이, Proxy 등 다양한 계층 형태로 구성이 가능해야 하며, 이를 확장 할 수 있어야 함
5. 인터페이스 일관성 : 인터페이스의 일관성을 지키고, 아키텍처를 단순화시켜 작은 단위로 분리해서 클라이언트, 서버가 독립적으로 개선 될 수 있어야 함
6. Code on Demand(Optional) : 자바 애플릿, 자바스크립트, 플래시 등 특정한 기능을 서버로 부터 클라이언트가 전달받아 코드를 실행 할 수 있어야 함

## Rest Ful API 조건

### 자원의 식별

- 웹 기반의 REST에서는 리소스 접근을 할 때 URI를 사용함
- URI를 통해 리소스와 식별자를 식별 할 수 있어야함
    - 예시) https://test.co.kr/user/100 ⇒ 리소스 : user, 식별자 : 100

### 메세지를 통한 리소스 조작

- Web에서는 다양한 방식으로 데이터를 전달 할 수 있음(HTML, XML, JSON, TEXT 등)
- 어떤 타입의 데이터를 보내는지 알려주기 위해 HTTP Header 부분에 content-type을 통해 데이터의 타입을 지정해 줄 수 있음
- 리소스 조작을 위해서 데이터 전체를 전달하지 않고, 이를 메세지로 전달 할 수 있음

### 자기 서술적 메세지

- 요청하는 데이터가 어떻게 처리 되어져야 하는지 충분한 데이터를 포함 할 수 있어야 함
- HTTP 기반의 REST에서는 HTTP 메서드와 Header 정보, 그리고 URI에 포함되는 정보로 표현할 수 있음
    - GET: https://test.co.kr/user/100 ⇒ 사용자 정보 요청
    - POST: https://test.co.kr/user/100 ⇒ 사용자 정보 생성
    - PUT: https://test.co.kr/user/100 ⇒ 사용자 정보 생성 및 수정
    - DELETE: https://test.co.kr/user/100 ⇒ 사용자 정보 삭제
    - 이 외에 담지 못한 정보들은 URI의 메세지를 통하여 표현

### Application 상태에 대한 엔진으로써의 하이퍼미디어

- REST API를 개발할 때 단순히 Client 요청에 대한 데이터만 응답 해주는 것이 아니라 관련된 리소스에 대한 Link 정보까지 같이 포함 되어져야 함(실제로 많이 사용되지 않음)

# URI 설계 패턴
## URI & URL

### URI(Uniform Resource Identifier)

- 인터넷에서 특정 자원을 나타내는 주소 값. 해당 값은 유일 함(응답은 달라질 수 있음)
    - 요청 : https://test.co.kr/user/exel
    - 응답 : user.exel

### URL(Uniform Resource Locator)

- 인터넷 상에서의 자원, 특정 파일이 어디에 위치하는지 식별 하는 주소(응답이 달라질 수 없음)
- URL은 URI의 하위 개념

## URI 설계 원칙(RFC-3986)

- 슬래시 구분자는 계층 관계를 타나내는데 사용
- URI 마지막 문자로 슬래시를 포함하지 않음
- 하이픈은 URI 가독성을 높이는데 사용함(wet-master 사용O)
- 밑줄(_)은 사용하지 않음(web_master 사용X)
- URI 경로에는 소문자가 적합
- 파일 확장자는 URI에 포함하지 않음(.jsp 등)
- 프로그래밍 언어에 의존적인 확장자를 사용하지 않음(.do 등)
- 구현에 의존적인 경로를 사용하지 않음
- 세션 ID를 포함하지 않음
- 프로그래밍 언어의 메소드 명을 이용하지 않음
- 명사에 단수형 보다는 복수형을 사용해야 함(users)
- 컨트롤러 이름으로는 동사나 동사구를 사용
- 경로 부분중 변하는 부분은 유일한 값으로 대체 함(/users/{100} ⇒ 뒤 식별자는 변하는 값이므로 유일한 값으로 식별되어야 함)
- CRUD 기능을 나타내는 것은 URI에 사용하지 않음(/users/100/read 사용 X ⇒ read는 제외하고 작성)
- URI Query Parameter 디자인
    - UR I쿼리 부분으로 컬렉션 결과에 대해서 필터링 할 수 있음(/users?age=29)
- URI 쿼리는 컬렉션 결과를 페이지로 구분하여 나타내는데도 사용(/users?page=0&size=10&sort=asc)
- API에 있어서 서브 도메인은 일관성 있게 사용해야 함
- 클라이언트 개발자 포탈 서브 도메인은 일관성 있게 만들어야 함

# HTTP 프로토콜

- HTTP란 RFC 2616에서 규정된 Web에서 데이터를 주고 받는 프로토콜
- 이름에는 하이퍼 텍스트 전송용 프로토콜로 정의되어 있지만 실제로는 HTML, XML, JSON, Image, Voice, Video, Javascript, PDF 등 다양한 컴퓨터에서 다룰 수 있는 것은 모두 전송 할 수 있음
- HTTP는 TCP를 기반으로 한 REST의 특징을 모두 구현하고 있는 Web 기반의 프로토콜
- HTTP는 메세지를 주고(Request) 받는(Response) 형태의 통신 방법
- 클라이언트는 서버에 요청을 보내고 일정 시간동안 응답이 오지 않으면 취소하고, 응답 메세지가 오면 수신함

## HTTP 메서드

- GET : 리소스 취득 (R, 멱등성, 안정성, PathVariable, QueryParameter)
- POST : 리소스 생성, 추가 (C, PathVariable, QueryParameter*(권장X), DataBody)
- PUT : 리소스 갱신, 생성 (C/U, 멱등성, PathVariable, QueryParameter*(권장X), DataBody)
- DELETE : 리소스 삭제 (D, 멱등성, PathVariable, QueryParameter)
- HEAD : 헤더 데이터 취득 (멱등성, 안정성)
- OPTIONS : 지원하는 메서드 취득 (멱등성)
- TRACE : 요청 메세지 반환 (멱등성)
- CONNECT : 프록시 동작의 터널 접속으로 변경

※ 멱등성 : 같은 요청에는 같은 응답을 보내줌

※ 안정성 : 요청으로 인한 서버 데이터 변화가 없음

## HTTP Status Code(상태코드)

- 1XX(처리중) : 처리가 계속 되고있는 상태. 클라이언트는 요청을 계속 하거나 서버의 지시에 따라서 재요청
- 2XX(성공) : 요청의 성공
- 3XX(리다이렉트) : 다른 리소스로 리다이렉트. 해당 코드를 받았을 때는 Response의 새로운 주소로 다시 요청
- 4XX(클라이언트 에러) : 클라이언트의 요청에 에러가 있는 상태. 재전송 하여도 에러가 해결되지 않음
- 5XX(서버에러) : 서버 처리중 에러가 발생한 상태. 재전송시 에러가 해결 되었을 수도 있음

### 자주 사용되는 코드

- 200 : 성공
- 201 : 성공, 리소스 생성 성공
- 301 : 리다이렉트, 리소스가 다른 장소로 변경됨
- 303 : 리다이렉트, 클라이언트에 자동으로 새로운 리소스로 요청 처리
- 400 : 요청 오류, 파라미터 에러
- 401 : 권한 없음(인증실패)
- 404 : 리소스 없음(페이지를 찾을 수 없음)
- 500 : 서버 내부 에러(서버 동작 처리 에러)
- 503 : 서비스 정지(점검 등)
