# Spring framework

## 시작하기

1. [스트링 부트 스타터](https://start.spring.io/) 사이트에서 프로젝트 생성
    - Project: Gradle Project
    - Language: Java
    - Spring Boot: 2.4.1
    - Group: hello
    - Artifact: hello-spring
    - Packaging: Jar
    - Java 11
    - Depenedency 추가
        - Spring Web
        - Thymeleaf
2. 프로젝트 열기 - build.gradle 선택

## 라이브러리

Gradle은 의존 관계가 있는 라이브러리를 함께 다운한다.

### 스프링 부트 라이브러리

- spring-boot-start-web
  - spring-boot-starter-tomcat : 톰캣 웹서버
  - spring-webmvc: 스프링 웹 MVC
- spring-boot-start-thymeleaf: 타임리프 템플릿 엔진(View)
- spring-boot-starter: 공통- 스프링부트 + 스프링 코어 + 로깅
  - spring-boot
    - spring-core
  - spring-boot-start-logging : 로깅
    - logback
    - slf4j

### 테스트 라이브러리

- spring-boot-start-test
  - junit: 테스트 프레임워크
  - assertj: 테스트 코드를 좀 더 쉽게 작성하도록 해주는 라이브러리
  - mockito: 목 라이브러리
  - spring-test: 스프링 통합 테스트 라이브러리

## View 설정

### Welcome Page

루트(/)로 접속했을 때 컨트롤러가 없으면 `resources/static/index.html`을 보낸다.

### thymeleaf 템플릿

`<html>` 태그에 `xmlns:th="http://www.thymeleaf.org"` 속성 추가

```html
<p th:text="'안녕하세요. ' + ${data}">안녕하세요. empty</p>
```

`안녕하세요. empty` 부분은 없어도 된다.

### 정적 컨텐츠

1. /hello-static.html 로 요청을 받음
2. hello-static 컨트롤러가 없으면
3. resouces:static/hello-static.html을 응답한다.

## Controller

1. 컨트롤러 클래스 생성
2. `@Controller` 어노테이션 붙이기
3. 컨트롤 메소드 작성
    - get: `@GetMapping()`
    - post: `@PostMapping()`
    - api응답: `@ResponseBody` - viewResolver를 사용하지 않음
    - 형식인수
      - model: `org.springframework.ui.Model`, Model.addAttribute() 메소드로 속성 추가
      - request parameter: `@RequestParam(name)`
    - return 값으로 html파일의 이름을 반환한다. ex) `return "hello"`

### 템플릿 엔진 동작

요청을 받으면 컨트롤러를 찾은 뒤에, 리턴 값을 이름으로 하는 html 파일을 `viewResolver`가 처리한다.

Spring boot 템플릿 엔진 기본 viewName 매핑
> resources:templates/ + {ViewName} + .html

## 빌드하고 실행하기

```zsh
./gradlew build
cd build/libs/
java -jar hello-spring-0.0.1-SNAPSHOT.jar
```

## 테스트 케이스 작성

> `Ctrl + Shift + T` 단축키로 테스트 코드로 이동하거나 생성 가능  
> test 코드는 배포되지 않음

1. 테스트할 클래스명 끝에 "Test"를 붙여 클래스 생성
2. 테스트할 메소드를 `@Test` 어노테이션을 붙여 작성
3. given, when, then 으로 나누어 구현
4. 필요한 경우 `@DisplayName()`으로 표시될 이름을 정할 수 있다.

- `@AfterEach`: 각각의 테스트 메소드가 종료될 때마다 이 메소드를 실행
- `@BeforeEach`: 테스트 메소드가 실행되기 전에 실행
- `org.assertj.core.api.Assertions`
  - `.assertThat(actual).isEqualTo(expected)` : equals()와 같음
  - `.assertThat(actual).isSameAs(expected)` : == 연산자와 같음
  - `.assertThat(actual).isInstanceOf(expected)` : instanceof 연산자와 같음
- `org.junit.jupiter.api.Assertions.assertThrows(Class, executable)` : Exception 체크

### 통합 테스트 케이스

- `@SpringBootTest`: 스프링 컨테이너와 함께 테스트
- `@Transactional`: 각 테스트가 끝난 후 변경사항을 롤백

## 스프링 빈과 의존관계

> 객체 의존관계를 외부에서 넣어주는 걸 DI(Dependency Injection) 의존성 주입이라 한다.

### 컴포넌트 스캔과 자동 의존관계

