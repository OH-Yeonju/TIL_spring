##### Spring IoC Container

##### Container?

- 스프링에서 핵심적인 역할을 하는 객체를 Bean이라고 하며

- Container는 Bean의 인스턴스화 조립, 관리의 역할, 사용 소멸에 대한 처리를 담당한다



##### AOP(Aspect Oriented Programming)

관점지향프로그래밍

- OOP에서 모듈화의 핵심 단위는 클래스인 반면, AOP에서 모듈화의 단위는 Aspect

- Aspect는 여러 타입과 객체에 거쳐서 사용되는 기능의 모듈화

- Spring framework의 필수 요소는 아니지만, AOP프레임워크는 Spring IoC를 보완한다



- 용어
  
  - Aspect : 여러 클래스에 공통적으로 구현되는 관심사의 모듈화
  
  - Join Point : 메서드 실행이나 예외처리와 같은 프로그램 실행중의 특정 지점. Spring에서는 메서드 실행을 의미한다
  
  - Pointcut : Join Point에서 Aspect를 적용하기 위한 조건 서술. Aspect는 지정한 pointcut에 일치하는 모둔 joinpoint에서 실행된다
  
  - Advice : 특정 조인포인트에서 Aspect에 의해서 취해진 행동. Around, Before, After 등의 Advice타입이 존재
  
  - Target 객체 : 하나 이상의 어드바이스가 적용될 객체. Spring AOP는 런타임 프록시를 사용하여 구현되므로 각체는 항상 프록시 객체가 된다.
  
  - AOP Proxy : AOP를 구현하기 위해 AOP 프레임워크에 의해 생성된 객체, Spring Framework에서 AOP프록시는 JDK dynamic proxy 또는 CGLIB proxy이다
  
  - Weaving : Aspect를 다른 객체와 연결하여 Advice 객체를 생성. 런타임  또는 로딩 시 수행할 수 있지만 Spring AOP는 런타임에 위빙을 수행



##### Spring AOP Proxy

- 실제 기능이 구현된 타겟 객체를 호출하면, 타겟이 호출되는 것이 아니가 advice가 적용된 proxy 객체가 호출됨



##### Spring MVC

- Servlet API를 기반으로 구축된 웹프레임워크

- 정식 명칭은 Spring Web MVC이지만, Spring MVC로 주로 알려져 있다

- DispatchServlet(FrontController)를 중심으로 디자인 되었으며, 뷰 리졸버, 핸들러 매핑, 컨트롤러와 같은 객체와 함께 요청을 처리하도록 구성되어 있다.
  

- 구성요소
  
  - DispatcherServlet - 클라이언트 요청처리
  
  - HandlerMapping - 요청을 어느 컨트롤러가 처리할지 결정
  
  - Controller - 요청에 따라 수행할 메서드를 선언하고 요청처리를 위한 로직 수행(비즈니스 로직 호출)
  
  - ModelAndView - 요청 처리를 하기 위해서 필요한 혹은 그 결과를 저장하기 위한 객체
  
  - ViewResolver - 컨트롤러에 선언된 뷰 이름을 기반으로 결과를 반환할 뷰를 결정
  
  - View - 응답화면 생성



##### Intercept

- HandlerInterceptor를 구현한 것(또는 HandlerInterceptorAdapter를 상속한 것)

- 요청을 처리하는 과정에서 요청을 가로채서 처리

- 접근 제어, 로그 등 비즈니스 로직과 구분되는 반복적이고 부수적인 로직 처리

- 주요 메서드
  
  - preHandle
    
    Controller(핸들러) 실행 이전에 호출
    
    false를 반환하면 요청을 종료한다
  
  - postHandle
    
    Controller(핸들러) 실행 후 호출
    
    정상 실행 후 추가 기능 구현 시 사용
    
    Controller에서 예외 발생 시 해당 메서드는 실행되지 않음
  
  - afterConpletion
    
    뷰가 클라이언트에게 응답을 전송한 뒤 실행
    
    Controller에서 예외 발생시, 네번째 파라미터로 전달이 된다(기본은 null)
    
    Controller에서 발생한 예외 혹은 실행 시간 같은 것들을 기록하는 등 후처리 시 주로 사용
