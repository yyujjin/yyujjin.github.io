---
categories:
- 👩‍💻 Today I learn
- 📡 RESTful API
  
tags:

---

### ❓ ResponseEntity<?> 란?

---

- Spring Framework에서 **HTTP 응답(response)을 표현하기 위해 사용되는 클래스**
- 제네릭 타입을 사용하여 응답 **본문(body)의 타입을 지정할 수 있음**
- `ResponseEntity<?>`에서 `<?>`는 와일드카드(Wildcard)로, 응답 본문의 타입을 특정하지 않고 다양한 타입의 데이터를 반환하겠다는 의미

**예시 코드:**

```java
java코드 복사
public ResponseEntity<?> postBook(@ModelAttribute BookDTO bookDTO) {
    log.info("getIsbn : {}", bookDTO.getIsbn());
    log.info("getTitle : {}", bookDTO.getTitle());

    boolean isBook = bookService.postBook(bookDTO);

    if (isBook) {
        return ResponseEntity.badRequest().body("이미 존재하는 책입니다.");
    }

    return ResponseEntity.ok().body(bookDTO);
}

```

### ✅ 명시적인 타입 사용

---

만약 반환되는 타입이 명확하다면 `ResponseEntity<BookDTO>` 또는 `ResponseEntity<String>`과 같이 **명시적으로 타입을 지정하는 것이 더 좋음**

**예시 코드:**

```java
java코드 복사
public ResponseEntity<BookDTO> postBook(@ModelAttribute BookDTO bookDTO) {
    // 같은 로직이지만, 명시적으로 BookDTO를 반환한다고 선언
}
```