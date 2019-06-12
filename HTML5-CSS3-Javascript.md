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





### CSS3

1. 박스 모델

   * 크기관련 속성들

2.  박스 유형

   * Block Box

   * Inline Box
   * Inline-Block Box

3. 박스 내부 테스트 정렬



#### Library vs Framework

Library: 완전연료. 사용자가 가공하여 사용할 수 있다.

Framework: 책장. 정해진 틀을 변경할 수 없으며 틀에 따라서 사용해야한다.







### JavaScript

특징

* 독립적인 인터프리터 언어
* 별도의 정형화된 프로그램 구조는 존재하지 않는다.
* 동적 타이핑을 지원. 변수들의 자료형을 자유롭게 변환할 수 있다.
* 객체 기반 언어. (Object Based)
  DOM(D Object Model), BOM(Browser Object Model) 같은 웹 브라우저 및 HTML 문서와의 인터페이스를 위한 다양한 객체들을 제공한다.
* Web Browser환경에서의 Event 처리를 지원한다.



```
<!DOCTYPE html>
<html>
<head>
	<script>
	var obj1="CSS3"; // 변수 선언
	function welcome(obj){
	document.write(obj);
	} // Fucntion 정의. 
    </script>
</head>

<body>
	<h3> Welcome! &nbsp; HTML5 웹 프로그래밍</h3><hr>
	<ol>
		<li>Using HTML! + <script> Welcome(obj1); </script></li>
		<li><script>welcome('Using Javascript');</script></li>
	</ol>
</body>
</html>
```

* Head부분에는 보통 선언, 정의를 한다.



##### Method vs Fuction

**Method**: 클래스, 구조체, 열거형에 포함되어있는 "함수"

**Fuction**: 독립적인 기능. 어떤 특정 개체에 종속되어 있지 않는 것 (Citizen)



객체지향 언어에서는 객체를 중요하게 생각한다.



**UTF-8 Encoding**

영문코드는 1byte, 한글코드는 3byte로 표현한다.
자바스크립트 코드 작성에 유리하면서 운영체제가 지원하는 문자세트에 관계없이 다국어 문자들을 한꺼번에 표현할 수 있다.



* 변수의 선언: 특정 자료형 값을 가진 변수에 다른 자료형 값을 저장하면 변수의 자료형은 자동으로 변환된다.



##### Global Object

* 어디서든지 접근할 수 있는 변수
* 사용의 자제
  * 소스와 데이터의 공개성
  * 비동기 로직이 용이하게 구현 가능
  * 모바일/PC 등 좋은 성능에서 안 좋은 성능까지 골고루 퍼져있는 브라우징 환경
    * 출처: https://unikys.tistory.com/324



#### 자료형

자료를 컴퓨터 메모리에 저장해서 표현하는 방식

메모리 크기와 저장방식, 값들의 저장방식(유형) 등에 따라 구분함!

* 기본 자료형: 간단히 한 값으로 표현할 수 있는 자료들 (이름, Yes/No ...)
* 객체 자료형: 여러 속성값들과 동작들을 그룹핑해서 표현하는 자료들 (자동차, 비행기, 학교 ...)



###### 기본 자료형 (String, number, Boolean, undefined)

* String

```
<!DOCTYPE html>
<html>
<head>
</head>

<body>
<h3>블록문 사용</h3><hr>
	<script>
    var str1="a";	// 선언
    var str2=new String("a");	//생성자 - 객체 생성에 관여하는 연산자. String은 꼭 'S'를 사용. 소문자x
        
    document.write(str1===str2);
    document.write(str1.length); // length 속성
    document.write(str1.indexOf("")); // indexof Method (대소문자 구문 필수!)
    document.write(str1.lastIndexOf("")); // lastIndexof Method (대소문자 구문 필수!)
    document.write(str.slice(-12, -6);); // slice method. 문자열을 잘라서 표시
    documnet.write(str1.concat(" ","plus")); // 이어붙이기
    
    </script>
</body>
</html>
```



###### new String()

