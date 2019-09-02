# 솔리디티 Solidity

- 객체지향형 프로그래밍 언어
- Javascript + java + C++
- 문법은 JS, 타입은 스트립하게 고정(JAVA), 객체는 
- EVM(Ethereum Virtual Marchine)에서 실행된다.
- .sol 확장자명을 가짐.
- 배포 지원
  (VSCode에서 작업할 경우 배포는 안된다. Compiler가 있다면 모를까..)



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