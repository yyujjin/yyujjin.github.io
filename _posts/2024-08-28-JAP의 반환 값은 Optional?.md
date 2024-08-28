---
categories:
- 👩‍💻 Today I learn
- JPA
  
tags:
- JPA
- Optional
- Java Programming
---

### 🤔 jpa의 모든 값은 Optional로 반환 되나?

---

- 모든 JPA 메서드가 `Optional`을 반환하는 것은 아님
- 목적과 사용 사례에 따라 다름
- 주로 `findById`와 같이 단일 엔터티를 조회할 때 사용 됨
- `Optional` 을 사용하지 않으면 객체나 리스트를 직접 반환, 하지만 만약 데이터가 없으면 `null`이나 빈 리스트를 반환할 수 있음

### ☑️ Optional을 반환하는 메서드 예시

---

- **`findById(Long id)` :** 주어진 ID로 엔터티를 조회할 때 사용됨
    - 데이터가 존재하지 않는다면, `Optional.empty()`를 반환

```java
Optional<User> user = userRepository.findById(1L);
if (user.isPresent()) {
    // 데이터가 존재할 때의 로직
} else {
    // 데이터가 존재하지 않을 때의 로직
}
```

### ☑️ Optional을 반환하지 않는 메서드 예시

---

- **`findAll()`** : 모든 엔터티를 리스트로 반환
    - 결과가 비어 있을 수는 있지만, 리스트 자체가 `null`이 되진 않음.

```java

List<User> users = userRepository.findAll();
```

- **`findByName(String name)`** : 특정 조건에 따라 데이터를 조회하고, 그 결과를 리스트로 반환하거나, 단일 객체로 반환
    - `Optional`로 감싸지지 않는 경우, 해당 메서드는 데이터가 존재할 것으로 가정하고, 그렇지 않으면 `null`을 반환할 수 있음

```java
List<User> users = userRepository.findByName("John");
```