새로 생성된 String(객체로서 생성됨)은 바꿀수 없음.

```
<script>
	var t3= new String("Hello");
	var t4 = t3.concat(" ", "World!");
	t3 = t3.concat(" ", "World!");
	
    document.write(t4+'<br>');
    document.write(t3+'<br>');
    document.write(t3===t4);
</script>
```



* Number 형
  * NaN(Not a Number) - 자료값이 수치형이 아님
  * Infinity - 시스템에서 표현 가능한 최대값을 벗어난 값
  
* Boolean 형
  
  * 자바스크립트에서는 정수 0과 -0 그리고 공백문자열(""), undefind형 변수, null객체는 boolean형으로 변환하면 모두 false이고, 그 외 모두는 true이다.
  * 생성자 같지만 생성자 아니다! (대문자로 시작하는 페이크)
  
  ```
  <h3> boolean형 </h3><hr>
  
  <script>
  	var state, num1=0, num2=88;
  	var str1=""; str2="Javascript";
  	var obj1="null";
  	var obj2=new Object();
  	
  	document.write(state+'<br>');
  	document.write(num1+'<br>');
  	document.write(num2+'<br>');
  	document.write(str1+'<br>');
  	document.write(str2+'<br>');
  	document.write(obj1+'<br>');
  	document.write(obj2+'<br>');
  </script>
  ```
  
* undefined

  ```
  <!DOCTYPE html>
  <html>
  <body>
  <h2>My First JavaScript</h2><hr>
  
  <script>
  var obj=new Object();
  var num;
  
  document.write(obj+'<br>');
  document.write(num+'<br><br>'); // 값이 선언되지 않은 변수는 undefined
  
  obj=null;
  document.write(obj+'<br><br>');
  
  obj=undefined;
  document.write(obj+'<br><br>');
  
  document.write((undefined==null)+'<br>');	// null값과 undefined의 값은 같은가? True
  document.write((undefined===null)+'<br>');	// null값과 undefined의 자료형은 같은가? False
  
  
  </script>
  </body>
  </html> 
  ```



###### typeof

* 특정 자료의 자료형을 확인하는 연산자

```
<!DOCTYPE html>
<html>
<body>
<h2>My First JavaScript</h2><hr>

<script>
var obj=new Object();
var num1;
// var Mycar;	// Mycar의 자료형은 undefined
// var Mycar=1234;	//	Mycar의 자료형은 Number
// var Mycar=[1234];	//	Mycar의 자료형은 Object
// var Mycar;	// 기존에 Mycar의 값은 초기화되지 않고 남아있다. 다른 언어에서는 에러.

document.write(typeof"John"+'<br>');
document.write(typeof 3.14+'<br>');
document.write(typeof NaN+'<br>');
document.write(typeof false+'<br>');
document.write(typeof true+'<br>');
document.write(typeof 0+'<br><br>');

document.write(typeof [1,2,3,4]+'<br>');	// 배열은 객체형
document.write(typeof function(){}+'<br>');
document.write(typeof Mycar+'<br><br>');	// 선언되지 않은 변수는 undefined

document.write(typeof null+'<br>');
document.write(typeof undefined+'<br>');
document.write(typeof ""+'<br>');
document.write(typeof ''+'<br>');

</script>
</body>
</html> 
```





##### 변수 선언후 같은 변수를 다시 선언하는 일.

위의 Mycar와 같이 Mycar에 값1234를 선언한 후

다음에 Mycar를 다시 선언하게 된다면 Javascript에서는 에러 나지 않지만 다른 언어에서는 에러가 날 것이다.

물리적인 동작에서 정상적인 코드가 아니기 때문에 프로그램은 오류를 수정하여 OK를 만드는 작업을 수행한다.

이는 자원의 낭비, 퍼포먼스에 나쁜 영향을 끼친다.





###### Java에서의 객체

int i=10;	//	메모리에 i라는 4byte의 공간을 할당. 값을 2진수 10(1010)

