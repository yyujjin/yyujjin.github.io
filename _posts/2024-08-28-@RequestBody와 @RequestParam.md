---
categories:
- ✨ Spring Boot
- RESTful API
  
tags:
- annotation
---

### 📌 **@RequestBody**

---

HTTP 요청의 **본문(body)**에 있는 데이터를 자바 객체로 변환하여 컨트롤러 메서드의 매개변수로 전달

```java
@PostMapping("/book")
public void createBook(@RequestBody Book book) {
}
```

#### 💡 DTO vs Map: @RequestBody에서 DTO를 사용하는 이유와 장점

- DTO 사용
    - DTO는 데이터의 구조를 명확하게 정의하고, 이를 통해 코드의 가독성, 유지보수성, 안전성을 높이는 데 도움이 됨
    - **유효성 검증:** DTO 클래스에 유효성 검증 어노테이션(`@NotNull`, `@Size`, `@Pattern` 등)을 추가하여 데이터 유효성을 쉽게 관리할 수 있음
- DTO를 사용하지 않는 방법
    - `Map<String, Object>` 또는 `@RequestBody String`을 사용할 수 있음
    
**결론 : POST 요청을 처리할 때 DTO를 사용하는 것이 일반적으로 권장됨**
    

### 📌 @RequestParam

---

HTTP 요청의 **쿼리 스트링, 폼 데이터, 또는 URL 경로**에서 특정 파라미터 값을 추출하여 컨트롤러 메서드의 매개변수로 전달

```java
@GetMapping("/book")
public void getBook(@RequestParam String isbn, @RequestParam String title) {
}
```