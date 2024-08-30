---
categories:
- 👩‍💻 Today I learn
- ✨ Spring Boot
- RESTful API
  
tags:

---
### 프론트에서 FORM 방식으로 데이터를 보낼 때

---

- `@RequestParam`을 사용하는 방법 :각 필드를 개별적으로 받는 방법
- `@ModelAttribute`를 사용하는 방법 : 여러 필드를 묶어서 DTO 객체로 받는 방법
    
    **⇒ 난 이 방식으로 받아보겠다.**
    

- **`@ModelAttribute` 란?**
    - HTTP 요청 파라미터를 자동으로 특정 객체의 필드에 매핑하는 데 사용됨
    - 이 애너테이션을 사용하면 클라이언트로부터 전달된 폼 데이터나 쿼리 파라미터를 **DTO(또는 도메인 객체)로 자동 바인딩**할 수 있음

```java
@RestController
public class BookController {

    @PostMapping("/book")
    public void postBook(@ModelAttribute BookDTO bookDTO) {
        ...
    }
}
```

### PostMan으로 `post` 요청하기

---

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/812b948e-9751-4209-8bc5-1e65635e7178/9a3f3598-fda3-49a7-b4c1-b0701f84f27b/image.png)

### 기본 값은 문자열

---

- HTML의 `<form>` 요소를 사용하여 데이터를 서버로 전송할 때, 전송할 수 있는 데이터의 타입은 기본적으로 문자열(`string`)

### **@ModelAttribute와 @RequestBody의 차이**

---

- **`@ModelAttribute`**
    - HTML **폼 데이터**를 객체로 변환하는 데 사용됨
    - 주로 `@Controller`와 함께 사용됨
- **`@RestController`**
    - RESTful 웹 서비스를 만들 때 사용됨
    - 메서드의 반환값이 자동으로 JSON 형태로 변환되어 응답 본문에 포함됨
    - `@RequestBody`를 사용하여 요청 본문에서 JSON 데이터를 객체로 변환 받음