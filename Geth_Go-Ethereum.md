# Geth (Go-Ethereum)

이더리움 프로토콜을 Go 언어로 구현한 풀 노드 클라이언트 프로그램

- 실제 이더 채굴
- 사용자간 이더리움 전송
- 스마트 컨트랙트 생성 및 배포
- 블록 내역 조회



Main net.

Test net.

Private net.



**genesis.json**

```json
{
        "config": {
                "chainId": 33,
                "homesteadBlock": 0,
                "eip155Block": 0,
                "eip158Block":0
        },

        "nonce": "0x0000000000000033",
        "timestamp": "0x0",
        "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "extraData": "0x00",
        "gasLimit": "0x800000",
        "difficulty": "0x400",
        "mixhash": "0x0000000000000000000000000000000000000000000000000000000000000000",
        // 
   "coinbase": "0x2222222222222222222222222222222222222222",
        // Wallet에 잔액을 가지고 시작할 수 있다.
   "alloc": {}
}
```



**계정생성**



**λ** **geth --datadir chaindata account new**

INFO [08-22|11:34:59] Maximum peer count                       ETH=25 LES=0 total=25
Your new account is locked with a password. Please give a password. Do not forget this password.
**Passphrase:** [비밀번호 입력]
**Repeat passphrase:** [비밀번호 재입력]
Address: {**72255c3599368bc80c831a8aebffb4988582b5e5**}



**λ** **geth --datadir chaindata account new**
INFO [08-22|11:35:27] Maximum peer count                       ETH=25 LES=0 total=25
Your new account is locked with a password. Please give a password. Do not forget this password.
**Passphrase:** [비밀번호 입력]
**Repeat passphrase:** [비밀번호 재입력]
Address: {**1d428f621a1ff7377f0168de89b5c853d7bd0a23**}





* genesis.json의 alloc에 Address 값을 넣어 Balance 값을 지정해 준다.

```json
"alloc": {"72255c3599368bc80c831a8aebffb4988582b5e5": {"balance":"300000000"},
                "1d428f621a1ff7377f0168de89b5c853d7bd0a23": {"balance":"240000000"}
        }
```



* Geth 초기화!
  **λ** geth --datadir .\chaindata\ init .\genesis.json



### JSRE ()

자바스크립트를 실행할 수 있는 콘솔 환경

Geth에서 지원하는 자바스크립트 환경

Interative geth

https://goodplayer.tistory.com/8



* 계정 주소 생성

```go
> personal.newAccount("비밀번호")
"0x881e612296d0d0727bda48d110b25ce44a877432"
```

* Coinbase 확인 및 변경

```go
> eth.coinbase
"0x72255c3599368bc80c831a8aebffb4988582b5e5"
> miner.setEtherbase(eth.accounts[1]);
true
> eth.coinbase
"0x1d428f621a1ff7377f0168de89b5c853d7bd0a23"
> miner.setEtherbase(eth.accounts[0]);
true
> eth.coinbase
"0x72255c3599368bc80c831a8aebffb4988582b5e5"
```

* 계정 잔액 확인

```go
eth.getBalance(eth.accounts[i]);	// i번째 계정주소의 Balance 확인
```



* 블록 생성 개수 확인

```go
> eth.blockNumber;
141
```



* 마이닝 상태 확인

```go
> eth.mining
false
```



* Mining 시작

```go
> miner.start(i);	// Mining에 사용할 CPU(or GPU) 쓰레드 개수
```



* Mining보상 토큰을 Ethereum 계산

```go
> web3.fromWei(eth.getBalance(eth.coinbase),"ether")
705.0000000003
```





* 계정 Transaction Unlock

```go
> personal.unlockAccount(eth.accounts[0])
Unlock account 0x72255c3599368bc80c831a8aebffb4988582b5e5
Passphrase:
true
> personal
{
  listAccounts: ["0x72255c3599368bc80c831a8aebffb4988582b5e5", "0x1d428f621a1ff7377f0168de89b5c853d7bd0a23", "0x881e612296d0d0727bda48d110b25ce44a877432"],  
  listWallets: [{
      accounts: [{...}],
      status: "Unlocked",
     // ....
```



