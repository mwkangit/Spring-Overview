# Spring Initializr

- ### Spring boot 기반으로 프로젝트를 만들어주는 사이트이다.




- ### Project

  - #### 필요한 라이브러리를 가져오고 build 하는 라이프사이클까지 관리하는 tool이다.

    - #### Gradle, Maven이 있으며 주로 Gradle을 사용한다.



- ### Spring boot

  - #### spring boot 버전을 선택하는 항목이다.

  - #### SNAPSHOT 은 아직 만들고 있는 버전이다.

  - #### M1 은 아직 정식 배포된 것이 아닌 버전이다.



- ### Project Metadata

  - #### Group 에는 보통 기업명, 기업 domain 명을 적는다.

  - #### Artifact 는 빌드되어 나올 때의 결과물 명이다.



- ### Dependencies

  - #### spring boot 에 어떤 라이브러리를 사용할 것인지 결정한다.

  - #### Spring Web은 web을 사용하게 해주는 엔진이다.

  - #### Thymeleaf 은 HTML 을 만들어주는 템플릿 엔진이다.



# Project



## resource



- #### XML, HTML, properties, 설정파일을 관리하는 영역이다.

- 

## gitignore



- #### git과 연관되어 소스파일만 올릴 수 있게 설정하는 영역이다.



## Library



- ### Gradle은 의존관계가 있는 라이브러리를 함께 다운로드 한다.



- ### Spring Boot Library

  - #### spring-boot-starter-web

    - #### spring-boot-starter-tomcat : 톰캣 (웹서버)

    - #### spring-webmvc : 스프링 웹 MVC

  - #### spring-boot-starter-thymeleaf : 타임리프 템플릿 엔진 (View)

  - #### spring-boot-starter (공통) : 스프링 부트 + 스프링 코어 + 로깅

    - #### spring-boot

      - #### spring-core

    - #### spring-boot-starter-logging

      - #### logback (Log 용도), slf4j (Interface 용도)

- ### Test Library

  - #### spring-boot-starter-test

    - #### junit : 테스트 프레임워크 (현재 5 version)

    - #### mockito : 목 라이브러리

    - #### assertj : 테스트 코드를 좀 더 편하게 작성하게 도와주는 라이브러리

    - #### spring-test : 스프링 통합 테스트 지원



# Practice



```html
<!-- resource/static/index.html -->
<!DOCTYPE HTML>
<html>
<head>
    <title>Hello</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" /> </head>
<body>
Hello
<a href="/hello">hello</a>
</body>
</html>
```

- #### Welcome page 기능을 제공받아서 브라우저 화면을 출력할 수 있다.

- #### HTML은 thymeleaf 템플릿 엔진을 이용하여 서버에서 브라우저로 알맞은 형식으로 전달한다.



```java
package hello.hellospring.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class HelloController {

    @GetMapping("hello") // map 어플리케이션에서  /hello라고 들어오면 이 메소드를 호출한다
    public String hello(Model model){
        model.addAttribute("data", "hello!!");
        return "hello";
    }
}

```

- #### @Controller로 이 클래스가 controller 역할을 한다는 것을 선언한다.

- #### @GetMapping은 get post의 형식으로 이 코드에서는 localhost:8080/hello url로 접속하면 controller 에서 get하기 때문에 hello() 메소드를 실행하게 된다.

- #### Spring에서 Model을 선언하여 hello() 메소드에 매개변수로 전달한다.

- #### model 변수에 data라는 key값으로 hello!!라는 value를 정의한 후 template 폴더의 hello라는 이름의 HTML을 전달하고 실행한다.



```html
<!-- resources/templates/hello.html -->
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Hello</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" /> </head>
<body>
<p th:text="'안녕하세요. ' + ${data}" >안녕하세요. 손님</p>
</body>
</html>
```

- #### ty는 thymeleaf를 의미한다.

