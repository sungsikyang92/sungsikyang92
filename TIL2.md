# 사혼의구슬조각마냥 흩어진 개념들을 

# 빠르게 그리고 정확히 다시 모으자..! 

# 취직해야지..! 더이상 미루는건 없다! 벼랑끝이다.

# [발생에러목록과해결과정(계속 반복되니 기록해놓자)](https://github.com/sungsikyang92/sungsikyang92/blob/main/Error_Process.md)

# 20220616_TIL





# 20220615_TIL

## Connection Pool

최초 연결에 따른 응답 속도 저하와 동시 접속자가 많을 때 발생하는 부하를 줄이기 위해 사용하는 것이 커넥션 풀이다. 커넥션 풀은 일정 개수의 DB커넥션을 미리 만들어두는 기법이다. DB 커넥션이 필요한 프로그램은 커넥션 풀에서 커넥션을 가져와 사용한 뒤 커넥션을 다시 풀에 반납한다. 커넥션을 미리 생성해두기 때문에 커네션을 사용하는 시점에서 커넥션을 생성하는 시간을 아낄수 잇다. 또한 동시 접속자가 많더라도 커넥션을 생성하는 부하가 적기 때문에 더 많은 동시 접속자를 처리할 수 있다. 커넥션도 일정 개수로 유지해서 DBMS에 대한 부하를 일정 수준으로 유지할 수 있게 해준다.

[프로퍼티들 살펴보기](https://tomcat.apache.org/tomcat-8.5-doc/jdbc-pool.html)

# 20220613_TIL

## MyBatis에서의 LocalDateTime

Dto에서 자료형을 LocalDateTime으로 설정했을때, 날짜를 인식하지 못하는 문제가 있었다. 

LocalDateTimeTypeHandler에 @MappedType(LocalDateTime.class)를 어노테이션 설정해주면 된다고 한다. 그러나 내가 이 페이지에 들어갔을때 수정을 할 수가 없었다. 그래서 Date로 자료형을 변경해서 했다.





# 20220609_TIL

**HiddenHttpMethodFilter**

Hidden 타입의 input 태그의 속성들을 읽어서 HttpServletRequestWrapper.getMethod() 반환 값을 변경해 요청된 HTTP 메소드의 타입을 PUT, DELETE, PATCH로 변경해주는 필터이다.



# 20220608_TIL

## 다양한 의존관계 주입 방법

*   생성자 주입
    *   생성자를 통해서 의존 관계를 주입받는 방법이다. 제일 권장되는 방법이다!
    *   특징
        *   생성자 호출시점에 딱 1번만 호출되는 것이 보장된다.
        *   **불변, 필수** 의존관계에 사용
            *   불변
                *   대부분의 의존관계 주입은 한번 일어나면 어플리케이션 종료시점까지 의존관계를 변경할 일이 없다. 대부분의 의존관계는 어플리케이션 종료 전까지 변하면 안된다(불변해야한다.)
                *   수정자 주입을 사용시, setXXX메서드를 public으로 열어두어야 하는데, 이는 누군가 실수로 변경할 수도 있고 변경하면 안되는 메서드를 열어두는 것은 좋은 설계 방법이 아니다.
                *   생성자 주입은 객체를 생성할 때 딱 1번만 호출됨으로 이후에 호출할 일이 없어서 불변하게 설계할 수 있다.
                *   **final 키워드**
                    *   생성자에서 혹시라도 값이 설정되지 않는 오류를 컴파일 시점에 막아준다.
        *   생성자가 딱 하나 있을 경우 @Autowired 생략해도 된다.
*   수정자 주입(setter 주입)
    *   seeter라 불리는 필드의 값을 변경하는 수정자 메서드를 통해서 의존관계를 주입하는 방법이다.
    *   특징
        *   **선택, 변경** 가능성이 있는 의존관계에 사용
        *   자바빈 프로퍼티 규약의 수정자 메서드 방식을 사용하는 방법이다.
*   필드 주입
    *   특징
        *   코드가 간결해서 많은 개발자들을 유혹하지만 외부에서 변경이 불가능해서 테스트 하기 힘들다는 치명적인 단점이 있다.
        *   DI 프레임워크가 없으면 아무것도 할 수 없다.
        *   사용을 권장하지 않는다.
            *   그러나
            *   테스트코드, 혹은 스프링 설정을 목적으로 하는 @Configuration같은 곳에서만 특별한 용도로 사용
*   일반 메서드 주입
    *   특징
        *   한번에 여러 필드를 주입 받을 수 있다.
        *   일반적으로 잘 사용하지 않는다.

***

## LOMBOK

### @RequiredArgsConstructor

생성자를 자동으로 생성해줌에 있어서, final이 붙은 인자를 필수로 사용한다.

## 빈 생명주기와 콜백

## 빈 스코프

스프링은 다양한 스코프를 지원한다.

*   싱글톤 : 기본 스코프, 스프링 컨테이너의 시작과 종료까지 유지되는 가장 넓은 범위의 스코프다.
*   프로토타입 : 스프링 컨테이너는 프로토타입 빈의 생성과 의존관계 주입까지만 관여하고 더는 관리하지 않는 매우 짧은 범위의 스코프이다.
*   웹 관련 스코프
    *   request : 웹 요청이 들어오고 나갈때 까지 유지되는 스코프
    *   session : 웹 세션이 생성되고 종료될 떄 까지 유지되는 스코프
    *   application : 웹의 서블릿 컨텍스와 같은 범위로 유지되는 스코프

### Dependency Lookup(DL) 의존관계 조회(탐색)

*   ObjectFactory - 기능이 단순, 별도의 라이브러리가 필요 없음, 스프링에 의존
*   ObjectProvider - ObjectFactory 상속, 옵션, 스트림 처리 등 편의 기능이 많고, 별도의 라이브러리 필요 없음, 스프링에 의존

### JSR-330 Provider

*   provider의 get()을 호출하면 내부에서는 스프링 컨테이너를 통해 해당 빈을 찾아서 반환한다.(DL)
*   자바 표준이고, 기능이 단순하므로 단위테스트를 만들거나 mock코드를 만들기 훨씬 쉬워진다.
*   딱 필요한 DL 정도의 기능만 제공한다.
*   특징
    *   get() 메서드 하나로 기능이 매우 단순하다.
    *   별도의 라이브러리가 필요하다
    *   자바 표준이므로 스프링이 아닌 다른 컨테이너에서도 사용할 수 있다.

#### 프로토타입 빈을 언제 사용할까?

매번 사용할 때 마다 의존관계 주입이 완료된 새로운 객체가 필요할 때 사용한다.

***

## 웹 스코프

*   특징
    *   웹 스코프는 웹 환경에서만 동작한다.
    *   웹 스코프는 프로토타입과 다르게 스프링이 해당 스코프의 종료시점까지 관리한다. 따라서 종료 메서드가 호출된다.
*   종류
    *   request: HTTP 요청 하나가 들어오고 나갈 때 까지 유지되는 스코프, 각각의 HTTP 요청마다 별도의 빈 인스턴스가 생성되고, 관리된다.
    *   session: HTTP Session과 동일한 생명주기를 가지는 스코프
    *   application: 서블릿 컨텍스트(ServletContext)와 동일한 생명주기를 가지는 스코프
    *   websocket: 웹 소켓과 동일한 생명주기를 가지는 스코프

만약 기본 포트인 8080 포트를 다른곳에서 사용중이어서 오류가 발생한다면, 8080을 실행중지시키고 다시 실행하거나 포트를 변경해야한다. 포트를 9090으로 변경한다면 `main/resources/application.properties`에 `server.port=9090` 설정을 추가해주자.

*   UUID를 사용해서 HTTP요청을 구분한다. 전세계 아이디 1개 만들어지는것이다. 같을 확률이 로또 당첨보다 희박하다한다.









# 20220607_TIL

## IoC, DI, 컨테이너

### 제어의 역전IoC(Inversion of Control)

*   프로그램의 제어 흐름을 직접 제어하는 것이 아니라 외부에서 관리하는 것을 제어의 역전(IoC)이라 한다.
*   프로그램에 대한 제어 흐름은 모두 AppConfig가 가지고 있다. 

**프레임워크 vs 라이브러리**

*   프레임워크가 내가 작성한 코드를 제어하고, 대신 실행하면 그것은 프레임워크가 맞다.(Junit)
*   반면에 내가 작성한 코드가 직접 제어의 흐름을 담당하면 그것은 라이브러리다.

### 의존관계 주입DI(Dependency Injection)

*   의존관계는 *정적인 클래스 의존 관계와, 실행 시점에 결정되는 동적인 객체 의존 관계* 둘을 분리해서 생각해야 한다.

    *   정적인 클래스 의존관계
        *   클래스가 사용하는 import코드만 보고 의존관계를 쉽게 판단할 수 있다. 정적인 의존관계는 애플리케이션을 실행하지 않아도 분석할 수 있다.

    *   동적인 클래스 의존관계
        *   애플리케이션 실행 시점에 실제 생성된 객체 인스턴스의 참조가 연결된 의존 관계다.
        *   애플리케이션 *실행시점(런타임)*에 외부에서 실제 구현 객체를 생성하고 클라이언트에 전달해서 클라이언트와 서버의 실제 의존관계가 연결되는 것을 *의존관계주입*이라 한다.
        *   객체 인스턴스를 생성하고, 그 참조값을 전달해서 연결된다.
        *   의존관계 주입을 사용하면 클라이언트 코드를 변경하지 않고, 클라이언트가 호출하는 대상의 타입 인스턴스를 변경할 수 있다.
        *   의존관계 주입을 사용하면 정적인 클래스 의존관계를 변경하지 않고, 동적인 객체 인스턴스 의존관계를 쉽게 변경할 수 있다.

### Ioc컨테이너, DI컨테이너

*   AppConfig처럼 객체를 생성하고 고나리하면서 의존관계를 연결해 주는 것을 Ioc컨테이너 또는 DI컨테이너라 한다.
*   의존관계 중비에 초점을 맞추어 최근에는 주로 DI컨테이너라고 한다.

***

## @Configuration - 설정정보, AppConfig에 설정을 구성한다는 뜻

## @Bean - 스프링 컨테이너에 스프링 빈으로 등록한다.

## ApplicationContext

*   스프링 컨테이너라 한다. 그리고 이는 인터페이스이다.
*   스프링 컨테이너는 @Configuration이 붙은 AppConfig를 설정 정보로 사용하고, @Bean이라 적힌 메서드를 모두 호출해서 반환된 객체를 스프링 컨테이너에 등록한다.

# BeanFactory

*   스프링 컨테이너의 최상위 인터페이스다.
*   스프링 빈을 관리하고 조회하는 역할을 담당한다.
*   **ApplicationContext**
    *   BeanFactory기능을 모두 상속받아서 제공한다.
    *   메세지소스를 활용한 국제화기능
    *   환경변수
        *   로컬, 개발, 운영등을 구분해서 처리
    *   애플리케이션 이벤트
        *   이벤트를 발행하고 구독하는 모델을 편리하게 지원
    *   편리한 리소스 조회
        *   파일,클래스패스,외부 등에서 리소스를 편리하게 조회

## BeanDefinition

*   역할과 구현을 개념적으로 나눈 것으로, 설정 메타 정보라고 한다.
*   스프링 컨테이너는 자바코드인지, xml인지 몰라도 되며, 오직 BeanDefinition만 알면 된다.
*   스프링 컨테이너는 BeanDefinition의 메타정보를 기반으로 스프링 빈을 생성한다.
    *   BeanClassName - 생성할 빈의 클래스 명(자바 설정 처럼 팩토리 역할의 빈을 사용하면 없음)
    *   factoryBeanName - 팩토리 역할의 빈을 사용할 경우 이름, 예)appConfig
    *   factoryMethodName - 빈을 생성할 팩토리 메서드 지정, 예)memberService
    *   Scope - 싱글톤(기본값)
    *   lazyInit - 스프링 컨테이너를 생성할 때 빈을 생성하는 것이 아니라, 실제 빈을 사용할 때 까지 최대한 생성을 지연처리 하는지 여부
    *   InitMethodName - 빈을 생성하고, 의존관계를 적용한 뒤에 호출되는 초기화 메서드 명
    *   DestroyMethodName - 빈의 생명주기가 끝나서 제거하기 직전에 호출되는 메서드 명
    *   Constructor arguments, Properties - 의존관계 주입에서 사용한다(자바 설정처럼 팩토리 역할의 빈을 사용하면 없음)

