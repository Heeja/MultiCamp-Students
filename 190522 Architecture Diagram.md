# Architecture Diagram

### **Computing Paradigm의 변화**

* 개발자 편의성 (사용자의 편의성을 위해 발전하지 않는다!)
  

#### Program 기법 측변 변화

1. 50년대 - **절차 중심적 기법**
2. 60~70년대 - **정보공학 기법 (DBMS)**
3. 80년대 - **객체지향 기법 (Smalltalk)**
   사람과 컴퓨터의 사고방식이 다름을 적용.
   사람의 생각이 컴퓨터로 처리되는 과정이 너무 오래걸림
4. 90년대 - **객체지향기법 세계화**
   객체 => Reuse(재사용!)
   * Web의 시대 시작!
5. 2000년대 - <u>**CBD(Component Based Development) 기법**</u>
   객체는 객체가 고장나면 통체로 교체한다.
   Because: 객체 하나 교체하는 것이 복잡하고 어렵기 때문에 객체그룹을 통체로 교체한다.
6. 2005년 - **FlameWork 개발 기법**
   Component: 기능 (구매, 장바구니)
   FlameWork: 구조 (틀 - CS,DB,WEB으로 확장하기 위한 연결 코드를 대신 해주는 기능)
   이것이 편하고 좋다고 마구 사용하였다. => 
7. 2010년 - **Functional 기법**
   Javascript(함수, 객체기반 스크립트 언어)


#### 구조적 측면 (Architecture)

1. Main Frame
2. 데스크탑 시대
3. Client/Server (CS) 시대
   * 개발자들의 지옥시대
   * 다양한 Client에 맞게 응용프로그램을 다시 만들어야하는 개발자들..
   * 누가 만들든지 똑같은 Request/Response를 만들자! - Protocol. HTTP
   * Why HTTP ? - **개발자들이 Text로 HTML을 만들면** 서비스가 가능하기 때문에. = <u>개발자들은 Text로 개발하기 편함!</u>
4. Web Site 시대
   * 정적 html + CSS + js (javascript)
   * 정적 처리의 한계!
   * Web Server와 연계되는 Program이 필요하게 되다.
     (C, C++, VB, 등.. 여러 언어로 Program 개발시도) - CGI(Common Gateway Interface)
   * 더 많은 사람이 서비스를 이용할 수 없을까?!
     (HTTP는 커넥션은 유지하지않는 Stateless 시스템)
   * 프로그램의 단위 = Process. (자원을 공유하지 않는 흐름)
     쓰레드 = Thread. 자원을 공유하는 흐름
   * Thread 프로그램이 너무 어려움을 개발자들이 알게됨!
   * Netscape의 NSAPI - Thread CGI
     MS사의 ISAPI 등.. 여러 Thread 시스템을 가져다 쓰는 시대가 도래하다.
   * Sun사의 Java Servlet의 장점
     1. process/request => thread/request
     2. Platform Dependent (종속성)
        머신에서 수용할 수 있는 한계점.
        여러 머신을 하나의 머신처럼..
        서로 다른시간에 구축되는 시스템의 환경이 같지 않고 다르다.
   * WORA(Write Once, Run Anywhere) - 자바의 크로스/플랫폼에 의한 이익을 표현하기 위한 표어
   * 변경될 것을 예상하고 최대한 간단히 만드는 것 - 객체지향
     (붙이는 코드, 태우는 코드 등등 각각 만듬)
5. Web Application = Web Site + CGJ
6. Web Services: B2B



-------------------------------------------------------------------------------

JAVA/Sun - JAVA를 개발한 Sun의 제품이 JAVA가 제일 잘 돌아갈 것이라는 OpenSource



Oracle이 Sun을 인수한 가장 큰 이유!

1. Java 세상을 독식
2. Mysql 파괴!



#### Google

2000년. 막대한 DB를 가지고 예측해보니 2014년에 데스크탑으로 인터넷을 하기보다는 밖에서, 걸어다니면서 Web Service를 이용할 것을 예측.

2014년 자신들이 망할 것을 또한 예측 => 어플리케이션을 통해 google에 접속할 수 있는 것이 필요하다! 없다면 우린 The End..

Mobile OS가 시장에서 부족함을 인지하고 MobileOS개발할 회사를 컨텍 => Android란 회사를 찾아 인수 및 개발!

Mobile Application => App으로 줄여부르며 작다는 것을 강조!

**그럼 App을 어떤 언어로 해야하는가?!**

* 가장 빠른 C언어로 만드는게 상식적이였지만 Google은 Java를 선택했다. because **개발 편의성 때문**
* Oracle사의 의도를 알았던 Google은 Java를 변형하여 쓰기로 결정
* DVM - (달빛)



Mobile JVM - Sun에 License 귀속.

Oracle은 Google에 Android 단말 한대당 $10~15 License를 부과하기 원함.. (법적다툼결과: (승) 1차 Oracle, 2차 Google, 3차 Oracle)



[소설] 안드로이드는 전기양을 꿈꾸는가?

- 사람이 안드로이드는 학대하지만.. 로봇애완동물은 실제 애완동물처럼 사랑을 품는다. => 현실은? 사람이 사람을 사랑하지 않는 세상이 아닌가?!

--------------------------------------



#### 프로그래머는 요리사와 같다.

쉐프가 만드는 짜장면 = C, Java로 만드는 완성도 높은 프로그램

일반인이 만드는 짜파게티 = python으로 만드는 간단한 프로그램

