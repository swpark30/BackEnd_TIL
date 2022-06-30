# Backend_TIL_Day_03



- 목차



## JSP



### JSP 내장 객체



response 객체

- JSP 페이지에서 처리한 결과를 웹 브라우저에 응답할 때 사용

- 헤더 설정, 코드 상태, 쿠키 등 정보 포함되어 있음

- 응답 콘텐츠 설정, 응답 헤더 설정, 상태 코드 설정과 관련된 메소드 제공

  

out 객체

- 웹 서버에서 웹 브라우저에게 출력 스트림으로 응답하기 위해 사용

  ```jsp
  out.println(“출력 문자열”);
  
  표현식 <%= 출력문자열 %>과 동일
  ```

- println() : 줄바꿈 적용되지 않음

- print()와 동일한 결과 (스페이스 한 칸 정도 차이)

- 줄바꿈 하기 위해서는 br 태그 사용

- 전송되는 데이터 타입 : 문자열

- 숫자 연산을 할 경우 숫자형으로 형변환 필요

   

### 액션 태그

- JSP 페이지 내에서 어떤 동작을 지시하는 태그
- 어떤 동작 또는 액션이 일어나는 시점에 페이지와 페이지 사이에서의 제어 이동 또는 다른 페이지의 
  실행 결과를 현재 페이지에 포함하는 기능 제공



#### 액션 태그 종류

- include 액션태그 

  - 다른 페이지의 실행 결과를 현재 페이지에 포함시킬 때 사용

  - 페이지를 모듈화할 때 사용

    ```jsp
    <jsp:include page=”포함될 페이지” flush=”true” />
    ```

  - 속성

    - page 속성
      - 결과가 포함될 페이지
    - flush 속성
      - 포함될 페이지로 제어가 이동될 때 현재 포함하는 페이지가 지금까지 출력 버퍼에 
        저장한 결과를 처리하는 방법을 결정
      - true
        - 현재 페이지가 지금까지 버퍼에 저장한 내용을 웹 브라우저에 출력하고 버퍼를 비움



- forward 액션 태그 

  - 현재 페이지에서 다른 특정 페이지로 전환

  - 웹 페이지 간의 제어를 이동시킬 때 사용

    ```jsp
    <jsp:forward page=”포워딩할 JSP 페이지” />
    ```

    

- param 액션 태그 

  - 이동하는 페이지에 파라미터 값을 전달할 때 사용

    

#### 자바빈(JavaBeans)

- DTO/VO와 같은 개념

- 데이터를 다루기 위해 자바로 작성되는 소프트웨어 컴포넌트로 재사용 가능

- 입력 폼의 데이터와 데이터베이스의 데이터 처리 부분에서 활용

- 클래스로 작성

  - 멤버 필드로 속성 (property)이 있고 멤버 메소드로 Getter/Setter 메소드 포함
  - setXXX() : 프로퍼티에 값 저장
  - getXXX() : 프로퍼티 값 반환

- 액션 태그를 이용해서 빈 사용

- 속성 접근 제어자는 private

- Getter/Setter 메소드와 클래스는 public

  

- 자바빈 관련 액션 태그

  - useBean 액션 태그

    - 자바빈을 JSP 페이지에서 이용할 때 사용

    - DTO / VO에 해당

      ```jsp
      <jsp:useBean id=”” class=”” scope=”” />
      ```

      

  - setProperty 액션 태그 

    - 프로퍼티 값을 세팅할 때 사용

      ```jsp
      <jsp:setProperty name=”” property=”” value=”” />
      ```

      

  - getProperty 액션 태그

    - 프로퍼티 값을 가져올 때 사용



모든 속성을 한꺼번에 설정

- form의 input 태그 속성명을 클래스 필드명과 동일하게 지정하고 설정

  ```jsp
  <jsp:setProperty property="*".. />
  ```





JSP 발전 과정

- 초기 : HTML 태그를 중심으로 자바를 이용해 화면 구현
- 화면에 대한 요구사항이 복잡해지면서 자바 코드를 대체하는 액션 태그 등장
- 복잡한 자바 코드를 제거하는 방향으로 발전
- 현재 JSP 페이지는 스크립트 요소보다 표현 언어나 JSTL을 사용



### 표현 언어 : EL(Expression Language)

- 자바코드가 들어가는 표현식을 좀 더 편리하게 사용하기 위해 JSP 2.0부터 도입된 데이터 출력 기능

