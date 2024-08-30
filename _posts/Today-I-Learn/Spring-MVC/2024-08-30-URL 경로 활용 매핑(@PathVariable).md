---
categories:
- 👩‍💻 Today I learn
- 🌐 Spring MVC
  
tags:

---

### **📌 @PathVariable 이란?**

---

- `@PathVariable`은 URL 경로에 변수를 삽입하고 이를 컨트롤러 메서드에서 받아 사용하는 데 사용됨
- 예를 들어, 만약 URL이 `/users/123`이라면, 이 중 `123` 부분을 변수로 받아올 수 있음

**📌 예시**

---

```java
@GetMapping("/users/{userId}")
public String getUser(@PathVariable("userId") String userId) {
    // userId에는 URL에서 전달된 123이 들어가게 됩니다.
    return "userProfile";
}
```

- 위 코드에서 `/users/123`이라는 요청이 들어오면, `@PathVariable("userId")`는 URL의 `{userId}`에 해당하는 `123` 값을 받아서 메서드의 `userId` 파라미터로 전달합니다.
- 따라서 `@PathVariable`을 사용하면 URL 경로의 특정 부분을 변수로 처리하여 해당 값을 메서드에서 활용할 수 있게 됩니다.

**📌 사용법**

---

Controller에서 아래와 같이 작성하면 간단하게 사용 가능하다.

1. GetMapping(PostMapping, PutMapping 등 다 상관없음)에 {**변수명**}
2. 메소드 정의에서 위에 쓴 변수명을 그대로 @PathVariable("**변수명**")
3. (Optional) Parameter명은 아무거나 상관없음(아래에서 String name도 OK, String employName도 OK)

```java
@RestController
public class MemberController { 
    // 기본
    @GetMapping("/member/{name}")
    public String findByName(@PathVariable("name") String name ) {
        return "Name: " + name;
    }
    
    // 여러 개
    @GetMapping("/member/{id}/{name}")
	public String findByNameAndId(@PathVariable("id") String id, @PathVariable("name") String name) {
    	return "ID: " + id + ", name: " + name;
    }
    
}
```

### ❓두 가지 매핑이 있을 경우

---

1. `@GetMapping("/member/{name}")`
2. `@GetMapping("/member/name")`

이와 같은 요청이 들어오면:

- `/member/name` 경로는 정확히 `/member/name`에 매핑된 메서드가 실행됩니다.
- URL 경로 `/member/name`이 정확히 일치하는 매핑이 있으면 그 매핑이 우선적으로 사용됩니다.

### 정리

- **정확한 URL 경로**가 일치하는 매핑이 가장 우선적으로 실행됩니다.
- 따라서, `/member/name`이라는 경로가 들어오면 `@GetMapping("/member/name")`에 매핑된 메서드가 실행됩니다.

만약 `@GetMapping("/member/{name}")`이 먼저 선언되어 있어도, 정확한 URL 매핑이 우선적으로 사용되므로 `/member/name`의 경우 `@GetMapping("/member/name")`이 실행됩니다.

### 🚀 동적 URL 매핑과 경로가 없는 경우의 처리

---

- 이 방식은 URL 경로의 특정 부분을 변수로 취급
- JSP 링크와 URL 경로가 일치할 때 해당 컨트롤러 부름

**로그인 클릭 → 파라미터로 login이 컨트롤러로 전송됨→ 컨트롤러는 `/login` 이렇게 인식해서 login 컨트롤러가 호출됨**

📁 jsp

```java
 <a href="login">로그인</a>
```

📁 controller

```java
@GetMapping("/{page}")
    public String requestPage(@PathVariable("page") String page)
```

📁 loginController

```java
@GetMapping("/login")
public String showLoginPage() {
    return "user/login";
}
```

**하지만 만약 해당 매핑 경로가 없다면 page에는 login이라는 문자열 그 자체로 넘어옴** 

**📁 loginController**  

```java
**//@GetMapping("/login") 이게 없다면**
public String showLoginPage() {
    return "user/login";
}
```

📁 controller

```java
@GetMapping("/{page}") **//문자열 그 자체로 파라미터 넘어옴**
    public String requestPage(@PathVariable("page") String page)
```