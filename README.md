# test_lan
UE4 测试局域网游戏

### 参考链接
http://www.jianshu.com/p/b4247a35cb61

### 项目环境
UE4.15
测试通过。

### 创建局域网游戏
1、在配置文件{Project}/Config/DefaultEngine.ini中添加配置
``` bash
[OnlineSubsystem]
DefaultPlatformService=Null
```
否则，就会报错：
``` bash
ScriptCore:Warning: Script Msg: CreateSession - Invalid or uninitialized OnlineSubsystem
```
<br>
<br>

2、创建局域网游戏：
在Blueprint中执行CreateSession，OpenLevel即可，参见Blueprint'LobbyGame'中的CreateGame函数

3、加入局域玩个游戏：
在Blueprint中执行FindSessions，JoinSession即可，参见Blueprint'LobbyGame'中的JoinGame函数

### RPC注意
测试代码在Blueprint'ThirdPersonCharacter'中。
架设有两台机器A、B、C，A创建了主机，B、C加入了A创建的游戏。那么：
1、有个同步变量ShowRepCube，如果A执行了ShowRepCube=true，那么B、C会收到A.ShowRepCube为true的效果；但是如果B执行了ShowRepCube=true，那么A、C不会收到B.ShowRepCube为true的效果。
原因在于，A是主机，是Server，改变变量后，会同步给所有客户端。
2、有个同步变量ShowRepSphere，如果B执行同步函数SeverShowRepSphere，那么A、C将受到B.ShowRepSphere为true的效果。



