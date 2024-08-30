---
categories:
- 📚 Book_rating_project(with.elly)
- 2024-08-22 ~ 2024-08-28
  
tags:
- JPA
- Entity
- Elly
---

```java
@Entity
@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
public class Tag {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    **//id 변수는 기본 키 + 자동 증가**
    private Long id; //id가 원래는 null이었다가 추가되면 id가 만들어지기에 final은 붙이지 않는다.
    private String name;
```

- `@Entity`
    - class 이름을 가진 테이블이 자동으로 생성됨
- `@AllArgsConstructor`
    - 클래스의 모든 필드를 매개변수로 받는 생성자를 자동으로 생성
- `@NoArgsConstructor`
    - 매개변수가 없는 기본 생성자를 자동으로 생성
- `@Id`
    - 기본 키 어노테이션
    - 엔티티는 무조건 기본키가 되는 컬럼을 알려줘야 함
- `@GeneratedValue(strategy = GenerationType.IDENTITY)`
    - 자동 증가 어노테이션
    - id 자동생성 시키는 방식이 여러개가 있는데 일단 보류

### Repository란?

---

- 데이터베이스에 대한 CRUD(생성, 읽기, 업데이트, 삭제) 작업을 처리하는 인터페이스
- `Spring Data JPA`를 사용하면 `Repository` 인터페이스를 정의하고, JPA가 자동으로 구현을 생성하여 **데이터베이스와 상호작용**할 수 있게 해줌
- mybatis + xml 이라고 생각하면 될 것 같다.

![스크린샷 2024-08-27 오전 12.45.33.png](/assets/img/TIL/2024-08-27/스크린샷%202024-08-27%20오전%2012.45.33.png)

### repository 인터페이스 생성하기

---

```java
public interface TagRepository extends JpaRepository**<Tag,Long>** {

}
```

- `<Tag,Long>`
    - 엔티티 이름, 프라이머리 키 타입
- `TagRepository`는 Spring Data JPA가 제공하는 CRUD 및 페이징 메서드를 자동으로 상속받으며, `Tag` 엔티티와 `Long` 타입의 ID를 기반으로 데이터베이스 작업을 수행할 수 있음

### Serviece에서 데이터 가져오기

---

```java
@Service
public class TagService {
    @Autowired
    private TagRepository tagRepository;

    public List<Tag> getTag() {
        return tagRepository.findAll(); //전체 데이터 가지고 오기

    }
}
```

- **`findAll()`**
    - `JpaRepository`의 기본 메서드 중 하나로 데이터베이스에 저장된 모든 엔티티를 리스트 형태로 반환함
    - 이 메서드는 `Entity` 타입의 전체 데이터를 가져옵니다.
    

### Controller 연결하기

---

```java
@RestController
public class TagController {

    @Autowired
    TagService tagService;

    @GetMapping("/tags")
    public List<Tag> getTag() {
        return tagService.getTag();
    }

}
```

- 궁금증 ❓
    
    🤔 `return tagRepository.findAll();` 이거 할 때 왜 id는 반환안해?
    
    🤖 실제로 `tagRepository.findAll()` 호출 시 반환되는 `List<Tag>`에는 각 `Tag` 엔티티 객체가 포함됩니다. 각 `Tag` 객체는 ID 필드를 포함하고 있으므로, 결과적으로 모든 `Tag` 레코드의 ID 값도 포함됩니다. 따라서, `List<Tag>`를 통해 각 `Tag` 객체의 ID를 확인할 수 있습니다.
    


![image.png](/assets/img/github_logo%20복사본.png)

---
[commit](https://github.com/yyujjin/book-rating-backend/commit/047a130e6681a1288300e39aa79917b3cd953dd6)

[commit](https://github.com/yyujjin/book-rating-backend/commit/67628f6d571bc480a08fd853aa37b875a703074b)