- 표현식 또는 액션 태그 대신 값을 표현

  ```jsp
  // 표현식 대신 사용
  <%= 값 %> 이렇게 표현한 것을 ${값} 이렇게 바꾼다
  
  parameter : ${param.이름}
  
  // 액션 태그 대신 사용 
  <jsp:getProperty name=”member” property=”id” />
  => ${member.id}
  ```

- 연산자

  - 산술 연산자 : +, -, \*, /, %, (div, mod)

  - 관계 연산자 : 

    - , >=, <, <=, ==, !=
    - (gt, ge, lt, le, eq, ne)

  - 논리 연산자

    - &&, ||, !, (and, or, not)

  - 조건 연산자

    - 수식 ? 참일때 값 : 거짓일때 값

  - empty 연산자

    - 값이 null 이거나 길이가 0이면 참(true)

      ```jsp
      ${empty 변수}
      ${not empty 변수} //변수가 null이 아니거나 0이 아니면 참
      ```

      

- EL 내장 객체

  - Scope

  -  요청 파라미터

  - 쿠키 값

  - JSP 내용

    - pageContext 객체

      - 컨텍스트 이름 (프로젝트명) 출력

      - getContextPath() 메소드 이용해서 컨텍스트 이름 가져오기

        ```jsp
        기존에는
        <a href=”/JSP01/el/login.jsp”>로그인</a>
        
        JSP표현
        <a href=”<%= request.getContextPath()%>/el/login.jsp”>로그인</a>
        el표현
        <a href=”${pageContext.request.contextPath}/el/login.jsp”>로그인</a>
        ```

  - 초기 파라미터



표현 언어로 바인딩 속성 출력

- request, session, application 내장 객체에 속성을 바인딩한 다른 서블릿이나 JSP에 전달 가능

- 자바 코드 사용하지 않고 바인딩된 속성 이름으로 바로 값 출력

  ```jsp
  request.setAttribute("바인딩이름", 값);
  
  el표현
  ${바인딩 이름}
  ```



scope 우선 순위

- request, session, application 내장 객체에는 데이터를 바인딩해서 다른 JSP로 전달
- 각 내장객체에 바인딩하는 속성 이름이 같은 경우
- 각 내장 객체에 지정된 출력 우선순위에 따라 순서대로 속성에 접근
  - 높은 쪽 page < request < session < application 낮은 쪽

- pageScope  : 현재 페이지 영역의 변수
- requestScope : 이전 페이지에서 받아온 영역의 변수
- sessionScope : session 영역의 변수
- applicationScope : application 영역의 변수



## JSTL (JSP Standard Tag Library)



- JSP 표준 태그 라이브러리

- JSP와 HTML을 같이 사용함으로써 가독성이 떨어지는 것을 보완하고자 만들어진 태그 라이브러리

- JSP 페이지 내에서 자바 코드를 사용하지 않고 태그를 사용하도록 함

- JSP 페이지의 로직을 담당하는 부분인 제어문 및 데이터베이스 처리 등을 표준 커스텀 태그 제공

- 사용하기 위해서는 라이브러리 별도 필요

  ```jsp
  <%@ taglib uri="" prefix="" />
  ```

  

JSTL 라이브러리 : 5개의 라이브러리로 구성

- core 

  - URI : http://java.sun.com/jsp/jstl/core

  - prefix : c

  - 변수의 선언 및 삭제 등의 변수와 관련된 작업

  - if, for문 등과 같은 제어문

  - url 처리 및 그밖에 예외처리 및 화면 출력

  - c:set 태그

    - 변수 선언

      ```jsp
      <c:set var=”변수명” value=”변수값” [scope] />
      ```

  - c:if 태그

    - 조건문을 사용할때 씀 : else 문 없을 때

      ```jsp
      <c:if test=”${조건식}” [scope] />
      ```

  - c:choose 태그

    - 자바의 switch문과 같지만, 조건에 문자열 비교도 가능하고 쓰임의 범위가 넓음

    - 서브 태그로 when과 otherwise를 가짐

    - else가 필요할 때

      ```jsp
      <c:when test=”조건식1”>내용1</c:when>
      <c:when test=”조건식2”>내용1</c:when>
      <c:otherwise>내용n</c:otherwise>
      ```

      

- format : 숫자/날짜/시간 지정, 국제화, 다국어 처리

- sql : 데이터베이스 작업 처리

- xml : XML 문서 처리

- functions : 함수 기능