- #### ${data}는 HelloController 클래스에서 전달받은 model의 key값을 사용했으므로 value인 hello!!로 대체된다.


   ![WebBrowzer Tomcat SpringContainer](https://user-images.githubusercontent.com/79822924/134794634-3d1a1654-5dab-4133-a0d9-380266482a4c.png)


   - #### 웹 브라우저에서 localhost:8080/hello를 서버로 요청하면 서버 내에서 helloController 내부의 메소드가 실행되어 return 값으로 templates/+{ViewName}+.html 파일을 실행할 준비를 마친 후 브라우저에 변환된 HTML 파일을 전송한다.

   

   # Build



   ## Window



   1. #### $gradlew build --> build 생성한다.

   2. #### $gradlew clean --> build했던 폴더 삭제한다.

   3. #### $gradlew clean build --> build 되었던 기록을 삭제하고 다시 build 한다.

   4. #### java -jar (Project Name)-0.0.1-SNAPSHOT.jar --> spring으로 생성된 jar 실행



   ## Linux



   1. #### $./gradlew build --> build 생성한다.

   2. #### $./gradlew clean --> build했던 폴더 삭제한다.

   3. #### $./gradlew clean build --> build 되었던 기록을 삭제하고 다시 build 한다.

   4. #### java -jar (Project Name)-0.0.1-SNAPSHOT.jar --> spring으로 생성된 jar 실행



# Static Contents



- ### Welcome Page와 같이 파일을 web browser에 바로 전송하는 방법이다



![static contents image](https://user-images.githubusercontent.com/79822924/134794671-f280c2a6-06e4-48f0-9037-6dffacf2eeaf.png)

- #### Controller이 우선 순위를 가지므로 Controller에서 hello-static이 있는지 확인한다.

- #### Controller에 hello-static이 없다면 spring boot는 spring 내부에서 hello-static.html을 찾아본다.

- #### HTML을 찾았다면 그대로 web browser에 HTML 형식으로 전달한다.



# MVC, Template Engine



- #### View는 화면을 출력하는 영역에 집중하며 다른 작업은 하지 않는 것이 좋으며 Controller는 business 로직 관련이나 내부적인 상황을 처리하는 것이 집중하는 것이 좋으므로 View와 Controller는 분리하는 것이 좋다.



```java
@Controller
public class HelloController {

    @GetMapping("hello-mvc")
	public String helloMvc(@RequestParam("name") String name, Model model) {
        model.addAttribute("name", name);
        return "hello-template";
    }
}
```

- #### @RequestParam 뒤에는 required 매개변수를 사용할 수 있는데 True이면 client가 무조건 요구되는 인자를 입력해야 한다. (required는 True가 default값이다) (ex : localhost:8080/hello-mvc?name=Spring)



```html
<html xmlns:th="http://www.thymeleaf.org">
    <body>
        <p th:text="'hello ' + ${name}">hello!empty</p>
    </body>
</html>
```

- #### Template engine이 실행되어 값이 HTML로 전송되면 hello!empty가 아닌 'hello ' + ${name}이 브라우저로 전송된다.


![MVC, Template Engine image](https://user-images.githubusercontent.com/79822924/134794673-123fe318-6297-4bc4-be2c-3ec87c48a42e.png)


- #### ViewResovler는 View를 찾아주고 Template에 연결하는 역할을 한다.  즉, 찾은 View를 Thymeleaf가 처리하여 매개변수 값을 변환 후 HTML로 브라우저에 전송한다.



# API



```java
@Controller
public class HelloController {

    @GetMapping("hello-api")
    @ResponseBody
    public Hello helloApi(@RequestParam("name") String name) {
        Hello hello = new Hello();
        hello.setName(name);
        return hello;
    }
    static class Hello {
        private String name;
        
        public String getName() {
            return name;
        }
        
        public void setName(String name) {
            this.name = name;
        }
    }
}
```

- #### API는 JSON을 기본으로 하고 있으며 JSON은 기본적으로 key, value 구조이다.

- #### HTML을 이용하지 않고 직접 HTTP body 영역에 데이터를 전송한다.

- #### 객체 자체를 전송하는 것이 가능하게 되어있다.


![Using ResponseBody image](https://user-images.githubusercontent.com/79822924/134794679-d4fa936e-802f-4ced-9cfb-67c967244b4a.png)

- #### @ResponseBody로 HttpMessageConverter를 viewResolver대신 사용한다.

- #### 기본 문자처리는 StringHttpMessageConverter를 이용한다.

- #### 기본 객체처리는 MappingJackson2HttpMessageConverter를 이용한다

- #### 클라이언트의 HTTP Accept 헤더오 서버의 Controller 반환 타입 정보를 조합하여 HttpMessageConverter이 선택된다.



# Practice



- ### 회원 관리 예제

  1. #### 데이터 : 회원 ID, 이름

  2. #### 기능 : 회원 등록, 조회

  3. #### 아직 데이터 저장소가 선정되지 않은 가사 시나리오

  4. #### 중복된 이름은 회원 등록 불가



# Component Scan & DI



- ### Controller가 Service를 통해 데이터에 접근 할 때 의존관계에 있다고 할 수 있다.  이러한 과정에서 Spring Container에서 Spring Bean이 관리된다고 표현한다.




```java
package hello.hellospring.controller;
import hello.hellospring.service.MemberService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;

@Controller
public class MemberController {
    private final MemberService memberService;
    
    @Autowired
    public MemberController(MemberService memberService) {
        this.memberService = memberService;
    }
}
```

- #### Spring Container은 spring 실행 시 생성되며 controller을 작동시키고 controller은 생성자를 실행시킨다.

- #### @Autowired를 통해 DI를 구현한다.  Spring bean에 등록된 MemberService를 자동으로 연결하여 가져온다.

- #### @Component 어노테이션이 존재해야 spring bean에 자동 등록된다.

- #### @Controller, @Service, @Repository는 @Component를 포함하여 spring bean에 자동 등록된다.

- #### 생성자에 @Autowired를 사용하면 객체 생성 시점에 spring container에서 해당 spring bean을 찾아서 주입한다.  생성자가 1개만 있으면 @Autowired는 생략 가능하다.

- #### Spring은 spring container에 spring bean을 등록할 때, 기본으로 싱글톤으로 등록한다.  싱글톤이란 모두 같은 인스턴스 하나만 사용하도록 객체 1개만 등록한다는 뜻이다.

- #### Spring 프로젝트 패키지 중 기본 패키지에 @Component가 있어야 Spring이 빌드 시 container에 bean으로 넣어준다.

- #### Controller를 통해 외부 요청을 받고 Service에서 비즈니스 로직을 만들고 Repository에서 데이터를 저장한다.



# Registering Spring Bean with Java Code



```java
package hello.hellospring;
import hello.hellospring.repository.MemberRepository;
import hello.hellospring.repository.MemoryMemberRepository;
import hello.hellospring.service.MemberService;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class SpringConfig {
    
    @Bean
    public MemberService memberService() {
        return new MemberService(memberRepository());
    }

    @Bean
    public MemberRepository memberRepository() {
        return new MemoryMemberRepository();
    }
}
```

- #### @Configuration, @Bean을 사용하여 직접 자바 코드로 bean에 넣어준다.

- #### Controller, Service, Repository는 어노테이션을 설정 후@Autowired로 자바 코드로 넣은 bean을 전달받을 수 있다. 

- #### DI에는 필드 주입, setter 주입, 생성자 주입이 있다.  세 방법 중 

  - #### 필드 주입 : 직접 객체 생성하는 부분에 어노테이션을 선언하는 것이다.

  - #### setter 주입 : setter을 통해 객체를 주입하는 것이다.

  - #### 생성자 주입 : 일반적인 방법으로 생성자를 통해 주입한다.

- #### 실무에서 일반적으로 컴포넌트 스캔을 이용하지만 구현 클래스를 변경해야 하는 상황이라면 설정을 통해 spring bean으로 등록한다. (ex : 아직 database를 만들지 않않은 상태로 프로그래밍 했지만 database가 완성되어 프로그램에 삽입해야하는 경우)



# Member Registration



```html
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
    <body>
        <div class="container">
            <form action="/members/new" method="post">
                <div class="form-group">
                    <label for="name">이름</label>
                    <input type="text" id="name" name="name" placeholder="이름을
입력하세요">
                </div>
                <button type="submit">등록</button>
            </form>
        </div> <!-- /container -->
    </body>
</html>
```

- #### form 내부는 /member/new 주소에 post방식으로 넘어온다는 뜻이다.

- #### input은 값을 입력할 수 있는 HTML 태그이다.

- #### name = "name"이므로 @PostMapping에 선언된 name 변수에 입력 값이 넣어진다.



```java
@Controller
public class MemberController {
    private final MemberService memberService;

    @Autowired
    public MemberController(MemberService memberService) {
        this.memberService = memberService;
    }

    @GetMapping(value = "/members/new")
    public String createForm() {
        return "members/createMemberForm";
    }
    
        @PostMapping(value = "/members/new")
    public String create(MemberForm form) {
        Member member = new Member();
        member.setName(form.getName());
        memberService.join(member);
        return "redirect:/";
    }
}
```

```java
package hello.hellospring.controller;

public class MemberForm {
    private String name;

    public String getName() {
        return name;
    }    

    public void setName(String name) {
        this.name = name;
    }
}
```

- #### HTML로 전달된 입력 값은 create() 메소드의 매개변수인 MemberForm의 name에 저장된다.  이때, spring에서 알아서 setName() 메소드를 호출하여 변수에 값을 넣는다.

- #### "redirect:/"는 다시 첫 화면으로 돌아가라는 의미이다.

- #### 이로써 입력된 값은 Arraylist에 저장된다.

- #### 단, database를 이용하는 것이 아니기 때문에 서버를 종료하면 모든 데이터는 초기화된다.



# Member Inquiry



```java
    @GetMapping(value = "/members")
    public String list(Model model) {
        List<Member> members = memberService.findMembers();
        model.addAttribute("members", members);
        return "members/memberList";
    }
```

- #### Model에 List를 넣은 후 HTML로 전송한다.



```html
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<body>
<div class="container">
    <div>
        <table>
            <thead><tr>
                <th>#</th>
                <th>이름</th>
            </tr>
            </thead>
            <tbody>
            <tr th:each="member : ${members}">
                <td th:text="${member.id}"></td>
                <td th:text="${member.name}"></td>
            </tr>
            </tbody>
        </table>
    </div>
</div> <!-- /container -->
</body>
</html>
```

- #### each를 통해  전달받은 List내부의 값을 loop을 돌면서 확인한다.

- #### List 각 객체 내부의 값을 (ID, name) 출력한다.  이때 ID, name은 자바 소스에 private으로 설정되어 있지만 HTML이 알아서 getter, setter을 이용하여 변수에 접근한다.



# H2 Database



- ### 개발이나 테스트 용도로 가볍고 편리한 database, 웹 화면을 제공해주는 database이다.



- #### 버전을 스프링 부트 버전에 맞춘 후 chmod 755 h2.sh로 권한을 부여한다.

- #### jdbc:h2:~/test로  home 경로에 test라는 database를 생성후 jdbc:h2:tcp://localhost/~/test 로 접근한다.



```sql
drop table if exists member CASCADE;
create table member
(
id
bigint generated by default as identity,
name varchar(255),
primary key (id)
);
```

- #### Query를 통해 member를 저장할 테이블을 생성한다.



```java
// build.gradle
implementation 'org.springframework.boot:spring-boot-starter-jdbc'
runtimeOnly 'com.h2database:h2'

// application.properties
spring.datasource.url=jdbc:h2:tcp://localhost/~/test
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
```

- #### build.gradle에 jdbc, h2 관련 라이브러리를 추가한다.

- #### application.properties에 h2 database와 연결을 추가한다.

# JDBC Repository 구현

```java
	private final DataSource dataSource;
    public JdbcMemberRepository(DataSource dataSource)
    {
        this.dataSource = dataSource;
    }
    @Override
    public Member save(Member member) {
        String sql = "insert into member(name) values(?)";
        Connection conn = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;try {
            conn = getConnection();
            pstmt = conn.prepareStatement(sql,
                    Statement.RETURN_GENERATED_KEYS);
            pstmt.setString(1, member.getName());
            pstmt.executeUpdate();
            rs = pstmt.getGeneratedKeys();
            if (rs.next()) {
                member.setId(rs.getLong(1));
            } else {
                throw new SQLException("id 조회 실패");
            }
            return member;
        } catch (Exception e) {
            throw new IllegalStateException(e);
        } finally {
            close(conn, pstmt, rs);
        }
    }
    @Override
    public Optional<Member> findById(Long id) {
        String sql = "select * from member where id = ?";
        Connection conn = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;
        try {
            conn = getConnection();
            pstmt = conn.prepareStatement(sql);
            pstmt.setLong(1, id);
            rs = pstmt.executeQuery();if(rs.next()) {
                Member member = new Member();
                member.setId(rs.getLong("id"));
                member.setName(rs.getString("name"));
                return Optional.of(member);
            } else {
                return Optional.empty();
            }
        } catch (Exception e) {
            throw new IllegalStateException(e);
        } finally {
            close(conn, pstmt, rs);
        }
    }

    private Connection getConnection() {
        return DataSourceUtils.getConnection(dataSource);
    }

    private void close(Connection conn) throws SQLException {
        DataSourceUtils.releaseConnection(conn, dataSource);
    }
```

- #### Application.properties에서 자동으로 datasource를 bean에 넣어줘서 DI로 datasource를 사용하면 된다.

- #### Database와 DataSourceUtils.getConnection()를 통해 연결하고 PreparedStatement를 통해 query를 전송하고 ResultSet을 통해 결과값을 받는다.

- #### PreparedStatement 인자로 Statement.RETURN_GENERATED_KEYS를 넣어서 insert시 key 값을 반환 받을 수 있게 한다.

- #### ExecuteUpdate()를 통해 database에 값을 저자하고 getGeneratedKeys()를 통해 값을 key값에 따라 반환받는다.

- #### ExecuteQuery()를 통해 query를 실행하여 key값으로 값을 조회할 수 있다.

- #### Database와 연결하여 사용 후 반드시 DataSourceUtils.releaseConnection()를 통해 연결을 해제해줘야 중첩 연결을 방지할 수 있다.

  

```java
     @Bean
     public MemberRepository memberRepository(){
       //  return new MemoryMemberRepository();
         return new JdbcMemberRepository(dataSource);
     }
```

- #### Config 소스파일은 Assembly라고 부르며 나머지 코드는 건들지 않고 추가하여 객체지향형의 다형성을 활용할 수 있다.

- #### DI를 사용하여 개방-폐쇄 원칙(OCP)을 잘 준수하고 기존 코드를 전혀 손대지 않고, 설정만으로 구현 클래스를 변경할 수 있다.



# Spring Integrated Testing



- ### Spring Container와 Database까지 연결한 통합 테스트를 진행한다.



```java
@SpringBootTest
@Transactional
class MemberServiceIntegrationTest {
    @Autowired MemberService memberService;
    @Autowired MemberRepository memberRepository;

    @Test
    public void 회원가입() throws Exception {
//Given
        Member member = new Member();
        member.setName("hello");
//When
        Long saveId = memberService.join(member);//Then
        Member findMember = memberRepository.findById(saveId).get();
        assertEquals(member.getName(), findMember.getName());
    }
    @Test
    public void 중복_회원_예외() throws Exception {
//Given
        Member member1 = new Member();
        member1.setName("spring");
        Member member2 = new Member();
        member2.setName("spring");
//When
        memberService.join(member1);
        IllegalStateException e = assertThrows(IllegalStateException.class,
                () -> memberService.join(member2));//예외가 발생해야 한다.
        assertThat(e.getMessage()).isEqualTo("이미 존재하는 회원입니다.");
    }
}
```

- #### @SpringBootTest를 통해 spring container와 테스트를 함께 실행한다.

- #### @Transactional은 test 실행 시 database로 데이터 insert query를 실행하고 test가 끝나면 rollback하여 database에 저장하였던 데이터가 모두 지워진다.  즉, @Transactional로 @AfterEach는 필요없으며 안전하게 다음 테스트 메소드를 이용할 수 있다.

- #### 통합 테스트보다는 단위 테스트를 주기적으로 하는 것이 좋으며 test 전용 database를 따로 제작하기도 한다.



# Spring JDBC Template



- ### JDBC API의 반복 코드를 대부분 제거하지만 SQL은 직접 작성해야한다.




```java
	private final JdbcTemplate jdbcTemplate;
    public JdbcTemplateMemberRepository(DataSource dataSource) {
        jdbcTemplate = new JdbcTemplate(dataSource);
    }
    @Override
    public Member save(Member member) {
        SimpleJdbcInsert jdbcInsert = new SimpleJdbcInsert(jdbcTemplate);
        jdbcInsert.withTableName("member").usingGeneratedKeyColumns("id");
        Map<String, Object> parameters = new HashMap<>();
        parameters.put("name", member.getName());
        Number key = jdbcInsert.executeAndReturnKey(new
                MapSqlParameterSource(parameters));
        member.setId(key.longValue());
        return member;}
    @Override
    public Optional<Member> findById(Long id) {
        List<Member> result = jdbcTemplate.query("select * from member where id = ?", memberRowMapper(), id);
        return result.stream().findAny();
    }
    @Override
    public List<Member> findAll() {
        return jdbcTemplate.query("select * from member", memberRowMapper());
    }
    @Override
    public Optional<Member> findByName(String name) {
        List<Member> result = jdbcTemplate.query("select * from member where name = ?", memberRowMapper(), name);
        return result.stream().findAny();
    }
    private RowMapper<Member> memberRowMapper() {
        return (rs, rowNum) -> {
            Member member = new Member();
            member.setId(rs.getLong("id"));
            member.setName(rs.getString("name"));
            return member;
        };
    }
```

- #### WithTableName()을 통해 사입할 table명을 명시하고 usingGneratedKeyColumns()를 통해 key열의 이름을 명시해준다.

- #### Parameters hashmap에 database에 저장할 요소를 저장한다.

- #### ExecuteAndReturnKey( new MapSqlParameterSource() )를 통해 데이터를 저장 후 key값을 가져온다.



# JPA



- ### JPA는 기존의 반복 코드를 줄이고 SQL도 JPA가 직접 만들어서 실행해준다.  또한, SQL과 데이터 중심의 설계에서 객체 중심의 설계로 전환할 수 있다.




```java
// build.gradle
// implementation 'org.springframework.boot:spring-boot-starter-jdbc'
implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
```

- #### JPA 라이브러리는 jdbc를 포함한다.



```java
// application.properties
spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=none
```

- #### Show-sql은 JPA가 생성하는 sql을 출력한다.

- #### Ddl-auto = none이면 테이블을 자동으로 생성하는 기능을 사용하지 않는 것이고 create이면 entity 정보를 바탕으로 테이블을 직접 생성해준다.



```java
@Entitypublic class Member {    @Id @GeneratedValue(strategy = GenerationType.IDENTITY)    private long id; // 고객이 아닌 시스템이 정하는 값이다    private String name;    public long getId() {        return id;    }    public void setId(long id) {        this.id = id;    }    public String getName() {        return name;    }    public void setName(String name) {        this.name = name;    }}
```

- #### @Entity를 이용하여 jpa가 관리하는 entity임을 나타내준다.

- #### GenerationType.IDENTITY를 통해 database가 알아서 ID값을 지정해주게 한다.



```java
public class JpaMemberRepository implements MemberRepository {    private final EntityManager em;    public JpaMemberRepository(EntityManager em) {        this.em = em;    }    public Member save(Member member) {        em.persist(member);        return member;    }    public Optional<Member> findById(Long id) {        Member member = em.find(Member.class, id);        return Optional.ofNullable(member);    }    public List<Member> findAll() {        return em.createQuery("select m from Member m", Member.class)                .getResultList();    }    public Optional<Member> findByName(String name) {            List<Member> result = em.createQuery("select m from Member m where m.name = :name", Member.class)                .setParameter("name", name)                .getResultList();        return result.stream().findAny();    }}
```

- #### Application.properties를 통해 자동으로 EntityManager이 bean에 등록되며 jpa는 EntityManager로 database를 관리한다.

- #### Persist()는 데이터를 database에 영구 저장한다는 뜻이다.

- #### Find()는 데이터를 조회할 때 사용하며 인자로는 조회할 타입, 식별자를 넣는다.

- #### CreateQuery는 query에 객체를 삽입하여 객체를 대상으로 query를 만들지만 sql로 자동 전환되어 database로 전송된다.  이러한 기능을 JPQL이라고 한다.



```java
@Transactionalpublic class MemberService {}
```

- #### JPA는 해당 클래스의 메소드를 실행할 때 transaction을 시작하고 메소드가 정상 종료되면 transaction을 commit한다.  만약 runtime error이 발생하면 rollback하므로 JPA를 통한 모든 데이터 변경은 transaction안에서 실행해야 한다.

- #### @Commit은 소스파일 실행 혹은 테스트 시 database에 변경 내용을 남겨 놓는다는 어노테이션이다.



# Spring Data JPA



- ### JPA를 Spring으로 감쌓서 제공하는 기술로 JPA를 편리하게 사용하게 해주는 기술이다.




```java
public interface SpringDataJpaMemberRepository extends JpaRepository<Member, Long>, MemberRepository {    @Override    Optional<Member> findByName(String name);}
```

- #### Spring Data JPA는 인터페이스 상에서 모두 해결할 수 있다.

- #### JpaRepository의 인자로는 사용할 객체의 타입, key의 타입을 넣는다.

- #### Spring Data JPA가 JpaRepository를 받고 있으며 구현체를 자동으로 만들어주고 Spring Bean에 자동으로 등록한다.

- #### JpaRepository에 이미 find ~ save 메소드가 만들어져 있어서 override되어 사용되지만 findByName은 특정 key값으로 조회하는 기능이 아니며 대상 범위가 프로젝트마다 다를 수 있으므로 직접 메소드를 선언해야한다.

- #### FindByName() 메소드는 메소드명에 find와 뒤의 Name을 이용하여 Spring Data JPA가 자동으로 select m from Member m where m.name = ? 이라는 JPQL을 만들어준다.


![Spring Data JPA](https://user-images.githubusercontent.com/79822924/135110420-c8f8bccc-0c0d-4d22-bd29-a97bf4bdc21e.png)


- #### 80% 정도의 단순화 query는 Spring Data JPA의 인터페이스로 구현하는 것이 가능하다.

- #### 복잡한 동적 쿼리는 Querydsl 라이브러리를 사용하여 query를 자바 코드로 안전하게 작성할 수 있고 동적 query도 편리하게 작성할 수 있다.



# AOP



- ### AOP(Aspect Oriented Programming)은 공통 관심 사항(cross-cutting concern)과 핵심 관심 사항(core concern)을 분리하여 원하는 곳에 공통 관심 사항을 적용할 수 있게 한다.




```java
@Component@Aspectpublic class TimeTraceAop {    @Around("execution(* hello.hellospring..*(..))")    public Object execute(ProceedingJoinPoint joinPoint) throws Throwable {        long start = System.currentTimeMillis();        System.out.println("START: " + joinPoint.toString());        try {            return joinPoint.proceed();        } finally {            long finish = System.currentTimeMillis();            long timeMs = finish - start;            System.out.println("END: " + joinPoint.toString()+ " " + timeMs +                    "ms");        }    }}
```

- #### @Aspect는 AOP를 적용하겠다는 어노테이션이다.

- #### @Component를 적용해도 되지만 config에 @Bean으로 bean에 등록하기도 한다.

- #### @Around로 공통 관심사를 적용할 메소드를 지정한다.  패키지명, 클래스면, 파라미터 타입을 순서대로 작성하며 코드의 의미는 패키지 하위 모든 메소드에 적용한다는 것이다.  * hello.hellospring.service..*(..)이면 service패키지 내부 메소드에만 공통 관심사가 적용된다.

- #### JointPoint.proceed()를 통해 메소드를 실행하고 종료되면  finally{}의 코드가 실행되어 각 메소드의 실행 시간이 console에 출력된다.   Proceed() 메소드는 필요시 다른 메소드로 변경 가능하다.



![AOP Proxy](https://user-images.githubusercontent.com/79822924/135110336-c4daa404-8ed6-481b-97c2-1b38dc769b76.png)


- #### DI를 이용하여 container은 실제 메소드를 실행하기 전에 가짜 메소드인 proxy를 만들어서 먼저 실행한다.  실제 메소드는 proxy가 종료 후 실행된다.  즉, proxy를 통해 미리 공통 관심사를 실행한 후 실제 메소드 한번 더 실행하는 것이다.

- #### GetClass() 메소드는 CGLIB를 이용한다.  CGLIB는 CG library로 멤버 서비스를 복제하여 코드를 조작하는 기술이다.



# Additional Knowledge



- #### Optional은 null로 반환 되는 값을 optional로 감싸서 표현하기 때문에 객체에 대한 반환값은 optional로 하는 것이 좋다.

- #### 실무에서는 동시성 문제가 발생할 수 있기 때문에 공유되는 변수는 HashMap보다는 CurrentHashMap을 사용한다..

- #### store.values().stream().filter(member -> member.getName().equals(name)).findAny(); 는 람다표현으로 stream()으로 loop을 돌면서 filter()을 통해 멤버중 name과 같은 이름을 가진 member을 반환하는데 findAny()로 순서 상관없이 먼저 발견한 member을 반환한다는 것이다.

- #### 자바는 테스트 케이스를 JUnit이라는 Framework로 테스트를 실행하여 간편하게 프로젝트를 테스트한다.

- #### @AfterEach는 테스트 메소드 하나 끝날때마다 호출되는 메소드이고  @BeforeEach는 테스트 메소드가 시작하기 전에 호출되는 메소드이고 @Test는 테스트를 진행하는 메소드이다.

- #### 테스트 케이스를 비교하는 라이브러리로 Assertions를 이용하며 assertThat(), assertEquals(), isEqualTo() 메소드를 자주 이용한다.

- #### findById().get()은 optional에서 값을 바로 꺼낼 때 이용하지만 권장하지는 않는다.

- #### 테스트 케이스는 given, when, then으로 나눠서 작성하는 것이 좋으며 given은 뭐가 주어졌는지, when은 주어진 것을 실행 했을때, then은 어떠한 결과가 나와야하는지를 의미한다.

- #### 테스트 및 소스코드에서 다 같은 객체를 공유할 때 Dependency Injection(DI)를 이용하여 같은 객체를 각 클래스에 넘겨주게 된다.

- #### TDD는 테스트 케이스를 먼저 만들고 개발을 시작하는 순서인 방법론이다.

- #### 테스트 케이스에서는 모든 테스트 메소드를 한번에 실행할 수 있지만 메소드 실행 순서는 보장되지 않는다.  이러한 상황에서 각 메소드가 데이터베이스를 갱신하면 서로 예상한 데이터 input이 다르게 되어 오류가 발생할 수 있다.  문제점을 해결하기 위해 @AfterEach로 각 테스트 메소드 종료 시 데이터를 reset하도록 한다.

- #### 테스트 코드는 실제 코드에 포함되지 않기 때문에 메소드명을 한글로 작성해도 된다.



# Keyboard Shortcut



- #### Shift + F6 --> 같은 이름을 가진 문자를 한번에 고칠 수 있다.

- #### ctrl + alt + v --> 코드에 대한 반환 결과 변수를 코드 앞에 자동으로 만들어준다.

- #### ctrl + shift + T --> 클래스 내부에서 누르면 테스트 케이스를 자동으로 만들어준다.

- #### ctrl + alt + m --> 코드 지정 후 누르면 지정된 코드를 따로 메소드로 생성한다.

- #### ctrl + B --> 지정된 객체의 원형 화면이 출력된다.

- #### alt + insert constructor --> 클래스가 생성자를 생성하여 DI를 수행할 수 있게 한다.

- #### ctrl + p --> 메소드에 어떤 매개변수가 들어가야 하는지 알려준다.



Image 출처 : [김영한 스프링 입문](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8)