

### 프로젝트 생성

C:\myBChain 폴더 생성

```
C:\myBChain>npm init -y
Wrote to C:\myBChain\package.json:

{
  "name": "myBChain",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}

C:\myBChain>npm i --save crypto-js
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN myBChain@1.0.0 No description
npm WARN myBChain@1.0.0 No repository field.

+ crypto-js@3.1.9-1
added 1 package from 1 contributor and audited 1 package in 0.794s
found 0 vulnerabilities
```



### Block의 생성

Block.js 파일 생성

```js
const SHA256 = require('crypto-js/sha256');

class Block {

    constructor(index, timestamp, transactions) {
        this.index = index;                 //
        this.timestamp = timestamp;         //
        this.prevHash = '';                 //
        this.nonce = 0;                     // 
        this.transactions = transactions;   //

        this.curHash = this.calculateHash();
    }

    calculateHash() {
        console.log("1"+SHA256('1').toString());
        console.log("2"+SHA256('2').toString());
        console.log("3"+SHA256('3').toString());
        console.log("4"+SHA256('4').toString());

        return SHA256('poi123');
    }
}

module.exports = Block;
```



test.js 생성

```js
const Block = require('./block');

const newBlock = new Block(1, Date.now(), 'aaa');
```

test.js 실행

```
C:\myBChain>node test.js
16b86b273ff34fce19d6b804eff5a3f5747ada4eaa22f1d49c01e52ddb7875b4b
2d4735e3a265e16eee03f59718b9b5d03019c07d8b6c51f90da3a666eec13ab35
34e07408562bedb8b60ce05c1decfe3ad16b72230967de01f640b7e4729b49fce
44b227777d4dd1fc61c6f884f48641d02b4d121d3fd328cb08b5531fcacdabf8a
```



printBlock 함수 추가

```js
const SHA256 = require('crypto-js/sha256');

class Block {

    constructor(index, timestamp, transactions) {
        this.index = index;                 //
        this.timestamp = timestamp;         //
        this.prevHash = '';                 //
        this.nonce = 0;                     // 
        this.transactions = transactions;   //

        this.curHash = this.calculateHash();
        // transactions의 값이 객체로 나오기 때문에 toString함수로 문자열로 변환한다.
    }

    calculateHash() {
        // console.log("1"+SHA256('1').toString());
        // console.log("2"+SHA256('2').toString());
        // console.log("3"+SHA256('3').toString());
        // console.log("4"+SHA256('4').toString());

        return SHA256(this.prevHash + this.timestamp + JSON.stringify(this.transactions)).toString();
    }

    printBlock() {
        console.log(JSON.stringify(this, null, 2));
    }
}

module.exports = Block;
```



block.js 수정

```
constructor(index, timestamp, transactions, prevHash) {
        this.index = index;
        this.timestamp = timestamp;
        this.prevHash = prevHash;
        this.nonce = 0;
        this.transactions = transactions;

        this.curHash = this.calculateHash();
    }
```



test.js 수정

```
const Block = require('./block');

const newBlock = new Block(1, Date.now(), 'aaa', '');
console.log('----');
const newBlock2 = new Block(2, Date.now(), 'bbb', newBlock.curHash);
console.log('----');

newBlock.printBlock();
console.log('----');

newBlock2.printBlock();
```



```
C:\myBChain>node test.js
----
----
{
  "index": 1,
  "timestamp": 1566175724248,
  "nonce": 0,
  "transactions": "aaa",
  "curHash": "9a4074dd11b755c1252ca1b90238d118406274c9f4577786ba1aa86c9541c396"
}
----
{
  "index": 2,
  "timestamp": 1566175724252,
  "nonce": 0,
  "transactions": "bbb",
  "curHash": "bdbc6f16dd339a0cfe200322367b06bb1252b42febf20914463a06d3f16a9b58"
}

C:\myBChain>node test.js
----
----
{
  "index": 1,
  "timestamp": 1566175786822,
  "prevHash": "",
  "nonce": 0,
  "transactions": "aaa",
  "curHash": "8e8a84f343c2a27f055755c19918ded970c79fb61a5bd28d3066eb1ab54be364"
}
----
{
  "index": 2,
  "timestamp": 1566175786827,
  "prevHash": "8e8a84f343c2a27f055755c19918ded970c79fb61a5bd28d3066eb1ab54be364",
  "nonce": 0,
  "transactions": "bbb",
  "curHash": "b8ca7ef29ec47312fc9695d03e4af32c8bec7bf4073ca61d9b150c4fe6e0d5bc"
}
```



### Block에 데이터에 Transaction 저장

transaction.js 생성

```js

class Transaction {

    constructor(fromAddress, toAddress, amount) {
        this.fromAddress = fromAddress;
        this.toAddress = toAddress;
        this.amount = amount;
    }

    printTransaction() {    // 이쁘게 출력해줌.
        console.log(JSON.stringify(this, null,2));
    }
}

module.exports = Transaction;
```



test.js 수정

