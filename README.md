# 集群聊天软件
支持用户注册、登录、好友管理、群组管理等功能。
1. 使用第三方json库实现消息的序列化和反序列化，[JSON for modern C++](https://github.com/nlohmann/json)，直接包含头文件json.hpp
2. TCP长连接通信协议，使用[muduo网络库](https://github.com/chenshuo/muduo)实现了Reactor模式的多线程服务器
3. 使用MySQL建立用户列表/好友列表/离线消息列表/群组信息列表
4. 使用[nginx](https://github.com/nginx/nginx)的负载均衡模块配置负载均衡器
5. 使用Redis作为中间件，依靠发布-订阅模式来实时建立集群服务器之间的通信。

## MySQL表设计
### User表
![image](https://user-images.githubusercontent.com/68554367/192934045-3fb2d752-722f-4762-b9c8-9a6e4c2ec20f.png)
### Friend表
![image](https://user-images.githubusercontent.com/68554367/192934078-197c8f98-3c26-4d92-b153-e38343ae682b.png)
### ALLGroup表
![image](https://user-images.githubusercontent.com/68554367/192934140-14704009-4b60-46e3-91f2-06280f7820bf.png)
### GroupUser表
![image](https://user-images.githubusercontent.com/68554367/192934174-0da91af7-0086-4cba-84aa-5794f5c0db72.png)
### OffineMessage表
![image](https://user-images.githubusercontent.com/68554367/192934194-e928a6af-ee21-4050-9772-cbb0197a414f.png)

## Nginx负载均衡配置
下载nginx源码，root权限下进行编译
```
./configure --with-stream
./make && make install
```
编译完成后，默认安装在/usr/local/nginx目录
