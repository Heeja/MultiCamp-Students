Web 3-Tier 구조

1. Client(Webbrowser)
2. Web Server
3. Storage



Redirection



대부분의 Web Server에서는 Domain(daum.net이나 naver.com)을 입력하면 Index.html을 Return하는 암묵적인 약속을 정했다.



https://logins.daum.net/accounts/login.do?slevel=1

?의 뒤쪽을 사용자 입력



url에 확장자명, 파일명이 보여지는 것은 보안에 굉장히 취약한 부분이다.

alias로 url을 전송하여 1차적 예방을 하려고 했다.
spring 에서 alias기능을 하도록 .do라는 문법이 있는데 사람들이 spring은 .do로 사용해야하는 줄 알고 대부분의 사람들이 .do로 url을 지정하게된다.
그래서 .do라는 url주소를 보게되면 이 Web Server는 Spring으로 동작하는 것을 알게되는 웃기는 상황이 벌어졌다.



#### 동적 웹

Client 스크립트 코드: javascript

Server 스크립트 코드: PHP, JSP, ASP

Web page를 표현할 때 다순 HTML문서이면 Client(스마트폰 같은)에서 직접적으로 표현을 하지만, 오늘날 동적인 Web page는 Javascript를 처리하여 표현하기 때문에 Client의 사양이 중요하게 되었다.



SPA(Single P Application)



비동기적 호출

첫 페이지를 불러온 상황에서 다음 동작에서 이 페이지를 갱신하지 않겠다는 객체를 

네트워크 밴드위스가 확연히 줄겠지만, 더 많은 리퀘스트가 전송될 수 있다.
(Ex. 추천검색어)



비기능적 요구사항

- 기획자에게 직접 물어보고 세부적인 사항을 정해야한다.
- 퍼포먼스는 어느정도까지인지, 접속자 수, 사양, 프로토콜 방식, 컨텐츠 구성방식, CGI기술 선택여부, DB 종류 선택 등..



인터넷 뱅킹

- R-DB로 구성되어 있다. 고정되어 있는 것이 많다. (고정 스키마)



NoSQL - 유튜브, 인스타그램 ...

- 사용자마다 사진, 영상, 텍스트 업로드 데이터가 다른데 고정된 스키마를 사용하기엔 부적합하다.
- 그래서 근래에는 
- 받아들이는 데이터(사진, 영상, 텍스트)에 따라 



**결론: 아주 디테일한 것 까지 알지 못하면 아키텍쳐를 만들 수 없다.**



##### 어디까지 배워야할까요?!?!

1. 객체지향 개념 (Object Oriented Concept)
2. Learn - Language Syntax > 1을 이해는데 도움
3. Make StandAlone Programs > 1,2를 이해하는데 도움
4. Make O/S or Web Application > 1,2,3을 이해는데 도움
5. Make Framework > 1~4를 이해하는데 도움
6. Object Oriented Analysis & Design - Work 1 year > 1~5를 이해하는데 도움

* 처음엔 단지 따라하는 정도, 한번 한다고 다 이해하는것은 거의 불가능.
  에자일하게 하는것이 아니라 제대로 프로젝트를 수행했을때!
  1~7년 가량 프로젝트를 수행해야 리더가 될 수 있을 것이다..



한 페이지에서 리퀘스트 되는 양이 많으면 좋은 서비스는 아닐 수 있다.



CGI의 최종 형태는 Web Browser에 html로 전달되어야 한다.
최종형태는 Client에서 구동될 수 있는, 구동되기 가장 좋은 형태로 전달되어야 한다.



Web Server와 CGI가 같은 구조에 있어야 구동된다.



#### 실습1 Enterprise Web Architecture 구성

1. Tomcat 설치
2. JDK 설치
3. 설치한 JDK의 JAVA_HOME 환경변수 설정

* Web page의 정적인 페이지를 수정할 경우 JDK(and JRE)는 아무동작하지 않는다.





### 웹 실습환경 구축 (P27)

웹 문서

* 컴퓨터 파일 
* HTML5 파일 (.htm, *.html)





### HTML5 문서 작성 (P36)

* HTML 구조

```
<!DOCTYPE HTML> //선언의 시작으로 HTML5 언어를 시작
<html>
<head>

</head>
<body>

</body>
</html>
```

* HTML 요소 표현
  \<a href="http://naver.com"> 네이버로 가자 \</a>
  \<a>: 	요소 시작. 요소명(a)
  href: 	속성
  "http://naver.com": 속성값. 속성값은 문자열 ""로 표현해줘야 한다.
  네이버로 가자: 요소내용
  \</a>: 종료태그

* HTML
  * Head
    * title, meta, link, style, script
  * Body
    * 글자: strong, b, i, super ...
    * 문단: h1~h6, pre, p, br, hr ...
    * 멀티미디어: img, audio, video
    * 하이퍼링크: a
    * 외부파일: iframe, object, embed
    * 문서 레이아웃: div, span
    * 입력양식: form, input, select, textarea ...
    * 시맨틱 문서: header, nav, ...



**!!!!HTML5 시멘틱 문서 구조가 나온 이유**

Google이 크롤링엔진.. 웹사이트, 웹페이지의 텍스트를 수집하여 잘 분류하기 위해..
**정보제공 문제** - 보안적 문제. 페이지의 의미&용도를 알 수 있게 된다(?)



**Inline Element**: 



**Inline Block**: span, a, img, input, select ...

**Line Block**: div, h1~6, p, pre, ul, ol, table, form ...



**Session**
CGI는 같은 메모리에서 동작한다.
같은 메모리에 있지만 아무대나 접근하지 않고 접근할 수 없다.
그래서 접근할 수 있는 공통 영역을 가지고 있다.
공통된 영역을 다시 사물함 처럼 구역을 나누어 가지고 있으며, 아무나 접근하지 않고 Session Key를 가진 사람이 접근할 수 있다.

**Session ID**
Session에 접근할 수 있는 Key