* 송금 Transaction 실행
  (**web3.toWei( 금액, "단위" )** 함수를 통해서 이더리움으로 거래하였다.)

```go
> eth.sendTransaction({from: eth.accounts[0], to:eth.accounts[2], value:web3.toWei(10,"ether")})
INFO [08-22|14:41:37] Submitted transaction                    fullhash=0x54e3c597f780bfb57c7b9b6c10ec671c3c1d918eda8ecfb75ba65e90095afdae recipient=0x881E612296d0d0727BdA48D110B25ce44a877432
"0x54e3c597f780bfb57c7b9b6c10ec671c3c1d918eda8ecfb75ba65e90095afdae"
```



* pendingTransaction 확인

```
> eth.pendingTransactions
[]

```



* 송금 처리를 하기 위해 Mining이 필요하다.

```go
> eth.getBalance(eth.accounts[2])
0
> miner.start(1)
INFO [08-22|14:44:30] Updated mining threads                   threads=1
INFO [08-22|14:44:30] Transaction pool price threshold updated price=18000000000
INnFuOl l[0
8-> 22|14:44:30] Starting mining operation
INFO [08-22|14:44:30] Commit new mining work                   number=212 txs=1 uncles=0 elapsed=1ms
INFO [08-22|14:44:31] Successfully sealed new block            number=212 hash=f73b9a…cdec39
INFO [08-22|14:44:31] 🔗 block reached canonical chain          number=207 hash=2c059c…643e37
INFO [08-22|14:44:31] Commit new mining work                   number=213 txs=0 uncles=0 elapsed=0s
INFO [08-22|14:44:31] 🔨 mined potential block                  number=212 hash=f73b9a…cdec39
> miner.stop()INFO [08-22|14:44:34] Successfully sealed new block            number=213 hash=9005b6…59829f
INFO [08-22|14:44:34] 🔗 block reached canonical chain          number=208 hash=e4a94b…6a3b13
INFO [08-22|14:44:34] Commit new mining work                   number=214 txs=0 uncles=0 elapsed=0s
INFO [08-22|14:44:34] 🔨 mined potential block                  number=213 hash=9005b6…59829f

true
> eth.getBalance(eth.accounts[2])
10000000000000000000
> web3.fromWei(eth.getBalance(eth.accounts[2]),"ether")
10
```



* Block정보 확인
  **eth.getBlock(i)** / i: 블록 번호
  Transaction이 없는 블록임을 확인 (**Line: 20, 42**)

```go
> eth.getBlock(0)
{
  difficulty: 1024,
  extraData: "0x00",
  gasLimit: 8388608,
  gasUsed: 0,
  hash: "0x34deb20e103b7665919665629ac67f78ccf1ad2f7a7ed8592d3f0a277d1ff581",
  logsBloom: "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
  miner: "0x2222222222222222222222222222222222222222",
  mixHash: "0x0000000000000000000000000000000000000000000000000000000000000000",
  nonce: "0x0000000000000033",
  number: 0,
  parentHash: "0x0000000000000000000000000000000000000000000000000000000000000000",
  receiptsRoot: "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
  sha3Uncles: "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
  size: 506,
  stateRoot: "0x91acbc3995238499b1ac0a4c929ec0fbec884f95d358a7c9a4b94566889e3e4f",
  timestamp: 0,
  totalDifficulty: 1024,
  transactions: [],
  transactionsRoot: "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
  uncles: []
}
> eth.getBlock(1)
{
  difficulty: 131072,
  extraData: "0xd983010802846765746887676f312e392e328777696e646f7773",
  gasLimit: 8380417,
  gasUsed: 0,
  hash: "0x00a4b86a387c7f648d5c31b64365715523b7270bad2072c4c80f1e044f6b60cd",
  logsBloom: "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
  miner: "0x72255c3599368bc80c831a8aebffb4988582b5e5",
  mixHash: "0xbae4f5a106e0519ef5afbe94046e5951a08dc790fbbd218de8af1c878d15f968",
  nonce: "0x40ab5458326e881b",
  number: 1,
  parentHash: "0x34deb20e103b7665919665629ac67f78ccf1ad2f7a7ed8592d3f0a277d1ff581",
  receiptsRoot: "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
  sha3Uncles: "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
  size: 537,
  stateRoot: "0x12c1cfa3b1bdf482cb818dd09f8bd4cc95ee405fa5b53c0380e57903599f71dd",
  timestamp: 1566451312,
  totalDifficulty: 132096,
  transactions: [],
  transactionsRoot: "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
  uncles: []
}
```

