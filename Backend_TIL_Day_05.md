# Backend_TIL_Day_05



- 목차
  - 스프링 프레임워크(Spring Framework)

    - 어노테이션을 이용한 DI 방법
    - 스프링에서 사용하는 어노테이션

  - Spring MVC
    - MVC 패턴
    - Spring MVC 구조




## 스프링 프레임워크(Spring Framework)



### 어노테이션을 이용한 DI 방법

- xml 설정 파일에서 bean 태그를 이용해서 설정하였던 빈 설정을 어노테이션을 이용해서
  자바 코드에서 설정
- 예 : xml 설정 파일에서 빈을 설정하지 않고 스프링 자바 소스 코드를 읽어서
  클래스에 @Component 어노테이션이 붙은 클래스를 객체화 (bean 설정)
- A1 클래스의 객체를 A2 클래스의 객체로 변경하려면 A1 클래스에서 @Component를 
  제거하고 A2 클래스에 @Component를 붙이면 된다
- @Autowired 어노테이션을 사용하여 bean을 자동 삽입한다.



xml 설정 파일에 context 네임스페이스 추가

-  빈 설정을 위한 어노테이션을 사용하기 위해서는 설정 파일에 context 네임스페이스가
  추가되어있어야 한다 ([Namespaces] 탭에서 추가)
- context:component-scan 태그를 사용하여 빈으로 등록된 클래스를 찾아서 클래스를 객체화



### 스프링에서 사용하는 어노테이션

- 어노테이션 종류
  - DI 관련 어노테이션
    - @Autowired / @Inject
    - @Qualifier
    - @Resource
  - 빈 생성 관련 어노테이션
    - @Component
      - @Controller
      - @Service
      - @Repository
    - @Configureation
      - @Bean
  - Spring MVC / Boot 관련 어노테이션 



DI 관련 어노테이션

- xml 설정 파일에 있는 bean에 대해 DI하거나 자바 코드에서 생성된 bean에 대해 
  DI할 수 있다

- @Autowired

  - 타입을 기준으로 의존성 주입

  - 스프링 빈에 의존하는 다른 빈을 자동으로 주입할 때 사용

  - 스프링에서 지원

    ```java
    @Autowired
    INameService nameService;
    ```

- @Inject

  - @Autowired와 동일
  - 자바에서 지원

- @Qualifier

  - 특정 빈의 이름을 지정

  - 동일한 interface 구현한 클래스가 여러 개 있는 경우

  - 사용하고자 하는 빈의 이름을 지정할 때 사용

    ```java
    @Autowired
    @Qualifier("anotherNameService")
    INameService nameService;
    ```

- @Resource

  - @Autowired와 @Qualifier를 같이 사용하는 것과 동일

  - 자바에서 지원

  - pom.xml에서 javax.annotation 라이브러리 추가 해야 함

    ```java
    @Resource(name="anotherNameService")
    INameService nameService;
    ```

    

빈 생성 관련 어노테이션

- 빈 생성을 위해 클래스 위에 추가되는 어노테이션

- 클래스 이름 위에 붙이면 클래스 파일에 대한 bean이 자동 생성
  (xml 파일에서 bean 생성하지 않음)

- 빈의 이름은 클래스 이름에서 첫 문자만 소문자로 지정됨

  - 예 : NameService 클래스의 빈 이름은 nameService

- 어노테이션을 이용하기 위해 xml 설정 파일에서 필요한 작업

  - xml 설정 파일에 context 네임스페이스 추가 필요

    ```java
    <context-component-scan base-package="패키지명" />
    ```

  - @Component 어노테이션이 적용된 클래스를 빈으로 등록

  - 빈으로 등록될 클래스가 들어 있는 패키지 지정

  - 상위 패키지를 지정하면 하위 패키지까지 빈으로 등록될 클래스 찾음

  - `<context:annotation-config />` 필요 없음

- @Component

  - 클래스를 빈으로 등록(부품 등록)

  - 빈 id 지정할 수 있음

    ```java
    @Component(“빈이름”)
    <bean id=”빈이름”>에 해당
    ```

- @Component 어노테이션의 의미론적 어노테이션

  - @Component : 일반적인 컴포넌트 의미
  - 특화된 @Component 어노테이션
    - 클래스의 역할에 따라 의미론적으로 구분
    - @Controller 컴포넌트
    - @Service 컴포넌트
    - @Repository 컴포넌트

- Spring MVC 구성에 따른 어노테이션 사용 

  



## Spring MVC



### MVC 패턴



웹 애플리케이션 개발

- 화면 : 프론트엔드 개발자(디자이너)
- 비즈니스 로직 : 백엔드 개발자
- 처음부터 새로 개발하는 것이 아니라 기존의 웹 애플리케이션 개발 방법에 따라 개발
- 많이 사용하는 표준화 소스 구조를 만들어 개발 진행