```js
const Block = require('./block');
const Transaction = require('./transaction');

const newBlock = new Block(1, Date.now(), 'aaa', '');
console.log('----');
const newBlock2 = new Block(2, Date.now(), 'bbb', newBlock.curHash);

const tx1 = new Transaction ('aaa','bbb',100);
const tx2 = new Transaction ('aaa','ccc',10);
console.log('----');
tx1.printTransaction();

console.log('----');
tx2.printTransaction();
```

출력 확인

```
C:\myBChain>node test.js
----
----
{
  "fromAddress": "aaa",
  "toAddress": "bbb",
  "amount": 100
}
----
{
  "fromAddress": "aaa",
  "toAddress": "ccc",
  "amount": 10
}
----
```



#### 블럭에 데이터 트랜잭션 삽입



test.js Block 부분 수정

```js
const newBlock = new Block(1, Date.now(), 'aaa', '');
console.log('----');
const newBlock2 = new Block(2, Date.now(), 'bbb', newBlock.curHash);
```



#### BlockChain 생성

우리는 블록이 아니라 블록체인을 생성하려고 한다.



blockchain.js 생성

```js
const Block = require('./block');
const Transaction = require('./transaction');

class Blockchain {

    constructor() {
        this.chain = [new Block(0, Date.now(), [], "GenesisBlock")];    // 블록이 생성되는데 블록이 1개 있는 블록 생성
    }

    printBlockchain(){
        console.log(JSON.stringify(this, null, 2));
    }
}

module.exports = Blockchain;
```



test.js에 추가

```js
const Block = require('./block');
const Transaction = require('./transaction');
const Blockchain = require('./blockchain');

const newBlock = new Block(1, Date.now(), 'Genesis Block', '');
console.log('----');
const newBlock2 = new Block(2, Date.now(), '[tx1, tx2]', newBlock.curHash);

const tx1 = new Transaction ('aaa','bbb',100);
const tx2 = new Transaction ('aaa','ccc',10);

const mychain = new Blockchain();

console.log('----');
//console.log(newBlock.curHash.toString());
//newBlock.printBlock();
//tx1.printTransaction();
mychain.printBlockchain();

console.log('----');
//console.log(newBlock2.curHash.toString());
//newBlock2.printBlock();
//tx2.printTransaction();

console.log('----');
//newBlock3.printBlock();
```



출력

```
C:\myBChain>node test.js
----
----
{
  "chain": [
    {
      "index": 0,
      "timestamp": 1566177665391,
      "prevHash": "GenesisBlock",
      "nonce": 0,
      "transactions": [],
      "curHash": "74f88f348c04ec8134c39336bda1367326e83ff46cbf719408098cc44f61ba8f"
    }
  ]
}
----
```



#### Block에 Block 추가



blockchain.js 수정

```
const Block = require('./block');
const Transaction = require('./transaction');

class Blockchain {

    constructor() {
        this.chain = [new Block(0, Date.now(), [], "GenesisBlock")];    // 블록이 생성되는데 블록이 1개 있는 블록 생성
    }

    addBlock(block) {
        block.prevHash = this.getLastestBlock().curHash;    // 기존에 가지고 있던 블록의 제일 마지막 currentHash값을 
        block.curHash = block.calculateHash();              // 변경된 값을 적용하여 Hash처리
        this.chain.push(block);                             // Block을 푸시
    }

    getLastestBlock() {
        return this.chain[this.chain.length -1];
    }

    printBlockchain(){
        console.log(JSON.stringify(this, null, 2));
    }
}

module.exports = Blockchain;
```



출력

```
C:\myBChain>node test.js
----
{
  "chain": [
    {
      "index": 0,
      "timestamp": 1566178209890,
      "prevHash": "",
      "nonce": 0,
      "transactions": [],
      "curHash": "e48a8c0c0143f6daaa10a731854886293faf2352af6e4045fd0fd2e9ffd860ac"
    },
    {
      "index": 1,
      "timestamp": 1566178209891,
      "prevHash": "e48a8c0c0143f6daaa10a731854886293faf2352af6e4045fd0fd2e9ffd860ac",
      "nonce": 0,
      "transactions": [
        {
          "fromAddress": "aaa",
          "toAddress": "bbb",
          "amount": 100
        }
      ],
      "curHash": "5712ce5c071cc1f49678d27328426de394bf975f53e89f3fdc9aec18694b38e6"
    },
    {
      "index": 2,
      "timestamp": 1566178209892,
      "prevHash": "5712ce5c071cc1f49678d27328426de394bf975f53e89f3fdc9aec18694b38e6",
      "nonce": 0,
      "transactions": [
        {
          "fromAddress": "aaa",
          "toAddress": "bbb",
          "amount": 100
        },
        {
          "fromAddress": "aaa",
          "toAddress": "ccc",
          "amount": 10
        }
      ],
      "curHash": "e320a7381b2c0614842ad0a8e3e51ab685c6464ba50589a61c90f27ae4ba4c3d"
    }
  ]
}
----
```



#### Block 조작 검증

blockchain.js 함수 추가