* Transaction 처리 블록 확인
  (**Line: 20. Transaction 내용**)

```go
> eth.getBlock(214)
{
  difficulty: 135044,
  extraData: "0xd983010802846765746887676f312e392e328777696e646f7773",
  gasLimit: 6806205,
  gasUsed: 42000,
  hash: "0xf7f80ed29847d941bdb658e184641050bd85b885266eb5389a4ff84569ef36dd",
  logsBloom: "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
  miner: "0x1d428f621a1ff7377f0168de89b5c853d7bd0a23",
  mixHash: "0xc1f342f62b8abf90039dde9448074c2d2257510a942870284ee0c0d1af4fb168",
  nonce: "0x04b89dc319f79fe6",
  number: 214,
  parentHash: "0x9005b6e901a2db9ba7f327410e3fe3a262a61d40cc91cb2d3bcd728c1c59829f",
  receiptsRoot: "0x4a834089e507602cac30bf5cdcfa16c70e5d183f6b4dbd1b5a2edfbb26591b30",
  sha3Uncles: "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
  size: 764,
  stateRoot: "0xc19bf26e0001912ff078d87c5bf2ef5c848726e98d667d713bbe5f8a9bb1e820",
  timestamp: 1566453313,
  totalDifficulty: 29277855,
  transactions: ["0x190cd4708184b868e6eaf55ddf474899c874615a3aa61777881e9b4dabf09067", "0x265df4e8e951a55440cf50102daabe82c80e7a9e6da9396b40890415ff3f7301"],
  transactionsRoot: "0x466686b9584d4f7fc1778ebf3b534f854a15282525f67dfd74dec34fa4dab3e2",
  uncles: []
}
```



* Transaction 확인
  **blockNumber**에 Trasaction이 저장된 블록 번호를 확인할 수 있다.


```go
> eth.getTransaction("0x190cd4708184b868e6eaf55ddf474899c874615a3aa61777881e9b4dabf09067")
{
  blockHash: "0xf7f80ed29847d941bdb658e184641050bd85b885266eb5389a4ff84569ef36dd",
  blockNumber: 214,
  from: "0x1d428f621a1ff7377f0168de89b5c853d7bd0a23",
  gas: 90000,
  gasPrice: 18000000000,
  hash: "0x190cd4708184b868e6eaf55ddf474899c874615a3aa61777881e9b4dabf09067",
  input: "0x",
  nonce: 0,
  r: "0x74561a5ff996de70cc6bd055e9b9d7de50011217598e08f10ec68c02b02b64d0",
  s: "0x4952411f682a159e268bfe46107caef77c96cdcc25126a846e53fab25560e67a",
  to: "0x5149c431ae1566d28248b60cb870dd112f811159",
  transactionIndex: 0,
  v: "0x66",
  value: 2000000000000000000
}
```





### 이더리움 클라이언트

* 블록체인 네트워크 노드
* 일반 사용자의 접속을 허용하고 블록체인과 연결 시켜주는 역할

