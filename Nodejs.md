# Node.js

#### REPL

R: read

E: eval

P: print

L: loop



#### 등장배경

Javascript는 브라우저 안에서 하는 것으로 대부분의 사람들이 생각했다. (고정관념!)

이러던 것을 node 엔진을 통해서 OS위에 Javascript를 사용할 수 있게 하였다.

Javascript를 좀더 빠르게 동작하기 위해서 V8 엔진을 google이 만들었다. 이를 토대로 Node 엔진을 제작..!

"**크롬 V8 Javascript Engine으로 Build된 <u>Javascript Runtime</u>이다.**"



#### Runtime

특정 언어로 만든 프로그램들을 실행할 수 있도록 하는 환경.

> Node는 Javascript 프로그램을 컴퓨터에서 실행할 수 있게 해준다.
>
> (브라우저도 Javascript Runtime중 하나이다.)



#### 이벤트 기반(Event-Driven)

* 이벤트가 발생할 때 미리 지정해둔 작업을 수행하는 방식

* 이벤트는 클릭이나 네트워크 요청 등이 있을 수 있다.

* **특정 이벤트가 발생할 떄 무엇을 할지 미리 등록해야 한다.**

  > 이벤트 리스너(Event Listener)에 Callback 함수를 등록한다고 한다.

* 여러 이벤트가 동시에 발생할 때 어떤 순서로 콜백 함수를 호출할지 정해야 한다.

  > 이를 이벤트 루프가 판단하여 호출한다. (이벤트 루프 개념)

* 이벤트 루프

  1. 이벤트 리스너에 콜백 함수 등록
  2. 이벤트 발생
  3. 등록된 콜백 함수 호출

```
function first(){
	second();
	console.log('첫 번째');
}
function second(){
	third();
	console.log('두 번째');
}
function third(){
	console.log('세 번째');
}
first();
```

