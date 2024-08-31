---
categories:
- 👩‍💻 Today I learn
- 📡 RESTful API
  
tags:
- Jackson
---

## ✨ **Jackson 라이브러리**

---

![image.png](/assets/img/TIL/JACKSON.png)

Java 객체를 JSON으로 직렬화(serialize)하거나 JSON을 Java 객체로 역직렬화(deserialize)하는 가장 널리 사용되는 라이브러리

### ✅ JSON 변환이 자동으로 이루어지기 위한 조건

---

- `spring-boot-starter-web` 의존성 추가하기
    - 웹 애플리케이션 개발을 위한 기본적인 설정과 의존성을 제공
    - 기본적으로 Jackson 라이브러리가 포함되어 있어, 별도의 설정 없이도 JSON 처리를 사용할 수 있음
- `@RestController` 어노테이션 적용하기
    - `@RestController`가 적용된 클래스의 메서드는 반환된 Java 객체를 JSON 형식으로 직렬화하여 HTTP 응답 본문에 포함 → json 자동 변환