- `@Component` : 스프링 빈으로 자동 등록
  - `@Controller`, `@Service`, `@Repository`, `@Configuration`는 `@Component`를 포함하고 있음.
- `@AutoWired` : 해당 스프링 빈을 컨테이너에서 찾아서 넣어준다.
- `@ComponentScan` : `@Component`가 붙어있는 클래스를 스캔하여 스프링 빈으로 등록함.
  - `excludeFilters = @ComponentScan.Filter(type = FilterType.ANNOTATION, classes = Configuration.class)` : `@Configuration` 어노테이션이 붙은 클래스를 제외
    - `FilterType.ANNOTATION` : default. 애노테이션을 인식
    - `FilterType.ASSIGNABLE_TYPE` : 타입. 자식 포함
    - `FilterType.ASPECTJ` : AspectJ 패턴
    - `FilterType.REGEX` : 정규표현식
    - `FilterType.CUSTOM` : 인터페이스를 구현해서 처리
  - `basePackages` : 탐색할 패키지의 시작 위치를 지정. default는 `@ComponentScan`이 붙은 클래스의 패키지 위치. 권장은 프로젝트 루트에 Config Class를 위치시키기.
  - 스프링 부트의 `@SpringBootApplication` 안에 `@ComponentScan`이 있다.

#### 어노테이션 만들기

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface MyIncludeComponent {
}
```

#### 같은 빈 이름 충돌

자동 빈 등록 vs 자동 빈 등록  
`ConflictingBeanDefinitionException`예외 발생

수동 빈 등록 vs 자동 빈 등록  
수동 빈이 자동 빈을 오버라이드함.

스프링 부트에서는 수동 빈과 자동 빈이 충돌하면 오류를 발생시킨다.

### 자바 코드로 직접 스프링 빈 등록하기

1. SpringConfig 클래스를 만들고 `@Configuration`을 붙인다.
2. 스프링 빈으로 등록할 객체를 반환하는 public 메소드를 `@Bean`과 함께 생성한다.

> `@Configuration`클래스의 `@Bean`메소드 들은 `CGLIB` 라이브러리를 통해 싱글톤 패턴으로 조작된다.

## 스프링 빈 조회

`AnnotationConfigApplicationContext`: 자바 코드로 만든 ac(ApplicationContext)  
`GenericXmlApplicationContext` : xml파일로 만든 ac

`ac.getBean()` 메소드로 Bean을 얻을 수 있음  
> 부모 타입으로 조회시 자식을 모두 가져옴.  
>> 자식이 둘 이상 있으면 중복 오류가 발생함.
>> 빈 이름을 지정해서 피할 수 있음.

`ac.getBeansOfType()` 메소드로 class에 해당하는 Bean의 Map을 가져올 수 있음.  
`ac.getBeanDefinitionNames()` 메소드로 정의된 이름의 배열을 가져올 수 있음.
> `beanDefinition.getRole()` 메소드로 사용자 정의 Bean(`BeanDefinition.ROLE_APPLICATION`)과 비교 가능

## 의존관계 주입

1. 생성자 주입
2. 수정자(setter) 주입
3. 필드 주입
4. 일반 메서드 주입

### 생성자 주입

생성자에 `@Autowired` 붙여서 사용  
생성자 호출 시점에 딱 1번만 호출됨. **불변, 필수**  
생성자가 한 개일 경우 `@Autowired`생략 가능

### 수정자 주입

setter에 `@Autowired` 붙여서 사용  
변경 가능성이 있을 때 사용

### 필드 주입

쓰지 말자... 테스트 코드에서나 쓰자.

`@Autowired`의 기본 동작은 주입할 대상이 없으면 오류가 발생함.

1. `required = false` 사용
2. 형식 인수에 `@Nullable` 붙이기
3. 형식 인수 `Optional<>`로 감싸기

## 스프링 DB 접근 기술

### H2 DB 설치

1. [링크](https://www.h2database.com/) 다운받아서 압축을 푼다.
2. `h2/bin/`에서 `chmod 755 h2.sh` 권한을 주고 `./h2.sh`로 실행한다.
3. DB파일 생성 방법
    1. `jdbc:h2:~/test` 최초 실행 시
    2. `~/test.mv.db` 파일 생성 확인
    3. `jdbc:h2:tcp://localhost/~/test` 로 접속.

### 순수 JDBC

`build.gradle` 파일에 관련 라이브러리 추가

```gradle
implementation 'org.springframework.boot:spring-boot-starter-jdbc'
runtimeOnly 'com.h2database:h2'
```

