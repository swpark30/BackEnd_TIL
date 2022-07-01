# Backend_TIL_Day_04



- 목차
  - JSTL (JSP Standard Tag Library)
    - core 라이브러리
    - 포매팅 태그 라이브러리
    - functions 라이브러리
  - 스프링 프레임워크(Spring Framework)
    - EJB (Enterprise JavaBean)
    - POJO (Plain Old Java Object)
    - 스프링 프레임워크의 특징
    - 의존성 (Dependency)
    - 스프링에서 의존성 주입 방법





## JSTL (JSP Standard Tag Library)



### core 라이브러리



c:forEach

- 반복문 수행

  ```jsp
  <c:forEach  var=”변수명” begin=”시작값” end=”마지막값” step=”증가값” 
              varStatus=”반복상태변수명”>
      
      varStatus : 반복 상태 속성 지정
      	index
      		items에서 정의한 항목을 가리키는 index 번호
          	기본 0부터 시작
          begin=1로 하면 index도 1부터 시작
          count : 몇 번째인지 표시. 1부터 시작
          first : 첫 번째이면 true
          last : 마지막 반복이면 true
  ```

  

c:url

- url 정보 저장

  ```jsp
  <c:url var=”변수명” value=”url 경로” />
  ```

  

c:redirect

- response.sendRedirect() 기능과 동일

- 매개변수 전달 가능

  ```jsp
  <c:redirect url=”redirect할 url”>
  	<c:param name=”id” value=”홍길동” />
  </c:redirect>
  ```

  

### 포매팅 태그 라이브러리

- 숫자 및 날짜와 관련된 포매팅 태그 라이브러리

- 라이브러리 : format

- prefix : fmt

- uri : http://java.sun.com/jsp/jstl/fmt

- 형식

  ```jsp
  <fmt:formatNumber></fmt:formatNumber>
  <fmt:formatDate></fmt:formatDate>
  <fmt:timeZone></fmt:timeZone>
  ```

  

### functions 라이브러리

- 함수 기능
- prefix : fn
- uri : http://java.sun.com/jsp/jstl/functions
- 자바와 동일
  - length()
  - toUpperCase()
  - indexOf()
  - contains()
  - trimg()
  - substring()





## 스프링 프레임워크(Spring Framework)



- 엔터프라이즈 애플리케이션 구축을 위한 솔루션
- 자바 애플리케이션 개발을 위한 포괄적인 인프라 지원을 제공하는 자바 플랫폼
  - 스프링에서 인프라를 처리하므로 개발자는 애플리케이션 개발에만 집중
- 모듈화되어 있어 필요한 부분만 사용 가능
- 국내에서는 자바 개발자들에게 표준 프레임워크



### 스프링의 장점

- 생산성 우수

  - 엔터프라이즈 애플리케이션 구축을 위한 솔루션이지만 가볍고 모듈화되어 있어서 필요한 부분만
    사용 가능

  - POJO 클래스와 약간의 설정만으로도 개발이 가능하므로 개발 생산성을 높일 수 있음

  - 실제 스프링을 적용하면 적용하지 않은 코드의 1/3 정도의 코드만으로 개발 가능

    

- 품질 보증

  - 스프링 프레임워크는 이미 검증된 많은 아키텍처 또는 디자인 패턴을 적용하여 만들어졌기 때문에
    코드에 아키텍처를 구현하기 위한 코드나 디자인 패턴을 사용하기 위한 코드를 개발자가 만들
    필요가 없음

  - 개발에 일관성을 제공해 주고 소프트웨어의 품질을 보증

    

- 유지보수 용이

  - 스프링 프레임워크를 사용하여 작성된 애플리케이션들을 유지보수하는데 소요되는 인력과 시간을
    줄일 수 있기 때문에
  - 여러 프레임워크 중에서 스프링 프레임워크가 업계표준으로 자리잡음



### EJB (Enterprise JavaBean)

- 규모가 커지고 복잡한 애플리케이션 제작을 위해 만들어진 기술

- 컴포넌트 기반

- extends, implements를 많이 사용해서 클래스 의존도가 높고, 복잡하고 제한이 많은 문제

- 별도로 종속되지 않고 간단한 자바 객체를 사용하자는 의도에서 나온 것이 POJO

- Java EE 등의 중량 프레임워크들을 사용하게 되면서 해당 프레임워크에 종속된 "무거운" 객체를 만들게

  되는 것에 반발해서 사용하게 된 용어



