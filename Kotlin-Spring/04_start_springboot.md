# Spring Boot란?

Spring Boot는 단순히 실행되며, 프로덕션 제품 수준의 스프링 기반 어플리케이션을 쉽게 만들 수 있음

Spring Boot 어플리케이션에는 Spring 구성이 거의 필요하지 않음

Spring Boot java-jar로 실행하는 Java 어플리케이션을 만들 수 있음

### 장점

- Spring 개발에 대해 빠르고, 광범위하게 적용할 수 있는 환경 제공
- 기본값 설정이 있지만 설정을 바꿀 수 있음
- 대규모 프로젝트에 공통적인 비 기능 제공(보안, 모니터링 등)
- XML 구성 요구사항이 전혀 없음

## ※ Servlet(서블릿) 이란?

클라이언트의 요청을 처리하고, 그 결과를 반환하는 Servlet 클래스의 구현 규칙을 지킨 자바 웹 프로그래밍 기술(자바를 사용하여 웹을 만들기 위해 필요한 기술)

톰캣과 같은 WAS가 자바 파일을 컴파일하여 Class로 만들고 메모리에 올려 Servlet 객체를 만들고, 이 Servlet 객체는 doPost, doGet을 통해 요청에 응답(WAS를 통해 컴파일 된 후 메모리에 적재되어 클라이언트의 HTTP GET, POST 등의 요청을 처리하는 자바 프로그램)

※ WAS(Web Application Server) : 인터넷 상에서 HTTP를 통해 사용자 컴퓨터나 장치에 어플리케이션을 수행해주는 미들웨어

### 특징

- 클라이언트의 요청에 대해 동적으로 작동하는 웹 어플리케이션 컴포넌트
- html을 사용하여 요청에 응답
- Java Thread를 이용하여 동작
- MVC 패턴에서 Controller로 이용
- HTTP 프로토콜 서비스를 지원하는 javax.servlet.http.HttpServlet 클래스를 상속 받음
- UDP보다 처리 속도가 느림
- HTML 변경 시 Servlet을 재컴파일 해야하는 단점이 있음

### 서블릿 컨테이너

클라이언트에서 요청을 하면 컨테이너는 HttpServletRequest, HttpServletResponse 두 객체를 생성하며 post, get여부에 따라 동적인 페이지를 생성하여 응답을 보냅니다.

- HttpServletRequest : http프로토콜의 request 정보를 서블릿에게 전달하기 위한 목적으로 사용하며 헤더 정보, 파라미터, 쿠키, URI, URL 등의 정보를 읽거 들이는 메서드와 Body의 Stream을 읽어 들이는 메서드를 가지고 있음
- HttpServletResponse : WAS는 어떤 클라이언트가 요청을 보냈는지 알고 있고, 해당 클라이언트에게 응답을 보내기 위한 HttpServletResponse 객체를 생성하여 서블릿에게 전달하고 이 객체를 활용해 content-type, 응답 코드, 응답 메세지 등을 전송함
- 주요기능
    - 생명주기 관리
    - 통신 지원 : 서블릿 컨테이너는 이렇게 소켓을 만들고 listen, accept 등의 기능을 API로 제공하여 복잡한 과정을 생략할 수 있게 해주고 개발자로서 비즈니스 로직에 더욱 집중할 수 있게 만들어 줌
    - 멀티스레딩 관리 : 서블릿 컨테이너는 해당 서블릿의 요청이 들어오면 스레드를 생성해서 작업을 수행합니다. 그렇기에 동시에 여러 요청이 들어와도 멀티스레딩 환경으로 동시다발적인 작업을 관리 할 수 있음
    - 선언적인 보안관리

# Hello World API 작성하기

### API 테스트 프로그램(Postman) 설치

1. [https://www.postman.com](https://www.postman.com/) 페이지에서 OS에 맞는 설치파일 다운로드 받아 설치(온라인도 지원)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2605a859-f16d-4c2c-99ba-011e72e8fe52/Untitled.png)

### 프로젝트 생성

1. [https://start.spring.io](https://start.spring.io/) 페이지에서 간단하게 프로젝트를 생성할 수 있음
2. 생성을 원하는 프로젝트 설정 진행 후 GENERATE 클릭

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6669ab82-94e1-4bd6-b531-ea43ff3c182c/Untitled.png)

1. 인텔리제이 IDE를 이용해 프로젝트 폴더를 열면 자동적으로 gradle이 돌아가면서 필요한 dependcy들을 다운로드 받음

### HelloWorld Rest API 생성

1. main.kotlin.com.example.reststudy.controller 경로에 ApiController 클래스 생성
2. Rest API 작성
    
    ```kotlin
    package com.example.reststudy.controller
    
    import org.springframework.web.bind.annotation.GetMapping
    import org.springframework.web.bind.annotation.RequestMapping
    import org.springframework.web.bind.annotation.RestController
    
    @RestController // 해당 Class는 REST API를 처리하는 Controller
    @RequestMapping("/api") // URI를 지정
    class ApiController {
    
        @GetMapping("/hello") // http://localhost:9090/api/hello
        fun hello(): String {
            return "hello spring boot"
        }
    }
    ```
    
3. Postman 요청 테스트
![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6669ab82-94e1-4bd6-b531-ea43ff3c182c/Untitled.png)
