# 솔리디티 Solidity

- 객체지향형 프로그래밍 언어
- Javascript + java + C++
- 문법은 JS, 타입은 스트립하게 고정(JAVA), 객체는 
- EVM(Ethereum Virtual Marchine)에서 실행된다.
- .sol 확장자명을 가짐.
- 배포 지원
  (VSCode에서 작업할 경우 배포는 안된다. Compiler가 있다면 모를까..)



https://steemkr.com/kr/@tenihil/introducing-ethereum-and-solidity-3

[ [모두의 연구소] Introducing Ethereum and Solidity 3장 요약본 ]



### 개발환경



#### Remix ide

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





### Gas 비용

https://www.slideshare.net/jaehyun/



![Halting Problem - Gas Cost Model Data Location Gas ë¹ì© Storage 32ë°ì´í¸ë¹ 20,000 Memory 32ë°ì´í¸ë¹ 1 Log 32ë°ì´í¸ë¹ 96 ( ë°ì´í¸ë¹ 3 ) Call ...](https://image.slidesharecdn.com/hs2q9narqzeijwk6hh5t-signature-b20f0e6656d30caa5fb58141ac5f8e8460ced9da611eb413b6a74efe95864e63-poli-171111074033/95/4-9-638.jpg?cb=1510386790)



Gas의 이해

[https://medium.com/@playdev/%EC%9D%B4%EB%8D%94%EB%A6%AC%EC%9B%80-%EA%B0%80%EC%8A%A4%EC%97%90-%EB%8C%80%ED%95%9C-%EC%9D%B4%ED%95%B4-gas-price-gas-limit-block-gas-limit-161268a5fc54](https://medium.com/@playdev/이더리움-가스에-대한-이해-gas-price-gas-limit-block-gas-limit-161268a5fc54)







### Contract



##### Created constructor

| status           | 0x1 Transaction mined and execution succeed                  |
| ---------------- | ------------------------------------------------------------ |
| transaction hash | 0xb780e1180c2993b213280485d4be8fe85cd04bfebf72ea46b08bc166b912c19a |
| contract address | 0x692a70d2e424a56d2c6c27aa97d1a86395877b3a                   |
| from             | 0xca35b7d915458ef540ade6068dfe2f44e8fa733c                   |
| to               | HelloWorld.(constructor)                                     |
| gas              | 3000000 gas                                                  |
| ransaction cost  | 380932 gas                                                   |
| execution cost   | 235864 gas                                                   |
| hash             | 0xb780e1180c2993b213280485d4be8fe85cd04bfebf72ea46b08bc166b912c19a |
| input            | 0x608060405234801561001057600080fd5b506040516105893803806105898339810180604052602081101561003357600080fd5b81019080805164010000000081111561004b57600080fd5b8281019050602081018481111561006157600080fd5b815185600182028301116401000000008211171561007e57600080fd5b5050929190505050806000908051906020019061009c9291906100a3565b5050610148565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f106100e457805160ff1916838001178555610112565b82800160010185558215610112579182015b828111156101115782518255916020019190600101906100f6565b5b50905061011f9190610123565b5090565b61014591905b80821115610141576000816000905550600101610129565b5090565b90565b610432806101576000396000f3fe608060405234801561001057600080fd5b50600436106100415760003560e01c8063954ab4b214610046578063a4136862146100c9578063ef690cc014610184575b600080fd5b61004e610207565b6040518080602001828103825283818151815260200191508051906020019080838360005b8381101561008e578082015181840152602081019050610073565b50505050905090810190601f1680156100bb5780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b610182600480360360208110156100df57600080fd5b81019080803590602001906401000000008111156100fc57600080fd5b82018360208201111561010e57600080fd5b8035906020019184600183028401116401000000008311171561013057600080fd5b91908080601f016020809104026020016040519081016040528093929190818152602001838380828437600081840152601f19601f8201169050808301925050505050505091929192905050506102a9565b005b61018c6102c3565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156101cc5780820151818401526020810190506101b1565b50505050905090810190601f1680156101f95780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b606060008054600181600116156101000203166002900480601f01602080910402602001604051908101604052809291908181526020018280546001816001161561010002031660029004801561029f5780601f106102745761010080835404028352916020019161029f565b820191906000526020600020905b81548152906001019060200180831161028257829003601f168201915b5050505050905090565b80600090805190602001906102bf929190610361565b5050565b60008054600181600116156101000203166002900480601f0160208091040260200160405190810160405280929190818152602001828054600181600116156101000203166002900480156103595780601f1061032e57610100808354040283529160200191610359565b820191906000526020600020905b81548152906001019060200180831161033c57829003601f168201915b505050505081565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f106103a257805160ff19168380011785556103d0565b828001600101855582156103d0579182015b828111156103cf5782518255916020019190600101906103b4565b5b5090506103dd91906103e1565b5090565b61040391905b808211156103ff5760008160009055506001016103e7565b5090565b9056fea165627a7a723058206a9d75a6858de37f6b1dec4a31ff173f36aa2a5448e7c19595709845d322c4820029000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000053131313131000000000000000000000000000000000000000000000000000000 |
| decoded input    | { 	"string _greeting": "11111" }                          |
| decoded output   | -                                                            |
| logs             | []                                                           |
| value            | [object HTMLTableRowElement] wei                             |



##### setGreeting()

| status           | 0x1 Transaction mined and execution succeed                  |
| ---------------- | ------------------------------------------------------------ |
| transaction hash | 0x7f381c5767b6a41f8917af02f6cbfd015c4f3b92ffc4cfe5ec6f6111872f7c5b |
| from             | 0x583031d1113ad414f02576bd6afabfb302140225                   |
| to               | HelloWorld.setGreeting(string) 0x0fdf4894a3b7c5a101686829063be52ad45bcfb7 |
| gas              | 3000000 gas                                                  |
| transaction cost | 13975 gas                                                    |
| execution cost   | 6357 gas                                                     |
| hash             | 0x7f381c5767b6a41f8917af02f6cbfd015c4f3b92ffc4cfe5ec6f6111872f7c5b |
| input            | 0xa41...00000                                                |
| decoded input    | { 	"string _greeting": "" }                               |
| decoded output   | {}                                                           |
| logs             | []                                                           |
| value            | 0 wei                                                        |



##### greeting()

| ransaction hash | 0x75d5c7c21548afd0fff542ae625cd13dddb4698e606dcea2997352e79a8a9eb9 |
| --------------- | ------------------------------------------------------------ |
| from            | 0xca35b7d915458ef540ade6068dfe2f44e8fa733c                   |
| to              | HelloWorld.greeting() 0x692a70d2e424a56d2c6c27aa97d1a86395877b3a |
| ransaction cost | 22723 gas (Cost only applies when called by a contract)      |
| execution cost  | 1451 gas (Cost only applies when called by a contract)       |
| hash            | 0x75d5c7c21548afd0fff542ae625cd13dddb4698e606dcea2997352e79a8a9eb9 |
| input           | 0xef6...90cc0                                                |
| decoded input   | {}                                                           |
| decoded output  | { 	"0": "string: 11111" }                                 |
| logs            | []                                                           |



#####  say()

| transaction hash | 0x45e339cf105d8213a598bfd5741308ffacfdda12472bd34f6c2d5518d992f9db |
| ---------------- | ------------------------------------------------------------ |
| from             | 0xca35b7d915458ef540ade6068dfe2f44e8fa733c                   |
| to               | HelloWorld.say() 0x692a70d2e424a56d2c6c27aa97d1a86395877b3a  |
| ransaction cost  | 22687 gas (Cost only applies when called by a contract)      |
| execution cost   | 1415 gas (Cost only applies when called by a contract)       |
| hash             | 0x45e339cf105d8213a598bfd5741308ffacfdda12472bd34f6c2d5518d992f9db |
| input            | 0x954...ab4b2                                                |
| decoded input    | {}                                                           |
| decoded output   | { 	"0": "string: 11111" }                                 |
| logs             | []                                                           |



#### 복습

Remix ide

```sol
pragma solidity ^0.5.8;

contract MyContract {
    string value;
    
    constructor(string memory _value) public {
    // public: 외부에서 접근이 가능하다.
        value = _value;
    }
    
    // get function
    function getValue() public view returns (string memory) {    // 값을 얻는 함수이니 인자는 불필요
    // view: 상태 변수에 대해서 보기(읽기)만 하겠다.
        return value;
    }
    
    // set function
    function setValue(string memory _value) public {
        value = _value; // 인자로 받은 _value를 현재 상태변수인 value에 적용
    }
}
```



### Remix Compile

* Current version을 설정
* Start to compile을 클릭하면 아래 contract가 생성된다.

![1567470857566](https://user-images.githubusercontent.com/50816203/64138997-57531b00-ce3a-11e9-911d-f4b30bdf6636.png)

### Remix 배포

* Environment
  * JavaScript VM: 가상 테스트용. 5개의 Accout 제공.
  * Injected Web3:
  * Web3 Provider: 실제로 열려있는 Geth Server에 접속하여 배포
* Account: Acount목록
* Gas Limit: 배포에 사용할 수수료
* Value: 거래할 코인 값 (단위 지정: Wei <<<< Gwei(Gas) <<<< Ether)

![image](https://user-images.githubusercontent.com/50816203/64139028-72258f80-ce3a-11e9-9849-8fe78c57c891.png)

* MyContract: 배포할 함수의 Compile
* Deploy: 값을 지정하여 배포
* At Address:
  Contract address를 명시하면 다른 Account가 배포한 Compile 실행
  (Gas 차감은 Deploy한 Account에게..)



#### Solidity 변수

* 변수 형식
  [type] [변수 name] = [변수값]
* 변수 종류
  * string: 문자열 **" "**
  * bool: **true/false**
  * int: **정수 (-256 ~ 255)**
  * uint: **양수 (0 ~ 255)**

```sol
pragma solidity ^0.5.8;

contract MyContract {
    //solidity 변수지정
    //[type] [변수 name] = [변수값]
   string public value;
   bool public isValid = true; // bool: true/false
   int public num1 = 100;      // int: 숫자. 기본으로 int256 셋팅.
   int public num2 = -100;      // int: 음수 지정 가능
   uint public unum1 = 200;
   uint public unum2 = -200;
   int256 public num256 = 256;
   uint256 public unum256 = 256;
   
   int8 num8 = 10;  // -128~127
   uint8 unum8 = 20; // 0~255
}
```



* enum
  * RED, GREEN, BLUE 의 값중 한개를 가질 수 있다.
  * Ex. Color.RED의 값은 enum Color의 RED **Index값** (=0)
  * Start Number를 줄 수 있다.

```sol
pragma solidity ^0.5.8;

contract MyContract {
    enum Color { RED, GREEN, BLUE };
    
    Color public color;
    
    constructor() public {
        color = Color.RED;
    }
    
    function activate() public {
        color = Color.BLUE;
    }
    
    function isActive() public view returns(bool) {
        return color == Color.GREEN;
    }
    
}
```



* 

```sol
pragma solidity ^0.5.8;

contract MyContract {
    enum Color { RED, GREEN, BLUE }
    
    Color public RED = Color.RED;
    Color public GREEN = Color.GREEN;
    Color public BLUE = Color.BLUE;
    
    function setColorRED(uint newColor) public {
        RED = Color(newColor);
    }
}
```





#### 구조체 사용

* 

```
pragma solidity ^0.5.8;

contract StructContract {
    struct Person {
        string _firstName;
        string _lastName;
    }
    
    Person[] public people;
    
    uint public peopleCount;
    
    function addPerson (string memory _firstName, string memory _lastName) public {
        people.push(Person(_firstName,_lastName));   // Person 구조체를 이용하여 Push해줘야 한다.
        peopleCount ++;                             // Person인 추가될때 만다 peopleCount 1씩 증가
    }
}
```



* addPerson을 통해 Person추가
* Person을 추가하니 peopleCount가 증가한다.
* people의 0번째, 1번째, 2번째에 기록된 것을 확인할 수 있다.

![image](https://user-images.githubusercontent.com/50816203/64139042-85d0f600-ce3a-11e9-82b5-02c42805cb1a.png)



#### 활용

* Person에 Address Mapping하여 추가

```sol
pragma solidity ^0.5.8;

contract StructContract {
    struct Person {
        uint _id;
        string _firstName;
        string _lastName;
    }
    
    uint public peopleCount;
    
    mapping (address => Person) public people;
    
    function addPerson (address _address, string memory _firstName, string memory _lastName) public {
        peopleCount ++; // 0번 부터 시작하지 않으려고 먼저 Count
        people[_address] = Person(peopleCount, _firstName, _lastName);
    }
}
```



* 투표수 확인

```sol
pragma solidity ^0.5.8;

contract StructContract {
    struct Person {
        uint _id;
        string _firstName;
        string _lastName;
    }
    
    uint public peopleCount;
    
    // 획득표 mapping
    mapping (address => uint) public voteResult;
    
    mapping (address => Person) public people;
    
    function addPerson (address _address, string memory _firstName, string memory _lastName) public {
        peopleCount ++; // 0번 부터 시작하지 않으려고 먼저 Count
        people[_address] = Person(peopleCount, _firstName, _lastName);
    }
    
    // 특정 address가 몇표를 획득했는가 확인하는 함수
    function vote (address _address) public {
        voteResult[_address] ++;
    }
}
```

* vote에 Person의 address를 넣으면 그 사람에게 투표하게 된다.
* VoteResult에 투표받은 사람의 address를 넣고 확인하면 몇표 받았는지 확인 할 수 있다. = 10

![image](https://user-images.githubusercontent.com/50816203/64139057-95e8d580-ce3a-11e9-9354-5bd0fdb9be57.png)



### Solidity Programing



####  함수 (function)

* 동일한 코드가 반복 사용될 때 반복되는 부분을 함수로 처리
  * 함수 내부에 선언된 변수는 지역변수
  * 함수 외부에 선언된 변수는 상태변수
* function 함수 이름 (입력 매개변수) 옵션(가시성) returns (출력 매개변수)
  * function name(x1, x2, ...) option returns (y1, y2...)
  * name : 함수의 이름
  * 매개변수 : 입력 시 사용되는 파라메터 (x1, x2, ...)
  * 반환값 : 결과 출력 시 사용되는 변수 (y1, y2, ...)함수 가시성
    * Public, private, internal, external
  * 기타 옵션
    * View, pure, payable



#### 조건문과 반복문

* If / if-else
* 삼항조건문
* For문
* While문
* Break / continue



#### 형변환

* 암묵적 변환
  * 데이터 손실이 없는 자료형
  * Int8 -> int16 은 암묵적 가능

* 명시적 형변환
  * 데이터 손실이 발생할 수 있는 경우 컴파일러가 암묵적 형변환을 해주지 않음
  * 개발자가 명시적으로 형변환, 데이터 손실 발생 가능



#### 배열

* length, push()
* Storage 배열
* Memory 배열
* 고정 바이트 배열
* 동적 바이트 배열



#### 상속

* 상속과 다형성 지원.
* contract Parent {}
* contract Child is Parent {}



### 특수 변수 / 함수

#### block 변수

* 블록 해시 반환
  * block.blockhash(uint blockNumber) returns (byte32)
  * 최근 256 블록 내의 블록만 가능
* 블록 넘버
  * block.number()

#### msg 변수

* msg.sender: 함수(contract)를 실행한 Address
* msg.value: 트랜젝션에 담긴 Ether 금액



#### 수학함수

* 해시 함수keccak256(...) returns (byte32)
* sha3(...) returns (byte32)



#### 폴백 함수 (fallback function)

* 컨트랙트별로 하나만 가질수 있음
* 컨트랙트로 전송된 이더를 처리하는 함수
* 요청한 함수가 없는 경우 호출
* 함수이름, 인자, 리턴값이 없는 빈 함수
* External 가시성을 가져야 함
* 내부에서 받은 이더를 어떻게 처리할 지 정할 수 있음.
* Payable 함수를 거치치 않고 순수하게 ether를 전송받는 경우
* 컨트랙트 함수를 거치지 않고 이더를 받고 싶으면 반드시 구현해야 함

```sol
function() external payable {   ......}
```



#### 계약 파기

* Selfdestruct
* Suicide



#### timestamp

* 관련 예약어
  * Second, minute, hour, day, week, year

```
pragma solidity ^0.5.8;

contract TimestampContract {
   uint256 public peopleCount = 0;
   mapping(uint => Person) public people;

   uint256 startTime;

   modifier onlyWhileOpen() {
      require(block.timestamp >= startTime);
   }

   struct Person {
      uint _id;
      string _firstName;
      string _lastName;
   }

   constructor() public {
      startTime = 1567437931178; // Update this value
   }

   function addPerson(string memory _firstName, string memory _lastName)	public	onlyWhileOpen{
      people[peopleCount] = Person(peopleCount, _firstName, _lastName);
   }
   function incrementCount() internal {
      peopleCount += 1;
   }
}
```



#### address

* 타입특수
* 변수20바이트 주소 저장
* \<address>.balance(uint256)
* \<address>.transfer() 제공



### 실습 - BankContract

https://medium.com/@soonhyungjung/%EC%9D%B4%EB%8D%94%EB%A6%AC%EC%9B%80-%EC%8A%A4%EB%A7%88%ED%8A%B8-%EA%B3%84%EC%95%BD-3-%EB%B8%94%EB%A1%9D%EC%B2%B4%EC%9D%B8-%EC%9D%80%ED%96%89-%EB%A7%8C%EB%93%A4%EA%B8%B0-44a9d58d687a

#### 이더 송금

* msg.sender
* msg.value
* payable
* address.transfer



#### EOA => CA => EOA 이더 송금

```sol
pragma solidity ^0.5.8;

contract EtherSendContract{
	mapping(address => uint256) public balances;
	address payable wallet;

constructor(address payable _wallet) public {
	wallet = _wallet;
}

function buyToken() public payable {
	balances[msg.sender] += 1;
	wallet.transfer(msg.value);
}
}
```



#### Bank 계약

```sol
pragma solidity ^0.5.8;

contract Bank {
    uint public bankBalance;

    // 누가(address) 얼마를(uint) 입금했는지 확인하기 위한 mapping
    mapping (address => uint) balanceOf;

    constructor() public {

    }

    // 은행에 코인 입금 함수
    function deposit() public payable { // 입출금 함수임을 표시 = payable
        // deposit을 수행할 때 보낸 금액만큼 추가
        balanceOf[msg.sender] += msg.value;
        bankBalance += msg.value;
    }

    // 은행에 맡긴 코인 출금 함수
    function withdraw(uint _amount) public payable {
        // 금액이 없을 경우 출금 안되도록 정의
        require(balanceOf[msg.sender] >= _amount);

        balanceOf[msg.sender] -= _amount;
        bankBalance -= _amount;
        msg.sender.transfer(_amount);
    }

    // 잔액 조회 함수
    function getBalanceOf(address _account) public view returns (uint) {
        return balanceOf[_account];
    }

    // 은행이 받은 모든코인 조회
    function getTotalBalance() public view returns (uint) {
        return bankBalance;
    }

}
```



#### 잔액 확인

```sol
function getBalance() public view returns (uint) {
	return address(this).balance;
}
```



#### 이벤트

```sol
pragma solidity ^0.5.8;

contract MyContract {
   address payable wallet;
   mapping(address => uint256) public balances;

   event Purchase(address indexed _buyer, uint256 _amount);

   constructor(address payable _wallet) public {
   	wallet = _wallet;
   }

   function() external payable {
   	buyToken();
   }

   function buyToken() public payable {
      balances[msg.sender] += 1;
      wallet.transfer(msg.value);
      emit Purchase(msg.sender, 1);
   }
}
```



#### Token 거래

```sol
pragma solidity ^0.5.8;

contract SimpleToken {
    address owner;

    string symbol = "SKKTLG";

    mapping(address => uint) public balanceOf;

    constructor() public {
        // balanceOf[msg.sender] = 1*(10**18);
        owner = msg.sender;
    }

    function transfer(address _to, uint _value) public {
        // transfer 실행자
        address _from = msg.sender;
        
        // 소지한 금액보다 높은 금액을 보낼 수 없도록
        require(balanceOf[_from] >= _value);
        
        balanceOf[_from] -= _value;
        balanceOf[_to] += _value;
    }

    function buy() public payable{
        // Token 환율
        uint SGken = msg.value*10;

        //require(msg.value >= );
        balanceOf[msg.sender] += SGken;

    }

    function sell(uint _value) public payable{
        require(balanceOf[msg.sender] >= _value);
        
        // Token 환율
        uint weiAmount = _value/10;

        balanceOf[msg.sender] -= _value;
        msg.sender.transfer(weiAmount);
    }

}
```



#### 투표

```sol
pragma solidity ^0.5.8;

contract Vote {
    uint8 numOfCandidate = 0;

    mapping (string => uint) score; // 각 후보별 특표수
    mapping (uint8 => string) public candidateList; // 후보자 리스트
    mapping (address => bool) isVoted;  // 투표 확인 유무 
    address payable owner;  // contract 삭제시 반환되는 코인을 받아야하기 때문에 payable

    constructor () public {
        owner = msg.sender;
    }

    // owner만 할 수 있도록 modifier 선언
    modifier ownerOnly {
        require(msg.sender == owner, "Only owner can call this function.");
        _;
    }

    // 한번 투표한 사람은 다시 투표하지 못하도록..
    modifier checkDuplicate {
        require(isVoted[msg.sender] == false, "You Voted!");
        _;
    }

    // 후보자 등록
    function addCandiate (string memory _candidate) public ownerOnly {  // owner만 후보자 등록 가능!
        // 후보자 중복확인
        bool found = false;
        for (uint8 i=0; i<numOfCandidate; i++) {
            // solidity에서는 문자열 값 비교가 안된다. 그래서 keccak256(해시함수)로 변환하고 이것으로도 부족해서 bytes로 변환하여 검사
            // bytes: ??
            if(keccak256(bytes(candidateList[i])) == keccak256(bytes(_candidate))){
                found = true;
                break;
            }
        }
        require (!found);

        candidateList[numOfCandidate] = _candidate;
        numOfCandidate ++;
    }

    // 투표
    function vote (string memory _candidate) public checkDuplicate {
        // require(isVoted[_candidate] == true, "You voted!");
        score[_candidate] ++;
        isVoted[msg.sender] = true;
    }

    // 후보자 수
    function getNumOfCandidate () public view returns (uint8) {
        return numOfCandidate;
    }

    // 후보자 확인
    function getCandidate(uint8 index) public view returns (string memory) {
        return candidateList[index-1];  // 배열은 0부터 시작해서 -1을 해주었다.
    }

    // 후보자 득표수 확인
    function getScore(string memory _candidate) public view returns (uint) {
        return score[_candidate];
    }

    // destroy contract 컨트랙트 삭제!
    function killContract() public ownerOnly {
        // 아래 계좌로 코인은 반환된다.
        selfdestruct(owner);
    }
}
```

* addCandidate: ""(쌍따옴표)안에 후보자 이름을 넣고 실행하면 후보자 등록
* vote: "[후보자이름]"을 입력하고 실행하면 1표씩 투표
* candidateList: 배열의 구조로 0~N을 입력하면 순서대로 후보자 이름 출력
* getCandidate: 1~N번째 후보자 확인
* getNumOfCandidate: 후보자 명수
* getScore: "[후보자명]"을 입력하면 득표수 확인
* killContract: Contract를 삭제한다! 거래되었던 ether는 selfdestruct()에게 돌려주게된다.

![image](https://user-images.githubusercontent.com/50816203/64227187-7bd3f380-cf1d-11e9-8471-8e4d50153a6d.png)



#### 추첨

```sol
pragma solidity ^0.5.8;

contract Lottery {
    // 응모자를 관리하는 매핑
	mapping (uint => address) public applicants;
	// 응모자 수
	uint public numOfApplicants;
    bool public isHolder;
	// 당첨자 정보
	address public winnerAddress;
	uint public winnerId;
	// 소유자
	address public owner;
	// 타임스탬프
	uint public timestamp;

    // 생성자
	constructor() public {
		numOfApplicants = 0;
		owner = msg.sender;
	}

    // owner만 사용할 수 있도록 선언
    modifier ownerOnly {
        require(msg.sender == owner, "Only owner can call this function.");
		_;
    }

    // 응모
    function enter() public {
        // 중복 신청 불가
        for(uint i=0; i < numOfApplicants; i++){
            require(applicants[i] != msg.sender);
        }
        // 응모 처리
        applicants[numOfApplicants++] = msg.sender;
    }

    // 추첨
    function hold() public ownerOnly {   // Owner만 추첨 가능
        // 최소 응모자
        require(numOfApplicants > 3);

        // timestamp 값 받아오기
        timestamp = block.timestamp;    // hole함수가 실행되어 transaction이 들어간 block의 timestamp
        // 채굴자는 채굴자가 만든 block의 timestamp를 정할 수 있는 단점..

        // 추첨
        winnerId = timestamp % numOfApplicants;    // timestamp를 사용자 수 만큼 나눈다.
        winnerAddress = applicants[winnerId];
    }
}
```

* enter: 응모 참여
* hold: 당첨자 뽑기. Owner만 실행할 수 있다.
* applicants: ID에 따른 응모자 Address
* numOfApplicants: 응모자 수
* owner: Contract 생성자 = Owner
* timestamp: 당첨 시기. hold를 하기 전에는 값이 없다.
* winnerAddress: 당첨자 Address 확인
* winnerId: 당첨자 ID 확인

![image](https://user-images.githubusercontent.com/50816203/64231576-fce5b780-cf2a-11e9-87e2-5d1aeda61f0b.png)





#### 크라우드 펀딩

```sol
pragma solidity ^0.5.8;

// 크라우드 펀딩은..
// 특정 시점을 기준으로 마감.
//

contract CrowdFunding {

    // 투자자들
    struct Investor {
        address payable addr;
        uint amount;
    }

    mapping (uint => Investor) public investors;
    // Funding 참여자 수
    uint public numOfInvestor;

    // 목표 금액
    uint goalAmount = 2*(10**18);
    // 모인 금액
    uint public totalAmount;

    address payable public owner;


    // Functions
    constructor () public {
        owner = msg.sender;
    }

    modifier onlyOwner {
        require(msg.sender == owner);
        _;
    }

    function fund() public payable {    // 실제 돈이 거래되기 때문에 payable!
        // if(){
            investors[numOfInvestor] = Investor(msg.sender, msg.value);
            numOfInvestor ++;
            totalAmount += msg.value;
        // } else {
        //     investors[]
        //     totalAmount += msg.value;
        // }
    }

    function checkGoalFunding() public onlyOwner payable{
        if(totalAmount >= goalAmount){
            owner.transfer(address(this).balance);
        } else {
            for(uint i=0; i<numOfInvestor; i++){    // 두번째 조건이 false일때 멈춘다!
                investors[i].addr.transfer(investors[i].amount);
            }
        }
    }

    // 혹시 모를 문제(해킹 등..)가 발생했을때 돈을 회수하기 위해..!
    function killContract() public onlyOwner {
        selfdestruct(owner);
    }
}
```

* checkGoalFunding:
* fund:
* killContract:
* investors:
* numOfInvestor:
* owner:
* totalAmount: 모금된 Funding 금액

![image](https://user-images.githubusercontent.com/50816203/64238792-04f92380-cf3a-11e9-8319-27a78a4ebe64.png)





### Geth Web 연동

* Gethrpc.bat을 작성
  * geth rpc 실행 code

```bat
geth --datadir chaindata --networkid 33
--nodiscover --maxpeers 0
--rpc -rpcaddr "0.0.0.0" --rpcport 8545
--rpccorsdomain "*"
--rpcapi "db,eth,net,web3,admin,devug,miner,shh,txpool,personal"
console
```



* Geth폴더에 넣어 . bat 실행.
* 명령어 결과를 통해 연결 확인
  Ex. 블록생성량 조회(eth.blockNumber / web3.eth.getBlockNumber().then(console.log))
* web3를 통한 명령어는 Promise Type으로 받기 때문에 .then으로 처리했다.

![image](https://user-images.githubusercontent.com/50816203/64306668-89958180-cfce-11e9-9e8a-5a7105c6a909.png)



#### Contract Test

* 변수 선언
  * **const abi = [ABI Copy Code]**
  * **const contractAddress = "[Contract Address]"**
  * Vote Contract 변수로 선언하여 실행한다.
    **var voteContract = new web3.eth.Contract(abi, contractAddress)**

##### contracttest.js 파일로 실행 해보자

```js
var Web3 = require('web3');
var web3 = new Web3('http://localhost:8545');

const abi = [
    {
        "constant": false,
        "inputs": [
            {
                "name": "_candidate",
                "type": "string"
            }
        ],
        "name": "addCandiate",
        "outputs": [],
        "payable": false,
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "constant": false,
        "inputs": [],
        "name": "killContract",
        "outputs": [],
        "payable": false,
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "constant": false,
        "inputs": [
            {
                "name": "_candidate",
                "type": "string"
            }
        ],
        "name": "vote",
        "outputs": [],
        "payable": false,
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "inputs": [],
        "payable": false,
        "stateMutability": "nonpayable",
        "type": "constructor"
    },
    {
        "constant": true,
        "inputs": [
            {
                "name": "",
                "type": "uint8"
            }
        ],
        "name": "candidateList",
        "outputs": [
            {
                "name": "",
                "type": "string"
            }
        ],
        "payable": false,
        "stateMutability": "view",
        "type": "function"
    },
    {
        "constant": true,
        "inputs": [
            {
                "name": "index",
                "type": "uint8"
            }
        ],
        "name": "getCandidate",
        "outputs": [
            {
                "name": "",
                "type": "string"
            }
        ],
        "payable": false,
        "stateMutability": "view",
        "type": "function"
    },
    {
        "constant": true,
        "inputs": [],
        "name": "getNumOfCandidate",
        "outputs": [
            {
                "name": "",
                "type": "uint8"
            }
        ],
        "payable": false,
        "stateMutability": "view",
        "type": "function"
    },
    {
        "constant": true,
        "inputs": [
            {
                "name": "_candidate",
                "type": "string"
            }
        ],
        "name": "getScore",
        "outputs": [
            {
                "name": "",
                "type": "uint256"
            }
        ],
        "payable": false,
        "stateMutability": "view",
        "type": "function"
    }
];

const contractAddress = "0xd1A6569c43d4C89C29290013E21E73c1C198E1d2";

var voteContract = new web3.eth.Contract(abi, contractAddress);

console.log();
voteContract.methods.getNumOfCandidate().call()
    .then((err, result) => {
        if (err) console.log('err = ', err);
        else console.log('result = ', result);
    })
```



## Ganache Tool

* remix에서 Test할 때 Mining 작업이 계속 되어야 Transaction, contract Test하기가 수월하다.
* 그래서 geth를 대체하는 가상 Node로 Ganache를 사용한다.
* **끄게되면 작업하던 내용이 사라짐!!**

![image](https://user-images.githubusercontent.com/50816203/64308230-8355d400-cfd3-11e9-9326-8898ba72fd0f.png)



#### Server Setting

* HostName: PC의 Ethernet 설정
* Port Number: Node의 포트번호
  * console로 geth를 실행중이라면 8545는 충돌 날 수 있다.
* Network ID:

![image](https://user-images.githubusercontent.com/50816203/64307682-d038ab00-cfd1-11e9-82f8-4ef0b34aaee4.png)



#### Block



![image](https://user-images.githubusercontent.com/50816203/64308197-69b48c80-cfd3-11e9-896b-0643a866250e.png)



#### Transaction



![image](https://user-images.githubusercontent.com/50816203/64307731-0118e000-cfd2-11e9-9180-16523351b9ab.png)