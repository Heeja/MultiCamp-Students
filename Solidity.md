# 솔리디티 Solidity

- 객체지향형 프로그래밍 언어
- Javascript + java + C++
- 문법은 JS, 타입은 스트립하게 고정(JAVA), 객체는 
- EVM(Ethereum Virtual Marchine)에서 실행된다.
- .sol 확장자명을 가짐.



### 개발환경

Remix ide

**웹으로도 개발이 가능함!!**



```
pragma solidity ^0.4.11;

contract HelloWorld {
    
string public greeting;

// 
function HelloWorld(string _greeting){
    greeting = _greeting;
}

function setGreeting(string _greeting){
    greeting = _greeting;
}

function say() constant returns (string){
    return greeting;
}

}
```





### EVM OPCODE

https://ethervm.io/

EVM이 처리가능한 코드 (어셈블리어)



High Level Langauge를 Compile하여 EVM에서 실행 가능하도록 변경한다.



High Level Langauge > remix > compile > bytecode > EVM > Ethereum



bytecode는 여러 블록에 배포가 될 수 있다.

각각의 bytecode는 contract address로 접근 할 수 있다.





ABI (Application Binary Interface)

* JSON 객체로 변환되는 Solidity Code.. > 실제 실행되어질 곳에서 사용하기 위해(?)
* 사람들이 사용하는 고급언어(High Level Langauge)들을 컨버팅한다.



solidity 0.4 > 0.5 차이

```sol
pragma solidity ^0.5.8;

contract HelloWorld {
    
string public greeting;

// Memory: 임시 변수라는 표시
// Public: 선언을 해줌으로서 공개
constructor(string memory _greeting) public {
    greeting = _greeting;
}

function setGreeting(string memory _greeting) public {
    greeting = _greeting;
}

function say() public view returns (string memory){
    return greeting;
}

}
```

