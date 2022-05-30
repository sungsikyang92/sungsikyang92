# TODAY I LEARNED - 20220519

### 1. Basic 인증

웹 애플리케이션에서 인증을 구현하는 가장 간단한 방법이다. 모든 HTTP 요청에 아이디와 비밀번호를 같이 보낸다.

최초 로그인한 후 HTTP요청 헤더의 Authorization: 부분에 `Basic <ID>:<Password>`처럼 아이디와 비밀번호를 콜론으로 이어붙인 후 Base64로 인코딩한 문자열을 함께  보낸다.

그러나 인코딩은 보안을 목적이 아니기에, 디코더만 있으면 누구나 디코딩해서 아이디와 비밀번호를 확인 할 수 있디ㅏ. 그래서 HTTP와 사용하기에는 취약하다. 반드시 HTTPS와 사용해야 한다.

또한 모든 요청이 일종의 로그인 요청이기 때문에, 이 솔루션을 이용하면 사용자를 로그아웃시킬 수 없다.

***

### 2. 토큰 기반 인증

토큰은 사용자를 구별할 수 있는 문자열이다. 최초 로그인 시 서버가 토큰을 만들어 준다. 토큰을 만들어 반환하면 클라이언트는 이후 요청에 아이디와 비밀번호 대신 토큰을 계속 넘겨 자신이 인증된 사용자임을 알린다.

```
Authorization: bearer <TOKEN>
```

서버는 인증 서버를 통해 토큰을 생성 및 저장하고, 요청을 받을 때마다 헤더의 토큰을 서버의 토큰과 비교해 클라이언트를 인증한다.

Basic Auth와의 차이점은, 아이디와 비밀번호를 매번 네트워크를 통해 전송해야 할 필요가 없으므로 보안 측면에서 좀 더 안정하다. 또 서버가 토큰을 마음대로 생성할 수 있으므로 사용자의 인가정보 또는 유효 시간을 정해 관리할 수 잇다. 디바이스마다 다른 토큰을 생성해 주고 디바이스마다 유효 시간을 다르게 정하거나 임의로 로그아웃을 할 수도 있다.

### 3. JSON 웹 토큰

서버에서 전자 서명된 토큰을 이용하면 Basic 인증과, 토큰 기반 인증과는 다르게 인증에 따른 스케일 문제를 해결할 수 있다.

JSON 웹 토큰은 전자 서명된 토큰 중의 하나이다.

`{header}.{payload}.{signature}`로 구성되어 있다.

```
Authorization: Bearer header.payload.signature
```

이를 Base64로 디코딩하면

```
{						//Header
"typ":"JWT",			//토큰의 타입을 의미
"alg":"HS512"			//토큰의 서명을 발행하는 데 사용된 해시 알고리즘의 종류를 의미
}.
{
"sub":"2134890123u78fhjd124kl"		//토큰의 주인을 의미, ID처럼 유일한 식별자여야 한다.
,
"iss: "demo app",					//토큰을 발행한 주체를 의미, 인스타그램이 발행했다면 instagram
"iat":12341234,						//토큰이 발행된 날짜와 시간을 의미한다.
"exp":12341234						//토큰이 만료되는 시간을 의미한다.
}.
vcbuowehrfbidasf980123h40cdvsbh1329vdfcndsfakl	//토큰을 발행한 주체 iss가 발행한 서명으로 토큰의 유효형 검사에 사용된다.
```

JWT에서 전자 서명은 {Header}.{Payload}와 시크릿키를 이용해 해시 함수에 돌린 암호화한 결과 값이다.







***

***

# TODAY I LEARNED - 20220519

### 1. Node.js

자바스크립트를 내 컴퓨터에서 실행할 수 있게 해주는 자바스크립트 런타임 환경이다. 브라우저 밖에서 실행할 수 있다는 것은, 자바스크립트를 클라이언트 언어뿐만 아니라 서버 언어로도 사용할 수 있다는 뜻이다.

*   NPM<sup>Node Package Manager</sup>은 Node.js의 패키지 관리 시스템이다.