* 함수 스택: main() [ third() [ second() [ first() ]

* 호출 스택: first() [ second() [ third() [ main() ]



**이벤트 루프** - 노드가 종료될 때까지 이벤트 처리를 위한 작업을 반복하여 이벤트 루프라 불린다.

​	이벤트 발생 시 호출할 콜백 함수를 관리, 호출된 콜백 함수의 실행 순서를 결정한다.

​	<http://latentflip.com/loupe>: 이벤트 루프 과정을 그림으로 보여주는 사이트



**테스크 큐(콜백 큐)**

이벤트 발생 후 호출되어야 할 콜백 함수들이 기다리는 공간.

콜백들이 이벤트 루트가 정한 순서대로 줄을 서 있어 콜백 큐라고도 부른다. (Stack 형식?!)



**백그라운드** - 나중에 수행되어야 할 콜백/이벤트 리스너들이 대기하는 공간



#### **블로킹,논블로킹 I/O**

* **논블로킹**: 오래 걸리는 함수를 백그라운드로 보내서 다음 코드가 먼저 실행되게 하고,
  그 함수가 다시 테스크 큐를 거쳐 호출 스택으로 올라오기를 기다리는 방식.

* **블로킹**: 이전 작업이 완료될 때까지 멈추지 않고 다음 작업을 수행하는 것.
* 동기/비동기 개념과 유사하다.



```
// 블로킹 방식
function longRunningTask(){
	//오래 걸리는 작업
	console.log('작업 끝');
}
console.log('시작');
longRunningTask();	//	오래 걸리는 작업이 완료 되어야 '다음작업'이 수행된다.
console.log('다음 작업');

// setTimeout을 사용하여 논블로킹 코드 변경

function longRunningTask(){
	//오래 걸리는 작업
	console.log('작업 끝');
}
console.log('시작');
setTimeout(longRunningTask,0);
// 콜스택에서는 '다음 작업'을 마저 수행하고, 0ms(실행 환경에 따라 다름) 후 longRunningTask함수를 실행한다.
console.log('다음 작업');
```



**setTimeout(callback,0)**

HTML5 에서는 4ms, Node에서는 1ms의 지연시간을 갖는다.



#### 싱글 스레드 / 프로세스

싱글 쓰레드의 한계로 모든 코드가 시간적 이득을 가지진 않는다.

노드 프로세스 외의 다른 컴퓨팅 자원을 사용 할 수 있는 작업이 많은 이득을 본다.

* 프로세스는 운영체제에서 할당하는 작업 단위
* **프로세스 간에는 메모리 등의 자원을 공유하지 않는다.**
* 노드 프로세스는 여러개의 스레드를 가지고 있지만, 직접 제어할 수 있는 스레드는 하나뿐이다. (=싱글 스레드)
* 노드는 스레드를 늘리는 대신, 프로세스를 복사하여 여러 작업을 동시에 처리하는 멀티 프로세스 방식을 사용한다.



#### 서버로서의 Node

* I/O이 많은 작업에 적합하다.
* CPU부하가 큰 작업은 적합하지 않다.
  (이미지, 영상 처리같은(인코딩,디코딩)을 사용하면 안된다!)



#### 노드의 장점

* 멀티 스레드 방식에 비해 컴퓨터 자원을 적게 사용
* I/O 작업이 많은 서버로 적합
* 멀티 스레드 방식보다 쉬움
* 웹 서버가 내장되어 있다.
* 자바스크립트를 사용한다.
* JSON 형식과 호환하기 쉽다.



#### 노드의 단점

* 싱글 스레드라서 CPU코어를 하나만 사용한다.
* CPU 작업이 많은 서버로는 부적합하다.
* 하나뿐인 스레드가 멈추지 않도록 관리해야 한다.
* 서버 규모가 커졌을 때 서버를 관리하기 어렵다.
* 어중간한 성능이다.



### ES2015+(ES6~)

**구문의 블록 안에 변수 선언은 Window의 멤버변수가 된다.**

그래서 var로 선언하지 않고 const, let으로 선언하는 것은 권장한다.



##### const, let

**블록 스코프를 가지므로 블록 밖에서는 변수에 접근할 수 없다.**

* **const**는 한번 대입하면 다른 값을 대입할 수 없다.



##### 템플릿 문자열

* Javascript에서는 큰따옴표(""), 작은따옴표('')로 감쌌다면, Node에서는 **백틱(``)**으로 감싼다.
  (백틱은 ~을 그냥 눌렀을때!)

```
const num4=2;
const result2=3;
const string2=`${num3}더하기 ${num4} 는 '${result2}'`;	// 여기가 백틱을 사용하는 부분
console.log(string2); */
```



##### 객체 리터럴

* 객체의 메서드에 함수를 연결할 때 콜론(:), function을 생략해도 된다.

* 객체의 속성명을 동적으로 생성할 수 있다.

  > 기존 문법(ES2015이전)에서는 속성명을 만들려면 객체 리터럴 밖에 작성해야 했다면, ES2015+부터는 객체 리터럴 안에 작성해도 된다.

**ES2015 이전 문법**

```
// ES2015 이전 문법
var sayNode=function(){
    console.log('Node');
}
var es='ES';

var oldObject={
    sayJS: function(){
        console.log('JS');
    },
    //sayNode: sayNode
    a: sayNode  // 왼쪽이 변수 이름. 오른쪽이 참조값. 여기서는 위에 saynode.
};
oldObject[es+6]='Fantastic';    // oldObject.ES6='Fantastic' 와 같은 구문

//oldObject.sayNode();      // Node 출력
oldObject.a();              // Node 출력
oldObject.sayJS();          // JS 출력
console.log(oldObject.ES6); // Fantastic 출력
```

**ES2015+ 부터 문법**

```
// ES2015+ 문법
const sayNode=function(){
    console.log('Node');
}
const es='ES';
const newObject={           // 객체 {}
    sayJS(){
        console.log('JS');  //
    },
    sayNode,                // 같은 이름의 변수나 Function이 있어 이름만 쓰였다.
    [es+6]: 'Fantastic',    //  
};

// newObject.sayNode();
sayNode();
newObject.sayJS();
console.log(newObject.ES6);
```



##### 화살표 함수(Arrow function)

* 사용방법은 아래의 코드스펜을 확인 해주세요.

* funtion 선언 대신 '**=>**' 기호로 함수를 선언한다. ('= >' 사이 띄어쓰기 안됨!)

  > function add1(x,y){return x+y;} >>> const add1=(x,y) =>{return x+y;}
  >
  > function not1(x){return !x;} >>> const not2= x => !x;

* return문을 줄일수 있다.

  > const add3 = (x,y) => x+y;
  >
  > const add4 = (x,y) => (x+y);

* **<u>this 바인드</u>** (짱 중요!)

```
var relationship1={
    name:'zero',
    friends: ['nero','hero','xero'],
    logFriends: function(){
        //console.log(this);                    // name, friends, logFriends
        var that=this;                          // relationship1을 가르키는 this
        //console.log(that);
        //console.log(that.friends[2]);
        this.friends.forEach(function(friend){
            console.log(that.name,friend);		// this=global(=forEach)
        })
    }
};
relationship1.logFriends();
console.log("\n");

const relationship2={
    name:'zero',
    friends: ['nero','hero','xero'],
    logFriends(){
        var that=this;
        this.friends.forEach(friend => {	// this=relationship2.
            console.log(this.name,friend);  // 여기서 this를 사용할 수 있다.
        })
    }
}
relationship2.logFriends();
```

##### 비구조화 할당

* 객체와 배열로부터 속성이나 요소를 쉽게 꺼낼 수 있다.

```
const candyMachine={
     status:{
         name:'node',
         count:5,
     },
     getCandy(){
         this.status.count--;
         return this.status.count;
     },
     a:10,
     b:20,
     c:50,
     d:{
         name: 'pupop',
         decount: 100,
     }
};
const {getCandy,status:{count},a,b,c,d:{name,decount}}=candyMachine;
// candyMachine 안에 getCandy와 status의 count를 선언. 끄집어 빼오는 형식(?)
```

* 배열의 비구조화

  > var array=['nodejs',{},10,true];
  >
  > var node=array[0];
  >
  > var obj=array[1];
  >
  > var bool=array[3];

|          기존 배열구조           |           비구조화 배열            |
| :------------------------------: | :--------------------------------: |
| var array=['nodejs',{},10,true]; | const array=['nodejs',{},10,true]; |
|        var node=array[0];        |   const [node,obj, ,bool]=array;   |
|        var obj=array[1];         |                                    |
|        var bool=array[3];        |                                    |





#### 3.3 모듈

* 노드는 코드를 모듈로 만들 수 있다는 점에서 브라우저의 자바스크립트와 다르다.
* 모듈: 특정한 기능을 하는 함수나 변수들의 집합
* 보통 파일 하나가 모듈 하나가 된다.



