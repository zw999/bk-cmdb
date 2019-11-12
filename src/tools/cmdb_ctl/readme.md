# cmdb 小工具

### 动态调整日志级别
- 使用方式

  ```
  ./tool_ctl log [flags]
  ```

- 命令行参数
  ```
  --set-default[=false]: set log level to default value
  --set-v="": set log level for V logs
  --addrport="": the ip address and port for the hosts to apply command, separated by comma
  --zk-addr="": the ip address and port for the zookeeper hosts, separated by comma, corresponding environment variable is ZK_ADDR
  ```
- 示例

  - ```
    ./tool_ctl log --set-default --addrport=127.0.0.1:8080 --zk-addr=127.0.0.1:2181
    ```

  - ```
    ./tool_ctl log --set-v=3 --addrport="127.0.0.1:8080" --zk-addr="127.0.0.1:2181"
    ```

### 优雅退出
- 使用方式

  ```
  ./tool_ctl shutdown [flags]
  ```

- 命令行参数
  ```
  --pids="": the processes to be shutdown, separated by comma
  --show-pids[=false]: show cmdb processes pid
  ```
- 示例

  - ```
    ./tool_ctl shutdown --pids=1234
    ```

  - ```
    ./tool_ctl shutdown --show-pids
    ```

### zookeeper操作
- 使用方式

  ```
  ./tool_ctl zk [command]
  ```

- 子命令
  ```
  ls          list children of specified zookeeper node
  get         get value of specified zookeeper node
  del         delete specified zookeeper node
  set         set value of specified zookeeper node
  ```
- 命令行参数
  ```
  --zk-path="": the zookeeper path
  --zk-addr="": the ip address and port for the zookeeper hosts, separated by comma, corresponding environment variable is ZK_ADDR
  --value="": the value to be set（仅用于set命令）
  ```
- 示例

  - ```
    ./tool_ctl zk ls --zk-path=/test --zk-addr=127.0.0.1:2181
    ```

  - ```
    ./tool_ctl zk get --zk-path=/test --zk-addr=127.0.0.1:2181
    ```

  - ```
    ./tool_ctl zk del --zk-path=/test --zk-addr=127.0.0.1:2181
    ```

  - ```
    ./tool_ctl zk set --zk-path=/test --zk-addr=127.0.0.1:2181 --value=test
    ```
    
### 回显服务器
- 使用方式

  ```
  ./tool_ctl echo [flags]
  ```

- 命令行参数
  ```
  --url="": the url for echo server to listen
  ```
- 示例

  - ```
    ./tool_ctl echo --url=127.0.0.1:8080/echo
    ```
### 检查主机快照
- 使用方式

  ```
  ./tool_ctl snapshot [flags]
  ```

- 命令行参数
  ```
  --bizId=2: blueking business id. e.g: 2
  --zk-addr="": the ip address and port for the zookeeper hosts, separated by comma, corresponding environment variable is ZK_ADDR
  ```
- 示例

  - ```
    ./tool_ctl snapshot --bizId=2 --zk-addr=127.0.0.1:2181
    ```

 ### 权限中心资源操作
 - 使用方式
 
   ```
   ./tool_ctl auth [command]
   ```

 - 子命令
   ```
   register    register resource to auth center
   deregister  deregister resource from auth center
   update      update resource in auth center
   check       check if user has the authority to operate resources

 - 命令行参数
   ```
   --app-code="": the app code used for authorize
   --app-secret="": the app secret used for authorize
   --auth-address="": auth center addresses, separated by comma
   --resource="": the resource for authorize
   --supplier-account="0": the supplier id that this user belongs to（仅用于check命令）
   --user-name="": the name of the user（仅用于check命令）
   ```

 - 示例
 
   - ```
     ./tool_ctl auth register --app-code=test --app-secret=test --auth-address=127.0.0.1 --resource=[{"basic":{"type":"test","action":"test"}}]
     ```
   
   - ```
     ./tool_ctl auth deregister --app-code=test --app-secret=test --auth-address=127.0.0.1 --resource=[{"basic":{"type":"test","action":"test"}}]
     ```
 
   - ```
     ./tool_ctl auth update --app-code=test --app-secret=test --auth-address=127.0.0.1 --resource=[{"basic":{"type":"test","action":"test"}}]
     ```
 
   - ```
     ./tool_ctl auth check --app-code=test --app-secret=test --auth-address=127.0.0.1 --resource=[{"basic":{"type":"test","action":"test"}}] --supplier-account=0 --user-name=test
     ```

### 检查拓扑结构
- 使用方式

  ```
  ./tool_ctl topo [flags]
  ```

- 命令行参数
  ```
  --bizId=2: blueking business id. e.g: 2
  --mongo-uri="": the mongodb URI, eg. mongodb://127.0.0.1:27017/cmdb, corresponding environment variable is MONGO_URI
  ```
- 示例

  - ```
    ./tool_ctl topo --bizId=2 --mongo-uri=mongodb://127.0.0.1:27017/cmdb
    ```