***

## 웹 어플리케이션과 싱글톤

*   스프링은 태생이 기업용 온라인 서비스 기술을 지원하기 위해 탄생
*   웹 어플리케이션은 보통 여러 고객이 동시에 요청을 한다.

스프링 없이 만들었던 순수한 DI 컨테이너인 AppConfig는 요청을 할 때 마다 객체를 새로 생성한다. 이는 고객 트래픽이 초당 100이 나온다면 초당 100개가 생성되고 소멸된다. 즉, 메모리 낭비가 심하다. 해결방안은 해당 객체가 딱 1개만 생성되고, 공유하도록 설계하면 되는데 이것이 바로 싱클톤 패턴이다.

### 싱글톤 패턴

*   클래스의 인스턴스가 딱 1개만 생성되는 것을 보장하는 디자인 패턴이다.
*   private생성자를 사용해서 외부에서 임의로 new 키워드를 사용하지 못하도록 막아야 한다.

### 싱글톤 패턴의 문제점들

*   싱글톤 패턴을 구현하는 코드 자체가 많이 들어간다.
*   의존관계상 클라이언트가 구체 클래스에 의존한다 -> DIP 위반
*   클라이언트가 구체 클래스에 의존해서 OCP원칙을 위반할 가능성이 높다.
*   테스트하기 어렵다
*   내부 속성을 변경하거나 초기화하기 어렵다.
*   private생성자로 자식 클래스를 만들기 어렵다.
*   유연성이 떨어진다.

## 싱글톤 컨테이너

*   싱글톤 컨테이너는 스프링 컨테이너라고도 불리우며 이는 싱글톤 패턴의 문제점(위의 문제점들)을 해결하면서, 객체 인스턴스를 싱글톤으로 관리한다.
    *   싱글톤 패턴을 위한 지저분한 코드가 들어가지 않아도 된다.
    *   DIP, OCP, 테스트, private ㅅ애성자로 부터 자유롭게 싱글톤을 사용할 수 있다.

## 싱글톤 방식의 주의점

*   싱글톤 객체는 상태를 유지(stateful)하게 설계하면 안된다.
*   무상태(stateless)로 설계해야 한다.
    *   특정 클라이언트에 의존적인 필드가 있으면 안된다.
    *   특정 클라이언트가 값을 변경할 수 있는 필드가 있으면 안된다.
    *   가급적 읽기만 가능해야 한다.
    *   필드 대신에 자바에서 공유되지 않는, 지역변수, 파라미터, ThreadLocal등을 사용해야 한다.
*   스프링 빈의 필드에 공유 값을 설정하면 정말 큰 장애가 발생할 수 있다.

***

## ComponentScan

*   basePackages : 탐색할 패키지의 시작 위치를 지정한다. 이 패키지를 포함해서 하위 패키지를 모두 탐색한다.
*   basePackageClasses : 지정한 클래스의 패키지를 탐색 시작 위로 지정한다.
*   지정하지 않으면 @ComponentScan이 붙은 설정 정보 클래스의 패키지가 시작 위치가 된다.

### 컴포넌트 스캔 기본 대상

*   @Component 
*   @Controller - 스프링 MVC 컨트롤러로 인식
*   @Service - 특별한 처리가 없다. 그러나 핵심 비즈니스 로직이 여기에 있겠구나 하고 알 수 있다.
*   @Repository - 스프링 데이터 접근 계층으로 인식하고, 데이터 계층의 예외를 스프링 예외로 변환해준다.
*   @Configuration - 스프링 설정 정보로 인식하고, 스프링 빈이 싱글톤을 유지하도록 추가 처리를 한다.

## FilterType 옵션

*   ANNOTATION: 기본값, 어노테이션을 인식해서 동작한다.
*   ASSIGNABLE_TYPE: 지정한 타입과 자식 타입을 인식해서 동작한다.
*   ASPECTJ: AspectJ 패턴 사용
*   REGEX: 정규 표현식
*   CUSTOM: TypeFilter라는 인터페이스를 구현해서 처리

**그러나 스프링 부트는 컴포넌트 스캔을 기본으로 제공하며, 개인적으로 옵션을 변경하면서 사용하기 보다는 스프링의 기본 설정에 최대한 맞추어 사용하는 것을 권장하고, 선호한다.**









# 20220606_TIL

**영한이형! 강의 다시 시작**

### concurrentHashMap

*   동시성이슈로 사용한다.

***

### Test

테스트를 위해서 테스트 패키지에 패키지와 테스트클래스를 만들어서 @Test 테스트어노테이션을 붙여준다.

1.   given
2.   when
3.   then

의 방식으로 테스트코드를 작성해주면 보기 쉽다.

테스트는 항상 테스트가 통과하지 않는 경우도 만들어서 확인해보아야한다.

## SOLID - 좋은 객체 지향 설계의 5가지 원칙

*   SRP(single responsibility principle) - 단일 책임 원칙
    *   **한 클래스는 하나의 책임만 가져야 한다.**
    *   변경이 있을 때 파급 효과가 적으면 단일 책임 원칙을 잘 따른 것
*   OCP(open/close principle) - 개방 폐쇄 원칙
    *   **소프트웨어 요소는 확장에서는 열려있으나 변경에는 닫혀 있어야 한다.**
    *   다형성을 활용
    *   인터페이스를 구현한 새로운 클래스를 하나 만들어서 새로운 기능을 구현
    *   문제점은 객체를 생성하고, 연관관계를 맺어주는 별도의 조립, 설정자가 필요하다 (**SPRING CONTAINER**)
*   LSP(liskov subsititution principle) - 리스코프 치환 원칙
    *   하위 클래스는 인터페이스 규약을 다 지켜야 한다.
*   ISP(Interface segregation principle) - 인터페이스 분리 원칙
    *   인터페이스가 명확해지고, 대체 가능성이 높아진다.
    *   적당한 사이즈로 다 분리되어야 한다.
*   DIP(dependency inversion principle) - 의존관계 역전 원칙
    *   **추상화에 의존해야지, 구체화에 의존하면 안된다.** 즉 구현 클래스에 의존하지 말고, 인터페이스에 의존하라는 뜻
    *   의존성 주입은 이 원칙을 따르는 방법 중 하나이다.
    *   ex) Service 클라이언트가 구현 클래스를 직접 선택하면 DIP 위반이다.

#### SOLD 정리

*   객체 지향의 핵심은 다형성
*   다형성만으로는 쉽게 부품을 갈아 끼우듯이 개발할 수 없다.
*   다형성만으로는 구현 객체를 변경할 떄 클라이언트 코드도 함께 변경된다.
*   다형성만으로는 OCP,DIP를 지킬 수 없다.





# 20220604_TIL

### SQL_ORDER BY 다중정렬

`ORDER BY 필드1, 필드2` 의 형태로 정렬하면 된다.





# 20220601_TIL

### 인터셉터(Intercepter)

