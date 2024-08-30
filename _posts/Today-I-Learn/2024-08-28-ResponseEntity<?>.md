---
categories:
- 👩‍💻 Today I learn
- ✨ Spring Boot
- RESTful API
  
tags:

---

### ❓ ResponseEntity<?> 란?

---

- Spring Framework에서 **HTTP 응답(response)을 표현하기 위해 사용되는 클래스**
- 제네릭 타입을 사용하여 응답 **본문(body)의 타입을 지정할 수 있음**
- `ResponseEntity<?>`에서 `<?>`는 와일드카드(Wildcard)로, 응답 본문의 타입을 특정하지 않고 다양한 타입의 데이터를 반환하겠다는 의미

### 예시 코드 설명

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

- **`ResponseEntity.badRequest().body("이미 존재하는 책입니다.");`**:
    - **`ResponseEntity.badRequest()`**: HTTP 상태 코드를 400 Bad Request로 설정합니다.
    - **`.body("이미 존재하는 책입니다.")`**: 응답 본문에 `"이미 존재하는 책입니다."`라는 메시지를 담습니다. 이 메시지는 `String` 타입이지만, `ResponseEntity<?>`로 선언된 메서드이기 때문에 문제가 없습니다.
- **`ResponseEntity.ok().body(bookDTO);`**:
    - **`ResponseEntity.ok()`**: HTTP 상태 코드를 200 OK로 설정합니다.
    - **`.body(bookDTO)`**: 응답 본문에 `bookDTO` 객체를 담습니다. 이 경우 `bookDTO`는 `BookDTO` 타입의 객체이지만, 역시 `ResponseEntity<?>`로 선언된 메서드이기 때문에 문제가 없습니다.

### 언제 `ResponseEntity<?>`를 사용하는가?

- **유연한 응답 타입 처리**: 메서드가 다양한 타입의 응답을 반환할 수 있을 때, `<?>`를 사용하여 어떤 타입이든 유연하게 처리할 수 있습니다.
- **특정 타입을 강제하지 않음**: 특정 타입을 강제하지 않고, 메서드 내에서 동적으로 응답 타입을 결정하고자 할 때 유용합니다.

### 대안: 명시적인 타입 사용

대신에, 만약 반환되는 타입이 명확하다면 `ResponseEntity<BookDTO>` 또는 `ResponseEntity<String>`과 같이 명시적으로 타입을 지정하는 것이 더 좋을 수 있습니다. 이는 코드의 가독성과 타입 안정성을 높이는 데 도움이 됩니다.

```java
java코드 복사
public ResponseEntity<BookDTO> postBook(@ModelAttribute BookDTO bookDTO) {
    // 같은 로직이지만, 명시적으로 BookDTO를 반환한다고 선언
}

```

이렇게 하면, 메서드를 사용하는 개발자가 어떤 타입의 응답을 기대할 수 있는지 명확하게 알 수 있습니다.