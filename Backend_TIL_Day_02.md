# Backend_TIL_Day_02



- 목차
  - servlet
    - 자바스크립트로 서블릿 요청
    - jQuery 사용해서 서블릿에 요청
    - 서블릿 포워딩
    - 바인딩

  - JSP(Java Server Page)
    - JSP 페이지 구성
    - JSP 내장 객체






## Servlet



### 자바스크립트로 서블릿 요청

- DOM 사용

  ```javascript
  /* 자바스크립트로 서블릿에 요청 : DOM 사용 */
  window.onload = function(){
      var formLogin = document.getElementById("frmLogin");
  
      formLogin.onsubmit = function(){
          // id : 참조객체변수
  
          var id = document.getElementById("id");
          var pw = document.getElementById("pw");
  
          if(id.value == "" || pw.value == ""){
              alert("아이디와 비밀번호는 필수입니다");
              return false;
          }else {
              formLogin.method = "post";
              formLogin.action ="loginJs";
              formLogin.submit();
          }
      }
  };
  ```

  

- name 속성 사용

  ```javascript
  /* 자바스크립트로 서블릿에 요청 : name 속성 사용 */
  function fn_validate() {
      var formLogin = document.frmLogin;
      var id = formLogin.user_id.value;
      var pw = formLogin.user_pw.value;
  
      if(id == "" || pw == ""){
          alert("아이디와 비밀번호는 필수입니다2");
          return false;
      }else {
          formLogin.method = "post";
          formLogin.action ="loginJs";
          formLogin.submit();
      }
  }
  ```

  

### jQuery 사용해서 서블릿에 요청

```javascript
/* jQuery 사용하여 서블릿에 요청 */
$(document).ready(function(){
    $("#loginBtn").on("click", function(){
        var id = $('#user_id').val();
        var pw = $('#user_pw').val();

        if(id == "" || pw == ""){
            alert("아이디와 비밀번호는 필수입니다3");
            return false;
        }else {
            $('#frmLogin').attr({
                mathod: "post",
                action: "loginJs"
            }).submit();

            /* $('#frmLogin').attr('method',"post").attr('action',"loginJs").submit(); */
        }	/* 이렇게 사용도 가능 */
    });
});
```





### 서블릿 포워딩

- 포워딩
  - 서블릿에서 다른 서블릿이나 JSP 페이지로 요청을 전달하는 기능
  - 용도
    - 요청에 대한 추가 작업을 다른 서블릿에서 수행
    - 요청에 포함된 정보를 다른 서블릿이나 JSP 페이지와 공유
    - 요청에 정보를 포함시켜 다른 서블릿으로 전달
    - 컨트롤러에서 뷰로 데이터 전달



#### 서블릿에서 포워딩 방법 4가지

1. redirect 방법

   - 웹 브라우저에 재요청하는 방식 

   - HttpServletResponse 객체의 sendRedirect() 메소드 이용

   - 형식 

     ```java
     sendRedirect("포워드할 서블릿 또는 JSP");
     ```

     

2. Refresh 방법

   - 웹 브라우저에 재요청하는 방식

   - HttpServletResponse 객체의 addHeader() 메소드 이용

   - 형식 

     ```java
     addHeader("Refresh", "경과시간(초);url=요청할 서블릿 또는 JSP");
     ```

   

3. location 방법

   - 자바스크립트에서 재용청하는 방식

   - 자바스크립트의 location 객체의 href 속성 이용

   - 형식

     ```java
      location.href  = "요청할 서블릿 또는 JSP"
     ```

     

4. dispatch 방법

   - 서블릿이 직접 요청하는 방식 (일반적으로 포워딩 기능 지칭)

   - 형식

     ```java
     RequestDipatcher dis = request.getRequestDipatcher("포워드할 서블릿 또는 JSP");
     dis.forward(request, response);
     ```



#### 포워딩 방법들의 차이점

- redirect, Refresh, location 방법
  - 서블릿이 웹 브라우저를 거쳐서 다른 서블릿이나 JSP에게 요청하는 방법
- dispatch 방법
  - 클라이언트를 거치지 않고 서블릿에서 바로 다른 서블릿에게 요청하는 방법
  - url이 바뀌지 않음 (즉, 클라이언트 측에서는 포워딩이 진행되었는지 알 수 없음)



포워딩 하면서 데이터 전달

```java
response.sendRedirect("second04?name=kim");
String name = request.getParameter("name");
```

1. 값 지정해서 전달
2. 변수 사용 : 변수값이 전달되도록
3. 한글 인코딩 : URLEncoder.encode() 사용



#### 바인딩

- 수십 개 또는 많은 양의 회원 정보나 상품 정보를 전달해야 할 경우 포워딩 방식만 
  사용할 경우 문제
- 서블릿에서 다른 서블릿 또는 JSP로 대량의 데이터를 공유하거나 전달할 때 
  바인딩(binding) 기능 사용