*   Dispatcher Servlet에서 Handler(Controller)로 요청을 보낼때, 또는 응답을 보낼 때 동작한다.
*   인터셉터 작성법
    -   org.springframework.web.servlet.HandlerInterceptor 인터페이스를 구현합니다.
    -   org.springframework.web.servlet.handler.HandlerInterceptorAdapter 클래스를 상속받습니다.
    -   Java Config를 사용한다면, WebMvcConfigurerAdapter가 가지고 있는 addInterceptors 메소드를 오버라이딩하고 등록하는 과정을 거칩니다.
    -   xml 설정을 사용한다면, <mvc:interceptors> 요소에 인터셉터를 등록합니다.

<img width="418" alt="image" src="https://user-images.githubusercontent.com/71358285/171334739-393ecd1f-66af-408b-ba74-e5b0e1373e4f.png">

### Argument Resolver

*   컨트롤러의 메소도의 인자로 사용자가 임의의 값을 전달하는 방법을 제공하고자 할 때 사용된다.
*   ex) 세션에 저장되어 있는 값 중 특정 이름의 값을 메소드 인자로 전달한다.

**아규먼트 리졸버 작성방법 1/2**

-   org.springframework.web.method.support.HandlerMethodArgumentResolver를 구현한 클래스를 작성합니다.
-   supportsParameter메소드를 오버라이딩 한 후, 원하는 타입의 인자가 있는지 검사한 후 있을 경우 true가 리턴되도록 합니다.
-   resolveArgument메소드를 오버라이딩 한 후, 메소드의 인자로 전달할 값을 리턴합니다.



**아규먼트 리졸버 작성방법 2/2**

-   Java Config에 설정하는 방법
    \- WebMvcConfigurerAdapter를 상속받은 Java Config 파일에서 addArgumentResolvers 메소드를 오버라이딩 한 후 원하는 아규먼트 리졸버 클래스 객체를 등록합니다.
-   xml 파일에 설정하는 방법

```xml
<mvc:annotation-driven>
	<mvc:argument-resolvers>
    	<bean class="ArgumentResolverClass"></bean>
    </mvc:argument-resolvers>
</mvc:annotation-driven>
```

1.   HeaderInfo.java
2.   HeaderMapArgumentResolver.java
3.   WebMvcContextConfiguration클래스에 addArgumentResolvers메소드를 오버라이딩, 인자로 넘어온 argumentResolvers에 생성한 아규먼트 리졸버를 넘긴다.
4.   Controller의 메소드인 list메소드의 인자로 HeaderInfo를 추가
5.   마지막 확인으로 콘솔에 headerInfo의 get메소드에 user-agent를 넘겨서 값이 잘 출력되는지 확인

이에 대해서는 이 [블로그](https://blog.neonkid.xyz/238)를 참조

***

### Logging

*   정보를 제공하는 일련의 기록인 log를 생성하도록 시스템을 작성하는 활동이다.
*   로그가 제공하는 정보의 양은, 이상적으로는 프로그램이 실행되는 중에도, 설정 가능해야 한다.
*   일반적인 로그 기록의 이점으로는
    *   재현하기 힘든 버그에 대한 유용한 정보를 제공할 수 있다.
    *   성능에 관한 통계와 정보를 제공할 수 있다. - ex)구문들 사이에 걸리는 시간
    *   설정이 가능할 때, 로그는 예기치 못한 특정 문제들을 디버그 하기 위해, 그 문제들을 처리하도록 코드를 수정하여 다시 적용하지 않아도, 일반적인 정보를 갈무리할 수 있게 한다.

**로그를 출력하는 방법**

*   System.out.print() 이용
*   로깅 라이브러리 이용
    *   java.util.logging
        -   JDK 1.4부터 포함된 표준 로깅 API
        -   별도 라이브러리 추가 불필요
        -   기능이 많이 부족해 다른 로그 라이브러리를 더 많이 사용
    *   Apache Commons logging
        -   아파치 재단에 Commons 라이브러리 중에 로그 출력을 제공하는 라이브러리
    *   Log4j
        -   아파치 제단에서 제공하며 가장 많이 사용되는 로깅 라이브러리
    *   Logback
        -   Log4j를 개발한 Ceki Gulcu가 Log4j의 단점 개선 및 기능을 추가하여 개발한 로깅 라이브러리

***

### SLF4J - Simple Logging Facade for Java

*   로깅 Facade이다. - Facade는 소프트웨어의 커다란 코드 부분에 대하여 간략화된 인터페이스를 제공해주는 디자인 패턴을 의미한다.

