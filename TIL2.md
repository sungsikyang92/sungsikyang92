# 사혼의구슬조각마냥 흩어진 개념들을 

# 빠르게 그리고 정확히 다시 모으자..! 

# 취직해야지..! 더이상 미루는건 없다! 벼랑끝이다.

## 20220523_TIL

#### JSP - Java Server Page

경로는 항상 WebContent 파일 아래에 있다.

html에서 자바언어를 사용할 수 있게 해준다. 그러나 모든 jsp는 서블릿으로 바뀌어서 동작한다. 

'<%@'는 페이지 지시자이다. `out.print(total) = <%=totla%>`

톰캣이 실행될 때, jsp를 servlet으로 바꾸어 실행시켜준다.

##### JSP의 실행순서

1.  브라우저가 웹서버에 JSP에 대한 요청 정보를 전달한다.
2.  브라우저가 요청한 JSP가 최초로 요청했을 경우만 JSP로 작성된 코드가 서블릿으로 코드로 변환한다. (java 파일 생성)
3.  서블릿 코드를 컴파일해서 실행가능한 bytecode로 변환한다. (class 파일 생성)
4.  서블릿 클래스를 로딩하고 인스턴스를 생성한다.
5.  서블릿이 실행되어 요청을 처리하고 응답 정보를 생성한다.

##### JSP 문법

*   JSP 페이지에서는 선언문(Declaration), 스크립트릿(Scriptlet), 표현식(Expression) 이라는 3가지의 스크립트 요소를 제공
    *   선언문(Declaration) - `<%! %>`: 선언문은 JSP 페이지 내에서 필요한 멤버변수나 메소드가 필요할 때 선언해 사용하는 요소
    *   스크립트릿(Scriptlet) - `<% %>`: 프로그래밍 코드 기술에 사용
        *   가장 일반적으로 많이 쓰이는 스크립트 요소
        *   주로 프로그래밍의 로직을 기술할 때 사용
        *   스크립트릿에서 선언된 변수는 지역변수
    *   표현식(Expression) - `<%= %>`: 화면에 출력할 내용 기술에 사용
        *   JSP 페이지에서 웹 브라우저에 출력할 부분을 표현 (즉, 화면에 출력하기 위한 것)
        *   스크립트릿내에서 출력할 부분은 내장객체인 out 객체의 print() 또는 println() 메소드를 사용해서 출력

*   JSP페이지에서 사용할 수 있는 주석
    *   HTML주석, 자바주석, JSP주석
        *   HTML 주석은 <!--로 시작해서 -->로 끝나는 형태
        *   JSP 페이지에서만 사용되며 <%--로 시작해서 --%>로 끝나는 형태
        *   자바 주석은 //, /**/을 사용해서 작성.

##### JSP 내장 객체

-   JSP를 실행하면 서블릿 소스가 생성되고 실행된다.
-   JSP에 입력한 대부분의 코드는 생성되는 서블릿 소스의 _jspService() 메소드 안에 삽입되는 코드로 생성된다.
-   _jspService()에 삽입된 코드의 윗부분에 미리 선언된 객체들이 있는데, 해당 객체들은 jsp에서도 사용 가능하다.
-   response, request, application, session, out과 같은 변수를 내장객체라고 한다.

<img width="2532" alt="스크린샷 2022-05-23 오후 6 29 41" src="https://user-images.githubusercontent.com/71358285/169789205-513ae87a-78ae-4b13-8377-3053f810b1f6.png">

***

##### Scope

