# 集群聊天软件
支持用户注册、登录、好友管理、群组管理等功能。
1. 使用第三方json库实现消息的序列化和反序列化，[JSON for modern C++](https://github.com/nlohmann/json)，直接包含头文件json.hpp
2. TCP长连接通信协议，使用[muduo网络库](https://github.com/chenshuo/muduo)实现了Reactor模式的多线程服务器
3. 使用MySQL建立用户列表/好友列表/离线消息列表/群组信息列表
4. 使用nginx的负载均衡模块配置负载均衡器
5. 使用Redis作为中间件，依靠发布-订阅模式来实时建立集群服务器之间的通信。