스프링 부트 DB 연결 설정 추가  
`resource/application.properties`

```properties
spring.datasource.url=jdbc:h2:tcp://localhost/~/test
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
```

> Connection 객체는 `DataSourceUtils.getConnection(DataSource)` 메소드로 생성한다.
>> DataSource는 `SpringConfig`의 필드로 생성자를 호출할 때 생성되고 Repository 객체가 생성될 때 주입된다.

## 스프링 JDBC Template

- `Configuration`에서 `DataSource`를 생성시에 주입받고, `Repository` 생성시에 주입한다.
- `Repository`는 필드로 `JdbcTemplate`를 가진다.
  - 생성자에서 `DataSource`를 주입받아 `JdbcTemplate` 생성시 주입한다.

### insert

- `SimpleJdbcInsert` 객체를 사용
- 데이터를 `Map<columnName, value>`로 래핑
- `jdbcInsert.excuteAndReturnKey(new MapSqlParameterSource(parameters))`의 반환값을 `Number`로 저장하여 사용

### select

- `jdbcTemplate.query(sql, RowMapper, args...)`로 실행. `List<Member>`로 받는다.
- `RowMapper`는 `ResultSet rs, int rowNum`을 형식인수로 갖고 `Member`를 반환하는 함수다.

```java
private RowMapper<Member> memberRowMapper() {
        return new RowMapper<Member>() {
            @Override
            public Member mapRow(ResultSet rs, int rowNum) throws SQLException {
                Member member = new Member();
                member.setId((rs.getLong("id")));
                member.setName(rs.getString("name"));
                return member;
            }
        };
    }
```

람다식으로 바꿀 수도 있다.

```java
private RowMapper<Member> memberRowMapper() {
        return (rs, rowNum) -> {
            Member member = new Member();
            member.setId((rs.getLong("id")));
            member.setName(rs.getString("name"));
            return member;
        };
    }
```

## JPA(Java Persistence API)

JPA는 Interface라서 구현체로 Hibernate를 사용한다.

- `build.gradle`에 관련 라이브러리를 추가한다.
  - `implementation 'org.springframework.boot:spring-boot-starter-data-jpa'`
- `application.properties`에 설정을 추가한다.
  - `spring.jpa.show-sql=true` : JPA가 생성하는 SQL을 출력한다.
  - `spring.jpa.hibernate.ddl-auto=none` : 테이블을 자동 생성하지 않는다.
- `Configuration`에 JPA를 사용하도록 코드를 작성한다.
  - `DataSource`와 `EntityManager`를 필드로 갖고, 주입받는다.
- row에 해당하는 클래스에 `@Entity`를 붙인다.
- PK에는 `@Id`, 생성되는 값에는 `@GeneratedValue`를 붙인다... 아마?
- `Service`에는 `@Transactional`를 붙인다. JPA를 통한 모든 데이터 변경은 트랜잭션 안에서 실행해야 한다. 오류 발생 시 롤백하고, 정상 종료시 커밋한다.
- `Repository`는 `EntityManager em`를 필드로 갖고 있으며 생성시에 주입받는다.

### insert

`em.persist(Entity)`를 사용한다.

### select

`em.createQuery(sql, Entity)`를 사용한다.  
`sql = "select m from Member m where m.name = :name"`  
`.getReslutList()`: 결과를 리스트로 반환  
`.setParameter(name, value)`: 값 설정

## Spring Data JPA

- `JpaRepository`와 `MemberRepository`(사용자 구현)를 상속하는 interface를 만든다...
- `findByName()` 같은 메소드 이름으로 찾는 값을 정할 수 있다.
- `Configuration` 변경
  - `MemberRepository`를 필드로 갖고 생성시에 주입받는다.

## AOP (Aspect Oriented Programming)

- 핵심 관심 사항과 공통 관심 사항을 분리
  - 서비스 로직의 소요 시간을 측정하는 것 등이 공통 관심 사항이다.

```java
@Component
@Aspect
public class TimeTraceAop {

    @Around("execution(* hello.hellospring..*(..))")
    public Object execute(ProceedingJoinPoint joinPoint) throws Throwable {
        long start = System.currentTimeMillis();

        System.out.println("START: " + joinPoint.toString());

        try {
            return joinPoint.proceed();
        } finally {
            long finish = System.currentTimeMillis();
            long timeMs = finish - start;

            System.out.println("END: " + joinPoint.toString() + " " + timeMs + "ms");

        }
    }
}
```