(python으로도 완성도 높은 프로그램을 만들 수 있다?)



-----



#### Model 1(One) Architecture



| html, Servlet(Server v..??)<br />1. 요청분석<br />(2.) biz (분리 - 왜 분리가 되는가?!)<br />3. 응답 |
| :----------------------------------------------------------: |
| Java EE (Enterprice Edition) - ee.jar<br /> 껍데기만 있는 ee.jar<br />일부러 텅 비어있게 만듬. <--- 구현체 (Any Web Container)<br />(Tomcat, Resin, Jrun) |
| Java SE (Standard Edition)<br />JRE [JVM] [rt.jar (runtime.jar)] |
|         Any Web Server (Apache, Nginx, IIS, NS ...)          |
|                           Any O/S                            |
|                           Any H/W                            |



Web Server = HTTP Protocol Litener



**한번 쓰고 마는 마인드 = 절차중심적 언어**

**내일 변화될 것을 염두에 두는 마인드 = 객체 지향 언어**



* **biz 왜 분리하여 사용하나?!**
  Text는 Binary보다 400% 큰 부피, CPU점유 15%, 메모리도 더더 많이 점유한다.
  **RMI**(자바 원격 함수 호출)로 Client와 서버와 통신



**JSP** - Java in HTML 형식을 HTML in Java로 변화



#### Model Two Architecture - Model One을 수정!!

1. JSP 페이지가 무수히 많이 생성되면서 유지보수에 어려움을 겪음
2. 모든 요청을 Servlet으로 받도록 Gateway Servlet으로 변화 - **Controller**
3. JSP는 View에만 집중



**Struts** - XML로 바꾼  Gateway Servlet 내용을 parsing하여 Servlet에 적용. Controller의 대체 Framework. (사람들은 Struts가 신기술인줄 알고 쏠림)

* struts를 사용하면 기존 Servlet보다 3배 자원이 더 소모된다..!



**안정성 추구**

Tx (Transection), Secure, Per ...



| Biz<br />xml: <A><Tx>,  <B><Sec>, <C><Per><br />EJB(Enterprise Java Beans)을 이용하여 규격을 선언<br /> |
| :----------------------------------------------------------: |
| Java EE - ee.jar: Tx, Sec, Per에 관한 구현체 WAS (Application Server: Jeus, Jross, Weblogic, Websphere, iplaner, oas...)<br />rmi+iiop Protocol을 사용한 통신 |
|                           Java SE                            |
|                           Any O/S                            |
|                           Any H/W                            |

WAS - 비지니스 컴포넌트 서비스를 해주는 ??

**Spring** - <bean>A "A라는 코드를 bean으로 만들어주세요"는 Framework (비표준)
bean밖에 없던 Spring에 사람들이 여러가지 추가하기 시작함.. - 사실상 비표준
**정부에서 전자정부표준 Framework를 만듬**



**SI(<u>System Integration</u>)** 어려움을 극복하기 - Biz마다 다른 언어로 되는 것을 경험하며 HTTP, XML을 전송프로토콜로 선택함! (Why? Text기 때문에!)

**표준 SOAP(<u>Simple Object Access Protocol</u>)** - XML 기반의 메시지를 컴퓨터 네트워크상에서 교환하는 프로토콜
HTTP기반으로 통신하기 때문에 Text인 데이터를 탈취당하기 쉬워졌다.



**POJO** (Plain Old Java Object) - 자바 언어 사양 외에 어떠한 제한에도 묶이지 않은 자바 오브젝트



#### Spring을 현실적으로 사용할 수 밖에 없는 이유
Spring을 통해 라이브러리(?)를 불러오는데 WAS의 서비스와 겹친다.
겹치는 서비스는 JVM이 관리하는 RAM에 그대로 객체로 탑재되며 자원의 낭비를 초래한다.
그렇다면 Spring or WAS 둘중 하나를 쓰는 것이 구조상 옳다. 그런데 Spring은 WAS의 기능을 무료로 사용할 수 있으나 약 5배정도 효율이 떨어지며 WAS는 구조적으로 높은 효율을 가지나 라이센스 비용이 주기적으로 든다.



**Functional 언어 특성**
객체지향언어로 구축된 거대한 시스템에 추가적인 기능, 덜어내야할 기능 등을 하기에는 객체지향언어로 너무 복잡함을 가졌다.
그래서 Functional 언어를 통해서 객체지향언어보다 빠르고 간결한 코드로 기능을 추가하고, 수정하며, 덜어내는 것을 선호하게 되었다.



**V8 엔진**

biz로 만들던 것을 js로 만들어 V8으로 돌릴 수 있게 되었다. - **Node.js**



**Colaboratioon BlockChain**

Public - 전 공개적인 Blockchain

Private - 비공개적인 Blockchain. 장부역할 O





**Mashup (매시업)**

- 웹으로 제공하고 있는 정보와 서비스를 융합하여 새로운 소프트웨어나 서비스, 데이터베이스 등을 만드는 것
- Ex) 네이버지도 API, Kakao API 등의 오픈API를 융합하여 소프트웨어 서비스 등을 만든다.



**프로그램 언어에서**

* Method: 어디엔가 소속된 함수

* Function: 소속되지 않은 함수



메모리에 탑재될 때 Functional 언어도 객체로 탑재된다.
(node.js, python 등등...)
처리는 객체로 처리되지만 

Java도 객체로 만들지 않으면 메모리에 객체로 탑재되지 않는다.