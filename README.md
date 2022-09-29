# 集群聊天软件
支持用户注册、登录、好友管理、群组管理等功能。
1. 使用第三方json库实现消息的序列化和反序列化，[JSON for modern C++](https://github.com/nlohmann/json)，直接包含头文件json.hpp
2. TCP长连接通信协议，使用[muduo网络库](https://github.com/chenshuo/muduo)实现了Reactor模式的多线程服务器
3. 使用MySQL建立用户列表/好友列表/离线消息列表/群组信息列表
4. 使用[nginx](http://nginx.org/en/download.html)的负载均衡模块配置负载均衡器
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
nginx安装需要配置环境：
```
sudo apt-get install libpcre3 libpcre3-dev
sudo apt-get install zlib1g-dev
sudo apt-get install openssl libssl-dev
```
[下载nginx源码](http://nginx.org/en/download.html)，root权限下进行编译
```
./configure --with-stream
./make && make install
```
编译完成后，默认安装在/usr/local/nginx目录
启动nginx，并配置负载均衡模块
```
cd sbin
sudo ./nginx
cd conf
sudo vim nginx.conf
```
![image](https://user-images.githubusercontent.com/68554367/192937685-b617e0be-8441-401c-a69e-ac6b84bc96eb.png)
[nginx负载均衡策略](https://www.w3schools.cn/nginx/nginx_upstream_hash.asp#:~:text=%E8%BD%AE%E8%AF%A2%EF%BC%88Round%20Robin%EF%BC%89%E7%AD%96%E7%95%A5%E6%98%AF,Nginx%20%E9%85%8D%E7%BD%AE%E4%B8%AD%E9%BB%98%E8%AE%A4%E7%9A%84%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%E7%AD%96%E7%95%A5%EF%BC%8C%E8%AF%A5%E7%AD%96%E7%95%A5%E5%B0%86%E5%AE%A2%E6%88%B7%E7%AB%AF%E7%9A%84%E8%AF%B7%E6%B1%82%E4%BE%9D%E6%AC%A1%E5%88%86%E9%85%8D%E7%BB%99%E5%90%8E%E7%AB%AF%E7%9A%84%E6%9C%8D%E5%8A%A1%E5%99%A8%E8%8A%82%E7%82%B9%EF%BC%8C%E5%AF%B9%E5%90%8E%E7%AB%AF%E9%9B%86%E7%BE%A4%E4%B8%AD%E7%9A%84%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%AE%9E%E7%8E%B0%E8%BD%AE%E6%B5%81%E5%88%86%E9%85%8D%E3%80%82)
配置完成，重启
```
./nginx -s reload
```

