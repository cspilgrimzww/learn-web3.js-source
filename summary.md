# Web3.js 源码阅读
### 初始化:
```js
var Web3 = require("web3");
var web3 = new Web3(new Web3.providers.HttpProvider("http://localhost:8545"))
web3.getBlock('latest');//get latest block
```
初始化了以下内容
#### 1.  _requestManager
即初始化参数中的HttpProvider("http://localhost:8081")，HttpProvider是web3提供的用于向json_rpc提供者（通常为某个geth节点）发送请求的Http请求对象，不指定参数，则默认向localhost:8545发送
#### 2. eth
Eth是Web用以管理以Eth_为前缀的接口的对象。
#### 3. db
DB()实例，管理以db_为前缀的json-rpc接口的对象。
#### 4. ssh
Shh()实例，管理以shh_为前缀的json-rpc接口的对象。
#### 5. net
Net()实例，管理以net_为前缀的json-rpc接口的对象
#### 6. personal
personal（）实例，用于管理以personal_为前缀的json-rpc接口的对象，PS：ethereum官方文档中未对该类接口进行说明，但web3可以调用到，说明ethereum其实是实现了该部分接口的，主要包括
- personal_newAccount 创建账户
- personal_unlockAccount解锁账户
- personal_signAndSendTransaction签名并发送交易
-  personal_lockAccount 锁住账户
-  personal_listAccount 列出所有账户
#### 7. settings
Settings()对象，保存了defaultBlock和defaultAccount，默认为'latest'和'undefined'，目前看来并没有什么卵用
#### 8. version
wev3当前版本号
#### 9. providers
包含了HttpProvider和IpcProvider两个请求控制器，初始化时提供的HttpProvider参数亦即源于此
#### 10. _extend
(占座)
### Property与Method
Property与Method是web3定义的两个类，
Web3中所有的调用由一个Property或Method来控制，使用上，propert调用不加括弧“（）”，如web3.syncing，syncing就是一个Property实例，Method的调用后跟括弧和参数，如`web3.getBlock()`,`web3.getTransactionByHash()`。