![img](https://steemitimages.com/DQmVTKkYB6JL15YmAmYDEbohFFAyoBgyXTd8HH8tka7EST5/image.png)

https://steemit.com/coinkorea/@etainclub/smart-contract-6-dapp



#### POSTMAN

https://www.getpostman.com/downloads/



* RPC API 실행
  * RPC blockNumber 알아보기
    Post방식, http://localhost:8545, Body - Raw: JSON(application/json) 으로 Send!

```json
{
	"jsonrpc" : "2.0",
	"method" : "eth_blockNumber",
	"id" : 10
}
```



**λ** geth --datadir chaindata --networkid 33 --nodiscover --maxpeers 0 --rpc -rpcaddr "0.0.0.0" --rpcpost 8545 --rpccorsdomain "*" --rpcapi "db,eth,net,web3,admin,devug,miner,shh,txpool,personal" console

- --maxpeers: 접속 수 설정
- 



```bash
λ geth --datadir chaindata --networkid 33 --nodiscover --maxpeers 0 --rpc -rpcaddr "0.0.0.0" --rpcport 8545 --rpccorsdomain "*" --rpcapi "db,eth,net,web3,admin,devug,miner,shh,txpool,personal" console
INFO [08-22|15:53:06] Maximum peer count                       ETH=0 LES=0 total=0
INFO [08-22|15:53:06] Starting peer-to-peer node               instance=Geth/v1.8.2-stable-b8b9f7f4/windows-amd64/go1.9.2
INFO [08-22|15:53:06] Allocated cache and file handles         database=c:\\work_dapp\\geth\\geth182\\chaindata\\geth\\chaindata cache=768 handles=1024
INFO [08-22|15:53:06] Initialised chain configuration          config="{ChainID: 33 Homestead: 0 DAO: <nil> DAOSupport: false EIP150: <nil> EIP155: 0 EIP158: 0 Byzantium: <nil> Constantinople: <nil> Engine: unknown}"
INFO [08-22|15:53:06] Disk storage enabled for ethash caches   dir=c:\\work_dapp\\geth\\geth182\\chaindata\\geth\\ethash count=3
INFO [08-22|15:53:06] Disk storage enabled for ethash DAGs     dir=C:\\Users\\student\\AppData\\Ethash                   count=2
INFO [08-22|15:53:07] Initialising Ethereum protocol           versions="[63 62]" network=33
INFO [08-22|15:53:07] Loaded most recent local header          number=247 hash=499a05…07aa62 td=33648264
INFO [08-22|15:53:07] Loaded most recent local full block      number=247 hash=499a05…07aa62 td=33648264
INFO [08-22|15:53:07] Loaded most recent local fast block      number=247 hash=499a05…07aa62 td=33648264
INFO [08-22|15:53:07] Loaded local transaction journal         transactions=7 dropped=7
INFO [08-22|15:53:07] Regenerated local transaction journal    transactions=0 accounts=0
WARN [08-22|15:53:07] Blockchain not empty, fast sync disabled
INFO [08-22|15:53:07] Starting P2P networking
INFO [08-22|15:53:07] RLPx listener up                         self="enode://6a4a73514fbe22ad4b6d1b4221f8e3cc224bb3a17f171991568ec3b59cffe5ebe42c7985900e8a5910c3f7df9bbcb8b2b30a3596cc4082b2d04ada4ec4fd2e97@[::]:30303?discport=0"
INFO [08-22|15:53:07] IPC endpoint opened                      url=\\\\.\\pipe\\geth.ipc
INFO [08-22|15:53:07] HTTP endpoint opened                     url=http://0.0.0.0:8545   cors=* vhosts=localhost
Welcome to the Geth JavaScript console!

instance: Geth/v1.8.2-stable-b8b9f7f4/windows-amd64/go1.9.2
INFO [08-22|15:53:07] Etherbase automatically configured       address=0x72255C3599368bc80C831a8aEBfFB4988582b5e5
coinbase: 0x72255c3599368bc80c831a8aebffb4988582b5e5
at block: 247 (Thu, 22 Aug 2019 15:30:59 KST)
 datadir: c:\work_dapp\geth\geth182\chaindata
 modules: admin:1.0 debug:1.0 eth:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 txpool:1.0 web3:1.0
>
```



* POSTMAN Send결과
  **result**: Mining된 블록 수

```json
{
    "jsonrpc": "2.0",
    "id": 1011,
    "result": "0xf7"
}
```





##### 디앱(dApp)에 대해서

http://news.kotra.or.kr/user/globalBbs/kotranews/782/globalBbsDataView.do?setIdx=243&dataIdx=175027