### POJO (Plain Old Java Object)

- 자바 언어 사양 외에 어떠한 제한에도 묶이지 않은 자바 객체

- 특정 환경과 규약에 종속되지 않아 필요에 따라 재사용될 수 있는 방식으로 설계된 객체

- 즉, 다른 클래스를 상속 받거나 인터페이스를 구현해야 하는 규칙이 없는 자바 클래스

- 미리 정의 클래스 확장 예

  - public class Test extends javax.serv.....{}

- POJO 대표적인 예

  - JavaBean
    - 생성자와 Getter/Setters만 지닌 단순 자바 객체
    - DTO / VO

- 대표적인 POJO 기반 프레임워크

  - 스프링 프레임워크
  - POJO를 사용하는 장점과 EJB에서 제공하는 엔터프라이즈 서비스와 기술을 그대로 사용할 수 있도록
    지원하는 프레임워크

  

#### 스프링 프레임워크의 특징

- POJO 기반 프레임워크
  - 자바 객체의 라이프사이클을 스프링 컨테이너가 직접 관리하고 스프링 컨테이너로부터 필요한
    객체를 얻어 옴
  
  
  
- DI (Dependency Injection) 지원
  
  - 의존성 주입
  - 각 계층이나 서비스들 사이 또는 객체들 사이의 의존성이 존재할 경우에 스프링 프레임워크가 서로
    연결시켜 줌 (클래스 간 약한 결합 가능)
  
  
  
- AOP (Aspect Oriented Programming) 지원
  
  - 관점 지향 프로그래밍
  - 트랜잭션 로깅, 보안 등 여러 모듈에서 공통적으로 지원하는 기능을 분리하여 사용 가능
  - 반복적인 코드를 줄이고 개발자가 비즈니스 로직에만 집중할 수 있도록 지원
  
  
  
- 뛰어난 확장성
  
  - 스프링 프레임워크의 소스는 모두 라이브러리로 분리되어 있어서 필요한 라이브러리만 가져다 
    사용하면 됨
  
  
  
- Model2방식의 MVC Framework 지원
  
  - Model2 / View / Controller
  - JSP MVC 때보다 코드가 간결



#### 스프링 프레임워크의 핵심 기능

- 의존관계에 있는 객체를 생성 조립해 주는 기능

  

- DI : 의존성 주입

  - 객체 간의 의존성을 개발자가 설정하는 것이 아니라 스프링 컨테이너가 주입시켜 주는 기능
  - 장점 : 객체를 쉽게 확장하고 재사용할 수 있음

  

- IoC (Inversion of Control) : 제어의 역전

  - 객체에 대한 제어권 문제

  - 기존에는 개발자에게 제어권이 있었음

    - new 연산자를 사용해서 객체 생성

  - 스프링 프레임워크에서는 객체의 제어권이 스프링에 있고 인스턴스의 라이프 사이클(생성에서
    소멸까지)을 개발자가 아닌 스프링 프레임워크가 담당

    

#### 스프링 웹 프로젝트

- Spring Legacy Project

  - 스프링 템플릿 프로젝트를 이용하는 프로젝트
  - 모델2 방식 (MVC)의 프로젝트 생성 시 사용

  

- Spring MVC Project

  - 서버 및 여러 설정 필요 (개발자 다 설정해야 함)

  - 실제 개발 업무에서 많이 사용

    

- Spring Starter Project

  - Spring Boot를 이용하는 프로젝트
  - 최대한 간단하게 실행하고, 배포가 가능한 수준의 웹 애플리케이션을 제작하기 위한 목적
  - 개발에 필요한 모든 환경 설정을 갖춰가면서 최소한의 개발을 해야 하는 경우 사용
  - 개발자 복잡한 설정 없이 모든 개발 환경이 준비되기 때문에 초보 개발자도 쉽게 웹 프로젝트 
    생성 가능
  - 최근에는 Spring Boot 프로젝트 많이 사용



