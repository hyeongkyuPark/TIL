## JSON 포맷

데이터 전송 포맷으로 현재 가장 많이 사용되는 포맷으로 Key: Value 형태료 표현(자바스크립트 객체와 비슷한 문법을 사용)

```json
{
	"phone_number":"010-1234-1234",
	"age":10,
	"isAgree":false,
	"account":{
		"email":"test@gmail.com",
		"password":"1234"
	},
	"agree_list": [1, 2, 3, 4]
}
```

### Post API 만들기

1. @RequestBody를 이용해 요청 객체를 받을 수 있음 Map타입으로 전체를 받아 올 수 있고, 명시적으로 받아 올 수 있음
2. Dto 객체를 이용해 받아올 수 있음)(Post는 Dto를 이용해 받아올때도 @RequestBody도 함께 써줘야 함)

```kotlin
@RestController
@RequestMapping("/api/post")
class PostApiController {
    @PostMapping("")
    fun post(@RequestBody requestBody: Map<String, String>) {
        requestBody.forEach{
            println("key : ${it.key}")
            println("value : ${it.value}")
        }
    }
    @PostMapping("/user")
    fun createUser(@RequestBody userDto: UserDto): UserDto {
        return userDto
    }
}
```
