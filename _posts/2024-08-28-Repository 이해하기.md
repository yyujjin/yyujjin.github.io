---
categories:
- 👩‍💻 Today I learn
  
tags:
- JPA
- Repository

### ✨ **Repository**

---

- **Repository**는 데이터베이스와 상호작용하기 위한 인터페이스
- `JpaRepository`, `CrudRepository` 등을 상속받아 사용할 수 있음
- `JpaRepository`는 **기본적인 CRUD 작업을 위한 메서드를 제공**

```java
public interface UserRepository extends JpaRepository<User, Long> {

    // 기본적으로 제공되는 메서드
    //JpaRepository 인터페이스를 상속받으면 이러한 메서드를 직접 구현할 필요는 없음
    //이외에 필요한 메서드에 대해서는 커스텀하면 됨. 
    
    //모든 데이터를 조회
    List<User> findAll();
    
    // 주어진 ID에 해당하는 데이터를 조회, 결과는 Optional<User>로 반환됨
    Optional<User> findById(Long id); //primery key로 찾기
    
    //엔터티를 저장하거나 업데이트
    //만약 엔터티가 이미 존재하면 업데이트하고, 존재하지 않으면 새로 삽입
    User save(User user);
    
    //주어진 ID에 해당하는 데이터를 삭제
    void deleteById(Long id);
}

```

### 📌 **Custom 메서드 추가**

---

- JPA가 기본적으로 제공하는 메서드 이외에, 추가적인 쿼리 메서드를 생성할 수 있음
- 메서드의 이름을 통해 쿼리가 자동으로 생성됨

```java
public interface UserRepository extends JpaRepository<User, Long> {

    List<User> findByName(String name);  // 이름으로 사용자 찾기
    
    List<User> findByEmailContains(String keyword);  // 이메일에 특정 단어가 포함된 사용자 찾기
}

```