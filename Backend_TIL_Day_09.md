# Backend_TIL_Day_09



- 목차





## CDATA

- 파싱되지 않는 문자 데이터
- 쿼리를 작성할 때, <, >, >=, &, || 등을 사용해야 하는 xml 태그로 인식해서 오류 발생 할 수 있음
- XML 파싱 대상이 아닌 단순 문자열로 처리하라는 의미



## REST

- 브라우저에서 페이지 요청 시
  - PC에서는 페이지 전체를 다시 전송해서 표시해도 문제 없지만 스마트폰 등의 모바일
    기기에서는 기존 화면은 그대로 유지하면서 필요한 내용만 추가해서 화면에 표시
    - 모바일 기기가 유선 기기보다 네트워크 전송량이 떨어지므로 현재 화면은 그대로 
      유지하면서 필요한 데이터만 전송 받아 빠르게 표시하기 위해
  - 데이터만 전송하는 기능의 표준화 필요성이 대두 되었는데 REST 방식이 그 대한으로 사용됨



### REST (Representational State Transfer)

- URI가 고유한 리소스를 처리하는 공통 방식
- 예 : /board/112로 요청할 경우
  - 게시글 중 112번째 글 의미
- REST 방식으로 제공되는 API를 REST API (또는 RESTful API)라고 함
- 트위터와 같은 Open API에서 많이 사용됨



#### 스프링에서 REST 방식의 데이터 처리

- 스프링 3버전
  - @ResponseBody 어노테이션 지원
  - 메소드 레벨 : 메소드 위에 붙임
- 스프링 4버전
  - @RestController 어노테이션 이용 : 권장
  - 컨트롤러 레벨
    - REST 기능을 하는 컨트롤러에 붙임
    - 모든 메소드에 적용



### Synchronous  vs Asynchronous 



#### Synchronous (동기식) 통신

- Request를 보내고 Request에 대한 Response를 받는 것으로 두 서버 사이의 
  Transaction을 맞추는 통신 방식
- Request를 보낸 Thread는 Response가 도착하기 전까지는 아무 것도 하지 못하는 
  Block 상태가 됨을 의미
- Request1 -> Response1, Request -> Response2



#### Asynchronous (비동기식) 통신

- 





## Ajax (Asynchronous JavaScript and XML)

- 클라이언트에서 비동기 방식으로 자바스크립트를 이용하여 화면 전환 없이 서버 측에
  데이터를 요청할 때 사용
- TEXT, HTML, XML, JSON 등의 데이터 처리 가능
- 웹 서버 환경에서 실행



### $.ajax() 메소드

- 사용자가 지정한 URL 경로에 있는 파일의 데이터를 전송
- 입력한 URL 경로의 파일로부터 요청한 데이터를 불러오는데 사용
- 불러올 수 있는 외부 데이터는 텍스트, HTML, XML, JSON 유형 등 다양