노드를 설치하기 전에, 이미 깔려있는지 확인하고 모두 삭제해주었다. [참고](https://no-free-lunch.tistory.com/9)

그러나 노드를 재설치하는 과정에서 download failed가 발생하였다.

이를 해결하기위해서는

`mkdir -p ~/.nodebrew/src` 후 다시 nodebrew를 통해 설치해주면 된다.

***

### 2. React

*   리액트 애플리케이션 생성

```bash
npx create-react-app 생성할이름
cd 생성한이름
npm stasrt
```

실행하면 `localhost:3000`이 브라우저에 실행된다.

*   리액트에서 html 파일은 index.html 하나밖에 없다. 다른 페이지들은 React.js를 통해 생성되고 index.html에 있는 root 엘리먼트 아래에 동적으로 렌더링된다.

[리액트 공식 튜토리얼 사이트](https://ko.reactjs.org/docs/getting-started.html)

*   state

    리액트가 관리하는 오브젝트다. 추후에 변경할 수 있는 변수를 state 오브젝트에서 관리한다. 자바스크립트 내에서 변경한 변수의 값을 HTML에 다시 렌더링하기 위해서.

***

### 3. SPA<sub>Single Page Application</sub>

한 번 웹 페이지를 로딩하면 사용자가 임의로 새로 고침하지 않는 이상 페이지를 새로 로딩하지 않는 애플리케이션을 의미한다.

서버에게 새 HTML 페이지를 요청하지 않고 자바스크립트가 동적으로 HTML을 재구성해 만드는 클라이언트 애플리케이션을 SPA라 한다. 이 렌더링 과정을 클라이언트-사이드 렌더링 이라한다.

***

### 4. 리액트와 관련해서 렌더링이란 무엇인가?

리액트는 브라우저에 보이는 HTML DOM 트리의 다른 버전인 ReactDOM을 갖고 있다. 컴포넌트의 state가 변하면 ReactDOM은 이를 감지하고 변경된 부분의 HTML을 바꿔준다. HTML이 업데이트되면 이 변경된 결과를 눈으로 확인할 수 있고, 이를 렌더링이라고 한다.

***

### 5. 마운팅<sub>mounting</sub>

렌더링이 맨 처음 일어나는 순간, ReactDOM트리가 존재하지 않는 상태에서 리액트가 처음으로 각 컴포넌트의 render() 함수를 콜해 자신의 DOM 트리를 구성하는 과정을 마운팅이라고 한다.

***

### 6. CORS <sup>Cross Origin Resource Sharing</sup>

처음 리소스를 제공한 모데인이 현재 요청하려는 도메인과 다르더라도 요청을 허락해주는 웹 보안 방침이다.

<img width="747" alt="image" src="https://user-images.githubusercontent.com/71358285/169270682-8bb6881b-88d4-4e5b-8629-25a03573a8fa.png">

CORS가 가능하려면 백엔드에서 CORS방침 설정을 해줘야 한다. 이를위해 나의경우 com.todo.ssiky.config라는 패키지에 WebMvcConfig라는 클래스를 생성했다.

[public doc](https://developer.mozilla.org/ko/docs/Web/HTTP/CORS)

***

### 7. JS Promise

비동기 오퍼레이션<sup>Asynchronous Operation</sup>에서 사용한다. Pending, Resolve, Rejecte 3가지 상태가 있다.

*   Pending - 오퍼레이션이 끝나길 기다리는 상태
*   Resolve - then의 매개변수로 넘어오는 함수를 실행한다. 오퍼레이션 중 에러가 나는 경우 reject()함수를 콜한다.
*   Reject - 

***

### 8. Fetch API

자바스크립트가 제공하는 메서드로 API 서버로 http 요청을 송신 및 수신할 수 있도록 도와준다.

fetch는 url을 매개변수로 받거나 url과 options를 매개변수로 받을 수 있다.

fetch() 함수는 위의 Promise 오브젝트를 리턴한다.



***

***

# TODAY I LEARNED - 20220518

### 1. POSTMAN API

REST API를 테스트할 때, 임시로 프론트엔드 UI를 만들지 않고 직관적인 GUI 포스트맨 프로그램을 사용한다.

포스트맨을 사용함으로써 간단히 RESTful API를 테스트할 수 있다.

***

### 2. DTO

Data Transfer Object를 사용하는 이유는,

1.   비즈니스 로직을 캡슐화<sub>encapsulation</sub>하기 위함이다. 외부 사용자에게 서비스 내부의 로직, 데이터베이스의 구조 등을 숨길 수 있다.

2.   클라이언트가 필요한 정보를 모델이 전부 포함하지 않는 경우가 많기 때문이다.

***

### 3. REST 제약조건

*   클라이언트-서버<sup>Client-Server</sup>
*   상태가 없는<sup>stateless</sup>
*   캐시되는<sup>Cacheable</sup>데이터
*   일관적인 인터페이스<sup>Uniform Interface</sup>
*   레이어 시스템<sup>Layered System</sup>
*   코드-온-디맨드<sup>Code-On-Demand</sup>

***

### 4. JPA(Java Persistence API)

ORM<sub>Object-Relational Mapping</sub>기술 표준으로 사용되는 인터페이스의 모음이다.

자바 어플리케이션에서 관계형 데이터베이스를 사용하는 방식을 정의한 인터페이스로. 'JPA의 구현을 위해서 이런 기능을 작성해라' 라고 말해주는 지침이 된다.

반복적인 CRUD SQL작업을 줄일 수 있게 해주며, 대표적으로 Hibernate가 있다.

***

### 5. H2

In-Memory 데이터베이스로 로컬 환경에서 메모리상에 데이터베이스를 구축해 준다. 데이터베이스 서버를 구축하는데 시간을 할애할 필요가 없으므로 초기 개발 시에 많이 사용한다.

디펜던시로 설정하면 @SpringBootApplication 어노테이션의 일부로 스프링이 알아서 애플리케이션을 H2 데이터베이스로 연결해준다.

실행 시 테이블이 생성되고, 종료 시 테이블이 함께 소멸된다.

***

### 6. UUID - Universally Unique Identifier

네트워크 상에서 고유성이 보장되는 id를 만들기 위한 표준 규약

***

### 7. @GeneratedValue

ID를 자동으로 생성하겠다는 뜻. 매개변수 generator로 어떤 방식으로 id를 생성할지 지정할 수 있다.

***

### 8. @GenericGenerator

Hibernate가 제공하는 기본 Generator가 아니라 나만의 Generator를 사용하고 싶을 경우 이용한다.

***

### 9. JpaRepository

기본적인 데이터베이스 오퍼레이션 인터페이스를 제공한다.

save, findById, findAll 등이 기본적으로 제공되는 인터페이스이다.

구현은 스프링 데이터 JPA가 실행 시에 알아서 해줌으로 save메서드를 구현하려고 "Insert into..."와 같은 sql 쿼리를 작성할 필요가 없다.

*   기본적인 쿼리가 아닌경우에는?

`List<TodoEntity> findByUserId(String userId);` `SELECT * FROM TodoRepository WHERE userId = '{userId}'`를 보면 메서드 이름은 쿼리, 매개변수는 쿼리의 where문에 들어갈 값을 의미한다.

*   더 복잡한 쿼리는?

@Query 어노테이션을 사용해 지정할 수 있다.

`Query("SELECT * FROM Todo t where t.userId = ?1")

?1은 메서드의 매개변수의 순서 위치다.

***

### 10. AOP(Aspect Oriented Programming)

공통 기능 구현과 핵심 기능 구현을 분리하는 것이 AOP의 핵심이다.

여러 객체에 공통으로 적용할 수 있는 기능을 분리해서 재사용성을 높여주는 프로그래밍 기법.

핵심 기능에 공통 기능을 삽입하는 방법은 세 가지가 있다.

1.   컴파일 시점에 코드에 공통 기능을 삽입하는 방법
     *   AOP 개발 도구가 소스 코드를 컴파일 하기 전에 공통 구현 코드를 소스에 삽입하는 방식으로 동작한다.
2.   클래스 로딩 시점에 바이트 코드에 공통 기능을 삽입하는 방법
     *   클래스를 로딩할 때 바이트 코드에 공통 기능을 클래스에 삽입하는 방식으로 동작한다.
3.   런타임에 프록시 객체를 생성해서 공통 기능을 삽입하는 방법
     *   스프링이 제공하는 AOP 방식이며 프록시를 이용한다.
     *   프록시 방식은 중간에 프록시 객체를 생성하고, 실제 객체의 기능을 실행하기 전후에 공통기능을 호출한다.

[more...](https://github.com/sungsikyang92/sungsikyang92/blob/main/AOP.md)

***

### 11. 로그 어노테이션 @Slf4j

로그는 크게 info, debug, warn, error로 나누고 이를 로그 레벨이라고 부른다.



***

***

# TODAY I LEARNED - 20220517

### 1. @RequestParam("매개변수")

url에서 전송받은 매개변수를 지정한 변수에 자동으로 값이 설정된다.

required 속성을 이용하면 필수 매개변수인 경우와 그렇지 않은 경우를 설정할 수 있다. 이를 생략하면 default값은 true이다. false로 설정하면 메서드 호출 시 지정한 이름의 매개변수가 전달되면 값을 저장하고 없으면 null을 할당한다.

***

### 2. Spring Study..

*   @Configuration

    해당 클래스를 스프링 설정 클래스로 지정한다. 이 애노테이션을 붙여야 스프링 설정 클래스로 사용할 수 있다.

*   @Bean

    스프링이 생성하는 객체를 빈 객체라고 부르는데, 이 애노테이션을 메서드에 붙이면 해당 메서드가 생성한 객체를 스프링이 관리하는 빈 객체로 등록한다.

*   AnnotationConfigApplicationContext 클래스

    자바 설정에서 정보를 읽어와 빈 객체를 생성하고 관리한다.

*   Singleton

    별도 설정을 하지 않은 경우 스프링은 한 개의 빈 객체만을 생성한다. 이때 빈 객체는 'Singleton'범위를 갖는다 라고 한다.

    단일 객체를 의미하는 단어로서 스프링은 기본적으로 한개의 @Bean 애노테이션에 대해 한 개의 빈 객체를 생성한다.

*   Dependency Injection

   *   '의존 주입'이라 한다. 의존은 변경에 의해 영향을 받는 관계를 의미한다.

   *   Dependency

       *   ex) MemberDao의 insert() 메서드를 insertMember()메서드로 변경하면 이 메서드를 사용하는 MemberRegisterService클래스릐 코드도 함께 변경된다. 이렇게 변경에 따른 영향이 전파되는 관계를 '의존한다' 한다.

       *   의존할 때 가장 쉬운 방법은 의존 대상 객체를 직접 생성하는 것이다. 그러나 클래스 내부에서 직접 의존 객체를 생성하는 것은 유지보수 관점에서 문제점을 유발할 수 있다.

       ```java
   	public clss MemberRegisterService{
       	//의존 객체 직접 생성함, 이는 유지보수 관점에서 문제점을 야기
           private MemberDao memberDao = new MemberDao();
      }
     ```
     
   *   Dependency Injection - 생성자 방식

       DI는 의존하는 객체를 직접 생성하는 대신 의존 객체를 전달받는 방식을 사용한다.

       ```java
       public clas MemberRegisterService{
           private MemberDao memberDao;
           
           public MemberRegisterService(MemberDao memberDao){
               this.memberDao = memberDao;
           }
       }
       ```

       직접 의존 객체를 생성했던 위의 코드와 달리 바뀐 코드는 의존 객체를 직접 생성하지 않고 생성자를 통해서 의존 객체를 전달받는다. 즉 생성자를 통해 MemberRegisterService가 Dependency하고 있는 MemberDao객체를 Injection받은 것이다.

       *   DI는 변경의 유연함으로 사용된다.

           위의 예를 들어 DI패턴을 사용하지 않으면, Dao변경이 일어날 때 문제가 생길 수 있다. 여러 클래스에 Dao를 직접 의존 객체 생성 하였다면, 그 모든 클래스에서 Dao를 변경해주어야 한다. 그러나 DI패턴을 사용하였다면, 실제 객체를 생성하는 한 곳만 수정해주면 다른 클래스들은 수정해 줄 필요가 없다.

   *   DI의 세터 메서드 방식

       세터 메서드는 자바빈 규칙에 따른다.

       *   메서드 이름이 set으로 시작한다.
       *   set 뒤에 첫 글자는 대문자로 시작한다.
       *   파라미터가 1개이다.
       *   리턴 타입이 void이다.

***

*   @Autowired

    스프링 빈에 의존하는 다른 빈을 자동으로 주입하고 싶을 때 사용한다.

***

### Map, HashMap, ConcurrentHashMap

***

### Optional<>

null값이 반환 될 가능성이 있는것들에, 그것을 명확하게 드러내기 위해 메소드 반환 타입으로 사용된다.

***

### 주저리주저리

*   스프링 컨테이너가 생성한 빈은 싱글톤 객체, 스프링 컨테이너는 @Bean이 붙은 메서드에 대해 한 개의 객체만 생성한다. 이는 다른 설정 메서드에서 memberDao()를 몇 번을 호출하더라도 항상 같은 객체를 리턴한다.





***

***



# TODAY I LEARNED - 20220516

### 1. Swagger

Swagger는 개발자가 REST 웹 서비스를 설계, 빌드, 문서화를 도와주는 오픈소스 소프트웨어이다.

Swagger 버전은 사람들이 가장 많이 사용한 2.9.2를 사용하였다. (혹시 문제생기면 검색해서 해결할 가능성이 높으니..!)

1.   build.gradled의 dependencies에 implementation 해준다.

```
	//swagger
	//https://mvnrepository.com/artifact/io.springfox/springfox-swagger-ui
	implementation group: 'io.springfox', name: 'springfox-swagger-ui', version: '2.9.2'
	implementation group: 'io.springfox', name: 'springfox-swagger2', version: '2.9.2'
```

2.   SwaggerConfig를 만들어준다.

```java
package com.dodo.bulldozer.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import springfox.documentation.RequestHandler;
import springfox.documentation.builders.ApiInfoBuilder;
import springfox.documentation.builders.PathSelectors;
import springfox.documentation.builders.RequestHandlerSelectors;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.web.plugins.ApiSelectorBuilder;
import springfox.documentation.spring.web.plugins.Docket;
import springfox.documentation.swagger2.annotations.EnableSwagger2;

@Configuration
@EnableSwagger2
public class SwaggerConfig {

    @Bean
    public Docket docket() {
        ApiInfoBuilder apiInfoBuilder = new ApiInfoBuilder();
        apiInfoBuilder.title("API 서버 문서");
        apiInfoBuilder.description("API 서버 문서 입니다.");

        Docket docket = new Docket(DocumentationType.SWAGGER_2);
        docket.apiInfo(apiInfoBuilder.build());

        ApiSelectorBuilder apiSelectorBuilder = docket.select().apis(RequestHandlerSelectors.basePackage("com.dodo.bulldozer"));
        apiSelectorBuilder.paths(PathSelectors.any());

        return apiSelectorBuilder.build();
    }
}
```

3.   http://localhost:'port'/swagger-ui.html 에 접속하여 확인한다.

class 에 @Api(tags = "설명해요")를 추가

각각 기능에 @ApiOperation(value = "간단설명", notes ="상세설명")을 추가해준다.

parameter가 있을 경우

```
@ApiImplicitParams({
	@ApiImplicitParam(name="파라미터이름", value="의미", example="example값")
})
```

도 추가해준다.

***

### 2. @PathVariable

브라우저에서 요청 URL로 전달된 매개변수를 가져올 수 있다.

```java
@RequestMapping(value = "/todo/{id}", method = "RequestMethod.GET")
public int notice(@PathVariable("num") long id) throws Exception {
    return id
}
```

URL이 `localhost:8080/bulldozer/todo/7` 이라면, 7이 id에 할당된다.







***

***





# TODAY I LEARNED - 20220515

### 1. JSON.stringify()

우선 JSON이란 무엇인가? >> [JSON 공식 페이지](http://json.org/json-ko.html)

JSON(JavaScript Object Notation)은 간단한 형식을 갖는 문자열로 데이터 교환에 주로 사용한다. 사람이 읽을 수 있는 텍스트 기반의 데이터 교환 표준이다. 텍스트 기반이므로 어떠한 프로그래밍 언어에서도 JSON 데이터를 읽고 사용할 수 있다. 

규칙은 중괄호를 사용해서 객체를 표현하고, 객체는 (이름,값) 쌍을 갖는다. 이때 이름과 값은 콜론으로 구분한다. 기본 자료형으로는 Number, String, Boolean, Array, Object, null이 있다.



그렇다면 'JSON.stringify(객체)' 는 무엇인가? 객체를 JSON으로 바꿔주는 것이다. 또한 replacer를 함수로 전달할 경우 변환 전 값을 변형할 수 있다.

`JSON.stringify(value[, replacer[, space]])`

예를 들어

~~~javascript
const ironman = {
    name: 'Tony',
    age: 40,
    job: 'super hero',
    wife: peper
}

const testJson = JSON.stringify(ironman);

alert(typeof testJson);
alert(testJson);
~~~

을 실행한다면 결과는,

<img width="444" alt="스크린샷 2022-05-15 오후 4 18 29" src="https://user-images.githubusercontent.com/71358285/168461803-6afcab62-cd4d-4be9-af89-3c46e1e98746.png"> 

<img width="444" alt="스크린샷 2022-05-15 오후 4 18 36" src="https://user-images.githubusercontent.com/71358285/168461817-3dad3778-393f-43d3-88c9-d7fdc1b81874.png">이다.

이렇게 변경된 문자열은 네트워크를 통해 전송하거나 저장소에 저장할 수 있다.

[이 링크는 JSON.stringify()의 MDN공식문서이다.](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)

***

### 2. 어노테이션 Annotation

1.   @Entity
     *   테이블과 링크될 클래스임을 명시한다.

2.   @Id
     *   해당 테이블의 PK 필드를 나타낸다.

3.   @GeneratedValue
     *   PK의 생성 규칙을 나타낸다.
     *   GenerationType.IDENTITY 옵션을 추가해 auto_increment가 되게한다.

4.   @Column
     *   테이블의 칼럼을 나타내며 굳이 선언하지 않아도, 해당 클래스의 필드는 모두 칼럼이 된다. 그럼에도 사용하는 경우는 기본값 외에 추가로 변경이 필요한 옵션이 있으면 사용한다.

5.   @NoArgsConstructor
     *   매개변수가 없는 기본 생성자를 구현해준다.

6.   @AllArgsConstructor

     *   클래스의 모든 멤버 변수를 매개변수로 받는 생성자를 구현해준다.

7.   @Getter
     *   클래스 내 모든 필드의 Getter 메소드를 자동생성

8.   @Builder

     *   오브젝트 생성을 위한 디자인 패턴 중 하나이다.
     *   Builder 클래스를 따로 개발하지 않고도 Builder 패턴을 사용해 오브젝트를 생성할 수 있다.

     *   생성자 상단에 선언 시 생성자에 포함된 빌드만 빌더에 포함한다.
     *   장점은 생성자 매개변수의 순서를 기억할 필요가 없다.

9.   @Data

     *   Getter/Setter 메서드를 구현해준다.

***

### 3. Entity 클래스에서는 절대 Setter 메소드를 만들지 않는다.

대신 해당 필드의 값 변경이 필요하면 명확히 그 목적과 의도를 나타낼 수 있는 메소드를 추가해야한다.

생성자를 통해 최종값을 채운 후 DB에 삽입한다. 값 변경이 필요한 경우 해당 이벤트에 맞는 public 메소드를 호출하여 변경한다.

***

### 4. 어노테이션들

1.   @RestController
     
     *   http와 관련된 코드 및 요청/응답 매핑을 스프링이 알아서 해준다.
     
     *   이 어노테이션을 사용하여 컨트롤러를 JSON형식으로 반환하는 컨트롤러로 만들어준다.
     
2.   @GetMapping
     *   해당 메서드의 리소스와 HTTP 메서드를 지정한다. 클라리언트가 이 리소스에 대해 Get 메서드로 요청하면 @GetMapping에 연결된 컨트롤러가 실행된다.
     *   @GetMapping에서 또한 URL 경로를 지정할 수 있다.

3.   @RunWith(SpringRunner.class)
     *   테스트를 진행할 때 JUnit에 내장된 실행자 외에 다른 실행자를 실행시킨다.
     *   스프링 부트 테스트와 JUnit 사이에 연결자 역할을 한다.

4.   @Autowired
     *   스프링이 관리하는 Bean을 주입 받는다.

5.   @WevMvcTest
     *   Web(Spring MVC)에 집중할 수 있는 어노테이션
     *   선언할 경우 @Controller, @ControllerAdvice 등을 사용할 수 있으나, @Service, @Component, @Repository등은 사용할 수 없다.

***

### 5. @RequestBody and @ResponseBody

*   @RequestBody

JSON 형식으로 전송된 요청 데이터를 커맨드 객체로 전달받는 방법이다.

이 애노테이션을 커맨드 객체에 붙이면 JSON형식의 문자열을 해당 자바객체로 변환한다.

보통 반환하고자 하는 리소스가 복잡할 때 사용한다.(오브젝트처럼 복잡한 자료형을 통째로 요청에 보내고 싶은 경우)

*   @ResponseBody

컨트롤러의 특정 메서드에 @ResponseBody를 적용하면 JSP가 아닌 텍스트나 JSON으로 결과를 전송할 수 있다.

HTTP의 BODY에 문자 내용을 직접 반환한다.

viewResolver 대신에 HttpMessageConverter가 동작한다.

기본 문자처리: StringHttpMessageConverter

기본 객체처리: MappingJackson2HttpMessageConverter

byte 처리 등등 기타 여러 HttpMessageConverter가 기본으로 등록되어 있다.

***

### 6. ResponseEntity

정상인 경우와 비정상인 경우 모두 JSON에 응답을 전송하는 방법이다. 예외에 대해 세밀한 제어가 필요한 경우 사용한다.

Spring MVC는 리턴 타입이 ResponseEntity이면 ResponseEntity의 body로 지정한 객체를 사용해서 변환을 처리한다.

ResponseEntity의 status로 지정한 값을 응답 상태 코드로 사용한다. 

```java
public ResponseEntity<Object> Todo(@PathVariable Long id){
	Todo todo = Todo.selectById(id);
    if (todo == null){
        return ResponseEntity.status(HttpStatus.NOT_FOUND)
            .body(new ErrorResponse("no todo"))
    }
    return ResponseEntity.status(HttpStatus.OK).body(todo);
}
```

ResponseEntity를 생성하는 기본 방법은 status와 body를 이용해서 상태 코드와 JSON으로 변환할 객체를 지정하는 것이다.

`ResponseEntity.status(상태코드).body(객체)`

200(OK) 응답 코드와 몸체 데이터를 생성할 경우 ok() 메서드를 이용해서 생성할 수도 있다.

`ResponseEntity.ok(todo)`

만약 몸체 내용이 없다면 다음과 같이 body를 지정하지 않고 build()로 바로 생성한다.

`ResponseEntity.status(HttpStatus.NOT_FOUND).build()`

몸체 내용이 없는 경우 status() 대신 사용할 수 있는 메서드는

```java
noContent():204
badRequest():400
notFound():404
```





***

### 7. TestRestTemplate











***

***





# TODAY I LEARNED - 20220514

### 1. What is REST API?

그런 REST API로 괜찮은가?

restful api design guidelines





REST(Representational State Transfer) API(RESTful API)란 REST 아키텍처의 제약 조건을 준수하는 애플리케이션 프로그래밍 인터페이스를 뜻한다.

즉 정보들이 주고 받아지는데 있어서 개발자들이 널리 사용하는 일정의 형식이며, 정해진 폼에 맞춰서 기능을 만드는것이다.

소프트웨어에가 다른 소프트웨어로부터 지정된 형식으로 요청, 명령을 받을수 있는 수단을 API라 한다.

서버에 REST API로 요청을 보낼때는 HTTP란 규약에 따라 신호를 전송한다.

정해진 폼에 맞추기 때문에, 각 요청을 보내는 주소만으로도 어떤 동적이나 정보를 위한것인지 추론이 가능하다

REST API에서는 GET POST DELETE PUT 혹은 PATCH까지 4~5가지를 사용한다.

put은 통째로 정보를 갈아 끼울때

patch은 정보 일부를 수정할때

URI는 명사로 이루어져야한다.

결국 http요청을 보낼 때, 어떤 URI에 어떤 메소드를 사용할지 개발자사들에 널리 지켜지는 약속이다.

형식이기 때문에 기술에 구애받지 않는다.



***

***





# TODAY I LEARNED - 20220513

### 1. JS  노드 생성/삽입/삭제하기

##### 1.1 노드생성

새로운 요소 노드 객체를 생성할 때는 createElement() 메서드를 사용한다.

```javascript
const element = document.createElement(요소의 이름);
const element = document.createElement("li");
```

새로운 텍스트 노드 객체를 생성할 때는 ceateTextNode() 메서드를 사용한다.

```javascript
const textnode = document.createTextNode(텍스트);
const textnode = document.createTextNode("TEXT");
```

##### 1.2 노드삽입

*   appendChild() 메서드

    요소 객체에 인수로 넘긴 노드 객체를 해당 요소의 마지막 자식 노드로 삽입한다.

    ```javascript
    요소 노드.appendChild(삽입할노드);
    li.appendChild(span);
    ```

*   insertBefore() 메서드

	지정한 자식 노드 바로 앞에 노드 객체를 삽입할 때 사용한다.

    ```javascript
    요소 노드.insertBefore(삽입할 노드, 자식 노드)
    <ul id="phoneList">
    <li>iPhone</li>
    <li>Galaxy</li>
    </ul>
    <script>
    const phoneList = document.getElementById("phoneList");
    const element = document.createElement("li");
    const text = document.createTextNode("BlackBerry");
    phoneList.insertBefore(element, phoneList.children[1]);
    element.appendChilde(text);
    </script>
    ```

<img width="125" alt="스크린샷 2022-05-13 오후 2 45 50" src="https://user-images.githubusercontent.com/71358285/168219008-5c330374-7190-4eb9-a198-69d4a08696a0.png">

##### 1.3 노드 옮기기

이미 있는 노드를 appendChild와 insertBefore 메서드로 문서에 삽입하면 해당 노드를 현재 위치엣허 삭제하고 새로운 위치에 삭제하여 이동시킨다.

##### 1.4 노드 삭제하기

removeChilde() 메서드로 노드의 자식 노드를 삭제한다.

```javascript
노드.revmoveChild(자식 노드)
```

***

***





# TODAY I LEARNED - 20220512

### 1.   마크다운에서 빈 체크박스와 체크된 체크박스 만들기

```
- [ ] //빈 체크박스
- [x] //체크된 체크박스
- [X] //체크된 체크박스
```
***

### 2.   spring project 초기 설정 (간편하게 stgart.spring.io에서 만들자)
     1.    spring initializr에서 projectg GENERATE

<img width="666" alt="image" src="https://user-images.githubusercontent.com/71358285/168215315-1222d0e0-13c4-4041-8d65-f20bb56574a7.png">

우선 Dependecies는

*   Spring Web
*   Lombok

을 추가해주었다.
***

### 3. ID 선택자와 CLASS 선택자

선택자의 종류는 많지만, 그 중 id선택자와와 class선택자를 비교해보자.

|          | ID선택자 | CLASS선택자 |
|----------| -------------------- | -------------------- |
|설명| 특정 id 속성이 있는 태그를 선택 | 특정 클래스가 있는 태그를 선택 |
|| 웹 표준에 id 속성은 웹 페이지 내부에서 중복되면 안된다는 규정이 있으므로 아이디 선택자는 특정 태그 하나를 선택할 때 사용한다. | 문서 안 복수의 요소에 스타일을 적용하는 경우에 사용한다. |
|형태|#아이디|.클래스|

태그선택자 < 클래스선택자 < 아이디선택자 < 인라인스타일 < !important 순서로 우선순위를 가진다.

```html
 <h2>선택자 우선순위 테스트</h2>
    <div id="test1" class="test1" style="background-color: purple;">우선순위 테스트</div>
    <p id="test2" class="test2" style="background-color: blue;">우선순위 테스트2</p>
```

***

### 4. AUTOFOCUS

input태그의 autofocus 속성은 페이지가 로드될 때 자동으로 포커스가 input으로 이동됨을 명시해주는 것이다.

***

### 5. JavaScript 시간 가져와서 나타내기

1.   Date객체를 생성한다.

```javascript
const date = new Date();
```

2.   객체 생성 후 가져오고 싶은 정보를 가져온다

```javascript
const getYear = String(date.getFullYear());
```

3.   월과 일의 경우 1자리 숫자일때 보기좋게 두 자리로 표현하기 위해서 padStart()함수를 사용한다.

```javascript
const getMonth = String(date.getMonth()).padStart(2,"0");
```

padStart는 매개변수로 두개를 받을 수 있는데, 앞은 몇자리수까지 나타낼것인지 그리고 뒤는 해당 자리수에 도달하기 위해 어떠한 문자를 채워넣을지 써주면 된다.

***

### 6. TDD(Test-Driven Development, TDD)

TDD란 "프로그램을 작성하기 전에 테스트를 먼저 작성하는 것"이라고 TDD를 주도한 켄트 벡이 정의했다.

TDD의 정의는 "업무 코드를 작성하기 전에 테스트 코드를 먼저 만드는 것" 이라고 정의된다.

코드를 검증하는 테스트 코드를 먼저 만든 다음에 실제 작성해야 하는 프로그램 코드 작성에 들어가라는 뜻이다.

이는 메소드나 함수같은 프로그램 모듈을 작성할 때 '작성 종료조건을 먼저 정해놓고 코딩을 시작한다'라는 의미로 받아들이면 편하다.

```java
public class Calculator{
  public int sum(int a, int b){
    return 0;
  }
  
  public static void main(String[] args){
 		Calculator calc = new Calculator();
    System.out.println(calc.sum(10, 20) == 30);
    System.out.println(calc.sum(1, 2) == 3);
    System.out.println(calc.sum(-10, 20) ==10);
    System.out.println(calc.sum(0,0) == 0);
  }
}
------실행결과------
  false
  false
  false
  true
```

위의 코드를 살펴보면, main메소드를 텟흐트 메소드처럼 사용하였다. sum 메소드는 구현하지 않고 비어있는 상태이고, 검증코드를 먼저 만들어 놓았다. 검증코드에 해당하는 테스트 케이스를 모두 만족하면, 즉 실행 결과가 모두 true로 나오면 sum 메소드가 정상적으로 작성됐다고 판단하기로 한다. 다시말해, 명시적인 코드로 개발 종료조건을 정해놓은 것, 이런 식의 개발 접근 방식이 Test-Driven Development이다.  

<p style="text-align:right;"><sub>출처 - TDD 실천법과 도구(채수원 저자)</sub></p>

***

### 7. gitignore가 작동하지 않을때 해결방법

git의 캐시 문제이므로 터미널을 열어서 캐시 삭제 후 다시 커밋하면 된다.

```bash
git rm -r --cached
git add .
git commit -m "leave a message"
```

![스크린샷 2022-05-12 오후 3.17.07](/Users/ssiky/Library/Application Support/typora-user-images/스크린샷 2022-05-12 오후 3.17.07.png)

이런식으로 gitignore에 적었지만, 업로드 되었던 파일들이 삭제가 된다.

***

### 8. querySelector()와 querySelectAll 그리고 getElementById()

| 이름             | 설명                                                         |
| ---------------- | ------------------------------------------------------------ |
| querySelector()  | selector의 구체적인 그룹과 일치하는 document안의 첫번째 엘리먼트를 반환한다. 일치하는게 없으면 null을 반환한다. |
|                  | css 엘리먼트 선택자로 많이 쓰인다. 좀 더 구체적으로 원하는 것을 선택하여 정보를 가져올 수 있다. |
| getElementById() | id를 통해 엘리먼트를 반환한다. document에 해당하는 ID의 엘리먼트가 없으면 null을 반환한다. |
|                  | dom방식이다.                                                 |

아래의 예시코드로 알아보자.

```javascript
<!DOCTYPE html>
<html>
<head>
  <title>getElementByIdExample</title>
	<script>
  	onload = function(){
  		const header = document.getElementById('header');
  		header.style.color='orange';
  		header.style.background='red';
  		header.innerHTML = 'From JavaScript';
		};
  </script>
</head>
<body>
	<h1 id="header">Header</h1>
</body>
</html>
```


```javascript
<!DOCTYPE html>
<html>
<head>
  <title>querySelectorExample</title>
	<script>
  	onload = function(){
  		const header = document.querySelector('h1');
  		header.style.color='orange';
  		header.style.background='red';
  		header.innerHTML = 'From JavaScript';
		};
  </script>
</head>
<body>
	<h1>Header</h1>
	<h1>Header</h1>
	<h1>Header</h1>
</body>
</html>
```
```javascript
<!DOCTYPE html>
<html>
<head>
  <title>querySelectorAllExample</title>
	<script>
  	onload = function(){
  		const headers = document.querySelectorAll('h1');
    	for (const i = 0; i < headers.length; i++){
            const header = headers[i];
              	header.style.color='orange';
		  		header.style.background='red';
  				header.innerHTML = 'From JavaScript';
        }
	};
  </script>
</head>
<body>
	<h1>Header</h1>
	<h1>Header</h1>
	<h1>Header</h1>
</body>
</html>
```



***

### 9. script의 defer

/html을 만나야 script가 실행되기 시작하게 한다. 페이지를 먼저 로드하고 script가 실행됨으로, 페이지를 불러 올 때 빠르게 불러온다는 착각을 주게 할 수 있다.

***

### 10. innerText와 innerHTML의 차이점

element.innerText는 element안의 text값들만 가져온다. 그러나 element.innerHTML은 element안의 HTML이나 XML을 가져온다.

***