Integer i2=new Integer(10);	// 메모리에 i2라는 4byte의 공간 할당. 값은 객체의 주소 값이 입력됨!





###### 객체 자료형 (Object, Function)

* Object
* Fuction



#### 객체

특정 사이트에 로그인한 후 새로운 브라우저(같은 브라우저)를 열어도 로그인이 된 상태로 브라우저가 열린다. (메모리를 공유하고 있다?!)

하지만 브라우저에서 지원하는 시크릿모드로 브라우저를 열면 로그인이 되지 않은 상태로 사이트가 열린다.

###### 

###### DOM (Document Object Model)

* Window 객체 안의 Document 객체 안의 html객체 ....
* Window 객체는 브라우저 창을 생성할 때마다 새로 생성
* 로그인, Cookie등의 공유 메모리는 메모리의 global 영역
* DOM instance 영역에 html, head, body 등의 객체가 있으며 이는 브라우저의 한 창을 닫는 순간 또는 로그인 한 순간 객체는 삭제된다. 그럼에도 로그인이 유지되는 이유는 globla 영역에 로그인된 메모리가 있기 때문..
* Script 안에 선언된 모든 변수는 Window 객체 안에 메모리된다.
  (Window의 멤버변수)
* 문서 내부(DOM instance)에서 Window를 언제든 바라볼 수 있다. 많은 이들이 이것을 global 영역이라고 부른다.
  (실제 global 메모리 영역이 따로 있으니 혼동되지 않도록 구분하여야 한다.)

###### BOM (Browser Object Model)



* 싱글톤 객체

  * 생성 방식

  ```
  var person1 = {
  	name: "고길동",
  	nickName: "얼음별 용사",
  	major: "가장",
  	age: 48
  };
  
  var person2 = new Object();
  
  person2.name="고길동";
  person2.nickName="얼음별 용사";
  person2.age=48;
  person2.major="가장";
  ```

  * 싱글톤 객체 생성 방식에서 객체변수의 입력값이 없는 것은 허용되지 않는다.

  

* 컨스트럭터(Constructor) 객체

  * 생성 방식

    ```
    var x1=new Object();
    var x2=new String();
    var x3=new Number();
    var x4=new Boolean();
    var x5=new Array();
    var x6=new Date();
    
    function person(name,year,score1,score2){
    	this.name=name;
    	this.year=yesr;
    	this.score1=score1;
    	this.score2=score2;
    }
    
    var guy=new person("조우진",3,80,90);
    var lady=new person("신은수",4,92,98);
    ```

  * 실습

    ```
    <script>
    var person = {
    	name: "장희재",
    	nickName: "빠라밤",
    	major: "후훗",
    	age: 22,
        weight: 70,
        birthday: null,
        salary: NaN
    };
    
    function person2(name,nickName,major,age,weight,birthday){
    	this.name=name;
        this.nickName=nickName;
        this.major=major;
        this.age=age;
        this.weight=weight;
        this.birthday=birthday;
    
    }
    
    var na=new person2("장희재","후후","정복학",22,70,null)
    
    
    
    document.write(na.name+'<br>');
    document.write(na.nickName+'<br>');
    document.write(na.major+'<br>');
    document.write(na.age+'<br>');
    document.write(na.weight+'<br>');
    document.write(na.birthday+'<br>');
    
    
    </script>
    ```

    



###### Object or Window

```
<script>
var person1 = {
	name: "장희재",
	nickName: "빠라밤",
	major: "후훗",
	age: 22,
    weight: 70,
    birthday: null,
    salary: NaN
};

function person(name,nickName,major,age){
	this.name=name;
    this.nickName=nickName;
    this.major=major;
    this.age=age;
    alert(this);
}

var person2 = {
	name: "장희진",
	nickName: "뾰롱",
	major: "쇼가",
	age: 20,
    weight: 47,
    birthday: null,
};

new person("장희재","후후","정복학",22,70,null);	// Object 객체
person("장희재","후후","정복학",22,70,null);
// Window 객체

</script>
```



### js(JavaScript) Prototype Chain