- 방법
  - 포워딩할 때 setAttribute("바인딩이름", 데이터) 메소드를 사용해서 바인딩 이름과
    데이터를 묶어서 설정한 후
  - 포워딩된 문서에서 getAttribute("바인딩 이름") 메소드 사용해서 바인딩된 데이터를
    추출해서 사용
  - redirect 방식으로는 전송 안 되고 dispatch 포워딩 방식 사용



#### DTO vs VO

- DTO (Data Transfer Object)

  - 데이터 저장 담당 클래스 (Model)
  - Controller, Service, View 등 계층간 데이터 교환을 위해 사용되는 객체
  - 비즈니스 로직을 갖지 않는 순수한 데이터 객체
  - Getter / Setter 메소드만 포함
  - 가변의 성격 (Setter : 값을 설정 (값이 바뀜))

  

- VO (Value Object)

  - 데이터 저장 담당 클래스 (Model)
  - DTO와 혼용해서 사용되지만 VO는 값(value)을 위해 사용되는 객체로 불변(read only)의 속성
  - 보통 Getter의 기능만 포함
  - 일반적으로 스프링에서 VO로 사용되지만 Getter / Setter 기능 다 사용하는 
    경우도 있음





## JSP(Java Server Page)



- 서버 사이드 스크립트 언어
- Java 기반으로 HTML 문서 내에 자바코드를 삽입해서 웹 서버에서 동적으로 웹 페이지를 
  생성한 후 클라이언트에게 반환
- JSP를 통해 HTML과 동적으로 생성된 컨텐츠를 혼합해서 사용
- Servlet을 보완한 스크립트 방식 표준
  - Servlet 기능 + 추가 기능
- JSP는 실행되면 Servlet(.java)으로 변환되어 컴파일되서 클래스(.class)파일로 만들어져 실행
- View를 담당하는 페이지로 사용



#### JSP와 서블릿과의 차이점

- JSP
  - HTML 내부에 Java 소스코드가 들어 있는 형식
  - 사용하기 편리
- Servlet
  - Java 코드 내에 HTML 코드 포함
  - 읽고 쓰기 불편



#### JSP 페이지의 구조

- 정적페이지 + 동적페이지
- 정적페이지 구현 : HTML 태그
- 동적 페이지 구현 : 스크립트 사용
  - <%@ %>
  - <% %>
  - <%! %>
  - <%= %>



#### JSP 페이지 내용 

- HTML 문서 내용 / JSP 태그 / 자바 코드



### JSP 페이지 구성

- #### 지시어 

  - JSP 페이지의 전체적인 속성을 지정할 때 사용

  - JSP 컨테이너에게 전달하는 JSP 페이지 관련 메시지

  - <%@ 지시어 속성1=값, 속성2=값, .....%>

    

  - page 지시어 

    - JSP 페이지에 대한 속성 설정

      ```jsp
      <%@ page ... %>
      ```

      

  - include 지시어

    - 공통적으로 포함될 내용을 가진 파일을 해당 JSP 페이지내에 삽입하는 기능을 제공

    - 복사 & 붙여넣기 방식으로 두 개의 파일이 하나의 파일로 합쳐진 후 하나의 파일로서 
      변환되고 컴파일

      ```jsp
      <%@ include file= "포함될 파일의 url" %>
      ```

      

  - taglib 지시어

    - 표현 언어 (EL : Expression Laguage), JSTL(JSP Standard Tag Library)를 JSP 페이지 내에서 사용

      ```jsp
      <%@ taglib prefix="c" uri="http...." %>
      ```

      

- #### 스크립트 요소

  - 선언문(Declaration)

    - JSP 페이지의 멤버 필드 선언 또는 메소드를 정의할 때 사용

    - 선언문에서 선언된 변수는 페이지 전체에서 사용 가능(전역 변수 의미)

    - 형식 

      ```jsp
      <%! 선언%>
      예 : <%! int a = 20; %>
      ```

      

  - 표현식(Expression)

    - 변수 값, 계산 결과, 함수 호출 결과를 직접 출력하기 위해 사용

      ```jsp
      <%= 식 %>
      <%= 변수명 %>
      예 : <%= 3*5 %>
      ```

      

  - 스크립트릿

    - 자유롭게 자바 코드를 기술할 수 있는 영역

    - 스크립트릿에서 선언된 변수는 지역 변수의 개념

      - 선언된 이후부터 사용 가능

        ```jsp
        <% 자바코드 %>
        ```

        

- #### 액션 태그



#### JSP 태그

- <%로 시작하고 %>로 종료

- @, !, =, -- 문자를 추가하여 태그의 의미 부여

  

#### 주석

- HTML 주석 : <!-- -->
- JSP 주석 : <%-- --%>
- 자바 주석 : // , /* */
- Ctrl + Shift + / : 해당 영역에 맞는 주석 표시



### JSP 내장 객체

- 클라이언트에서 웹 서버에게 JSP 페이지를 요청하면 자동으로 생성
- 객체 생성하지 않고 바로 사용 가능



- #### 내장 객체 종류

  - 입출력 : request / response / out

  - 서블릿 : page / config

  - 컨텍스트 : session / application / pageContext

  - 예외 처리 : exception










