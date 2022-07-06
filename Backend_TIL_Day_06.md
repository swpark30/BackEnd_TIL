# Backend_TIL_Day_06



- 목차
  - MVC
    - RequestMapping 다중 맵핑
    - View 페이지에서 컨트롤러로 데이터 전달

  - 스프링 데이터베이스 연동
    - MyBatis(마이바티스)
    - MyBatis 연동 스프링 프로젝트 작성 순서






## MVC



### RequestMapping 다중 맵핑

- 한 개의 메소드를 여러 요청 경로로 접근 처리 가능

- @RequestMapping(value={“요청경로1”, “요청경로2”})

  

### View 페이지에서 컨트롤러로 데이터 전달

1. form을 통한 데이터 전달

   - form 데이터를 컨트롤러로 전송할 때 스프링에서 HTTP 요청 파라미터 가져오는 방법 

     1. getParameter() 메소드 사용

        - request.getParameter("no");

     2. @RequestParam 어노테이션 사용

        - 메소드의 파라미터로 설정
        - (@RequestParam("stdNo") String stdNo, ....)

     3. Command 객체 사용

        - 데이터 저장용 클래스 생성(Student)
        - 요청을 수행하는 메소드에서 Student 객체 사용(커맨드 객체)
        - Command 객체는 자동으로 View의 Model에 등록
        - View 페이지에서 $(객체.필드명)
        - 주의 
          - form의 `<input>`태그의 name 속성명과 Student 클래스의 멤버 필드명이
            동일해야 함
          - 이름이 다르면 필드에 값이 저장되지 않음

     4. @ModelAttribute 어노테이션

        - Command 객체 사용 시 Model 설정 이름(객체 이름)변경 가능

        - @ModelAttribute(“stdInfo”) Student student

        - ${stdInfo.stdNo}

          

2. url을 통한 전달

   - @PathVariable 어노테이션 사용

     ```jsp
     학번 : ${stdNo}
     
     <a href="/project/student/studentDetailView/${stdNo}">${stdNo}</a>
     
     @RequestMapping("/student/studentDetailView/{stdNo}")
     public String studentDetailView(@PathVariable String stdNo){...}
     ```

   - HashMap으로 받기

     - 여러 개의 값을 HashMap으로 받을 수 있음
     - 학생 검색 폼
       - 검색 조건 : type
       - 검색 값(입력값) : keyword

   - 컨트롤러

     - @RequestParam HashMap<String, Object> param





## 스프링 데이터베이스 연동

- MyBatis 사용



### MyBatis(마이바티스)

- ORM(Object Relational Mapping : 객체 관계 맵핑)프레임워크
- 자바에서 JDBC를 이용할 경우 java 언어와 SQL 언어가 한 파일에 존재해서 
  재사용성이 좋지 않음
- MyBatis가 JDBC의 이런 단점을 개선하여 SQL 명령어를 별도의 XML 파일에 분리하고
  SQL 명령어와 자바 객체를 맵핑해주는 기능을 제공
- SQL 재사용
- 효율적, 쉬움
- 특징
  - SQL 명령어를 자바 코드에서 분리하여 XML 파일에서 관리



#### MyBatis 연동 스프링 프로젝트 작성 순서

1. MVC 프로젝트 생성
2. pom.xml 기본설정
   - java : 11
   - Spring : 5.2.22.RELEASE
   - Maven 1.8
3. 프로젝트 설정
   - Java Compiler
   - Java Build Path
   - Project Facets
4. pom.xml에 데이터베이스 의존성 설정 (라이브러리 추가) 
   - Spring JDBC 의존성 : spring-jdbc
   - Connection Pool 의존성 : commous-dbcp
   - mysql 의존성
5. 데이터베이스 연결 정보설정
   - jdbc.properties 파일 생성
     - jdbc.driverClassName
     - url / username / password
   - 스프링 설정 파일 생성 : application-config.xml
     - DataSource / Mapper 지정
   - web.
6. 클래스 구성 : CRUD 기능 구현
   - 컨트롤러
   - 서비스 인터페이스 / 클래스
   - VO
   - DAO / Mapper (XML)
   - 뷰 페이지 작성
   - 페키지 생성
     - controller
     - dao
     - model
     - service