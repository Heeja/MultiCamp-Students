### Enterprise Web Architecture

HTML로는 페이지를 표현하는데 한계를 느낀 개발자들..
더 보기좋고 인지하기 쉬운 인터페이스를 만들기 위해 **CSS**를 채택하여 표준으로 정한다.



HTML 만으로는 회원가입, 로그인, 기타 등의 서비스를 지원하기 어렵다.
그래서 응용프로그램 (***CGI**)을 만들기 시작함!
C언어, VB, C++ 등으로 응용프로그램을 만들기 시작함



Thread 기반 CGI (NSAPI, ISAPI)을 통해 명령이 내려오면 Client의 Process가 아니라 Application Process로 구동한다.
Ex) 윈도우 탐색기를 실행 했을때 OS를 거쳐 H/W까지 명령을 전달하고 윈도우 탐색기를 실행하기 위한 Process를 띄운다.



하지만 여러 응용프로그램에 따라서 Process가 실행되기보다!
Web Application을 위한 Process하나만을 띄워 시스템적 부화를 막도록 한다.

-그림참조-

Application Process안에 은수 Proc, 길동 Proc가 Code도 정보도 함께 사용하며 구동한다.



서버에서 수용할 수 있는 Client에는 한계가 있다. 또 용도가 바뀐다면 Application도 변경되고, 시스템 수정도 조금 필요할 수 있다.
Ex) 교육생이 증가하면서 역삼-MultiCamp에 수용할 수 있는 인원을 초과하였다. 그래서 선릉-MultiCamp을 추가하여 교육생을 수용하였다.



CGI - Servlet

- Thread
- Platform





Web Server는 직접적으로 CGI와 연동되지 않는다
Java EE에서 ee.jar파일을 인터페이스로는 되어도 실행은 되지 않는다.
인터페이스 안에 구현체를 넣어야하는데 이 구현체를 Implementation(=Web Container: Tomcat, Resin, Jeus...)라고 한다.



하드웨어의 종류마다 전기신호에 대한 응답이 다르다.
**JRE**: Machine이 처리할 수 있도록 Class에게 받은 Code를 Machine언어로 변경하여 알려준다.
**.Class**: Machine Code가 아니다. byte Code (JRE가 알아듣는 언어)이다.
**.Java**: 사람이 알아보는 언어. (자연어)
**classLoader**: Byte Code를 읽어들이는 엔진
**bytecodeVerifier**: Byte Code를 검수하는 엔진
**machine Code Generator**: 검수된 Byte Code를 Machine Code로 변경하는 엔진



Java언어는



JVM이 코드를 받아들이는 것을 Load한다고 한다.

**Load**

1. main을 제외한 Static 멤버를 초기화한다.
2. Static에 Servlet 적재.
3. 상속관계 파악 - 스스로 실행한 적이 있는지 물어본다.
4. ee.jar(- 구현체), rt,jar에서 찾아서 온다.
5. 객체생성 - eden영역에 data와 Method를 올린다.
   (객체라는 것을 통해 다른 멤버를 구분하고, 
   각각의 Method (기능)도 객체마다 올라가야한다.)
6. 같은 파일을 컴파일하면 객체가 추가로 생성되더라도 같은 내용이 중복되어 올라가게된다.
   중복되는 것을 줄이기 위해서는 컴파일을 수정해야한다.
7. 그래서 Method를 Method Area의 일반영역에 올려 중복되어 올라가는 Method를 하나만 올려 객체가 가져다 사용하게된다.
8. garbage collection (URL참조: <https://d2.naver.com/helloworld/1329>)
   객체지향 - 객체가 한번 실행되고 사라지는 것을 지향..



Dinamic Node

Pre Node

PC-register: 각 Thread가 다음 명령어를 기억하는 공간



Source Code를 만들고 

Platform에 맞춰서 새로 개발하지 않아도 된다.



개발: Byte Code까지 만드는것

JAVA는 JRE 종속적인 프로그래밍 언어이다.
JRE가 없으면 작동하지 못한다.



Source Code를 Byte Code로 컴파일하면 3배 증가
Byte Code를 Machine Code로 변환하면 15배 증가



cmd프로그램은 DOS에서 실행하는 명령어(자연어)를 해석하여 Machine에게 전달해주고 Machine이 처리한 내용을 사용자가 알아볼 수 있도록 다시 해석하여 자연어로 표현해준다.
(Linux에서는 shell이 같은 역할을 수행한다.)



'new connect()', 'new member()' 등 Source Code에 매번 직접 코딩해야하는 번거로움
그래서 찾는 것이 FrameWork다.
FrameWork는 서비스와 무관하다. (서점의 책장과 같은 역할)

요즘에는 XML에 <bean>을 사용한다.

```
<bean class="Member">
<bean class="Connection"
...
```

parser





Javascript - Client의 browser에서 돌아가는 프로그램 언어. Loose한 프로그램

1. 문법 - Loose
2. 실행 - Script (컴파일을 하지 않는 언어. = interpreting)



**JQuery** - 웹페이지를 보기좋게 꾸미는 Javascript FrameWork

**분산 어플리케이션** - Machine이 다른 것이 아니라 Process가 다른 어플리케이션 간에 연동.
Process간에 데이터 공유는 연동되지 않으면 불가능하다.



H/W = 몸 / OS = 두뇌 / Server = 생각

우리는 H/W를 30%정도만 사용하고 70%가 남아있음에도 불구하고 증설하거나 보완한다.
남은 자원을 효율적으로 사용하기 위해서 하나의 H/W에서 여러개의 Server를 사용하기 시작한다.



Virtual Machine 기술을 이용하여 하나의 H/W에서 여러개의 Server를 사용하기 시작했으나 효율이 좋지 못하다..
그래서 Container형식의 Docker를 사용하기 시작한다.



**Docker**

* Docker를 사용하고자하면 Docker를 설치해야 한다.
* Docker를 만든사람이 Linux를 더 잘 알고있어서인지 Docker가 Linux에 최적화 되어있다.
* Network가 되지않으면 사용에 제한이 크다.



Blockchain은 활용면에서 Database 역할을 할 것이다.



