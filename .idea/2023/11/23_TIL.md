# Learn From Project 

---

### Lombok 생성자 Builder 패턴. 
생성자 메서드로 @Builder를 사용한다. 
<br /> 결과적으로 생성자 레벨에서 생성자의 파라미터 필드에 대해서만 빌더 메서드를 생성한다. 
```java 
public class TestBuild {
    @Builder
    public TestBuild(String username, int age) {
        this.username = "My name is " + username;
        this.age = age + 1;
    }
}
```

### Swagger UI