- Simple Spring Maven (Maven Project)

  - Spring 라이브러리의 기본 세트를 포함하는 Maven을 사용하여 간단한 Spring 프로젝트 생성

  - Maven (메이븐)

    - Java용 프로젝트 관리도구

    - XML 기반의 정적인 빌드 제공

    - 그레이들(Gradle)
      - 그루비(groovy) 스크립트 기반의 동적인 빌드 기능 제공
      - 안드로이드 앱을 만들 때 필요한 공식 빌드 시스템
      - 메이븐보다 빌드 작업이 간단하며 프로그래밍만으로 기능 추가 가능
      - 별도의 빌드 스크립트를 통하여 사용할 애플리케이션 버전, 라이브러리 등 설정




#### 의존성 (Dependency)

- 객체 간 의존성

- 한 클래스가 다른 클래스의 객체를 통해 그 클래스의 메소드를 실행할 때 이를 '의존'한다고 표현

- new 연산자를 통해 다른 클래스의 객체 생성 사용

- 예1

  - MemInsertController 클래스에서

  - MemberDAO 클래스의 객체 dao를 생성

    ```jsp
    MemberDAO dao = new MemberDAO();
    dao.insert(dto);
    
    BoardDTO dto = new BoardDTO();
    ```
  
  - DI(Dependency Injection : 의존성 주입)

    - 외부에서 빈(객체)을 만들어 필요로 하는 곳에 전달해 주도록 하는 것
    - 즉, 개발자가 new 연산자를 사용하여 직접 객체를 생성하지 않고 외부에서 생성된 bean을 IoC 
      컨테이너가 넣어 주는 방식
    - 일반적으로 부품(빈)을 조립해서 사용한다고 함
  
  - DI 방법을 사용하는 이유

    - 의존하는 객체의 클래스가 변경되거나 다른 클래스의 객체를 사용하게 될 경우
    - 의존 관계(결합 관계)에 있는 다른 모든 클래스들의 소스 코드도 변경해야 하는데 의존성 
      주입 방법을 사용하면, 클래스 결합 상태를 변경하거나 객체를 주입하는 부분만 수정하면 
      되므로 수정할 코드의 양을 줄일 수 있다는 장점이 있음



#### 스프링에서 의존성 주입 방법

- XML을 이용한 방법

  - XML 설정 파일에 bean 태그 설정

- Annotation을 이용한 방법

  - 자바코드에서 '@어노테이션이름'으로 설정

  

1. 스프링을 사용하지 않는 DI

   1.1 DI를 사용하지 않는 코드

   - 의존성 관계가 있는 객체를 개발자가 new 연산자를 이용해서 직접 생성

   

   1.2 DI를 사용하는 코드

   - 생성자 기반 DI

     - 의존성 관계에 있는 객체를 new를 통해 직접 생성하지 않고 생성자를 통해 외부에서 전달

     

   - Setter 기반 DI

     - Setter 메소드를 이용하여 의존성 주입 수행

   

2. 스프링을 사용한 DI

   2.1 XML을 이용한 DI

   - XML 파일에 빈(bean : 부품)을 정의 하고 의존성 설정

     ```java
     <bean id=”이름” class=”패키지명.클래스명”>
         
     <ref bean=”의존하는 빈”>
     ```

   - XML을 이용해서 의존성을 주입하기 위해서는 클래스에 생성자 또는 Setter 메소드가 있어야 함

   - 스프링은 Pre-loading 방식 사용

     - ApplicationContext를 이용해서 컨테이너를 구동하면 컨테이너가 구동되는 시점에서
       스프링 설정 파일에 등록된 빈을 생성하고 컨테이너에 로드

     

   - 생성자 기반 DI

     - 클래스에 생성자가 있고 스프링 설정 파일(xml)에서 빈을 정의할 때

       ```java
       <constructor-arg ref=”의존하는 빈”> // 태그를 이용하여 의존성 주입
       ```
   
     - Main에서 객체 생성하지 않고 XML 설정 파일에서 빈 생성
   
     - main() 하는 역할
   
       - 컨테이너 객체 생성
       - 컨테이너에서 컴포넌트(빈) 가져옴
   
     
   
   - Setter 기반 DI
   
     - 클래스에 반드시 Setter 메소드가 있어야 하고 스프링 설정 파일(xml)에서 태그 
       이용하여 의존 객체 주입
     
       ```java
       <property name=”nameService” ref=”nameService” />
       // name : Setter 메소드 이름 (setNameService())
       // ref : 참조 객체 이름
       ```
     
     - 주의
     
       - Setter 메소드를 사용할 경우에는 기본 생성자 외에 다른 생성자를 정의해서는 안 됨

 

