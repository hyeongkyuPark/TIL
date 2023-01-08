## 01. 기본적인 GET 사용법

- 기본적으로 GetMapping을 사용하면 쉽게 Get메서드를 정의 할 수 있음
    - path 속성을 사용해 명시적으로 선언 및 여러개 맵핑 가능(@GetMapping(path= [”/path”, “/path2”]))
    - 속성없이 문자열만 사용하면 한 개 경로에 맵핑(@GetMapping(”/hello”))
- GetMapping이 나오기 전에는 RequestMapping을 사용
    - 메서드와 패스를 사용 목적에 맞게 명시적으로 넣어줘야 함

```kotlin
@RestController
@RequestMapping("/api/get")
class GetApiController {

    // 1. 기본적인 Get 사용방법
    @GetMapping(path = ["/hello"])
    fun getHello(): String {
        return "get Hello"
    }

    // 2. 과거 Get 사용방법
    // 과거 주소 지정 방식(명시적으로 메서드를 선언해줘야 했음)
    @RequestMapping(path = ["/hi"], method = [RequestMethod.GET])
    fun hi(): String {
        return "hi~!"
    }
}
```

## 02. PathVariable 받기

- @PathVariable를 사용하여 쉽게 받아 올 수 있음
    - 기본적으로 name 속성을 따로 주지 않으면 맵핑 경로에 사용한 이름으로 받아옴
    - name 속성을 지정하고 원하는 변수명으로 받아올 수 있음

```kotlin
// 3. path variable 받기
    // http://localhost:9090/api/get/path-variable/{name}
    @GetMapping("/path-variable/{name}")
//  fun getPathVariable(@PathVariable name: String): String {
    fun getPathVariable(@PathVariable(name = "name") pathName: String): String { // 받는 이름과 사용 이름을 다르게 설정
        return "pathVariable test :: $pathName"
    }
```

## 03. QueryParam 받기

1. @RequestParam에 속성 없이 사용하면 모든 쿼리를 받아옴
2. @RequestParam에 name 속성을 이용해 정해진 쿼리만 받아올 수 있음
3. DTO 클래스를 인자로 받으면 자동으로 맵핑 가능
- 2, 3번은 명시한 쿼리를 빼고 요청하면 400에러가 발생함
    - `required = false` 속성으로 옵션적으로 받도록 설정 가능

```kotlin
 // 4-1. queryParam(key, value) 받기
    // ?key=value&key2=value2
    @GetMapping("/query-param")
    fun getQueryParams(@RequestParam queryParam: Map<String, String>): String {
        var result = queryParam.map { "${it.key} = ${it.value}" }

        return "queryParams test :: $result"
    }

    // 4-2. 정해진 이름의 queryParam(key, value) 받기
    @GetMapping("/query-param02")
    fun getQueryParams02(
        @RequestParam(name = "name") name: String,
        @RequestParam(name = "email") email: String,
        @RequestParam(name = "age", required = false) age: Int,
    ): String {
        return "$name $email $age"
    }

    // 4-3. DTO를 이용해 queryParam(key, value) 받기
    @GetMapping("/query-param03")
    fun getQueryParams03(userDto: UserDto): String {
        return "${userDto.name} ${userDto.email} ${userDto.age}"
    }
```
