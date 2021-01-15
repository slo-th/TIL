# Spring framework

## 1. 목차

- [1. 목차](#1-목차)
- [2. 시작하기](#2-시작하기)
- [3. 빌드하고 실행하기](#3-빌드하고-실행하기)
- [4. 라이브러리](#4-라이브러리)
  - [4.1. 스프링 부트 라이브러리](#41-스프링-부트-라이브러리)
  - [4.2. 테스트 라이브러리](#42-테스트-라이브러리)
- [5. 테스트 케이스 작성](#5-테스트-케이스-작성)
  - [5.1. 통합 테스트 케이스](#51-통합-테스트-케이스)
- [6. 스프링 Bean과 의존관계](#6-스프링-bean과-의존관계)
  - [6.1. 컴포넌트 스캔과 자동 의존관계](#61-컴포넌트-스캔과-자동-의존관계)
  - [6.2. 자바 코드로 직접 스프링 Bean 등록하기](#62-자바-코드로-직접-스프링-bean-등록하기)
- [7. 의존관계 주입 @Autowired](#7-의존관계-주입-autowired)
  - [7.1. 생성자 주입](#71-생성자-주입)
  - [7.2. 수정자 주입](#72-수정자-주입)
  - [7.3. 필드 주입](#73-필드-주입)
  - [7.4. 메서드 주입](#74-메서드-주입)
- [8. @Autowired의 동작](#8-autowired의-동작)
  - [8.1. Bean의 중복](#81-bean의-중복)
  - [8.2. 조회한 모든 Bean이 필요할 때](#82-조회한-모든-bean이-필요할-때)
  - [8.3. Bean이 없음](#83-bean이-없음)
- [9. 스프링 Bean 조회](#9-스프링-bean-조회)
  - [9.1. ApplicationContext](#91-applicationcontext)
  - [9.2. beanDefinition](#92-beandefinition)
- [10. Bean 생명주기Lifecycle 콜백callback](#10-bean-생명주기lifecycle-콜백callback)
  - [10.1. 스프링 Bean의 Lifecycle](#101-스프링-bean의-lifecycle)
  - [10.2. Lifecycle callback](#102-lifecycle-callback)
    - [10.2.1. InitalizingBean, DisposableBean 인터페이스](#1021-initalizingbean-disposablebean-인터페이스)
    - [10.2.2. @Bean 설정에 메서드 지정](#1022-bean-설정에-메서드-지정)
    - [10.2.3. 애노테이션 @PostConstruct, @PreDestroy 사용](#1023-애노테이션-postconstruct-predestroy-사용)
- [11. Bean Scope](#11-bean-scope)
- [12. Web Scope](#12-web-scope)
  - [12.1. 환경 추가](#121-환경-추가)
  - [12.2. 포트 변경](#122-포트-변경)
  - [12.3. request](#123-request)
    - [12.3.1. 오류](#1231-오류)
    - [12.3.2. 해결방법](#1232-해결방법)
- [13. 롬복Lombok 라이브러리](#13-롬복lombok-라이브러리)
  - [13.1. 설정](#131-설정)
  - [13.2. 사용하기](#132-사용하기)
- [14. AOP (Aspect Oriented Programming)](#14-aop-aspect-oriented-programming)
- [15. View](#15-view)
  - [15.1. Welcome Page](#151-welcome-page)
  - [15.2. thymeleaf 템플릿](#152-thymeleaf-템플릿)
  - [15.3. 정적 컨텐츠](#153-정적-컨텐츠)
- [16. Controller](#16-controller)
  - [16.1. 템플릿 엔진 동작](#161-템플릿-엔진-동작)
- [17. 스프링 DB 접근 기술](#17-스프링-db-접근-기술)
  - [17.1. H2 DB 설치](#171-h2-db-설치)
  - [17.2. 순수 JDBC](#172-순수-jdbc)
- [18. 스프링 JDBC Template](#18-스프링-jdbc-template)
  - [18.1. insert](#181-insert)
  - [18.2. select](#182-select)
- [19. JPA(Java Persistence API)](#19-jpajava-persistence-api)
  - [19.1. insert](#191-insert)
  - [19.2. select](#192-select)
- [20. Spring Data JPA](#20-spring-data-jpa)

## 2. 시작하기

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

## 3. 빌드하고 실행하기

```zsh
./gradlew build
cd build/libs/
java -jar hello-spring-0.0.1-SNAPSHOT.jar
```

## 4. 라이브러리

Gradle은 의존 관계가 있는 라이브러리를 함께 다운한다.

### 4.1. 스프링 부트 라이브러리

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

### 4.2. 테스트 라이브러리

- spring-boot-start-test
  - junit: 테스트 프레임워크
  - assertj: 테스트 코드를 좀 더 쉽게 작성하도록 해주는 라이브러리
  - mockito: 목 라이브러리
  - spring-test: 스프링 통합 테스트 라이브러리

## 5. 테스트 케이스 작성

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

### 5.1. 통합 테스트 케이스

- `@SpringBootTest`: 스프링 컨테이너와 함께 테스트
- `@Transactional`: 각 테스트가 끝난 후 변경사항을 롤백(DB)

## 6. 스프링 Bean과 의존관계

객체 의존관계를 외부에서 넣어주는 걸 DI(Dependency Injection) 의존관계 주입이라 한다.  
스프링 Bean으로 등록된 객체는 기본적으로 싱글톤 패턴으로 관리된다.

### 6.1. 컴포넌트 스캔과 자동 의존관계

- `@Component` : 스프링 Bean으로 등록
  - `@Controller`, `@Service`, `@Repository`, `@Configuration`는 `@Component`를 포함
- `@ComponentScan` : `@Component`가 붙어있는 클래스를 스캔하여 스프링 Bean으로 등록
  - `@SpringBootApplication`는 `@ComponentScan`를 포함
  - `basePackages` : 탐색할 패키지의 시작 위치
    - default: `@ComponentScan`이 붙은 클래스의 패키지 위치
    - recommend: 프로젝트 루트에 Config Class를 위치
  - `excludeFilters` : 제외할 대상
    - `FilterType`
      - `FilterType.ANNOTATION` : default. 애노테이션을 인식
      - `FilterType.ASSIGNABLE_TYPE` : 타입. 자식 포함
      - `FilterType.ASPECTJ` : AspectJ 패턴
      - `FilterType.REGEX` : 정규표현식
      - `FilterType.CUSTOM` : 인터페이스를 구현해서 처리

#### 어노테이션 만들기 <!-- omit in toc -->

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface MyIncludeComponent {
}
```

### 6.2. 자바 코드로 직접 스프링 Bean 등록하기

1. 클래스를 만들고 `@Configuration`을 붙임
2. 스프링 Bean으로 등록할 객체를 반환하는 public 메소드를 만들고 `@Bean`를 붙임

## 7. 의존관계 주입 @Autowired

### 7.1. 생성자 주입

생성자에 `@Autowired` 붙여서 사용  
생성자 호출 시점에 딱 1번만 호출됨. **불변, 필수**  
생성자가 한 개일 경우 `@Autowired`생략 가능

### 7.2. 수정자 주입

setter에 `@Autowired` 붙여서 사용  
변경 가능성이 있을 때 사용

### 7.3. 필드 주입

쓰지 말자... 테스트 코드에서나 쓰자.

### 7.4. 메서드 주입

메서드에 `@Autowired` 붙임

## 8. @Autowired의 동작

### 8.1. Bean의 중복

- 자동 Bean 등록 vs 자동 Bean 등록  
  - `ConflictingBeanDefinitionException`예외 발생
- 수동 Bean 등록 vs 자동 Bean 등록  
  - 수동 Bean이 자동 Bean을 오버라이드함.
- 스프링 부트에서는 수동 Bean과 자동 Bean이 충돌하면 오류를 발생시킨다.

해결 방법

- `@Autowired`는 먼저 타입을 조회하고
  - 중복: 필드 또는 형식인수 이름으로 조회 (권장하지 않음)
- `@Qualifier`구분자 사용 -> `@Qualifier`끼리 매칭 -> 이름 조회
- `@Primary` 사용

> `@Qualifier`가 `@Primary`보다 우선순위가 높다.

### 8.2. 조회한 모든 Bean이 필요할 때

| Type                | 설명                                                             |
| ------------------- | ---------------------------------------------------------------- |
| `Map<String, Type>` | Type으로 조회한 Bean의 이름을 Key로 갖고, Bean을 value로 갖는다. |
| `List<Type>`        | 조회한 모든 Bean을 리스트로 갖는다.                            |

> 해당하는 Bean이 없으면 Bean 컬렉션을 주입한다.

### 8.3. Bean이 없음

`@Autowired`의 기본 동작은 주입할 대상이 없으면 `NoSuchBeanDefinitionException`예외 발생

1. `@Autowired(required = false)` 사용
2. 형식 인수에 `@Nullable` 붙이기
3. 형식 인수 `Optional<>`로 감싸기

## 9. 스프링 Bean 조회

- `AnnotationConfigApplicationContext`: 자바 코드로 만든 ac(ApplicationContext)
- `GenericXmlApplicationContext` : xml파일로 만든 ac

### 9.1. ApplicationContext

- `getBean()` 메소드로 Bean을 얻을 수 있음  
  - 부모 타입으로 조회시 자식을 모두 가져옴.  
  - 자식이 둘 이상 있으면 `NoUniqueBeanDefinitionException` 예외 발생
    - Bean 이름을 지정해서 피할 수 있음.
- `getBeansOfType()` : Type에 해당하는 Bean의 Map을 가져올 수 있음.  
- `getBeanDefinitionNames()` : 정의된 이름의 배열을 가져올 수 있음.

### 9.2. beanDefinition

- `beanDefinition.getRole()` : 사용자 정의 Bean(`BeanDefinition.ROLE_APPLICATION`)과 비교 가능

## 10. Bean 생명주기Lifecycle 콜백callback

### 10.1. 스프링 Bean의 Lifecycle

스프링 컨테이너 생성 -> 스프링 빈 생성 -> 의존관계 주입 -> 초기화 콜백 -> 사용 -> 소멸전 콜백 -> 스프링 종료

### 10.2. Lifecycle callback

#### 10.2.1. InitalizingBean, DisposableBean 인터페이스

1. `InitalizingBean`, `DisposableBean` 를 구현
2. `afterPropertiesSet()` 메서드에 초기화 구문 작성
3. `destroy()` 메서드에 소멸 구문 작성

> 거의 사용하지 않음

#### 10.2.2. @Bean 설정에 메서드 지정

1. `@Bean(initMethod = "", destroyMethod = "")` 따옴표 사이에 메서드 이름 작성

> 외부 라이브러리에 사용

#### 10.2.3. 애노테이션 @PostConstruct, @PreDestroy 사용

1. 초기화 메서드에 `@PostConstruct`, 소멸 메서드에 `@PreDestroy` 애노테이션 붙이기

> 스프링에서 권장하는 방식
> 자바 표준 기술
> 컴포넌트 스캔과 잘 어울림

## 11. Bean Scope

빈이 존재하는 범위

- 싱글톤: default, 스프링 컨테이너의 시작과 종료까지
- 프로토타입: 빈의 생성과 의존관계 주입까지
- 웹
  - request : 웹 요청이 들어오고 나갈 때 까지
  - session : 세션의 생성과 종료까지
  - application : 웹의 서블릿 컨텍스트와 같은 범위
  - websocket : 웹 소켓과 같은 범위

## 12. Web Scope

### 12.1. 환경 추가

```groovy
// build.gradle
dependencies {
  implementation 'org.springframework.boot:spring-boot-starter-web'
}
```

### 12.2. 포트 변경

```properties
# application.properties
server.port=9090
```

### 12.3. request

`@Scope(value = "request")` 사용

#### 12.3.1. 오류

`@Autowired` 사용 시 생성되지 않은 Bean을 주입 할 수 없어서(request가 들어올 때 생성되기 때문) 오류가 발생함.

#### 12.3.2. 해결방법

1. `Provider` 사용하기
   1. 필드를 `ObjectProvider<>`로 감싼다.
   2. 사용 할 로직에서 `Provider.getObject()`를 호출해서 사용한다. (지연 생성)
2. 프록시 사용하기
   1. `@Scope`의 속성으로 `proxyMode = ScopedProxyMode.TARGET_CLASS`를 추가한다.

## 13. 롬복Lombok 라이브러리

### 13.1. 설정

`build.gradle`에 라이브러리와 환경 추가

```groovy
configurations {
  compileOnly {
    extendsFrom annotationProcessor
  }
}

dependencies {
  compileOnly 'org.projectlombok:lombok'
  annotationProcessor 'org.projectlombok:lombok'
  testCompileOnly 'org.projectlombok:lombok'
  testAnnotationProcessor 'org.projectlombok:lombok'
}
```

1. Settings(Ctrl + Alt + S) -> plugin -> lombok 플러그인 설치
2. Settings -> Annotation Processors 검색 -> Enable annotation processing 체크

### 13.2. 사용하기

|         Annotation         | 설명                                         |
| :------------------------: | -------------------------------------------- |
| `@RequiredArgsConstructor` | `final` 필드를 형식인수로 가지는 생성자 생성 |
|         `@Getter`          | `Getter` 생성                                |
|         `@Setter`          | `Setter` 생성                                |

> 생성자가 하나일 때 `@Autowired` 생략 가능  
> `@RequiredArgsConstructor`로 하나만 생성해서 쓸 수 있음.

## 14. AOP (Aspect Oriented Programming)

- 핵심 관심 사항과 공통 관심 사항을 분리
  - 서비스 로직의 소요 시간을 측정하는 것 등이 공통 관심 사항이다.

```java
@Component
@Aspect
public class TimeTraceAop {

    // 소요 시간을 출력하는 로직
    @Around("execution(* hello.hellospring..*(..))") // 적용할 범위
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

## 15. View

### 15.1. Welcome Page

루트(/)로 접속했을 때 컨트롤러가 없으면 `resources/static/index.html`을 보낸다.

### 15.2. thymeleaf 템플릿

`<html>` 태그에 `xmlns:th="http://www.thymeleaf.org"` 속성 추가

```html
<p th:text="'안녕하세요. ' + ${data}">안녕하세요. empty</p>
```

`안녕하세요. empty` 부분은 없어도 된다.

### 15.3. 정적 컨텐츠

1. /hello-static.html 로 요청을 받음
2. hello-static 컨트롤러가 없으면
3. resouces:static/hello-static.html을 응답한다.

## 16. Controller

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

### 16.1. 템플릿 엔진 동작

요청을 받으면 컨트롤러를 찾은 뒤에, 리턴 값을 이름으로 하는 html 파일을 `viewResolver`가 처리한다.

Spring boot 템플릿 엔진 기본 viewName 매핑
> resources:templates/ + {ViewName} + .html

## 17. 스프링 DB 접근 기술

### 17.1. H2 DB 설치

1. [링크](https://www.h2database.com/) 다운받아서 압축을 푼다.
2. `h2/bin/`에서 `chmod 755 h2.sh` 권한을 주고 `./h2.sh`로 실행한다.
3. DB파일 생성 방법
    1. `jdbc:h2:~/test` 최초 실행 시
    2. `~/test.mv.db` 파일 생성 확인
    3. `jdbc:h2:tcp://localhost/~/test` 로 접속.

### 17.2. 순수 JDBC

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

## 18. 스프링 JDBC Template

- `Configuration`에서 `DataSource`를 생성시에 주입받고, `Repository` 생성시에 주입한다.
- `Repository`는 필드로 `JdbcTemplate`를 가진다.
  - 생성자에서 `DataSource`를 주입받아 `JdbcTemplate` 생성시 주입한다.

### 18.1. insert

- `SimpleJdbcInsert` 객체를 사용
- 데이터를 `Map<columnName, value>`로 래핑
- `jdbcInsert.excuteAndReturnKey(new MapSqlParameterSource(parameters))`의 반환값을 `Number`로 저장하여 사용

### 18.2. select

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

## 19. JPA(Java Persistence API)

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

### 19.1. insert

`em.persist(Entity)`를 사용한다.

### 19.2. select

`em.createQuery(sql, Entity)`를 사용한다.  
`sql = "select m from Member m where m.name = :name"`  
`.getReslutList()`: 결과를 리스트로 반환  
`.setParameter(name, value)`: 값 설정

## 20. Spring Data JPA

- `JpaRepository`와 `MemberRepository`(사용자 구현)를 상속하는 interface를 만든다...
- `findByName()` 같은 메소드 이름으로 찾는 값을 정할 수 있다.
- `Configuration` 변경
  - `MemberRepository`를 필드로 갖고 생성시에 주입받는다.
