# 이론수업

### SDL

* 개발 공정에서 단계가 진행 될 수록 수정비용이 증가한다.
* 이를 예방하기 위해서는 개발 초기단계부터 보안 시스템을 유념하여 개발하는 것이 좋다.



### 방화벽

* 외부의 공격으로부터 조건(정책)에 따라서 부합되는 통신만 허용하는 장비/소프트웨어



### IDS/IPS (침입 탐지 시스템)



### SQL Injection (CWE-89)

* 외부 입력값을 Query 조작 문자열 포함 여부를 검증하지 않고 Query 작성 및 실행에 사용하는 경우, Query의 구조와 의미가 변경되어서 실행 되는 것
* Database 또는 Data에 대해 공격
  * 권한 밖의 데이터를 조회, 수정, 삭제, 생성
* 서버에 대한 공격
  * Database가 동작하는 서버의 제어권을 획득해서 원격으로 서버를 제어
* 메타문자: 어떤 기능에 대해서 특별한 의미와 용도를 가지는 문자
  (SQL: ', #, ;, - ...  /  URL: ?, &, =, ...)



### XSS공격 (Cross-Site Scripting) (CWE-79)

* 공격자가 전달한 스크립트 코드가 사용자 브라우저를 통해 실행되는 것
* 동적인 Web Page에서 스크립트가 실행되면
  * 브라우저에 저장된 또는 PC에 저장된 정보를 탈취하는 것이 가능하여 진다.
  * 가짜 페이지를 만들고 사용자로 부터 정보를 입력하게 만들고, 입력한 정보를 탈취할 수 있다.
  * 원격으로 스크립트가 실행된 PC를 제어 가능할 수 있다.
    (Zombie PC => BeFF)



#### 동적/정적 Web Page

* 정적: 서버에서 정보를 바꾸지 않는 이상 Web Page가 변경되지 않는 것.
  (페이지가 변경되려면 새로운 페이지로 이동하거나, 개발자가 페이지를 수정해야한다.)
  * CGI(Comeon Gateway I) - 
  * 기본적으로 html로 페이지가 만들어지며, Image, CSS, Javascript 등으로 구성되있다.
* 동적: 사용자의 요청에 따라서 다른 내용으로 바뀐다.



### Session, Cookie

* HTTP의 특성인 Stateless으로 인해서 접속을 유지하기 위해 접속유지를 검증하는 것(?)
* 연결이 끊기고 다시 요청을 보냈을 때, 동일한 사용자를 식별하기 위해서 서버는 Client에게  Cookie를 가지게 한다. 이 쿠키와 세션이 한쌍을 이루어 요청과 요청의 관계를 이어준다.

* 네트워크로 전송이 되기 때문에 쉽게 노출되어 있고, 변조가 가능하다.
* 보안성을 강화하기 위해 서버에서는 추가적인 인증을 통해 Session ID를 지정한다.
* Session Hijacking



### 입력값 검증

* 입력 값의 정상 유무 확인하는 과정.

1. 입력화면 - ID/PW는 입력
2. 사용자 입력을 요청 파라미터로 서버에 전달
   http://.../check.jsp?id=...
3. 요청 파라미터로 전달된 값은 서버 내부 처리를 위해서 사용
   Select * from users where id=…..;

###### Command Injection (CWE-78)

* 시스템에 명령을 수행할 수 있는 쉘 환경을 유도

* 운영체제 명령어 실행 부분이 존재하는 경우

* 외부 입력값의 검증 & 제한 없이 운영체제 명령어 실행 부분에 사용되는 경우 발생한다.

  * 외부 입력값을 검증 제한 없이 명령어로 사용하는 경우

    .../doSomething.jsp?cmd=dir : 서버에서 dir한 결과가 반환

    의도하지 않은 명령어가 실행되어 서버의 제어권을 공격자에게 주는 상황이 될 수 있다.

    ```
    String input = request.getParameter("cmd");
    Runtime.getRuntime().exec(input);
    
    .../doSomething.jsp?fname=help.txt : c:\data\help.txt 내용이 화면에 출력
    .../doSomething.jsp?fname=help.txt %26 ipconfig : 의도하지 않은 추가 명령어가 실행된다.
    String input = request.getParameter("fname");
    Runtime.getRuntime().exec("type c:\data\" + input);
    ```


​    

###### Open Redirect (CWE-601)

* 일반 사용자들이 피싱 사이트로 자신도 모르게 접속하게 유도



### 에러 처리

* 이차적인 문제가 발생하지 않도록 해야한다.
* 오류 메시지를 통해 정보가 유출될 수 있다.
* 오류 상황 대응 부재: 서비스가 중단되거나, 시스템이 잘못된 방향으로 동작할 수 있다.
* 부적절한 예외 처리: 오류에 대해 잘못 대응.. 



### 인증 / 인가

* 특징 인증
  * 바이오 인증



### 인가

* 권한 = 접근통제

1. 화면
2. 기능: 처리 전 서버에서 권한을 확인
3. 데이터: 



### Secure Cording

* 구현시 Secure Cording 한다
* 정해진 규칙에 맞추어 개발을 진행한다. (좁은 의미로)
* 소프트웨어 개발 생명주기() 전 단계에 걸쳐 취약점을 가지지 않도록 개발한다. (넓은 의미로)
* 개발자 + 분석가, 설계자, 테스터, 운영자 및 사용자 모두가 각각 직무에 맞는 보안 활동을 수행해야한다.





## IT 시스템에 대한 보안 정책

### 네트워크 보안

* 방화벽: 기본적으로 패킷에 대해 사전에 설정한 접근제어목록에 따라 허용 또는 차단하는 기능
* IDS: 방화벽으로는 탐지할 수 없는 트래픽이나 컴퓨터 사용을 탐지한다.
  호스트 기반의 공격이 발생하면 이벤트를 발생시키고 DB에 기록하거나 사전에 정한 규칙에 따라 보안 이벤트를 이용하여 경고한다.
* IPS: IDS와 유사하지만 허용되지 않은 사용자나 서비스에 대해 사용을 거부하여 내부자원을 보호한다.



### 시스템 보안

* OS와 연관이 많다.
* 주기적으로 시스템 악성코드 점검을 통해 시스템이 안전한 상태로 유지되도록 한다.



### 어플리케이션 보안

* 90% 이상이 잘못 만들어진 어플리케이션으로 보안사고가 발생한다.
* 방화벽, IDS/IPS, 시스템 보안에서 잘 막아가니 그나마 취약한 어플리케이션에서 공격이 이루어 지는 것 같다. (물리보안)



### OWASP 2013 (2017)

* **개발 보안** (내가 안전하게 만드는 것)
* **공급망 관리**
  (공개 API, 프레임워크 같은 다른 사람이 만든것을 사용하는 것에 대해 보증할 수 있도록..)
* 정보보호 사전보안
* 보안강화
  [ 분석 / 설계 / 구현  / 테스트 / 이행 ] - [ 운영 / 유지보수 ]
* 보안 내재화라고도 한다.
  (정보보호 백서 2019에서 보안 내재화를 강조하고 있다.)
* **공공 시스템 뿐만 아니라 민간영역까지 확대하는 중에 있다.**



### ISMS(ISMS-P)

- **정보보호 및 개인정보 보호 관리체계 인증**
  (Personal Information& information Security Management System)
- 운영 / 유지보수
- PIMS+ISMS = ISMSP



#### DRM

* 디지털 권리 관리(Digital Rights Management)





#### DLP

* 데이터 유출 방지(Data Loss Prevention)





## 보안 사고 사례

#### 웹 어플리케이션 취약점 (k* 해킹사례)

고객번호를 조회

search.jsp?고객번호=123

1. 로그인 여부 확인 (인증 여부)
2. 처리에 필요한 정보가 전달되었는지 확인 (요청 파라미터 점검)
3. 파라미터를 가지고 Select.
4. 결과를 반환

결과

1. 일치하면: 고객정보가 출력
2. 일치하지 않으면: 메시지 출력

**문제점!**

1. 특정 직원이 접근 권한이 있는지 체크하지 않는다.
   (데이터에 대한 접근 통제가 이루어지지 않았다.)
   - 모든 사람을 조회할 수 있다. (고객 정보 모두 조회 가능)
   - 애플리케이션에서 (search.jsp) 고객정보 조회 권한을 줘야했다.
2. IDS/IPS를 우회하기 위해 한번에 정보를 검색하지 않고 3초에 1번 1건씩. 1600만번 조회하여 3개월 동안 데이터를 가져감.



#### 웹 서버 취약점 (__k Broad B_nd)

* 파일 업로드
  1. 파일 크기 제한 X - 서버 자원 고갈을 유발. 정상적인 서비스 방해 (=Dos, DDos)
     - 서버의 디스크(Storage) 자원 고갈
     - 업로드, 다운로드 중에 연결이 지속되는 시간이 길어져, 서버 연결자원이 고갈된다.
  2. 파일 종류 제한 X -
     - 서버에서 실행되는 파일을 업로드 - 서버 제어권 탈취
       (SSS(Server Side Script): PHP, JSP, ASP, JS ...)
     - 클라이언트에서 실행 되는 파일을 업로드 - 악성 코드 유포장소로 활동
  3. 해결점
     - 외부 접근 가능 경로에 저장

패스워드

1. 패스워드 생성 규칙
   - 영문 + 숫자 + 특수문자 : 8자리, 10가지 이상. 문자연속x.
     숫자만= 10ⁿ, 영숫특=(24+10+8)ⁿ
   - 사전에 등록된 PW 사용불가
   - 일정한 규칙을 가지지 않도록 한다.
   - 개인의 정보과 연관성이 없도록 한다.
2. 저장(보관)
   - 암호화하여 보관 해야 한다.
     (해쉬 암호화: 어떤 값을 일정한 크기의 유일한 값으로 만든다.)
   - 해쉬: 고정된 길이, 유일한 값. 단방향(일방향)
3. 관리 정책
   - 변경 주기
   - 히스토리 (동일한 비밀번호 다시 사용 자재)
   - 최소 사용 기간



##### 암호화

비도: 보안강도 (비도가 높을 수록 암호문을 가지고 key를 알아내는데 오랜시간이 걸린다.)

수학적으로 암호문이 공개되어도 key값을 알아내기 어려워야 좋은 암호 알고리즘 이라고 한다.

암호 알고리즘, Key, 암호문 3가지를 모두 가지고 있는 관리자(admin)

관리자는 정보를 가져가기 쉽다. 사용자의 PW를 알지 못하도록 단방향을 사용하도록 하였다.



#### 계정 관리 미비, 암호화 정책 미비 (Hyun대 케pi탈)

1. 퇴사한 직원의 계정으로 여전히 접속되어 회원의 개인정보를 탈취
2. 암호화되어 있는 개인정보 DB. 복호화를 위해 어플리케이션의 로그를 탈취



### OpenSSL 하트 블리드 취약점

* OpenSSL: 보안 통신을 지원해주는 라이브러리
* HeartBeat: 클라이언트와 서버 간에 세션연결이 유지되는지 확인하는 기능
* 클라이언트가 보낸 메시지의 길이와 서버에서 처리하는 메시지의 길이를 비교하지 않으면 필요 이상의 정보를 응답하게 된다.



## 보안취약점 정보 활용

* 취약점 DB
  * CWE (Common Weakness Enumeration)
    * 미국 국토안보부에서 관리. http://cwe.mitre.org
    * SW의 취약점을 사전식으로 분류해 쉽게 접근하도록 함.
  * CVE (Common Vulnerabilities Exposures)
    * 일반적인 취약점 노출. http://cve.mitre.org
  * SANS TOP 25
    * 시대가 바뀌면 환경도 바뀐다.
      환경이 바뀌니 오류가 아니였던 것이 오류가 되고, 안전했던 것이 안전해지지 않더라...
    * 구성 요소 간 안전하지 않은 상호작용 (6가지) - 인젝션...
    * 위험한 자원 관리 (8가지) - 버퍼오버플로우
    * 허점이 많은 방어 (11가지)
  * OWESP TOP 10
* Secure Coding Guide
  * CERT
  * 개발보안 가이드
* 방법론
  * MS-SDL
  * 7 Touch Point
  * CLASP



### CSRF (Cross Site Request Forgery) (CWE-352)

* 서버로 전달된 요청을 요청 절차와 주체에 대한 검증을 수행하지 않고 요청을 처리했을 때 발생

## 구성요소 간 안전하지 않은 상호작용

**CWE-89**: [SQL Injection](#SQL Injection (CWE-89))

**CWE-78**: [Command Injection](#Command Injection (CWE-78))

**CWE-79**: [XXS](#XSS공격 (Cross-Site Scripting) (CWE-79))

**CWE-434**: 위험한 유형의 파일 업로드를 제한하지 않은 것

**CWE-352**: 사이트 간 요청 위조 = [CSRF](#CSRF (Cross Site Request Forgery) (CWE-352))

**CWE-601**: 신뢰할 수 없는 사이트로 URL 접속지를 변경 = [Open Redirect](#Open Redirect (CWE-601))

## 위험한 자원 관리

### BoF(Buffer OverFlow) (CWE-120)

**CWE-22**: 특정 디렉토리에 존재하는 파일을 제공하는 서비스 - 파일 다운로드

**CWE-494**: 무결성 검사 없이 코드 다운로드.

**CWE-829**: 신뢰할 수 없는 제어영역에서 온 기능을 포함하는 것

**CWE-676**: 잠재적으로 위험이 있는 함수를 사용하는 것

**CWE-131**: 버터 크기를 잘못 계산

**CWE-134**: 형식 문자열을 통제하지 않음
	Format String: 출력 형식을 지정하는 문자. %s, %c, %n 등..

**CWE-190**:  정수 오버플로우 또는 랩 어라운드



## 방어 미비

입력 -> 처리 -> 결과

입력

1. 신뢰 할 수 있는 곳에서 오는 입력 (서버가 보유한 값 ex. 자기에서 가지고 있는 값)
2. 신뢰하지 못하는 입력 (외부 입력 값 - 사용자 입력)

안전한 처리를 위해서

* (2)을 최소화 한다.
* (2)의 입력을 꼭 필요한 값 만을 수용한다.





CWE-327

​	암호화

1. 안전한 알고리즘 = 일정한 수준을 유지할 수 있는 비도 (비도=Key 길이에 비례)
2. 키 길이 준수
3. 키 보관



## OWASP Top 10 - 2013

A7: 기능 수준의 접근 통제 누락 - 회원가입 페이지에서 게시판 조회기능이 있거나 그런...

A9: 알려진 취약점이 있는 컨포넌트 사용

##### [Exploit Database](http://www.exploit-db.com)





##### [Android Secure Coding Guide](https://www.jssec.org/dl/android_securecoding_en.pdf)





## 소프트웨어 개발보안 가이드

​	[행정안전부 소프트웨어 개발 보안 가이드](https://www.mois.go.kr/frt/bbs/type001/commonSelectBoardArticle.do?bbsId=BBSMSTR_000000000015&nttId=57473)



### 설계단계 보안요구항목



### 소프트웨어 개발보안 방법론

#### [SDL (Secure Development Lifecycle)](#SDL)

|     분석(설계)     |           구현           | 테스트 | 배포(이행) |
| :----------------: | :----------------------: | :----: | :--------: |
| 20개 보안 요구사항 | 47개 보안 약점, 소스코드 |        |            |

요구사항 정의서

1. 정적 쿼리
2. 동적 쿼리 입력값 검증
3. 사용자 권한 Down

추적표



##### 소프트웨어 개발 단계별 보안 활동

|       요구사항 분석       |                           설계                            |                        구현                         |                   테스트                   |
| :-----------------------: | :-------------------------------------------------------: | :-------------------------------------------------: | :----------------------------------------: |
| 요구사항 중 보안항목 식별 | 보안 요구사항과 위협에 대한 보안통제를 고려해 위협원 도울 | 표준 코딩 정의서 및 SW개발보안 가이드를 준비해 개발 |         실행 코드 보안취약점 진단          |
|                           |                   외부 인터페이스 식별                    |          소스코드 보안약점 진단(도구 활용)          | (동적 분석: 스캐닝, 모의 침투 테스트 등..) |
|                           |                      보안 통제 수립                       |                                                     |                                            |



* 정적 - 소스코드(White Box)
  * 형태, 문법(구문), 내용 (=코드리뷰)
* 동적 - 실행 파일(Black Box)
  * 결과(값, 성능, 보안) (=디버깅, 부하 테스트, 모의 해킹(침투테스트))



* 약점(Weakness): 보안 취약점의 근본적인 원인이 될 수 있는 결함, 실수, 버그 등의 오류
* 취약점(Vulnerability): 외부 공격으로 시스템의 보안정책을 침해하는 시스템 상의 허점



##### 개발보안 비용 효과

| 구분           | 설계단계 | 코딩단계 | 통합단계 | 베타제품 | 제품출시 |
| -------------- | -------- | -------- | -------- | -------- | -------- |
| 설계과정 결함  | 1배      | 5배      | 10배     | 15배     | 30배     |
| 코딩 과정 결함 |          | 1배      | 10배     | 20배     | 30배     |
| 통합 과정 결함 |          |          | 1배      | 10배     | 20배     |



![img](https://lh5.googleusercontent.com/5qqpIqjJSXiuBrDbjQvW3UqnAWkjXdgFe2uMK8JD65yMg1dehnarxVHXeWtTfhnx3F8W2Ax6NDKwFWZMuYQWw9b0Duy27EB-mTf5dKGLHMs4YxLRJJ2mc2NOaxtK8MMzT1gtIClV)



#### MS-SDL(Microsoft SDL)

MS에서는 보안 수준이 높은 소프트웨어를 개발하기 위해 다음 3가지 요소가 필요하다고 정의한다.

1. 반복 가능한 프로세스
2. 엔지니어 교육
3. 측정 기준 및 책임성



| 1. 교육                                           | 2. 계획/분석                                                 | 3. 설계                                       | 4. 구현                                               | 5. 시험/검증                                                 | 6. 배포/운영                                | 7. 대응                                  |
| ------------------------------------------------- | ------------------------------------------------------------ | --------------------------------------------- | ----------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------- | ---------------------------------------- |
| **소프트웨어 개발 보안교육<br />(Core Training)** | 소프트웨어의 질과 버그 경계 정의<br />(Define Quality Gates / Bug bar) | 공격 영역 분석<br />(Attack surface analysis) | 도구 명세<br />(Specify Tool)                         | 동적/퍼징 테스팅<br />(Dynamic/Fuzz Testing)                 | 사고 대응 계획<br />(Reasponse Plan)        | 사고 대응 수행<br />(Response execution) |
|                                                   | 보안과 프라이버시 위협 분석<br />(Analyze Security and Privary Risk) | **위협 모델링<br />(Threat Modeling)**        | 금지된 함수 사용 제한<br />(Enforce Banned Functions) | 공격 영역/위협 모델 검증<br />(Verify Threat Models/Attack Surface) | 최종 보안 검토<br />(Final Security review) |                                          |
|                                                   |                                                              |                                               | **정적 분석<br />(Static Analysis)**                  |                                                              | 기록 보관 (Release Archive)                 |                                          |

[MS-SDL 자세한 정보](https://www.microsoft.com/en-us/securityengineering/sdl)





##### 위험 모델링 (Threat Modeling)

* "어떤 위협이 있을까"에 집중해야 한다. "위협을 어떻게 처리해야 할까"는 목적에 맞지 않는다.
* 위협을 파악하고, 어떻게 대응할 수 있는지 결정하여 방법을 제공하는 것.
  (위협만 파악되면 대응법은 제공할 시스템이 되어있다는 말(?))
* 모델링 단계
  1. 팀소집 - 리더, 구성원 (10명 내외). 리더는 코딩능력은 부족해도 침해대응 능력이 탁월해야 한다.
  2. 어플리케이션 분해 - 구조화된 다이어그램(도식화)으로 표현한다. DFD(데이터 흐름도) 사용을 권장한다.
     * **두리뭉실한 문제점들을 그림화하여 시스템(문제점)을 잘 이해하도록 한다.**
     * 서비스 하나의 프로세스로 보고 상호작용을 확인하기 위한 배경도를 그린다.
     * 어플리케이션 분해 레벨에 따라 상세정보를 기술한다.
     * 서술되는 세부사항 하나하나가 공격목표가 될 수 있어 위협이 될 수 있는 목표를 식별할 수 있다.
  3. 위협 결정 - 위협을 식별하고 위협을 분류(STRIDE)한다. 위협트리 생성
  4. 우선순위 결정 - 할당된 자원을 효율적으로  사용하기 위해서 결정한다.
     - DREAD를 통해 위험도를 산정하고 산정한 위험도를 가지고 우선순위를 결정한다.
  5. 대응기법 방법
     1. 무시 (ignore)
     2. 알림 (Alert) - 안전하지 않다.
        - 사용자에게 알리는 것은 위협을 전가시키는 행위가 된다
     3. 제거 (Remove)
        - 위협이 되는 기능(서비스)을 없애버리게 된다. 
     4. 수정 (Fix)
        - 기능을 살리고 위협을 없앤다.
        - 추가적인 비용(시간, 물질, 인력 등)이 들어갈 수 있다.
  6. 대응할 기법 기술 선택
     - 위험 결정에서 분류한 것을 토대로 기법과 기술을 선택한다.



##### Seven Touchpoint



##### OWASP CLASP

* 활동 중심, 역할 중심의 프로세스로 구성된 집합 - 프로젝트를 진행하는데 역할(Role)을 구조화
* 5개의 뷰로 구성
  1. Concept View (Ⅰ)
     - CLASP 정의
     - 적용 사례
  2. Role-Based View (Ⅱ)
     - 프로젝트를 진행할 때 개별 구성원(Role)의 역할을 정의 (PM, Programer, Desinger ...)
  3. Activity-Assessment View (Ⅲ)
  4. Activity-Implementation View (Ⅳ)
     - 구성원 역할에 관한 활동을 정의
     - 보안 강화 활동 24가지 정의
     - 타당성 근거 및 비용 산정 근거
  5. Vulnerability View (Ⅴ)
     - 104개의 취약점에 대한 설명 (개발자에게 알림)
* [CLASP Concepts (참고)](https://www.owasp.org/index.php/CLASP_Concepts)



#### Hash 버전

- MD5는 사용 X (벌써 깨졌음)
- SHA버전 중 SHA-2(256,224) 이상으로. 곧 2도 깨질거같음.
  [SHA 위키백과](https://ko.wikipedia.org/wiki/SHA)



## 웹 어플리케이션 보안을 위한 기본 지식

#### Proxy

* 네트워크 패킷을 캐싱하여 준다.
* 캐싱된 패킷을 가지고 요청/응답에 대해 모니터링과 분석을 할 수 있다.
* N/W설정을 통해 Proxy 연동 사용



### HTTP와 웹 구조

* Stateless= ConnectionLess (연결유지 X)
  (¹연결 후 ²요청/응답. 응답완료 후 ³연결해제)
* 요청이 있어야 응답을 한다.
* 최초 문서를 공유하기 위해 구현된 네트워크.
* 문서를 제공하기 위해 구축 하다보니 Stateless구조로 구현이 되었다.
* 현재는 서버의 구조는 모듈(Mutable)구조를 갖는다.



[Spring MVC 프레임워크 처리 구조](https://zetawiki.com/wiki/스프링_MVC_처리구조)

![img](http://pic002.cnblogs.com/images/2012/93867/2012101109363253.jpg)



시작: Method _ URI _ HTTP.1.0  _ 200 _ OK 

* Method Type: **GET**, **POST**, OPTIONS, HEAD, PUT, DELETE
* HTTP 응답 상태 코드

| 상태코드 |               설명                |
| :------: | :-------------------------------: |
|   1xx    |           정보를 제공함           |
|   2xx    |     요청이 성공적으로 이뤄짐      |
|   3xx    | 요청한 해당 자원이 다른 곳에 있음 |
|   4xx    |        요청에 문제가 있음         |
|   5xx    |        서버에 에러가 있음         |



헤더: Content-Type 

​		Content-Length

​		Referer, Cookie

​	

##### nc를 이용한 HTTP 메소드 테스트

nc KALI#1_IP 80↳ ⇐ 웹서버에 연결

GET / HTTP/1.0↳  ⇐ 요청 시작

↳            				 ⇐ 요청 헤더의 끝



```
root@kali:~# nc 192.168.49.128 80 ⇐ 연결
GET / HTTP/1.0 ⇐ 요청 시작
 ⇐ 요청 헤더 끝
HTTP/1.1 200 OK ⇐ 응답 시작 
Date: Wed, 24 Jul 2019 07:31:17 GMT ⇐ 응답 헤더
Server: Apache/2.4.23 (Debian)
Set-Cookie: PHPSESSID=lchio2qconjrv4p74cksmp4mp4; path=/
Expires: Thu, 19 Nov 1981 08:52:00 GMT
Cache-Control: no-store, no-cache, must-revalidate, post-check=0, pre-check=0
Pragma: no-cache
Vary: Accept-Encoding
Content-Length: 498
Connection: close
Content-Type: text/html; charset=UTF-8
 ⇐ 응답 헤더 끝
<html> ⇐ 응답 본문
<body>
	<form action="login.php" method="post">
	Username : <input type="text" name="username" size="10" required />
	Password : <input type="password" name="password" size="10" required />
	<input type="submit" name="login" value="Login" />
	</form>
	<br/>
	<table width="580" border="1" cellpadding="2" style="border-collapse:collapse">
	<tr>
		<th width="30">number</th>
		<th width="300">title</th>
		<th width="50">name</th>
		<th width="60">date</th>	
	</tr>
	</table>
</body>
</html>

root@kali:~#
```

* openeg 사이트에서 제공하는 메소드 목록을 확인

  ```
  root@kali:~# nc 192.168.49.1 8080↳ ⇐ 연결
  OPTIONS / HTTP/1.0↳ ⇐ 요청
  ↳
  HTTP/1.1 200 OK ⇐ 응답
  Server: Apache-Coyote/1.1
  Allow: GET, HEAD, POST, PUT, DELETE, OPTIONS ⇐ 해당 서버는 6개의 메소드를 제공한다.
  Content-Length: 0
  Date: Wed, 24 Jul 2019 07:35:23 GMT
  Connection: close
  
  root@kali:~#
  ```

  

* openeg 사이트에 GET 방식의 요청과 HEAD 방식의 요청 결과를 비교

  ```
  root@kali:~# nc 192.168.49.1 8080↳ ⇐ 연결
  GET /openeg/login.do HTTP/1.0↳ ⇐ GET 방식의 요청
  
  HTTP/1.1 200 OK ⇐ GET 방식 요청에 대한 응답
  Server: Apache-Coyote/1.1                                          ⇐ 응답 헤더
  Set-Cookie: JSESSIONID=055EE06171EA9E955B76BADA20863367; Path=/openeg
  Content-Type: text/html;charset=UTF-8
  Content-Language: ko-KR
  Content-Length: 3681
  Date: Wed, 24 Jul 2019 07:39:52 GMT
  Connection: close                                                  
                                                                     ⇐ 응답 헤더의 끝
  ⇐ 응답 본문의 시작
  
  
  
  <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
  <html>
  <head>
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
  <title>Login</title>
  <link href="/openeg/css/main.css" rel="stylesheet"
  	type="text/css">
           :
  <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
  		    <div id="aside">
  				
  				
  				<form action="login.do" method="post">
  					<fieldset>
  						<center>
  							<label for="userId">메일주소 : </label> <input type="text"
  								id="userId" name="userId" class="loginInput" value="" />
  							<span class="error"></span><br />
  							<label for="userPw">비밀번호 : </label> <input type="password"
  								id="userPw" name="userPw" class="loginInput" /> <span
  								class="error"></span><br />
  							<br /> <input type="submit" value="로그인" class="submitBt" /> <input
  								type="button" value="회원가입" class="submitBt"
  								onClick='window.open("member/join.do","_blank","width=400,height=400, toolbar=no, menubar=no, scrollbars=no, resizable=no, copyhistory=no");' />
  						</center>
  					</fieldset>
  				</form>		    </div>
  			<div id="footer">
                                 :
  </body>
  </html>⇐ 응답 본문의 끝
  
  root@kali:~# nc 192.168.49.1 8080↳ ⇐ 연결
  HEAD /openeg/login.do HTTP/1.0↳ ⇐ HEAD 방식의 요청
  
  HTTP/1.1 200 OK ⇐ HEAD 방식 요청 결과
  Server: Apache-Coyote/1.1                                              ⇐ 응답 헤더
  Set-Cookie: JSESSIONID=170194BCC4622C98AB74D7AC810A7371; Path=/openeg
  Content-Type: text/html;charset=UTF-8
  Content-Language: ko-KR
  Content-Length: 3681
  Date: Wed, 24 Jul 2019 07:40:13 GMT
  Connection: close
                                                                        ⇐ 응답 헤더 끝
  ```

* openeg 사이트에 PUT 메소드를 이용해서 자원을 생성

  ```
  root@kali:~# nc 192.168.49.1 8080
  PUT /hello.html HTTP/1.0
  Content-Type: text/html
  Content-Length: 42
  
  <html><body>Hello, World!!!</body></html>
  HTTP/1.1 403 Forbidden
  Server: Apache-Coyote/1.1
  Content-Type: text/html;charset=utf-8
  Content-Length: 964
  Date: Wed, 24 Jul 2019 07:54:02 GMT
  Connection: close
  
  <html><head><title>Apache Tomcat/6.0.24 - Error report</title><style><!--H1 {font-family:Tahoma,Arial,sans-serif;color:white;background-color:#525D76;font-size:22px;} H2 {font-family:Tahoma,Arial,sans-serif;color:white;background-color:#525D76;font-size:16px;} H3 {font-family:Tahoma,Arial,sans-serif;color:white;background-color:#525D76;font-size:14px;} BODY {font-family:Tahoma,Arial,sans-serif;color:black;background-color:white;} B {font-family:Tahoma,Arial,sans-serif;color:white;background-color:#525D76;} P {font-family:Tahoma,Arial,sans-serif;background:white;color:black;font-size:12px;}A {color : black;}A.name {color : black;}HR {color : #525D76;}--></style> </head><body><h1>HTTP Status 403 - </h1><HR size="1" noshade="noshade"><p><b>type</b> Status report</p><p><b>message</b> <u></u></p><p><b>description</b> <u>Access to the specified resource () has been forbidden.</u></p><HR size="1" noshade="noshade"><h3>Apache 
  
  root@kali:~#
  ```

* **Q1.** Kali#2에서 HTTP 메소드를 이용해서 openeg 사이트의 hello.html 파일을 삭제해 보세요.

  ```
  root@kali:~# nc 192.168.111.1 8080
  DELETE /hello.html HTTP/1.0
  
  HTTP/1.1 204 No Content
  Server: Apache-Coyote/1.1
  Date: Wed, 24 Jul 2019 08:26:03 GMT
  Connection: close
  root@kali:~#
  ```

* **Q2.** Kali#2에서 HTTP PUT 메소드를 이용해서 openeg 사이트의 hello.html 파일을 2번 생성해 보세요.

  ```
  root@kali:~# nc 192.168.111.1 8080
  PUT /hello.html HTTP/1.0
  Content-Type: text/html
  Content-Length: 42
  
  <html><body>Hello, World!!!</body></html>
  HTTP/1.1 201 Created
  Server: Apache-Coyote/1.1
  Content-Length: 0
  Date: Wed, 24 Jul 2019 08:28:09 GMT
  Connection: close
  
  root@kali:~# nc 192.168.111.1 8080
  PUT /hello.html HTTP/1.0
  Content-Type: text/html
  Content-Length: 42
  
  <html><body>Hello, World!!!</body></html>
  HTTP/1.1 204 No Content
  Server: Apache-Coyote/1.1
  Date: Wed, 24 Jul 2019 08:28:14 GMT
  Connection: close
  
  root@kali:~# nc 192.168.111.1 8080
  PUT /hello.html HTTP/1.0
  Content-Type: text/html
  Content-Length: 42
  
  <html><body> WOW WOO WO helaksjdawlkj</body></html>
  HTTP/1.1 204 No Content
  Server: Apache-Coyote/1.1
  Date: Wed, 24 Jul 2019 08:37:49 GMT
  Connection: close
  
  root@kali:~#
  ```



### 인증과 인가



#### 인증방식

| 인증방식               | 설명                                                         |
| ---------------------- | ------------------------------------------------------------ |
| Type.1 (인식기반)      | 자신이 알고 있는 것으로 인증한다.<br />Ex) 패스워드, 일회용 패스워드(OTP), 개인식별번호(PIN) |
| Type.2 (소유기반)      | 자신이 가지고 있는 것으로 인증한다.<br />Ex) 메모리카드, 스마트카드, 마그네틱카드 |
| Type.3 (신체 특징기반) | 사용자의 고유 특징으로 인증한다.<br />Ex) 홍채, 지문, 정맥, 음성, 서명(필체) |



#### 인가를 위한 접근 통제 기술

| 접근통제 기술                                           | 설명                                                         |
| ------------------------------------------------------- | ------------------------------------------------------------ |
| 접근제어목록<br />(ACL: Access Control List)            | 사용자, 자원 중심의 목록을 작성하여 목록에 비교하여 접근 통제 |
| 접근통제표<br />(ACM: Access Control Matrix)            | 자원 중심의 접근통제 표를 작성하여 접근 통제                 |
| 강제적 접근통제<br />(MAC: Mandatory Access Control)    | 사용자와 자원에 적절한 보안등급(레이블)을 부여하여 통제      |
| 역할기반 접근통제<br />(RBAC: Role Base Access Control) | 사용자에게 역할(Role)을 부여하고 각 역할 별로 권한을 부여.   |

