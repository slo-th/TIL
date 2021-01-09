# Spring framework

[인프런 스프링 입문 - 코드로 배우는 스프링 부트, 웹 MVC, DB 접근 기술](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8/)

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

1. 테스트할 클래스명 끝에 "Test"를 붙여 클래스 생성
2. 테스트할 메소드를 `@Test` 어노테이션을 붙여 작성
3. given, when, then 으로 나누어 구현

- `@AfterEach`: 각각의 테스트 메소드가 종료될 때마다 이 메소드를 실행
- `@BeforeEach`: 테스트 메소드가 실행되기 전에 실행
- `assertThat(want).isEqualTo(got)` 방식으로 체크
- `assertThrows()` : 예외 체크

### 통합 테스트 케이스

- `@SpringBootTest`: 스프링 컨테이너와 함께 테스트
- `@Transactional`: 각 테스트가 끝난 후 변경사항을 롤백

## 스프링 빈과 의존관계

> 객체 의존관계를 외부에서 넣어주는 걸 DI(Dependency Injection) 의존성 주입이라 한다.

### 컴포넌트 스캔과 자동 의존관계

- `@Component` : 스프링 빈으로 자동 등록
  - `@Controller`, `@Service`, `@Repository`는 `@Component`를 포함하고 있음.
- `@AutoWired` : 해당 스프링 빈을 컨테이너에서 찾아서 넣어준다.

### 자바 코드로 직접 스프링 빈 등록하기

1. SpringConfig 클래스를 만들고 `@Configuration`을 붙인다.
2. 스프링 빈으로 등록할 객체를 반환하는 public 메소드를 `@Bean`과 함께 생성한다.

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
