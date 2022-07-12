# Backend_TIL_Day_10



- 목차





@RestController 이용해서 REST 기능 구현

- 컨트롤러 레벨
  - REST 기능을 하는 컨트롤러에 붙임
  - 모든 메소드에 적용
- 컨트롤러에서 브라우저로 기본형 데이터, VO 객체의 속성값, Map에 저장된 데이터 등의 데이터 전손 가능



@Controller vs @RestController

- @Controller : 결과를 뷰 페이지(jsp)로 표시
  - 뷰 페이지 이름을 반환
- @RestController
  - 별도의 뷰를 제공하지 않은 채 데이터 전달





## 스프링 부트 (Spring Boot) 

- 스프링 프레임워크를 사용하는 프로젝트를 아주 간편하게 설정할 수 있는 
  스프링 프레임워크의 서브 프로젝트

  

- 특징

  - XML 기반 설정 과정 없이 간단히 프로젝트를 시작할 수 있다
  - 메이븐의 pom.xml 파일에 의존성 라이브러리의 버전을 일일이 지정하지 않아도 됨
    (스프링 부트가 권장 버전 관리)
  - 단독 실행되는 스프링 애플리케이션 구현 가능
  - 프로젝트 환경 구축에 필요한 서버 외적인 툴들이 내장되어 있어서 별도 설치 필요 없음
    - 톰캣 내장되어 있음



#### 스프링 부트 프로젝트 생성 과정

1. 스프링 부트 프로젝트 생성
   - 프로젝트명 / Group / Artifact / 패키지명
   - Dependencies 선택
     - SQL : JDBC API / MyBatis Framework / MySQL Driver
     - Web : Spring Web
2. 프로젝트 생성 후 확인
   - pom.xml 내용 확인
     - java.version / jdbc / mysql-connector / tomcat
   - 자동 생성된 클래스 파일 확인 
     - ServletInitializer.java
       - 스프링 부트 애플리케이션을 web.xml 없이 톰캣에서 실행하게 해주는 클래스
       - 스프링 부트에는 web.xml, context.xml 설정 파일 없음
     - ..... Application.java
       - @SpringBootAplication 붙어 있음
       - 스프링 부트 애플리케이션으로 설정하는 어노테이션
       - main() 메소드 포함
3. 스프링 설정 파일 
   - application.properties 파일이 자동 생성됨
     (내용이 없는 빈 파일로 생성)
   - 추가할 내용
     - 포트 번호
     - 데이터베이스 연결 정보
     - mapper.xml 위치 지정
       - src/main/resources 파일에 생성할 것
   - 여기서 컨트롤러 추가하고 ("/") 실행시켜서 오류 있는지 확인
4. JSP 뷰 설정
   - 스프링 부트는 JSP 뷰가 기본이 아니기 때문에
   - JSP 뷰를 사용할 경우 추가 설정 필요
     - application.properties 파일에 JSP 설정 추가
     - pom.xml 의존성 라이브러리 추가
     - src/main/webapp 폴더에 WEB-INF/views 폴더 추가
     - hello.jsp 생성
     - 컨트롤러에서 @RequestMapping 추가해서 hello.jsp 실행되는지 확인
     - 스프링 부트에서 리소스 파일 경로 확인
5. DB 연동 CRUD 기능 구현
   - spring_mvc_mybatis에서 product 코드는 그대로 사용
   - 파일 위치 주의



