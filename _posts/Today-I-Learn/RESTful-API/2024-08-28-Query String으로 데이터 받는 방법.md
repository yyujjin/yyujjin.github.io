---
categories:
- 👩‍💻 Today I learn
- 📡 RESTful API
  
tags:

---
### 📌 @RequestParam

---

HTTP 요청의 **쿼리 스트링, 폼 데이터, 또는 URL 경로**에서 특정 파라미터 값을 추출하여 컨트롤러 메서드의 매개변수로 전달

**예시:**

### 프론트엔드에서 서버로 전송되는 URL:

```
plaintext코드 복사
/book?isbn=9781617294945&title=Spring%20in%20Action
```

### 서버 측 (Spring MVC 컨트롤러):

```java
@GetMapping("/book")
public void getBook(@RequestParam String isbn, @RequestParam String title) {
    // 'isbn'과 'title' 파라미터가 자동으로 매핑되어 메서드의 매개변수로 전달됩니다.
    System.out.println("ISBN: " + isbn);
    System.out.println("Title: " + title);
    // 추가적인 처리 로직
}
```