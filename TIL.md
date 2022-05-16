# TODAY I LEARNED - 20220515

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

### 3. @ResponseBody









***

***





# TODAY I LEARNED - 20220514

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

### 2. JPA 제공 어노테이션

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
     *   기본 생성자 자동 추가해주는 역할
6.   @Getter
     *   클래스 내 모든 필드의 Getter 메소드를 자동생성
7.   @Builder
     *   해당 클래스의 빌더 패턴 클래스를 생성
     *   생성자 상단에 선언 시 생성자에 포함된 빌드만 빌더에 포함한다.

***

### 3. Entity 클래스에서는 절대 Setter 메소드를 만들지 않는다.

대신 해당 필드의 값 변경이 필요하면 명확히 그 목적과 의도를 나타낼 수 있는 메소드를 추가해야한다.

생성자를 통해 최종값을 채운 후 DB에 삽입한다. 값 변경이 필요한 경우 해당 이벤트에 맞는 public 메소드를 호출하여 변경한다.

***

### 4. 어노테이션들

1.   @RestController
     *   이 어노테이션을 사용하여 컨트롤러를 JSON형식으로 반환하는 컨트롤러로 만들어준다.
2.   @GetMapping
     *   HTTP Method인 Get의 요청을 받을 수 있는 API를 만들어 준다.
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

*   @ResponseBody

컨트롤러의 특정 메서드에 @ResponseBody를 적용하면 JSP가 아닌 텍스트나 JSON으로 결과를 전송할 수 있다.

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