![2_5_1_scope_](https://user-images.githubusercontent.com/71358285/169790477-e2da8ea2-ff79-403d-98cb-3d8ce04fc217.jpg)

**4가지 Scope**

-   Application : 웹 어플리케이션이 시작되고 종료될 때까지 변수가 유지되는 경우 사용
    -   웹 어플리케이션이 시작되고 종료될 때까지 변수를 사용할 수 있다.
    -   ServletContext 인터페이스를 구현한 객체를 사용한다.
    -   jsp에서는 application 내장 객체를 이용한다.
    -   서블릿의 경우는 getServletContext()메소드를 이용하여 application객체를 이용한다.
    -   웹 어플리케이션 하나당 하나의 application객체가 사용된다.
    -   값을 저장할 때는 application객체의 setAttribute()메소드를 사용한다.
    -   값을 읽어 들일 때는 application객체의 getAttribute()메소드를 사용한다.
    -   모든 클라이언트가 공통으로 사용해야 할 값들이 있을 때 사용한다.

-   Session : 웹 브라우저 별로 변수가 관리되는 경우 사용
    -   웹 브라우저별로 변수를 관리하고자 할 경우 사용한다.
    -   웹 브라우저간의 탭 간에는 세션정보가 공유되기 때문에, 각각의 탭에서는 같은 세션정보를 사용할 수 있다.
    -   HttpSession 인터페이스를 구현한 객체를 사용한다.
    -   JSP에서는 session 내장 변수를 사용한다.
    -   서블릿에서는 HttpServletRequest의 getSession()메소드를 이용하여 session 객체를 얻는다.
    -   값을 저장할 때는 session 객체의 setAttribute()메소드를 사용한다.
    -   값을 읽어 들일 때는 session 객체의 getAttribute()메소드를 사용한다.
    -   장바구니처럼 사용자별로 유지가 되어야 할 정보가 있을 때 사용한다.

-   Request : http요청을 WAS가 받아서 웹 브라우저에게 응답할 때까지 변수가 유지되는 경우 사용
    -   http 요청을 WAS가 받아서 웹 브라우저에게 응답할 때까지 변수값을 유지하고자 할 경우 사용한다.
    -   HttpServletRequest 객체를 사용한다.
    -   JSP에서는 request 내장 변수를 사용한다.
    -   서블릿에서는 HttpServletRequest 객체를 사용한다.
    -   값을 저장할 때는 request 객체의 setAttribute()메소드를 사용한다.
    -   값을 읽어 들일 때는 request 객체의 getAttribute()메소드를 사용한다.
    -   forward 시 값을 유지하고자 사용한다.
    -   앞에서 forward에 대하여 배울 때 forward 하기 전에 request 객체의 setAttribute() 메소드로 값을 설정한 후, 서블릿이나 jsp에게 결과를 전달하여 값을 출력하도록 하였는데 이렇게 포워드 되는 동안 값이 유지되는 것이 Request scope를 이용했다고 합니다.
-   Page : 페이지 내에서 지역변수처럼 사용
    -   하나의 페이지가 수행될 때까지 값을 저장하고 있는것이 pageScope
    -   PageContext 추상 클래스를 사용한다.
    -   JSP 페이지에서 pageContext라는 내장 객체로 사용 가능 하다.
    -   forward가 될 경우 해당 Page scope에 지정된 변수는 사용할 수 없다.
    -   사용방법은 Application scope나 Session scope, request scope와 같다.
    -   마치 지역변수처럼 사용된다는 것이 다른 Scope들과 다릅니다.
    -   jsp에서 pageScope에 값을 저장한 후 해당 값을 EL표기법 등에서 사용할 때 사용됩니다.
    -   지역 변수처럼 해당 jsp나 서블릿이 실행되는 동안에만 정보를 유지하고자 할 때 사용됩니다.

***

##### [EL (Expression Language)](https://www.boostcourse.org/web326/lecture/258517/?isDesc=false)

Servlet에서 사용되는 자바를 좀 더 간결하고 보기 쉽게 해준다.

EL 문법을 사용하지 않고 문자열 그대로 표시할 때, `<%@ page isELIgnored = "true" %> `

*   scope별 표현 언어의 사용

    *   ```jsp
        <%
            pageContext.setAttribute("p1", "page scope value");
            request.setAttribute("r1", "request scope value");
            session.setAttribute("s1", "session scope value");
            application.setAttribute("a1", "application scope value");
        %>    
        
        pageContext.getAttribute("p1") : ${pageScope.p1 }<br>
        request.getAttribute("r1") : ${requestScope.r1 }<br>
        session.getAttribute("s1") : ${sessionScope.s1 }<br>
        application.getAttribute("a1") : ${applicationScope.a1 }<br>
        <br><br>
        pageContext.getAttribute("p1") : ${p1 }<br>
        request.getAttribute("r1") : ${r1 }<br>
        session.getAttribute("s1") : ${s1 }<br>
        application.getAttribute("a1") : ${a1 }<br>
        ```

***

##### [JSTL(JSP Standard Tag Library)](https://www.boostcourse.org/web326/lecture/258523/?isDesc=false)

*  JSP 안에 자바코드와 HTML코드가 섞여있을때 수정하기 어려움을 느낀다. 이를 해결하기 위해 등장함
*  JSTL(JSP Standard Tag Library)은 JSP 페이지에서 조건문 처리, 반복문 처리 등을 html tag형태로 작성할 수 있게 도와줍니다






arie.kim@sunykorea.ac.kr

## 20220522_TIL

#### HTTP - Hypertext Transfer Protocol

-   HTTP는 서버와 클라이언트가 인터넷상에서 데이터를 주고받기 위한 프로토콜(protocol)입니다.
-   HTTP는 계속 발전하여 HTTP/2까지 버전이 등장한 상태입니다.

#### HTTP 작동방식

-   HTTP는 서버/클라이언트 모델을 따릅니다.
-   장점
    \- 불특정 다수를 대상으로 하는 서비스에는 적합하다.
    \- 클라이언트와 서버가 계속 연결된 형태가 아니기 때문에 클라이언트와 서버 간의 최대 연결 수보다 훨씬 많은 요청과 응답을 처리할 수 있다.
-   단점
    \- 연결을 끊어버리기 때문에, 클라이언트의 이전 상황을 알 수가 없다.
    \- 이러한 특징을 무상태(Stateless)라고 말한다.
    \- 이러한 특징 때문에 정보를 유지하기 위해서 Cookie와 같은 기술이 등장하게 되었다.

#### URL - Uniform Resource Locator

-   인터넷 상의 자원의 위치
-   특정 웹 서버의 특정 파일에 접근하기 위한 경로 혹은 주소

<img width="1081" alt="스크린샷 2022-05-22 오후 7 20 00" src="https://user-images.githubusercontent.com/71358285/169690695-3dfe43dc-7693-4f32-9b64-2e5524162269.png">

<img width="2785" alt="스크린샷 2022-05-22 오후 7 24 12" src="https://user-images.githubusercontent.com/71358285/169690823-e9e20d50-f6a6-4acc-8c36-9d99f8e83707.png">

-   요청 메서드 : GET, PUT, POST, PUSH, OPTIONS 등의 요청 방식이 온다.
-   요청 URI : 요청하는 자원의 위치를 명시한다.
-   HTTP 프로토콜 버전 : 웹 브라우저가 사용하는 프로토콜 버전이다.

첫번째 줄의 요청메소드는 서버에게 요청의 종류를 알려주기 위해서 사용됩니다.

각각의 메소드 이름은 다음과 같은 의미를 가집니다.

참고로 최초의 웹 서버는 GET방식만 지원해줬습니다.

-   GET : 정보를 요청하기 위해서 사용한다. (SELECT)
-   POST : 정보를 밀어넣기 위해서 사용한다. (INSERT)
-   PUT : 정보를 업데이트하기 위해서 사용한다. (UPDATE)
-   DELETE : 정보를 삭제하기 위해서 사용한다. (DELETE)
-   HEAD : (HTTP)헤더 정보만 요청한다. 해당 자원이 존재하는지 혹은 서버에 문제가 없는지를 확인하기 위해서 사용한다.
-   OPTIONS : 웹서버가 지원하는 메서드의 종류를 요청한다.
-   TRACE : 클라이언트의 요청을 그대로 반환한다. 예컨데 echo 서비스로 서버 상태를 확인하기 위한 목적으로 주로 사용한다.

***

#### 웹 프론트엔드

*   사용자에게 웹을 통해 다양한 콘텐츠를 제공한다. 또한, 사용자의 요구사항에 반응해서 동작한다.
*   웹콘텐츠를 잘 보여주기 위해 구조를 만들어야 합니다.(신문,책등과 같이) - HTML
*   적절한 배치와 일관된 디자인 등을 제공해야 합니다.(보기 좋게) - CSS
*   사용자 요청을 잘 반영해야 합니다.(소통하듯이) - Javascript

#### 웹 백엔드

*   정보를 처리하고 저장하며, 요청에 따라 정보를 내려주는 역할을 한다.
*   프로그래밍 언어(JAVA, Python, PHP, Javascript 등)
*   웹의 동작 원리
*   알고리즘(algorithm), 자료구조 등 프로그래밍 기반 지식
*   운영체제, 네트워크 등에 대한 이해
*   프레임워크에 대한 이해(예: Spring)
*   DBMS에 대한 이해와 사용방법(예: MySQL, Oracle 등)

***

#### [Browser](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/#The_rendering_engine)

*   Parsing - 토큰단위로 다 잘라서 의미를 해석하고 의미에 따라서 실행하는것

*   Head - 문서에 대한 자세한 정보들이 포함되어 있다.
*   body - 화면에 표현되어야 할 것들 div..p..등
*   HTML은 계층적으로 존재
*   JS와 CSS가 html안에 여기저기 존재한다.

***

#### 웹서버

-   웹 서버는 소프트웨어(Software)를 보통 말하지만, 웹 서버 소프트웨어가 동작하는 컴퓨터를 말합니다.
-   웹 서버의 가장 중요한 기능은 클라이언트(Client)가 요청하는 HTML 문서나 각종 리소스(Resource)를 전달하는 것입니다.
-   웹 브라우저나 웹 크롤러가 요청하는 리소스는 컴퓨터에 저장된 정적(static)인 데이터이거나 동적인 결과가 될 수 있습니다.

*   클라이언트와 웹서버는 HTTP로 통신. 
*   웹페이지에는 아주 많은 요소들이 있는데, 하나로 합쳐서 보여주는것을 렌더링한다 라고 함.

***

#### WAS - Web Application Server

*   클라이언트는 서비스를 제공하는 서버에게 정보를 요청하여 응답 받은 결과를 사용한다.
*   DBMS는 다수의 사용자가 데이터베이스 내의 데이터에 접근할 수 있도록 해주는 소프트웨어이다.
*   미들웨어 - 클라이언트 쪽에 비즈니스 로직이 많을 경우, 클라이언트 관리(배포 등)로 인해 비용이 많이 발생한다. 비즈니스 로직을 클라이언트와 DBMS사이의 미들웨어 서버에서 동작하도록 함으로써 클라이언트는 입력과 출력만 담당하도록 한다.
*   WAS는 일종의 미들웨어로 웹 클라이언트(브라우저)의 요청 중 웹 어플리케이션이 동작하도록 지원하는 목적을 가진다.
*   **웹 서버 vs WAS**
    -   WAS도 보통 자체적으로 웹 서버 기능을 내장하고 있습니다.
    -   현재는 WAS가 가지고 있는 웹 서버도 정적인 콘텐츠를 처리하는 데 있어서 성능상 큰 차이가 없습니다.
    -   규모가 커질수록 웹 서버와 WAS를 분리합니다.
    -   자원 이용의 효율성 및 장애 극복, 배포 및 유지보수의 편의성을 위해 웹서버와 WAS를 대체로 분리합니다.

***

#### Java Web Application

WAS에 설치되어 동작하는 어플리케이션이다. HTML, CSS, 이미지, 자바로 작성된 클래스, 각종 설정 파일 등이 포함된다. 복잡할 웹어플리케이션일수록 이러한것들이 복잡하고 많이 들어있다.

![](https://cphinf.pstatic.net/mooc/20180124_133/15167752967943AqfC_PNG/1_5_1_____.PNG)



##### Context - server.xml에 등록하는 웹 어플리케이션

*   컨테이너 실행 시 웹 어플리케이션당 하나의 컨텐스트가 생성
*   웹 어플리케이션과 같을 수도 있고 다를 수도 있다.
*   컨텍스트 이름은 중복될 수 없다.
*   명사형으로 지정한다.
*   대소문자를 구분한다.

***

#### Servlet

*   자바 웹 어플리케이션의 구성요소 중 동적인 처리를 하는 프로그램의 역할입니다.

*   서블릿을 정의해보면 서블릿(servlet)은 WAS에 동작하는 JAVA 클래스입니다. 

*   서블릿은 HttpServlet 클래스를 상속받아야 합니다.

*   서블릿과 JSP로부터 최상의 결과를 얻으려면, 웹 페이지를 개발할 때 이 두 가지(JSP, 서블릿)를 조화롭게 사용해야 합니다.

*   예를 들어, 웹 페이지를 구성하는 화면(HTML)은 JSP로 표현하고, 복잡한 프로그래밍은 서블릿으로 구현합니다.

*   response.setContentType() - 응답결과에 어떠한 타입으로 보내줄 것인지 설정해주는 메서드

*   서블릿 생명주기 메서드란 서블릿 실행 단계마다 호출되어 기능을 수행하는 콜백 메서드를 말한다.

    1.   메모리에 없으면 메모리에 올린다 -> lifecycleservlet생성

    2.   init 호출

    3.   service 호출

         *   **service(request, response) 메소드**

             HttpServlet의 service메소드는 템플릿 메소드 패턴으로 구현합니다.

             -   클라이언트의 요청이 GET일 경우에는 자신이 가지고 있는 doGet(request, response)메소드를 호출
             -   클라이언트의 요청이 Post일 경우에는 자신이 가지고 있는 doPost(request, response)를 호출

    4.   새로고침하면 service 호출 - 한번 호출 된 이후에는 service만 호출
    5.   코드 수정 후(어플리케이션 변경) 저장하면 destroy 호출
    6.   웹페이지 새로고침하면 1~3새로 호출

***

#### HttpServletRequest, HttpServletResponse

WAS는 웹 브라우저로부터 Servlet요청을 받으면,

-   요청할 때 가지고 있는 정보를 HttpServletRequest객체를 생성하여 저장합니다.
-   웹 브라우저에게 응답을 보낼 때 사용하기 위하여 HttpServletResponse객체를 생성합니다.
-   생성된 HttpServletRequest, HttpServletResponse 객체를 서블릿에게 전달합니다.

**HttpServletRequest**

-   http프로토콜의 request정보를 서블릿에게 전달하기 위한 목적으로 사용합니다.
-   헤더정보, 파라미터, 쿠키, URI, URL 등의 정보를 읽어 들이는 메소드를 가지고 있습니다.
-   Body의 Stream을 읽어 들이는 메소드를 가지고 있습니다.

**HttpServletResponse**

-   WAS는 어떤 클라이언트가 요청을 보냈는지 알고 있고, 해당 클라이언트에게 응답을 보내기 위한 HttpServleResponse객체를 생성하여 서블릿에게 전달합니다.
-   서블릿은 해당 객체를 이용하여 content type, 응답코드, 응답 메시지등을 전송합니다.

##### getHeaderNames() - 모든 헤더 이름을 문자열 Enumeration 객체로 반환해준다.

## 20220521_TIL

#### **데이터베이스와 데이터베이스 관리 시스템**

-   Q> 데이터베이스와 데이터베이스 관리 시스템을 어린이도 알 수 있을 정도로 설명해주세요.
-   A> 도서관에 있는 책들이 데이터베이스라고 한다면, 도서관 사서분들이나 도서 정보를 찾아주는 컴퓨터를 DBMS라고 볼 수 있습니다.



#### **데이터베이스의 기본개념 (정의)**

-   데이터의 집합 (a Set of Data)
-   여러 응용 시스템(프로그램)들의 통합된 정보들을 저장하여 운영할 수 있는 공용(share) 데이터의 집합
-   효율적으로 저장, 검색, 갱신할 수 있도록 데이터 집합들끼리 연관시키고 조직화되어야 한다.



#### **데이터베이스의 특성**

-   실시간 접근성(Real-time Accessability)
    \- 사용자의 요구를 즉시 처리할 수 있다.

-   계속적인 변화(Continuous Evolution)
    \- 정확한 값을 유지하려고 삽입·삭제·수정 작업 등을 이용해 데이터를 지속적으로 갱신할 수 있다.

-   동시 공유성(Concurrent Sharing)
    \- 사용자마다 서로 다른 목적으로 사용하므로 동시에 여러 사람이 동일한 데이터에 접근하고 이용할 수 있다.

-   내용 참조(Content Reference)
    \- 저장한 데이터 레코드의 위치나 주소가 아닌 사용자가 요구하는 데이터의 내용, 즉 데이터 값에 따라 참조할 수 있어야 한다.



#### **데이터베이스 관리 시스템 (Database Management System = DBMS)**

-   데이터베이스를 관리하는 소프트웨어
-   여러 응용 소프트웨어(프로그램) 또는 시스템이 동시에 데이터베이스에 접근하여 사용할 수 있게 한다
-   필수 3기능
    \- 정의기능 :  데이터 베이스의 논리적, 물리적 구조를 정의
    \- 조작기능 : 데이터를 검색, 삭제, 갱신, 삽입, 삭제하는 기능
    \- 제어기능 :  데이터베이스의 내용 정확성과 안전성을 유지하도록 제어하는 기능
-   Oracle, SQL Server, MySQL, DB2 등의 상용 또는 공개 DBMS가 있다.

  

#### **데이터베이스 관리 시스템의 장/단점**

-   장점
    \- 데이터 중복이 최소화
    \- 데이터의 일관성 및 무결성 유지 
    \- 데이터 보안 보장
-   단점
    \- 운영비가 비싸다
    \- 백업 및 복구에 대한 관리가 복잡
    \- 부분적 데이터베이스 손실이 전체 시스템을 정지

***

#### **MySQL_MAC_OS** >>>> [MySQL DOC](https://dev.mysql.com/doc/refman/5.7/en/create-database.html)

1.   설치

`brew install mysql`

2.   실행

`mysql.server start`

3.   종료

`mysql.server stop`

#### **운영체제의 백그라운드로 MySQL이 계속 실행되도록 하고싶다면?**

*   `brew services start mysql` 데몬형태로 실행
*   `brew services restart mysql` 서비스 재시작
*   `brew services stop mysql`서비스 종료
*   `brew services list`데몬으로 실행되고 있는 프로그램 리스트 

#### **SQL(Structured Query Language)**

-   SQL은 데이터를 보다 쉽게 검색하고 추가, 삭제, 수정 같은 조작을 할 수 있도록 고안된 컴퓨터 언어입니다.
-   관계형 데이터베이스에서 데이터를 조작하고 쿼리하는 표준 수단입니다.
-   DML (Data Manipulation Language): 데이터를 조작하기 위해 사용합니다.
    INSERT, UPDATE, DELETE, SELECT 등이 여기에 해당합니다.
-   DDL (Data Definition Language): 데이터베이스의 스키마를 정의하거나 조작하기 위해 사용합니다.
    CREATE, DROP, ALTER 등이 여기에 해당합니다.
-   DCL (Data Control Language) : 데이터를 제어하는 언어입니다.
    권한을 관리하고, 테이터의 보안, 무결성 등을 정의합니다.
    GRANT, REVOKE 등이 여기에 해당합니다.

#### **MySQL 관리자 계정인 root로 데이터베이스 관리 시스템에 접속**

`mysql -u root -p`

#### **DATABASE 생성하기**

`create database "DB이름"`

#### **DATABASE CREATE USER**

`CREATE USER connectuser@localhost IDENTIFIED BY 'connect123!@#';`

#### **GIVE PRIVILEGES TO USER**

`GRANT ALL PRIVILEGES ON connectdb.* TO 'connectuser'@'localhost';`

#### **MAKING DBMS ACCEPTION**

`FLUSH PRIVILEGES;`

#### **ACCESS TO DB WITH USER**

`mysql -h 127.0.01 -u "USER NAME" -p "DB NAME";` then type password.

If U R using UR laptop -h will be 127.0.0.1

#### **GET MySQL VERSION AND CURRENT DATE**

`SELECT VERSION(), CURRENT_DATE;`

#### **IMPORT sql file to DB at specific user**

`mysql -u "USERNAME" -p "DBNAME" < "FILENAME.sql";` then type password.

#### **CHECKING TABLE'S STRUCTURE**

`desc "TABLENAME";`

#### **데이터 조작어 DML**

*   SELECT

    *   CONCAT - 컬럼을 설정한 문자열로 이어붙여 나오게 해준다.

    `SELECT CONCAT(name, '-', job, '*', salary, 'TEST', boss) 테스트중 from employee;`

    *   LIKE - '%'는 0에서부터 여러 개의 문자열을 나타냄, '_'는 단 하나의 문자를 나타내는 와일드 카드
    *   UPPER(), LOWER()

    `SELECT UPPER(NAME)FROM TABLE`, `SELECT LOWER(NAME) FROM TABLE`

    *   SUBSTRING(문자열, 시작인덱스, 몇글자까지)
    *   LPAD, RPAD

    `SELECT LPAD('HI',5,'?'), RPAD('DAN',10,'K')`

    -   FLOOR(x) : x보다 크지 않은 가장 큰 정수를 반환합니다. BIGINT로 자동 변환합니다.
    -   CEILING(x) : x보다 작지 않은 가장 작은 정수를 반환합니다.
    -   ROUND(x) : x에 가장 근접한 정수를 반환합니다.
    -   POW(x,y) POWER(x,y) : x의 y 제곱 승을 반환합니다.
    -   GREATEST(x,y,...) : 가장 큰 값을 반환합니다.
    -   LEAST(x,y,...) : 가장 작은 값을 반환합니다.
    -   CURDATE(),CURRENT_DATE : 오늘 날짜를 YYYY-MM-DD나 YYYYMMDD 형식으로 반환합니다.
    -   CURTIME(), CURRENT_TIME : 현재 시각을 HH:MM:SS나 HHMMSS 형식으로 반환합니다.
    -   NOW(), SYSDATE() , CURRENT_TIMESTAMP : 오늘 현시각을 YYYY-MM-DD HH:MM:SS나 YYYYMMDDHHMMSS 형식으로 반환합니다. 
    -   DATE_FORMAT(date,format) : 입력된 date를 format 형식으로 반환합니다.
    -   PERIOD_DIFF(p1,p2) : YYMM이나 YYYYMM으로 표기되는 p1과 p2의 차이 개월을 반환합니다.

*   INSERT

*   UPDATE

    `UPDATE 테이블명 SET 필드1=필드1의값, 필드2=필드2의값... WHERE 조건식`

*   DELETE

​	`DELETE FROM 테이블명 WHERE 조건식`

#### **데이터 정의어 DDL**

*   컬럼추가

    `alter table 테이블명 add  필드명 타입 [NULL | NOT NULL][DEFAULT ][AUTO_INCREMENT];`

*   컬럼삭제

​	`alter table 테이블명 drop 필드명`

*   테이블 이름 변경

​	`alter table  테이블명 rename 변경이름`

***

### Maven

애플리케이션을 개발하기 위해 반복적으로 진행해왔떤 작업들을 지원하기 위하여 등장한 도구이다. 이것으로 빌드, 패키징, 문서화, 테스트, 의존성관리 등 형상관리서버와 연동, 배포등의 작업을 손쉽게 할 수 있다.

Maven 전에 CoC를 알아야하는데, 이것을 예를 들자면 프로그램의 소스파일은 어떤 위치에 있어야 하고, 소스가 컴파일된 파일들은 어떤 위치에 있어야하는지를 미리 정해놨다는 것이다.

Maven을 사용함으로써 설정 파일에 몇 줄 적어서, 직접 다운로드 받거나 하지 않아도 라이브러리를 사용할 수 있다.

또한 Maven에 설정한 대로 모든 개발자가 일관된 방식으로 빌드를 수행할 수 있다. 

***

### JDBC - Java Database Connectivity

*   자바를 이용한 데이터베이스 접속과 SQL 문장의 실행, 그리고 실행 결과로 얻어진 데이터의 핸들링을 제공하는 방법과 절차에 관한 규악

#### **JDBC를 이용한 프로그래밍 방법**

1.  import java.sql.*;
2.  드라이버를 로드 한다.
3.  Connection 객체를 생성한다.
4.  Statement 객체를 생성 및 질의 수행
5.  SQL문에 결과물이 있다면 ResultSet 객체를 생성한다.
6.  모든 객체를 닫는다.

![](https://cphinf.pstatic.net/mooc/20180201_49/1517475141729UGWfv_PNG/2_11_1_JDBC_.PNG)