# Tip
### VMware下虚拟机 host 网络模式连接外网的方法
  1. 将宿主机网络共享给host网络
  2. 配置虚拟机的网络ip和host网关一个网段下
  3. 配置虚拟机网关以及nameserver为host网关
  4. 即可实现host模式连接外网