[SLF4J를 이용해 로깅 라이브러리 사용하기](https://www.boostcourse.org/web326/lecture/59006/?isDesc=false)<sub>출처 - 네이버 부스트코스</sub>

***

### 파일 업로드 & 다운로드

#### Multipart

*   웹 클라이언트가 요청을 보낼 때 HTTP 프로토콜의 바디 부분에 데이터를 여러 부분으로 나눠서 보내는 것이다. 보통 파일을 전송할 때 사용한다.

*   HttpServletRequest는 파일업로드를 지원하지 않으므로, 파일 업로드를 처리하려면 별도의 라이브러리를 사용해야 한다. 대표적으로 아파치의 commons-fileupload가 있다.

*   #### Spring MVC에서 파일을 업로드하려면 

     1. 아래의 라이브러리 추가

    ```xml
    <dependency>
    <groupId>commons-fileupload</groupId>
    <artifactId>commons-fileupload</artifactId>
    <version>1.2.1</version>
    </dependency>
    <dependency>
    <groupId>commons-io</groupId>
    <artifactId>commons-io</artifactId>
    <version>1.4</version>
    </dependency>
    ```

    2.   MultipartResolver Bean을 추가

    ```java
    @Bean
    public MultipartResolver multipartResolver() {
    org.springframework.web.multipart.commons.CommonsMultipartResolver multipartResolver = new org.springframework.web.multipart.commons.CommonsMultipartResolver();
    multipartResolver.setMaxUploadSize(10485760); // 1024 * 1024 * 10
    return multipartResolver;
    }
    ```

    3.   파일 업로드 폼
         *   enctpye을 반드시 확인해야한다.

    ```jsp
    <form method="post" action="/upload"
                  enctype="multipart/form-data">
    ......
    <input type="file" name="file">
    <input type="submit">
    </form>
    ```

    4.   Controller 업로드 처리

    *   @PostMapping 사용
    *   업로드 파일이 하나일 경우 `@RequestParam("file") MultipartFile file`
    *   업로드 파일이 여러 개일 경우 `@RequestParam("file") MultipartFile[] files`
    *   MultipartFile의 메소드를 이용해서 파일 이름, 파일 크기 등을 구하고 InputStream을 얻어 파일을 서버에 저장한다.

    5.   Controller 다운로드 처리

    ```java
    response.setHeader("Content-Disposition", "attachment; filename=\"" + fileName + "\";");
    response.setHeader("Content-Transfer-Encoding", "binary");
    response.setHeader("Content-Type", contentType);
    response.setHeader("Content-Length", fileLength;
    response.setHeader("Pragma", "no-cache;");
    response.setHeader("Expires", "-1;");
    ```

    





# 20220531_TIL

### PasswordEncoder를 Bean에 등록하는 이유

*   spring security를 이용해서 로그인 처리를 하기 위해서 반드시 암호가 인코딩 되어있어야만 올바르게 작동이 된다.

스프링시큐리티 어렵다..





# 20220530_TIL

### 웹에서의 상태 유지 기술

*   HTTP 프로토콜은 상태 유지가 안되는 프로토콜이다.

*   상태 유지를 위해 Cookie와 Session기술이 있다.

    *   Cookie

        *   클라리언트 단에 저장되는 작은 정보의 단위로 사용자 컴퓨터에 저장

        *   클라이언트에서 생성하고 저장될 수 있고, 서버 단에서 전송한 쿠키가 클라이언트에 저장될 수 있다.

        *   저장된 정보를 다른 사람 또는 시스템이 볼 수 있는 단점

        *   유효시간이 지나면 사라짐

        *   쿠키의 동작 이해

            1.   웹 클라이언트에서 요청을 WAS로 보낸다.
            2.   WAS 에서 쿠키생성
            3.   WAS에서 쿠키를 포함한 응답은 웹클라이언트로 보낸다.
            4.   웹클라이언트에서 쿠키를 포함한 요청을 WAS에게 한다.
            5.   WAS가 쿠키를 받아서 검사한다.

        *   쿠키는 이름과 값 쌍으로 정보를 저장한다. 이 외에도 도메인, 경로, 유효기간maxAge, Expires, 보안(Secure), HttpOnly 속성을 저장할 수 있다.

            ##### javax.servlet.http.Cookie

            **서버에서 쿠키 생성, Response의 addCookie메소드를 이용해 클라이언트에게 전송**

            ```java
            Cookie cookie = new Cookie(이름, 값);
            response.addCookie(cookie);
            ```

            *   쿠키는 (name, value)의 쌍 정보를 입력하여 생성한다.

            *   쿠키의 이름은 일반적으로 알파벳과 숫자, 언더바로 구성한다. 

            **클라이언트가 보낸 쿠키 정보 읽기**

            `Cookie[] cookies = request.getCookies();`

            *   쿠키 값이 없으면 null이 반환된다.
            *   Cookie가 가지고 있는 getName()과 getValue()메소드를 이용해서 원하는 쿠키 정보를 찾아 사용한다.

            **클라이언트에게 쿠키 삭제 요청**

            *   쿠키를 삭제하는 명령은 없다, 대신 maxAge가 0인 같은 이름의 쿠키를 전송한다.

            ```java
            Cookie cookie = new Cookie("이름", null);
            cookie.setMaxAge(0);
            response.addCookie(cookie);
            ```

            **쿠키의 유효기간 설정**

            *   메소드 setMaxAge()
                *   인자는 유효기간을 나타내는 초 단위의 정수형
                *   만일 유효기간을 0으로 지정하면 쿠키의 삭제
                *   음수를 지정하면 브라우저가 종료될 때 쿠키가 삭제
            *   유효기간을 10분으로 지정하면
                *   cookie.setMaxAge(10 * 60)

        #### Spring MVC에서의 Cookie 사용

        *   @CookieValue 어노테이션 사용
            *   컨트롤러 메소드의 파라미터에서 CookieValue어노테이션을 사용함으로써 원하는 쿠키정보를 파라미터 변수에 담아 사용할 수  있다.
            *   컨트롤러메소드`(@ CookieValue(value="쿠키이름", required=false, defaultValue="기본값")String 변수명)`



*   Session
    *   클라이언트 별로 서버에 저장되는 정보가 세션이다.
    *   서버가 종료되거나 유효시간이 지나면 사라진다.
    *   세션의 동작 이해
        1.   웹 클라이언트가 서버측에 요청을 보내게 되면 서버는 클라이언트를 식별하는 session id를 생성한다.
        2.   서버는 session id를 이용해서 key와 value를 이용한 저장소인 HttpSession을 생성한다.
        3.   서버는 session id를 저장하고 있는 쿠키를 생성하여 클라이언트에 전송한다.
        4.   클라이언트는 서버측에 요청을 보낼때 session id를 가지고 있는 쿠키를 전송한다.
        5.   서버는 쿠키에 있는 session id를 이용해서 그 전 요청에서 생성한 HttpSession을 찾고 사용한다.

    ##### 세션 생성 및 얻기

    ```java
    HttpSession session = request.getSession();
    HttpSession session = request.getSession(true);
    ```

    *   reqeust의 getSession()메소드는 서버에 생성된 세션이 있다면 세션을 반환하고 없다면 새롭게 세션을 생성하여 반환한다.
    *   새롭게 생성된 세션인지 알아보는 메서드는 HttpSession이 가지고 있는 isNew()메서드이다.

    `HttpSession session = request.getSession(false);`

    *   request의 getSession()메소드에 파라미터로 false를 전달하면, 이미 생성된 세션이 있다면 반환하고 없으면 null을 반환한다.

    ##### 세션에 값 저장

    `setAttribute(String name, Object value)`

    *   name과 value의 쌍으로 객체 Object를 저장하는 메소드이다.
    *   세션이 유지되는 동안 저장할 자료를 저장한다.

    `session.setAttribute(이름, 값)`

    ##### 세션에 값 조회

    getAttribute(String name)메소드

    *   세션에 저장된 자료는 다시 getAttribute(String name)메소드를 이용해 조회한다.
    *   반환 값은 Object 유형이므로 저장된 객체로 자료유형 변환이 필요하다.
    *   메소드 setAttribute()에 이용한 name인 "id"를 알고 있다면 바로 다음과 같이 조회한다.

    ``String value = (String) session.getAttribute("id");`

    ##### 세션에 값 삭제

    *   removeAttribute(String name) 메소드
        *   name 값에 해당하는 세션 정보를 삭제한다.
    *   invalidate() 메소드
        *   모든 세션 정보를 삭제한다.

    ##### javax.servlet.http.HttpSession

    ![123](https://user-images.githubusercontent.com/71358285/170928943-a9af1773-c0bc-491e-a458-771edf0e17be.png)
    ![2](https://user-images.githubusercontent.com/71358285/170928954-0b01a0c3-1a3f-43e1-b511-cc4a6d046c5d.png)

    ##### 세션은 클라이언트가 서버에 접속하는 순간 생성

    *   특별히 지정하지 않으면 세션의 유지 시간은 기본 값으로 30분 설정된다.

    *   세션의 유지 시간이란 서버에 접속한 후 서버에 요청을 하지 않는 최대 시간이다.

    *   30분 이상 서버에 전혀 반응을 보이지 않으면 세션이 자동으로 끊어진다.

    *   이 세션 유지 시간은 web.xml 파일에서 설정 가능하다.

        ```xml
        <session-config>
        	<session-timeout>30</session-timeout>
        </session-config>
        ```

### Spring Security

아이디와 암호를 이용해서 로그인하는 과정을 인증(Authentication)이라고 한다.

로그인을 하더라도 어느 정도 이상의 등급이 되지 않을 경우 이용하지 못하는 경우, 이 부분을 인가(Authorization)이라고 한다.

그러나 **Spring Security**를 사용하면 편리하게 인증/인가를 구현할 수 있다.

스프링 시큐리티는 스프링 기반의 어플리케이션의 보안(인증과 권한)을 담당하는 프레임워크를 말한다.

스프링 시큐리티를 사용하지 않았다면, 자체적으로 세션을 체크하고 리다이렉트 등을 해야한다.

스프링 시큐리티는 필터기반으로 동작하기 때문에 스프링 MVC 와 분리되어 관리 및 동작한다.

스프링 시큐리티 3.2부터는 자바 config설정으로 간단하게 설정할 수 있도록 지원한다.

*   접근 주체(Principal) - 보호된 대상에 접근하는 유저
*   인증(Authentication) - 인증은 '증명하다'라는 의미로 예를 들어, 유저 아이디와 비밀번호를 이용하여 로그인하는 과정을 말한다.
*   인가(Authorization) - '권한부여'나 '허가'와 같은 의미로 사용된다. 즉, 어떤 대상이 특정 목적을 실현하도록 허용(Access)하는 것을 의미한다.
*   권한 - 인증된 주체가 어플리케이션의 동작을 수행할 수 있도록 허락되었는지를 결정할 때 사용한다.

#### Spring Security Filter

![mceclip0](https://user-images.githubusercontent.com/71358285/171006901-7c3fbc50-4989-44d6-b1b5-1d590a282309.png)

<sub>그림 출처 : https://youmekko.github.io/2018/04/26/2018-04-26-Filter/</sub>

클라이언트는 요청을 보내고, 그 요청을 서블릿이나 JSP등이 처리하게 된다. 스프링 MVC에서는 요청을 가장 먼저 받는 것이 DispatcherServletㅇ이다. 이 DispatcherServlet이 요청을 받기 전에 다양한 필터들이 있을 수 있다. 필터가 하는 역할은 클라이언트와 자원 사이에서 요청과 응답 정보를 이용해 다양한 처리를 하는데 목적이 있다. 스프링 시큐리티는 다양한 기능을 가진 필터들을 10개 이상 기본적으로 제공한다. 이렇게 제공되는 필터들은 Security Filter Chain이라고 말한다.

![mceclip1](https://user-images.githubusercontent.com/71358285/171006923-2be038a1-f0a7-4926-99a4-d2c88f842fe4.png)

<sub>그림출처 : https://atin.tistory.com/590M</sub>

위의 그림은 시큐리티 필터 체인과 각각의 필터에서 사용하는 객체들에 대해 잘 표현하고 있다.

*   SecurityContextPersistenceFilter - SercurityContextRepository에서 SecurityContext를 가져오거나 저장하는 역할을 한다.
*   LogoutFilter - 설정된 로그아웃 URL로 오는 요청을 감시하며, 해당 유저를 로그아웃 처리한다.
*   (UsernamePassword)AuthenticationFilter - (아이디와 비밀번호를 사용하는 form 기반 인증)설정된 로그인 URL로 오는 요청을 감시하며, 유저 인증 처리
    1.   AuthenticationManager를 통한 인증 실행
    2.   인증 성공 시,  얻은 Authentication객체를 SecurityContext에 저장 후 AuthenticationSuccessHandler실행
    3.   인증 실패 시, AuthenticationFailureHandler 실행
*   DefaultLoginPageGeneratingFilter - 인증을 위한 로그인폼 URL을 감시한다.
*   BasicAuthenticationFilter - HTTP 기본 인증 헤더를 감시하여 처리한다.
*   RequestCacheAwareFilter - 로그인 성공 후, 원래 요청 정보를 재구성하기 위해 사용된다.
*   SecurityContextHolderAwareRequestFilter - HttpServletRequestWrapper를 상속한 SecurityContextHolderAwareRequestWrapper 클래스로 HttpServletRequest정보를 감싼다. SecurityContextHolderAwareRequestWrapper 클래스는 필터 체인상의 다음 필터들에게 부가정보를 제공한다.
*   AnnoymousAuthenticationFilter - 이 필터가 호출되는 시점까지 사용자 정보가 인증되지 않았다면 인증 토큰에 사용자가 익명 사용자로 나타난다.
*   SessionManagementFilter - 이 필터는 인증된 사용자와 관련된 모든 세션을 추적한다.
*   ExceptionTranslationFilter - 이 필터는 보호된 요청을 처리하는 중에 발생할 수 있는 예외를 위임하거나 전달하는 역할을 한다.
*   FilterSecurityInterceptor - 이 필터는 AccessDecisionManager로 권한부여 처리를 위암함으로써 접근 제어 결정을 쉽게해준다.

#### 스프링 시큐리티 인증관련 아키텍쳐

아이디와 암호를 임력했을 때, 이를 처리하는 필터는 AuthenticationFilter이다.

![mceclip2](https://user-images.githubusercontent.com/71358285/171006942-7a64ff15-ce96-4a02-8e12-2adc300ad195.png)

<sub>출처 : http://www.springbootdev.com</sub>

1.   클라이언트(유저)가 로그인을 시도한다.
2.   AuthenticationFilter는 AuthenticationManager, AuthenticationProvider(s), UserDetailsService를 통해 DB에서 사용자 정보를 읽어온다. 중요한 것은 UserDetailsService가 인터페이스라는 것이다. 해당 인터페이스를 구현한 빈을 생성하면 스프링 시큐리티는 해당 빈을 사용하게 된다. 즉, 어떤 데이터베이스로부터 읽어들일지 스프링 시큐리티를 이용하는 개발자가 결정할 수 있게 된다.
3.   UserDetailsService는 로그인한 ID에 해당하는 정보를 DB에서 읽어들여 UserDetails를 구현한 객체로 반환한다. 프로그래머는 UserDetails를 구현한 객체를 만들어야 할 필요가 있을 수 있다. UserDetails정보를 세션에 저자앟게 된다.
4.   스프링 시큐리티는 인메모리 세션저장소인 SecurityContextHolder에 UserDetails정보를 저장하게 된다.
5.   클라이언트에게 sessionId(JSESSION ID)와 함께 응답을 하게 된다.
6.   이후 요청에서는 요청 쿠키에서 JSESSION ID 정보를 통해 이미 로그인 정보가 저장되어 있는지를 확인한다. 이미 저장되어 있고 유효하면 인증 처리를 해준다.









# 20220529_TIL

### GITIGNORE 안먹힐때 !

나의 경우 대부분 미리 에드 커밋하구나서 이미 추적중인데 뒤늦게 파일을 gitignore하고싶을때이다.

`git rm -r --cached 파일명1 파일명2 ...`

이렇게 git에 upload하고 싶지 않은 파일을 git에서 rm해주면 된다.





# 20220528_TIL

#### jdbc.queryForObject()

*   SQL의 DML중 SELECT를 실행했을 때 하나의 객체결과값이 나올 때 사용하는 메소드이다.

#### jdbc.query()

*   많은 결과 값(로우 값)을 처리 할 수 있는 메소드이다.

### web.xml 한글 인코딩 설정

```xml
	<filter>
		<filter-name>encodingFilter</filter-name>
		<filter-class>org.springframework.web.filter.CharacterEncodingFilter
		</filter-class>
		<init-param>
			<param-name>encoding</param-name>
			<param-value>UTF-8</param-value>
		</init-param>
	</filter>
	<filter-mapping>
		<filter-name>encodingFilter</filter-name>
		<url-pattern>/*</url-pattern>
	</filter-mapping>
```

아아... encodingFilter의 url-pattern을 '/'로 해놨었다.. 이걸 놓쳐서 몇시간 삽질인가.. '/*'으로 해야 정상적으로 한글 인코딩이 된다.







# 20220527_TIL

#### [Spring JDBC]NamedParameterJdbcTemplate 

기존에 사용하던 JdbcTemplate은 쿼리문에서 데이터를 넣을 부분에 ?를 이용하여 처리하였다. 이러한 방식은 인자 위치에 대한 순서가 강제되게 된다. 이를 보완해서 나온 방법이 NamedParameterJdbcTemplate이며, ?대신에 변수를 이용하여 처리함으로써 순서에 강제받지 않게된다.

기존 JdbcTemplate 방식

```sql
SELECT name, address, phone FROM table WHERE name = ?
```

NamedParameterJdbcTemplate 방식

```sql
SELECT name, address, phone FROM table WHERE name = :name;
```

#### [Spring JDBC]SimpleJdbcInsert

Insert 구문을 자동생성 해준다. 이 클래스를 활용하면, 직접 INSERT구문을 사용하지 않고도 DB에 데이터를 저장할 수 있다.



[Spring JDBC에 대하여 정리되어있는 GitHub](https://github.com/benelog/spring-jdbc-tips/blob/master/spring-jdbc-core.md)

Map은 인터페이스 HashMap은 구현 클래스인데. 

왜 Map<> map = new HashMap<>();함?

HashMap<> map = new HashMap<>(); 안하고? 차이는?

#### RowMapper

*   ResultSet을 전달받고 필요한 정보를 ResultSet의 로우 하나만을 매핑하기 위해 사용한다.







# 20220526_TIL

### Spring과  SpringBoot

Spring은 SpringFramework로써 개발자들의 반복된 코드작성을 해소해주기 위해서 개발되었다. 개발자들에게 봄이왔다는 의미로 네이밍을 Spring이 되었다.

그러나 여기에서도 보완점이 있어서 Springboot가 나오게되었다.

SpringBoot는 Spring에 비해

1.   간편한 설정
2.   편리한 의존성 관리와 자동권장 버전 관리
3.   내장 서버로 인한 간단판 배포 서버 구축
4.   스프링 Security, Data JPA 등의 다른 스프링 프레임워크 요소를 쉽게 사용

이라는 장점이 있다.

***

### [Rest API](https://www.boostcourse.org/web326/lecture/58986/?isDesc=false)

REST API로 시스템을 개발할 때 변경에 유연하고 확장성이 높은 코드를 작성할 수 있게 해준다.

***

### Web API

웹 서버 또는 웹 브라우저를 위한 애플리케이션 프로그래밍 인터페이스이다. HTTP 서비스이고 다양한 클라이언트에서 접근이 가능하도록 설계되어있다. Web환경을 통해 제공되는 데이터 CRUD 인터페이스를 제공한다.

REST API 아키텍처 스타일을 완벽하게 구현하지 못할 경우

***

### @RestController

*   Spring 4 에서 Rest API 또는 Web API를 개발하기 위해 등장한 애노테이션합니다.

*   이전 버전의 @Controller와 @ResponseBody를 포함합니다.

    *   @ResponseBody
        *   컨트롤러의 특정 메서드에 @ResponseBody를 적용하면 JSP가 아닌 텍스트나 JSON으로 결과를 전송할 수 있다.
        *   HTTP의 BODY에 문자 내용을 직접 반환한다.
        *   viewResolver 대신에 HttpMessageConverter가 동작한다.
        *   기본 문자처리: StringHttpMessageConverter
        *   기본 객체처리: MappingJackson2HttpMessageConverter
        *   byte 처리 등등 기타 여러 HttpMessageConverter가 기본으로 등록되어 있다.

*   MessageConvertor가 중요하며, @EnableWebMvc로 사용하게 되면 기본 제공된다.

    *   http와 관련된 코드 및 요청/응답 매핑을 스프링이 알아서 해준다.

    *   이 어노테이션을 사용하여 컨트롤러를 JSON형식으로 반환하는 컨트롤러로 만들어준다.

*   문제는 JSON으로 변환하기 위해서는 Jackson 라이브러리가 꼭 필요하다.

***

### MockMVC

WebAPI를 테스트하기위해서 WAS를 실행해야한다는 문제를 해결하기 위해 스프링 3.2부터 생겼다.



Controller를 단위 테스트한다는 것은 controller가 사용하는 Service에 대한 부분은 함께 테스트하지 않는다는 것이다. 이를 위해 Service에 대한 부분은 Mock객체를 사용하고, Mokito를 이용해 목객체를 생성한다. [예제](https://www.boostcourse.org/web326/lecture/59389?isDesc=false)

***

### Swagger

*   Web API 문서화를 위한 도구이다.

*   API들이 가지는 명세를 관리하기 위한 프로젝트이다.
*   자동으로 Web API를 문서갱신 시켜준다.

[Swagger-ui확인 및 기능테스트 예제](https://www.boostcourse.org/web326/lecture/58990/?isDesc=false)









# 20220525_TIL

### 테스팅

응용 프로그램 또는 시스템의 동작과 성능,안전성이 요구하는 수준을 만족하는지 확인하기 위해 결함을 발견하는 과정.

*   정적 테스트 - 프로그램을 개발하기 전에 요구사항 등을 리뷰하는 것
*   동적 테스트 - 프로그램 개발 이후에 실제 실행하면서 테스트하는 것

테스트는

	1. 금전적 손실방지, 2. 시간 낭비, 3. 비즈니스의 이미지 손상, 4. 부상이나 사망을 방지하기 위해 필요하다.

테스트는 언제 필요한가?

#### TDD

DD란 "프로그램을 작성하기 전에 테스트를 먼저 작성하는 것"이라고 TDD를 주도한 켄트 벡이 정의했다.

TDD의 정의는 "업무 코드를 작성하기 전에 테스트 코드를 먼저 만드는 것" 이라고 정의된다.

코드를 검증하는 테스트 코드를 먼저 만든 다음에 실제 작성해야 하는 프로그램 코드 작성에 들어가라는 뜻이다.

이는 메소드나 함수같은 프로그램 모듈을 작성할 때 '작성 종료조건을 먼저 정해놓고 코딩을 시작한다'라는 의미로 받아들이면 편하다.

TDD를 적용해 테스트를 먼저 개발함으로써 개발자는 자연스레 객체의 내부 구현 보다 객체의 인터페이스를 먼저 생각하게 되고 이는 좋은 객체 지향 설계를 가져갈 수 있는 첫 걸음이 됩니다. 즉, 응집도가 높고 결합도가 낮은 코드를 개발할 확률이 더 높아진다는 이야기 입니다.

#### JUnit

테스트를 위한 자바언어의 프레임워크이다.

![2](https://user-images.githubusercontent.com/71358285/170159552-21fd5e5e-df51-4753-93a7-bb948b7d4bd9.png)
![12](https://user-images.githubusercontent.com/71358285/170159563-ce70c9ce-7a02-4eab-8580-8f9da5ad33cd.png)

![3](https://user-images.githubusercontent.com/71358285/170159618-35745592-9b83-4b01-a218-5bced146a327.png)

[JUnit실습](https://www.boostcourse.org/web326/lecture/58976?isDesc=false)

#####  스프링 테스트 어노테이션 사용하기[링크](https://www.boostcourse.org/web326/lecture/58977/?isDesc=false)

1.   스프링 프레임워크를 사용하도록 기존코드를 변경해야한다.
     *   pom.xml에 관련 라이브러리를 추가하고 Maven update 수행
2.   Java Config 파일을 생성해줘야한다.
     *   클래스에 @Configuration어노테이션을 붙여 스프링 설정 파일이라는것을 알려준다. (스프링 빈 컨테이너인 ApplicationContext에서 읽어들인다.)
     *   @ComponentScan을 사용하여 특정 패키지를 한다. 그 패키지 이하에서 컴포넌트를 찾도록 수행된다.
3.   스프링 빈 컨테이너가 클래스를 찾아 빈으로 등록할 수 있도록 클래스 위에 @Component를 붙인다.

4.   테스트 클래스 위에

     *   @RunWith(SpringJUnit4ClassRunner.class - 스프링 빈 컨테이너가 내부적으로 생성되도록 한다.
     *   @ContextConfiguration(classes = {ApplicationConfig.class}) - 내부적으로 생성된 스프링 빈 컨테이너가 사용할 설정파일을 지정할 때 사용합니다.

5.   테스트 클래스 내부 메서드에

     *   @Autowired

         CalculatorService calculatorService;



##### Mock 객체 이용

테스트를 위해 가짜 객체를 쉽게 만들어 줄 수 있는 프레임워크이다. 사용하기 위해서는 pom.xml에 파일을 추가해줘야한다.

1.   테스트클래스 위에 `@RunWith(MockitoJUnitRunner.class) `을 추가해준다.

2.   ```java
     @Mock
     CalculatorService calculatorService;
     ```

     해당 클래스가 목 객체를 참조하도록 한다. 즉 객체를 생성하지 않아도 자동으로 객체가 생성되고 해당 필드가 초기화된다.

3.   ```Java
     @InjectMocks
      MyService myService;
     ```

     위의 어노테이션이 붙은 필드는 목 객체를 사용하는 해당 서비스 객체를 생성하여 초기화하라는 의미이다.

***

### Spring JDBC

*   JDBC 프로그래밍의 반복되는 저수준의 세부 개발요소를 스프링 프레임워크가 처리해준다.

*   **Spring JDBC 패키지**

    **org.springframework.jdbc.core**

    -   JdbcTemplate 및 관련 Helper 객체 제공

    **org.springframework.jdbc.datasource**

    -   DataSource를 쉽게 접근하기 위한 유틸 클래스, 트랜젝션매니져 및 다양한 DataSource 구현을 제공

    **org.springframework.jdbc.object**

    -   RDBMS 조회, 갱신, 저장등을 안전하고 재사용 가능한 객제 제공

    **org.springframework.jdbc.support**

    -   jdbc.core 및 jdbc.object를 사용하는 JDBC 프레임워크를 지원

#### **JDBC Template**

-   org.springframework.jdbc.core에서 가장 중요한 클래스입니다.
-   리소스 생성, 해지를 처리해서 연결을 닫는 것을 잊어 발생하는 문제 등을 피할 수 있도록 합니다.
-   스테이먼트(Statement)의 생성과 실행을 처리합니다.
-   SQL 조회, 업데이트, 저장 프로시저 호출, ResultSet 반복호출 등을 실행합니다.
-   JDBC 예외가 발생할 경우 org.springframework.dao패키지에 정의되어 있는 일반적인 예외로 변환시킵니다.

#### ConnectionPool

-   DB연결은 비용이 많이 듭니다.
-   커넥션 풀은 미리 커넥션을 여러 개 맺어 둡니다.
-   커넥션이 필요하면 커넥션 풀에게 빌려서 사용한 후 반납합니다.

#### DataSource

-   DataSource는 커넥션 풀을 관리하는 목적으로 사용되는 객체입니다.
-   DataSource를 이용해 커넥션을 얻어오고 반납하는 등의 작업을 수행합니다.

### STATIC IMPORT객체에 선언된 변수를 클래스 이름없이 가져다 쓸 수 있게 해준다.

*   ex) **import** **static** kr.or.connect.daoexam.dao.RoleDaoSqls.*;

***

### Spring MVC

*   MVC는 Model View Controller의 약자이다.
    *   Model - 뷰가 렌더링하는데 필요한 데이터이다. ex) 사용자가 요청한 상품목록이나, 주문내역
    *   View - 실제로 보이는 부분이며, 모델을 사용해 렌더링한다. ex) JSP,PDF, XML등으로 결과를 표현한다.
    *   Controller - 사용자의 액션에 응답하는 컴포넌트이다. 모델을 업데이트하고 다른 액션을 수행한다.

![1](https://user-images.githubusercontent.com/71358285/170194959-b4c03a9b-8ef6-424e-865b-db9336b1c9e9.png)

스프링 MVC 프레임 워크에서 가장 큰 주체는 DispatcherServlet이다. [DispatcherServlet자세히 보기](https://jess-m.tistory.com/15)

#### [DispatcherServlet](https://www.boostcourse.org/web326/lecture/258533/?isDesc=false)

#### 프로젝트 구성 순서

1.   웹어플리케이션 프로젝트

     1.   pom.xml에 라이브러리들을 추가해준다.
          1.   자바 버전확인
          2.   Spring 라이브러리
          3.   Servelt JSP JSTL 라이브러리
          4.   MySQL
          5.   DataSource
     2.   Navigarot에서 .settings > facet에서 jst.web version확인해준다.
     3.   Maven Update로 적용을 해주고, 이클립스 restart

2.   Spring MVC를 위한 설정

     *   DispatcherServlet을 FrontController로 설정
         *   web.xml파일에 설정, javax.servlet.ServletContainerInitializer, org.springframework.web.WebApplicationInitializer의 세가지 방법이 있다.
     *   Config 생성
         *   @Configuration
         *   @EnableWebMvc - Web에 필요한 부분들을 대부분 자동으로 설정해준다.
         *   @ComponentScan - 범위를 지정해줌으로서 컨테이너 관리에 용이하다.
         *   WebMvcConfigurerAdapter 상속 - 기본 설정 이외의 설정이 필요할 경우 해당 클래스를 상속 받은 후, 메소드를 오버라이딩 하여 구현한다. 그러나 최신버전에서는 이제 사용하지 않는다.

3.   Spring MVC에서 Controller 실습

     **Spring MVC가 지원하는 메소드 인수 애노테이션**

     -   **@RequestParam**
     
     -   **@RequestHeader**
     
     -   **@RequestBody**
     
         -   JSON 형식으로 전송된 요청 데이터를 커맨드 객체로 전달받는 방법이다.

             이 애노테이션을 커맨드 객체에 붙이면 JSON형식의 문자열을 해당 자바객체로 변환한다.

             보통 반환하고자 하는 리소스가 복잡할 때 사용한다.(오브젝트처럼 복잡한 자료형을 통째로 요청에 보내고 싶은 경우)

     -   @RequestPart
     
     -   **@ModelAttribute**

     -   **@PathVariable**

     -   @CookieValue

      
     
     **@RequestParam**

     -   Mapping된 메소드의 Argument에 붙일 수 있는 어노테이션
     -   @RequestParam의 name에는 http parameter의 name과 멥핑
     -   @RequestParam의 required는 필수인지 아닌지 판단

      
     
     **@PathVariable**
     
     -   @RequestMapping의 path에 변수명을 입력받기 위한 place holder가 필요함
     -   place holder의 이름과 PathVariable의 name 값과 같으면 mapping 됨
     -   required 속성은 default true 임
     
      
     
     **@RequestHeader**
     
     -   요청 정보의 헤더 정보를 읽어들 일 때 사용
     -   @RequestHeader(name="헤더명") String 변수명
     
      
     
     **Spring MVC가 지원하는 메소드 리턴 값**
     
     -   **org.springframework.web.servlet.ModelAndView**
     -   org.springframework.ui.Model
     -   java.util.Map
     -   org.springframework.ui.ModelMap
     -   org.springframework.web.servlet.View
     -   **java.lang.String**
     -   java.lang.Void
     -   org.springframework.http.HttpEntity<?>
     -   org.springframework.http.ResponseEntity<?>
     -   **기타 리턴 타입**

***

## 레이어드 아키텍처(Layered Architecture)

*   Controller에서 중복되는 부분을 처리하려면?
    *   별도의 객체로 분리한다.
    *   별도의 메소드로 분리한다.
    *   컨트롤러와 서비스(비즈니스 메서드)
        *   비즈니스 메소드를 별도의 서비스객체에서 구현하도록 하고 컨트롤러는 서비스객체를 사용하도록 한다. 이를 비즈니스메서드라고한다.
*   서비스 객체란?
    *   비즈니스 로직을 수행하는 메소드를 가지고 있는 객체를 서비스 객체라고 한다.
    *   보통 하나의 비즈니스 로직은 하나의 트랜잭션으로 동작한다.
*   트랜잭션이란?
    *   하나의 논리적인 작업을 의미한다.
    *   원자성(Atomicity), 일관성(Consistency), 독립성(Isolation), 지속성(Durability)의 4가지로 구분된다.
        *   원자성 - 전체가 성공하거나 전체가 실패하는 것을 의미한다.
            *   중간에 오류가 발생하면, 앞의 작업들을 모두 원래대로 복원시켜야 한다. 이를 롤백이라고 한다. 끝까지 모두 성공했을때만 정보를 모두 반영한다. 이를 커밋이라고 한다. 롤백하거나 커밋을 하게되면 하나의 트랜잭션 처리가 완료된다.
        *   일관성 - 트랜잭션의 작업 처리 결과가 항상 일관성이 있어야 한다는것.
            *   트랜잭션이 진행되는 동안 데이터가 변경되더라도 업데이트된 데이터로 트랜잭션이 진행되는것이 아니라, 처음에 트랜잭션을 진행 하기 위해 참조한 데이터로 진행된다. 
        *   독립성 - 둘 이상의 트랜잭션이 동시에 병행 실행되고 있을 경우에는 어느 하나의 트랜잭션이라도 다른 트랜잭션의 연산에 끼어들 수 없다. 하나의 특정 트랜잭션이 완료될때까지, 다른 트랜잭션이 특정 트랜잭션의 결과를 참조할 수 없다.
        *   지속성 - 트랜잭션이 성공적으로 완료도히었을 경우, 결과는 영구적으로 반영되어야 한다는 것.
*   JDBC 프로그래밍에서 트랜잭션 처리 방법
    *   DB에 연결된 후 Connection객체의 setAutoCommit 메서드는 디폴트로 true이다. 이를 false로 지정하여 입력, 수정, 삭제 SQL이 실행을 한 후 모두 성공했을 경우 Connection이 가지고 있는 commit() 메소드를 호출한다.

*   @EnableTransactionManagement
    *   Spring Java Config파일에서 트랜잭션을 활성화 할 때 사용하는 애노테이션입니다.
    *   Java Config를 사용하게 되면 PlatformTransactionManager 구현체를 모두 찾아서 그 중에 하나를 매핑해 사용합니다.
    *   특정 트랜잭션 메니저를 사용하고자 한다면 TransactionManagementConfigurer를 Java Config파일에서 구현하고 원하는 트랜잭션 메니저를 리턴하도록 합니다.
    *   아니면, 특정 트랜잭션 메니저 객체를 생성시 @Primary 애노테이션을 지정합니다.

*   레이어드 아키텍처를 위한 설정의 분리
    *   DispatcherServlet을 경우에 따라 2개 이상 설정할 수 있는데 이 경우에 각각의 설정 파일에서 생성한 빈을 서로 사용 할 수 없다.
    *   이를 동시에 사용하기위해서는 ContextLoaderListener를 사용하면 된다.
    *   그러면 각각의 ApplicationContext가 생성되는데, 이 때 ContextLoaderListener가 생성하는 인스턴스가 root컨텍스트가 되고 DispatcherServlet이 생성한 인스턴스는 root컨텍스트를 부모로하는 자식 컨텍스트가 된다.













# 20220524_TIL

### Spring

#### Spring Framework란?

*   소프트웨어적 의미로는 '기능을 미리 클래스나 인터페이스 등으로 만들어 제공하는 반제품'
*   일정한 기준에 따라 개발이 이루어지므로 개발 생산성과 품질이 보장된 애플리케이션을 개발할 수 있다.
*   여러 가지 빈(클래스 객체)를 스프링이 권한을 가지고 직접 관리한다.

*   원하는 부분만 가져다 사용할 수 있도록 모듈화가 잘 되어 있다.
*   IoC 컨테이너이다. > 서블릿이나 빈 등을 개발자가 코드에서 생성하지 않고 프레임워크가 직접 수행
*   AOP기능을 이용해 자원 관리 > 핵심 기능 외 부수 기능들을 분리 구현함으로써 모듈성을 증가시키는 방법
*   DI 기능을 지원 > 클래스 객체를 개발자가 코드에서 생성하지 않고 프레임워크가 생성하여 사용하는 방법
*   선언적으로 트랜잭션을 관리 할 수 있다.

![2_10_1___](https://user-images.githubusercontent.com/71358285/169957990-25971d10-447e-4841-b9c0-029a96fe61e3.png)

##### 컨테이너(Container)

컨테이너는 인스턴스의 생명주기를 관리하며, 생성된 인스턴스에게 추가적인 기능을 제공합니다.

예를 들어, Servlet을 실행해주는 WAS는 Servlet 컨테이너를 가지고 있다고 말합니다.

WAS는 웹 브라우저로부터 서블릿 URL에 해당하는 요청을 받으면, 서블릿을 메모리에 올린 후 실행합니다.

개발자가 서블릿 클래스를 작성했지만, 실제로 메모리에 올리고 실행하는 것은 WAS가 가지고 있는 Servlet 컨테이너입니다.

Servlet컨테이너는 동일한 서블릿에 해당하는 요청을 받으면, 또 메모리에 올리지 않고 기존에 메모리에 올라간 서블릿을 실행하여 그 결과를 웹 브라우저에게 전달합니다.

컨테이너는 보통 인스턴스의 생명주기를 관리하며, 생성된 인스턴스들에게 추가적인 기능을 제공하는 것을 말합니다.

##### [IoC(Inversion of Control)](https://isstory83.tistory.com/91) - 객체를 대신 생성해주고 싱글턴으로 관리해주는 기능등을 IOC제어의 역전이라고 한다.

컨테이너가 코드 대신 오브젝트의 제어권을 갖고 있어 IoC(제어의 역전)이라 합니다.

예를 들어, 서블릿 클래스는 개발자가 만들지만, 그 서블릿의 메소드를 알맞게 호출하는 것은 WAS입니다.

이렇게 개발자가 만든 어떤 클래스나 메소드를 다른 프로그램이 대신 실행해주는 것을 제어의 역전이라고 합니다.

*   작업을 수행하는 쪽에서 Object를 생성하는 제어 흐름의 개념을 거꾸로 뒤집는다.
*   IoC 에서는 Object가 자신이 사용할 Object를 생성하거나 선택하지 않는다.
*   또한 Object는 자신이 어떻게 생성되고 어떻게 사용되는지 알 수 없다.
*   모든 Object는 제어 권한을 위임받는 특별한 Object에 의해서 만들어 지고 사용된다.

##### DI(Dependency Injection)

클래스 사이의 의존 관계를 빈(Bean) 설정 정보를 바탕으로 컨테이너가 자동으로 연결해주는 것을 말합니다.

<img width="784" alt="스크린샷 2022-05-24 오후 3 29 32" src="https://user-images.githubusercontent.com/71358285/169963698-bb7a9793-6749-4f54-8bdf-4d0c9bce0447.png">

##### Spring에서 제공하는 IoC/DI 컨테이너

-   BeanFactory : IoC/DI에 대한 기본 기능을 가지고 있습니다.
-   ApplicationContext : BeanFactory의 모든 기능을 포함하며, 일반적으로 BeanFactory보다 추천됩니다. 트랜잭션처리, AOP등에 대한 처리를 할 수 있습니다. BeanPostProcessor, BeanFactoryPostProcessor등을 자동으로 등록하고, 국제화 처리, 어플리케이션 이벤트 등을 처리할 수 습니다.

-   BeanPostProcessor : 컨테이너의 기본로직을 오버라이딩하여 인스턴스화 와 의존성 처리 로직 등을 개발자가 원하는 대로 구현 할 수 있도록 합니다.
-   BeanFactoryPostProcessor : 설정된 메타 데이터를 커스터마이징 할 수 있습니다.

#### ApplicationContext

파라미터를 받지 않은 빈생성메서드를 미리 생성해서, 반환받은 객체를 관리한다. 그리고 파라미터에 생성된 객체들과 같은 타입이 있을 경우에 파라미터에 전달해서 객체를 생성한다.

### Java config를 이용한 설정을 위한 Spring 어노테이션

*   @Configuration  
    *   config파일이라고 알려주는 어노테이션,  스프링 설정 클래스
*   @Bean 
    *   bean을 정의하는 어노테이션
*   @ComponentScan
    *   @Controller, @Service, @Repository, @Component 어노테이션이 붙은 클래스를 찾아 컨테이너에 등록
*   @Component
    *   알아서 어노테이션 붙어있는것들 찾아서 등록하게 해준다. 반드시 패키지명을 알려줘야, 범위를 정해서 그 부분만 스캔한다.
*   @Autowired
    *   해당 객체의 타입이 있으면 주입해준다.
    *   굳이 setter메서드가 필요하지 않다.

### 



### 톰캣은 서블릿 컨테이너라 불리는데, 톰캣을 실행하면 서블릿의 생성,초기화,서비스실행,소멸에 관한 모든 권한을 가지고 서블릿을 관리하기 때문





# 20220523_TIL

### JSP - Java Server Page

경로는 항상 WebContent 파일 아래에 있다.

html에서 자바언어를 사용할 수 있게 해준다. 그러나 모든 jsp는 서블릿으로 바뀌어서 동작한다. 

'<%@'는 페이지 지시자이다. `out.print(total) = <%=totla%>`

톰캣이 실행될 때, jsp를 servlet으로 바꾸어 실행시켜준다.

#### JSP의 실행순서

1.  브라우저가 웹서버에 JSP에 대한 요청 정보를 전달한다.
2.  브라우저가 요청한 JSP가 최초로 요청했을 경우만 JSP로 작성된 코드가 서블릿으로 코드로 변환한다. (java 파일 생성)
3.  서블릿 코드를 컴파일해서 실행가능한 bytecode로 변환한다. (class 파일 생성)
4.  서블릿 클래스를 로딩하고 인스턴스를 생성한다.
5.  서블릿이 실행되어 요청을 처리하고 응답 정보를 생성한다.

#### JSP 문법

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

#### JSP 내장 객체

-   JSP를 실행하면 서블릿 소스가 생성되고 실행된다.
-   JSP에 입력한 대부분의 코드는 생성되는 서블릿 소스의 _jspService() 메소드 안에 삽입되는 코드로 생성된다.
-   _jspService()에 삽입된 코드의 윗부분에 미리 선언된 객체들이 있는데, 해당 객체들은 jsp에서도 사용 가능하다.
-   response, request, application, session, out과 같은 변수를 내장객체라고 한다.

<img width="2532" alt="스크린샷 2022-05-23 오후 6 29 41" src="https://user-images.githubusercontent.com/71358285/169789205-513ae87a-78ae-4b13-8377-3053f810b1f6.png">

***

### Scope

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

### [EL (Expression Language)](https://www.boostcourse.org/web326/lecture/258517/?isDesc=false)

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

### [JSTL(JSP Standard Tag Library)](https://www.boostcourse.org/web326/lecture/258521?isDesc=false)

*  JSP 안에 자바코드와 HTML코드가 섞여있을때 수정하기 어려움을 느낀다. 이를 해결하기 위해 등장함
*  JSTL(JSP Standard Tag Library)은 JSP 페이지에서 조건문 처리, 반복문 처리 등을 html tag형태로 작성할 수 있게 도와줍니다



# 20220522_TIL

### HTTP - Hypertext Transfer Protocol

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

### URL - Uniform Resource Locator

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

### 웹 프론트엔드

*   사용자에게 웹을 통해 다양한 콘텐츠를 제공한다. 또한, 사용자의 요구사항에 반응해서 동작한다.
*   웹콘텐츠를 잘 보여주기 위해 구조를 만들어야 합니다.(신문,책등과 같이) - HTML
*   적절한 배치와 일관된 디자인 등을 제공해야 합니다.(보기 좋게) - CSS
*   사용자 요청을 잘 반영해야 합니다.(소통하듯이) - Javascript

### 웹 백엔드

*   정보를 처리하고 저장하며, 요청에 따라 정보를 내려주는 역할을 한다.
*   프로그래밍 언어(JAVA, Python, PHP, Javascript 등)
*   웹의 동작 원리
*   알고리즘(algorithm), 자료구조 등 프로그래밍 기반 지식
*   운영체제, 네트워크 등에 대한 이해
*   프레임워크에 대한 이해(예: Spring)
*   DBMS에 대한 이해와 사용방법(예: MySQL, Oracle 등)

***

### [Browser](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/#The_rendering_engine)

*   Parsing - 토큰단위로 다 잘라서 의미를 해석하고 의미에 따라서 실행하는것

*   Head - 문서에 대한 자세한 정보들이 포함되어 있다.
*   body - 화면에 표현되어야 할 것들 div..p..등
*   HTML은 계층적으로 존재
*   JS와 CSS가 html안에 여기저기 존재한다.

***

### 웹서버

-   웹 서버는 소프트웨어(Software)를 보통 말하지만, 웹 서버 소프트웨어가 동작하는 컴퓨터를 말합니다.
-   웹 서버의 가장 중요한 기능은 클라이언트(Client)가 요청하는 HTML 문서나 각종 리소스(Resource)를 전달하는 것입니다.
-   웹 브라우저나 웹 크롤러가 요청하는 리소스는 컴퓨터에 저장된 정적(static)인 데이터이거나 동적인 결과가 될 수 있습니다.

*   클라이언트와 웹서버는 HTTP로 통신. 
*   웹페이지에는 아주 많은 요소들이 있는데, 하나로 합쳐서 보여주는것을 렌더링한다 라고 함.

***

### WAS - Web Application Server

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

### Java Web Application

WAS에 설치되어 동작하는 어플리케이션이다. HTML, CSS, 이미지, 자바로 작성된 클래스, 각종 설정 파일 등이 포함된다. 복잡할 웹어플리케이션일수록 이러한것들이 복잡하고 많이 들어있다.

![](https://cphinf.pstatic.net/mooc/20180124_133/15167752967943AqfC_PNG/1_5_1_____.PNG)



### Context - server.xml에 등록하는 웹 어플리케이션

*   컨테이너 실행 시 웹 어플리케이션당 하나의 컨텐스트가 생성
*   웹 어플리케이션과 같을 수도 있고 다를 수도 있다.
*   컨텍스트 이름은 중복될 수 없다.
*   명사형으로 지정한다.
*   대소문자를 구분한다.

***

### Servlet

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

### HttpServletRequest, HttpServletResponse

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

# 20220521_TIL

### **데이터베이스와 데이터베이스 관리 시스템**

-   Q> 데이터베이스와 데이터베이스 관리 시스템을 어린이도 알 수 있을 정도로 설명해주세요.
-   A> 도서관에 있는 책들이 데이터베이스라고 한다면, 도서관 사서분들이나 도서 정보를 찾아주는 컴퓨터를 DBMS라고 볼 수 있습니다.



### **데이터베이스의 기본개념 (정의)**

-   데이터의 집합 (a Set of Data)
-   여러 응용 시스템(프로그램)들의 통합된 정보들을 저장하여 운영할 수 있는 공용(share) 데이터의 집합
-   효율적으로 저장, 검색, 갱신할 수 있도록 데이터 집합들끼리 연관시키고 조직화되어야 한다.



### **데이터베이스의 특성**

-   실시간 접근성(Real-time Accessability)
    \- 사용자의 요구를 즉시 처리할 수 있다.

-   계속적인 변화(Continuous Evolution)
    \- 정확한 값을 유지하려고 삽입·삭제·수정 작업 등을 이용해 데이터를 지속적으로 갱신할 수 있다.

-   동시 공유성(Concurrent Sharing)
    \- 사용자마다 서로 다른 목적으로 사용하므로 동시에 여러 사람이 동일한 데이터에 접근하고 이용할 수 있다.

-   내용 참조(Content Reference)
    \- 저장한 데이터 레코드의 위치나 주소가 아닌 사용자가 요구하는 데이터의 내용, 즉 데이터 값에 따라 참조할 수 있어야 한다.



### **데이터베이스 관리 시스템 (Database Management System = DBMS)**

-   데이터베이스를 관리하는 소프트웨어
-   여러 응용 소프트웨어(프로그램) 또는 시스템이 동시에 데이터베이스에 접근하여 사용할 수 있게 한다
-   필수 3기능
    \- 정의기능 :  데이터 베이스의 논리적, 물리적 구조를 정의
    \- 조작기능 : 데이터를 검색, 삭제, 갱신, 삽입, 삭제하는 기능
    \- 제어기능 :  데이터베이스의 내용 정확성과 안전성을 유지하도록 제어하는 기능
-   Oracle, SQL Server, MySQL, DB2 등의 상용 또는 공개 DBMS가 있다.

  

### **데이터베이스 관리 시스템의 장/단점**

-   장점
    \- 데이터 중복이 최소화
    \- 데이터의 일관성 및 무결성 유지 
    \- 데이터 보안 보장
-   단점
    \- 운영비가 비싸다
    \- 백업 및 복구에 대한 관리가 복잡
    \- 부분적 데이터베이스 손실이 전체 시스템을 정지

***

### **MySQL_MAC_OS** >>>> [MySQL DOC](https://dev.mysql.com/doc/refman/5.7/en/create-database.html)

1.   설치

`brew install mysql`

2.   실행

`mysql.server start`

3.   종료

`mysql.server stop`

### **운영체제의 백그라운드로 MySQL이 계속 실행되도록 하고싶다면?**

*   `brew services start mysql` 데몬형태로 실행
*   `brew services restart mysql` 서비스 재시작
*   `brew services stop mysql`서비스 종료
*   `brew services list`데몬으로 실행되고 있는 프로그램 리스트 

### **SQL(Structured Query Language)**
-   SQL은 데이터를 보다 쉽게 검색하고 추가, 삭제, 수정 같은 조작을 할 수 있도록 고안된 컴퓨터 언어입니다.
-   관계형 데이터베이스에서 데이터를 조작하고 쿼리하는 표준 수단입니다.
-   DML (Data Manipulation Language): 데이터를 조작하기 위해 사용합니다.
    INSERT, UPDATE, DELETE, SELECT 등이 여기에 해당합니다.
-   DDL (Data Definition Language): 데이터베이스의 스키마를 정의하거나 조작하기 위해 사용합니다.
    CREATE, DROP, ALTER 등이 여기에 해당합니다.
-   DCL (Data Control Language) : 데이터를 제어하는 언어입니다.
    권한을 관리하고, 테이터의 보안, 무결성 등을 정의합니다.
    GRANT, REVOKE 등이 여기에 해당합니다.

### **MySQL 관리자 계정인 root로 데이터베이스 관리 시스템에 접속**

`mysql -u root -p`

### **DATABASE 생성하기**

`create database "DB이름"`

### **DATABASE CREATE USER**

`CREATE USER connectuser@localhost IDENTIFIED BY 'connect123!@#';`

### **GIVE PRIVILEGES TO USER**

`GRANT ALL PRIVILEGES ON connectdb.* TO 'connectuser'@'localhost';`

### **MAKING DBMS ACCEPTION**

`FLUSH PRIVILEGES;`

### **ACCESS TO DB WITH USER**

`mysql -h 127.0.01 -u "USER NAME" -p "DB NAME";` then type password.

If U R using UR laptop -h will be 127.0.0.1

### **GET MySQL VERSION AND CURRENT DATE**

`SELECT VERSION(), CURRENT_DATE;`

### **IMPORT sql file to DB at specific user**

`mysql -u "USERNAME" -p "DBNAME" < "FILENAME.sql";` then type password.

### **CHECKING TABLE'S STRUCTURE**

`desc "TABLENAME";`

### **IMPORT DATA FROM .SQL FILES**

`source '경로';`

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



# TODAY I LEARNED - 20220520

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

|      | ID선택자                                                     | CLASS선택자                                              |
| ---- | ------------------------------------------------------------ | -------------------------------------------------------- |
| 설명 | 특정 id 속성이 있는 태그를 선택                              | 특정 클래스가 있는 태그를 선택                           |
|      | 웹 표준에 id 속성은 웹 페이지 내부에서 중복되면 안된다는 규정이 있으므로 아이디 선택자는 특정 태그 하나를 선택할 때 사용한다. | 문서 안 복수의 요소에 스타일을 적용하는 경우에 사용한다. |
| 형태 | #아이디                                                      | .클래스                                                  |

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

![스크린샷 2022-05-12 오후 3.17.07](/Users/ssiky/Library/Application Support/typora-user-images/스크린샷 2022-05-12 오후 3.17.07.png)

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