웹 애플리케이션 모델

- 표준화된 소스 구조

  - 모델1 방식
    - 모든 클라이언트의 요청과 비즈니스 로직을 JSP가 담당
    - 클라이언트 요청 -> JSP(화면 기능/로직처리) -> DAO -> 데이터베이스
    - 기능 구현이 쉽고 편리
    - 웹 사이트 화면 기능이 복잡해지고 화면 기능과 비즈니스 로직 기능이 섞이면서
      유지보수 문제 발생
    - 코드 재사용성 떨어져서 비효율적
  - 모델2 방식(MVC 패턴)
    - 모델1 방식의 단점 보완
    - 웹 애플리케이션의 각 기능을 분리해서 구현
      - 클라이언트 요청 처리
      - 응답 처리
      - 비즈니스 로직 처리
    - 각 기능이 분리되어 모듈화되어 있으므로 모듈별 개발이 가능
    - 모듈을 비슷한 프로그램 개발에 사용할 수 있어 코드 재사용성도 높음
    - 응용프로그램 확장성 및 이식성이 좋아짐
    - 개발 후 서비스 제공 시 유지보수 편리
    - 현재 모든 웹 프로그램은 모델2 방식으로 개발

  

  MVC 패턴

  - M : Model (DTO / DAO)
  - V : View (JSP 페이지)
  - C : Controller

  

  FrontController 패턴

  - 모든 클라이언트 요청을 한 곳에서 처리하도록 하나의 대표 컨트롤러 사용
  - 별도의 클래스를 추가하지 않고 FrontController가 다 처리
    (FrontController 내용이 길고 복잡해짐)
  - 클라이언트의 요청을 한 곳으로 집중시켜서 효율적으로 개발 및 유지보수 가능

  

  Command 패턴

  - FrontController가 모든 클라이언트 요청을 직접 다 처리하지 않고 각 작업에 해당되는
    클래스가 처리
  - FrontController가 수행하던 작업을 각 클래스로 분산 처리
  - 각 클래스는 통일 형식(규격)으로 처리하도록 interface로 구현

  

### Spring MVC 구조

- DispatcherServlet
  - 컨트롤러 선택 (HandlerMapping을 통해)해서 요청을 컨트롤러에게 전달
  - View 검색 (ViewResolver)해서 해당되는 View로 서비스 응답



Spring MVC Project

- 프로젝트 생성

  - 기본 컨트롤러와 뷰 페이지 자동 생성되어 있음
  - 컨트롤러
  - 뷰 페이지

- 전체구조 파악

  - 컨트롤러 위치

  - 뷰 페이지 위치

    

### 스프링 컨트롤러

- 스프링 컨트롤러는 빈으로 등록되어야 하며 비즈니스 로직이 실행되기 위해
  비즈니스 객체를 의존성 주입 해야 함
- @Controller 어노테이션 사용
- @RequestMapping 어노테이션을 사용하여 url 맵핑
- 요청처리 메소드 구현
  - @RequestMapping 아래에 작업을 처리할 메소드 추가
  - 필요한 클래스(객체)는 파라미터로 받아서 사용
- 뷰 페이지 이름 반환
  - return "뷰페이지 이름만(확장자 없음)";



컨트롤러 클래스 작성

- 클래스 생성하고 @Controller 어노테이션 붙임

- @RequestMapping 어노테이션을 사용하여 요청경로 지정

- 요청 처리 메소드 구현

- 뷰 페이지 이름 반환

- views 폴더에 newView.jsp 생성

  

### 데이터 전달

- Controller => 뷰 페이지
- View => Controller
  - Form을 통한 데이터 전달 : Form 데이터처리 
  - url을 통한 데이터 전달
- View 페이지로 데이터 전달 방법
  - Model 사용
  - ModelAndView 사용
- Model 사용
  - Model 인터페이스 
  - Model Attribute 추가하기 위해 고안
  - key/value 형태로 값을 임시 저장 
  - Controller에서 Model에 데이터를 저장하고 View 이름을 return 하면 
    View 페이지로 Model이 전달되고 View 페이지에서 key를 사용해서 Model에 저장된 
    Data사용
- Model 사용 형식
  - 요청 처리 메소드에서 Model 객체를 파라미터로 받아서 addAttribute() 메소드로 
    key / value 설정
  - return 되는 뷰페이지로 전달 후 data 추출
- ModelAndView 사용
  - ModelAndView 클래스 사용
  - 데이터와 뷰 둘 다 설정
  - 반환값으로 ModelAndView 객체 반환
  - ModelAndView mv = new ModelAndView();
  - mv.addObject("name", "홍길동"); // 데이터 설정
  - mv.setViewName("showInfo2"); // 뷰 이름 설정
  - return mv; // ModelAndView 객체 반환