```js
isChainValid() {    // 중간에 조작된 블록이 있는지 검증!
        for (let i=1; i<this.chain.length; i++){
            const curBlock = this.chain[i];
            const prevBlock = this.chain[i-1];

            // 블록 내부 Hash값 검증
            if(curBlock.curHash !== curBlock.calculateHash()){  // 현재 블록의 해시값이 해시처리한 해시값과 다른가?!
                console.log('Err1: Chain [', i, '] Error')
                return false;
            }

            // 이전 블록 Hash값 검증
            if(curBlock.prevHash !== prevBlock.curHash){  // 현재 블록의 이전블록 해시값이 이전블록의 해시값과 다른가?!
                console.log('Err2: Chain [', i, '] Error')
                return false;
            }
        }
        return true;
    }
```



test.js 출력 추가

```js
mychain.printBlockchain();
console.log("Chain valid?", mychain.isChainValid());
```



출력

```
C:\myBChain>node test.js
----
{
  "chain": [
    {
      "index": 0,
      "timestamp": 1566179042737,
      "prevHash": "",
      "nonce": 0,
      "transactions": [],
      "curHash": "f12eca3b72d8f3d33c112f0d1069cf46216c05dabe807c2f9d51287e455e33cb"
      
...

      "curHash": "0dae235ee18adb74b299394d9b1fd92983107d50af4e83a24e351bd52ffc87f5"
    }
  ]
}
Chain valid? true
```



#### Block 조작 테스트





#### 작업 증명

Block.js 함수 추가

```

```



#### Mining 적용

block.js

```js
const SHA256 = require('crypto-js/sha256');

class Block {

    constructor(index, timestamp, transactions) {
        this.index = index;                 //
        this.timestamp = timestamp;         //
        this.prevHash = '';                 //  blockchain으로 block을 add할때 preHash값을 받아올 것 이다.
        this.nonce = 0;                     // 
        this.transactions = transactions;   //

        this.curHash = this.calculateHash();
        // transactions의 값이 객체로 나오기 때문에 toString함수로 문자열로 변환한다.
    }

    calculateHash() {
        // console.log("1"+SHA256('1').toString());
        // console.log("2"+SHA256('2').toString());
        // console.log("3"+SHA256('3').toString());
        // console.log("4"+SHA256('4').toString());

        return SHA256(this.prevHash + this.timestamp + this.nonce + JSON.stringify(this.transactions)).toString();
    }

    printBlock() {
        console.log(JSON.stringify(this, null, 2));
    }

    miningBlock(difficulty) {
        while(this.curHash.substring(0, difficulty) !==
                 Array(difficulty + 1).join('0')) {
            this.nonce++;
            this.curHash = this.calculateHash();
            console.log("mining...", this.nonce, "...", this.curHash);
        }
    }
 
}

module.exports = Block;
```



blockchain.js

```js
const Block = require('./block');
const Transaction = require('./transaction');

class Blockchain {

    constructor() {
        this.difficulty = 2;
        this.chain = [new Block(0, Date.now(), [], "GenesisBlock")];    // 블록이 생성되는데 블록이 1개 있는 블록 생성
    }

    addBlock(block) {
        block.prevHash = this.getLastestBlock().curHash;    // 기존에 가지고 있던 블록의 제일 마지막 currentHash값을 
        //block.curHash = block.calculateHash();              // 변경된 값을 적용하여 Hash처리
        block.miningBlock(this.difficulty);
        this.chain.push(block);                             // Block을 푸시
    }

    getLastestBlock() {
        return this.chain[this.chain.length -1];
    }

    printBlockchain(){
        console.log(JSON.stringify(this, null, 2));
    }

    isChainValid() {    // 중간에 조작된 블록이 있는지 검증!
        for (let i=1; i<this.chain.length; i++){
            const curBlock = this.chain[i];
            const prevBlock = this.chain[i-1];

            // 블록 내부 Hash값 검증
            if(curBlock.curHash !== curBlock.calculateHash()){  // 현재 블록의 해시값이 해시처리한 해시값과 다른가?!
                console.log('Err1: Chain [', i, '] Error')
                return false;
            }

            // 이전 블록 Hash값 검증
            if(curBlock.prevHash !== prevBlock.curHash){  // 현재 블록의 이전블록 해시값이 이전블록의 해시값과 다른가?!
                console.log('Err2: Chain [', i, '] Error')
                return false;
            }
        }
        return true;
    }
}

module.exports = Blockchain;
```



test2.js

```js
const Block = require('./block');
const Transaction = require('./transaction');
const Blockchain = require('./blockchain');

const tx1 = new Transaction ('aaa','bbb',100);
const tx2 = new Transaction ('aaa','ccc',10);

const mychain = new Blockchain();

const newBlock = new Block(1, Date.now(), [tx1]);
const newBlock2 = new Block(2, Date.now(), [tx1, tx2]);

mychain.addBlock(newBlock);
mychain.addBlock(newBlock2);

//newBlock.miningBlock(1);
mychain.printBlockchain();
```