**매우 중요하다!!**

참조: <https://poiemaweb.com/js-prototype>

* 개인 실습

```
<!DOCTYPE html>
<html>
<body>
<script>
	function Person(){
    }
    Person.prototype.eyes=2;
    Person.prototype.nose=1;
    var p1=new Person();
    var p2=new Person();
    document.write(p1.eyes+":"+p1.nose);
    document.write('<br>');
    document.write(p2.eyes+":"+p2.nose);
    document.write('<br>');
    
    p1.eyes=1;
    document.write(p1.eyes+'<br>');
    document.write(Person.prototype.eyes);
    
    document.write('<br>');
    document.write(p2.__proto__.prototype);
    document.write('<br>');
    document.write(p1.__proto__.__proto__.constructor.__proto__);
    document.write('<br>');
    document.write(p1.__proto__.constructor);
    document.write('<br>');
    document.write(Person.__proto__.constructor);
    document.write('<br>');
    document.write(Object.constructor);
    document.write('<br>');
    document.write(p1.__proto__===Person.prototype);
    // p1의 Person 프로토타입과 Person의 트로토타입이 같은지 알아보는 방법.
    // p1.__proto__로는 Object로만 표현된다. Person prototype이라고 표시되지 않는다.
    
</script>
</body>
</html> 
```



#### 객세 생성 - 싱글톤 vs 컨스트럭터

싱글톤 - 가지고 있는 정보를 바꾸지 않을때.

컨스트럭터 - 





```
<script>
var p1={	// {}컬리브레이스를 주는 순간 p1은 객체로 생성
	eyes=3,
	nose=4
}
document.write(p1.__proto__===Object.prototype); // true
document.write(Object===p1.constructor); // true
</script>
```



객체를 생성하는 2가지 방법

1. 객체리터럴 사용

   ```
   var p1 = { name: "OOO" }
   ```

   

2. Object 생성자를 직접 이용

   ```
   var p2 = new Object();
   p2.name="OOO";
   ```

   

3. 사용자 지정 생성자 이용

   ```
   function Person(name){
   // 지정 생성자 이름은 대문자로 시작하는 것이 좋다
   	this.name=name;
   }
   ```

   ```
   var Person=function(name){
   // function의 객체 주소를 Person이 할당 받다.
   	this.name=name;
   }
   ```



**hasOwnProperty**

```
<script>
    var p1={
        eyes:3,
        nose:4
    }
    document.write(p1.hasOwnProperty('eyes')); // true
</script>
```



JS Strict Mode



JS Hosting

* 변수로 선언하는 것을 맨 위로 끌어올리다.

* 선언과 정의

  ```
  fn();	//error
  var fn=function() {alert("test");}
  
  fn2();	//ok
  function() var fn2={alert("test");}
  ```

  

**Javascript에서의 배열(array)**

* Java에서는 선언된 배열의 length를 변경할 수 없지만,
  JavaScript에서는 선언된 배열의 length를 추가할 수 있다.

  ```
  <!DOCTYPE html>
  <html>
      <head>
      <script>
          var student=[88,92,76];
  
          document.write("<hr>배열 student크기: "+student.length+"<br>");
          for(i=0;i<student.length;i++){
              document.write("student["+i+"]=");
              document.write(student[i]+"<br>");
          }
          student[6]=84;  // 동적 배열 크기 확장
          student[4]="결석";
          document.write("<hr>배열 student 크기: "+student.length+"<br>");
          for(i=0;i<student.length;i++){
              document.write("student["+i+"]="+student[i]+"<br>");
          }
      </script>
      </head>
      <body>
                  
      </body>
  </html>
  ```

  

#### setTimeout()

* form 태그 안에서 button을 통해 function을 호출하여 setTimeout()을 수행할 경우 수행되지 않는다.
* form 태그 밖으로 button이 나와야 setTimeout()을 수행한다.





#### CRUD

대부분의 Softeware가 가지는 기본적인 데이터 처리 기능

* Create
* Reading
* Update
* Delete