# Rest API 간단 예제 | Spring

Spring Boot CLI를 사용해서 아래와 같이 프로젝트를 생성한다.

```
$ spring init --build=maven --java-version=1.8 --dependencies=web spring-example
```

DTO(Data Transfer Object) 객체인 User 클래스를 정의한다.

```java
public class User {
  private String email;
  private String firstName;
  private String lastName;

  public User(String email, String firstName, String lastName) {
    this.email = email;
    this.firstName = firstName;
    this.lastName = lastName;
  }

  public String getEmail() {
    return email;
  }

  public void setEmail(String email) {
    this.email = email;
  }

  public String getFirstName() {
    return firstName;
  }

  public void setFirstName(String firstName) {
    this.firstName = firstName;
  }

  public String getLastName() {
    return lastName;
  }

  public void setLastName(String lastName) {
    this.lastName = lastName;
  }
}
```

비지니스 로직을 분리하기 위해 UserService를 정의한다. 필요하다면 DB를 연결하고 DAO(Data Access Object)를 정의해도 되지만 간단한 예제이므로 메모리에 데이터를 저장 후 반환한다.

```java
@Service
public class UserService {
  private List<User> users = new ArrayList<>();

  UserService() {
    users.add(new User("a@example.com", "a", "a"));
    users.add(new User("b@example.com", "b", "b"));
    users.add(new User("c@example.com", "c", "c"));
  }

  public List<User> getUsers() {
    return users;
  }
}
```

UserController를 정의하고 UserService 객체에 의존성을 주입하여 데이터를 반환하는 엔드 포인트를 정의한다. `@RestController`를 사용해도 되지만 회사에서 `@Controller`를 사용하기 때문에 `@ResponseBody`와 함께 사용하여 데이터를 JSON 형태로 내려줬다.

```java
@Controller
public class UserController {

  @Autowired
  UserService userService;

  @ResponseBody
  @RequestMapping(value = "/api/users", method = RequestMethod.GET)
  public List<User> getUsers() {
    return userService.getUsers();
  }
}
```

mvn 명령어로 스프링 부트 프로젝트를 시작하자.

```
$ mvn spring-boot:run
```

[localhost:8080/api/users](http://localhost:8080/api/users)에 접속해서 정상적으로 데이터가 반환되는지 확인한다.

```
[
  { email: "a@example.com", firstName: "a", lastName: "a" },
  { email: "b@example.com", firstName: "b", lastName: "b" },
  { email: "c@example.com", firstName: "c", lastName: "c" }
]
```
