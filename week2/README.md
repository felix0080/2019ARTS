# Algorithm
  1. In schools in the country known as Codelandia, a special five-point grading scale is used.Each grade is a English letter from 'A' to 'E' with a value from 5 to 1 respectively.
  Grade	Value
  A	5
  B	4
  C	3
  D	2
  E	1
  A student is considered to have passed the class if the average value of their grades is greater than or equal to the passing mark.Given the passing mark and a student's grades, find out if they have successfully passed the class or not.

```golang
//Answer
var bs =[]byte{'E','D','C','B','A'}
func passingMark(passMark float32, grades string) bool {
	gradessum:=0
	for _,value := range grades {
		gradessum=gradessum+6-int(rune(value)-rune(64))
	}
	avg:=float32(gradessum)/float32(len(grades))
	return avg>=passMark
}
```
  2. Given an integer n, return the largest number that contains exactly n digits.
```golang
//Answer
func largestNumber(n int) int {
	sum:=1
	for i := 0; i < n; i++ {
		sum=sum*10
	}
	return sum-1
}
```
  3. You are given a two-digit integer n. Return the sum of its digits.
```golang
//Answer
func addTwoDigits(n int) int {
	return n%10 + n/10
}
```
  4. n children have got m pieces of candy. They want to eat as much candy as they can, but each child must eat exactly the same amount of candy as any other child. Determine how many pieces of candy will be eaten by all the children together. Individual pieces of candy cannot be split.
```golang
//Answer
func candies(n int, m int) int {
    return m-m%n
}
```
# Review
  [kubernetes-flat-nat-less-networking](https://medium.com/devopslinks/kubernetes-flat-nat-less-networking-4c12dc4ca78a)
  1. 文章讲述了kubernetes实现无nat扁平化的pod-pod,pod-node,node-pod通信实现的L3实现方式，是通过brige ，和 CNI,veth-pair,使得container->birge->nodes net dev->other node,言简意赅
  2. 文章也提到了这种方式并不是最佳实践，需要SDN,和结合lstio服务来实现，之后文章会继续叙述相关内容
  3. 总的来说还不错，不过讲的不深入
# Tip
### VMware下虚拟机 host 网络模式连接外网的方法
  1. 将宿主机网络共享给host网络
  2. 配置虚拟机的网络ip和host网关一个网段下
  3. 配置虚拟机网关以及nameserver为host网关
  4. 即可实现host模式连接外网
### 对docker设置代理
  1. 假设已经有代理服务器，docker已经安装
  2. 创建docker服务插件目录 /etc/systemd/system/docker.service.d
  3. 在目录中加 http-proxy.conf
  4. 编辑内容
  ```golang
  [Service]
  Environment="HTTP_PROXY="
  ```
  5. 重新加载 systemctl daemon-reload
  6. 重启docker 
### 永久关闭swap
  1. vi /etc/fstab
  2. 注释掉swap
  3. 重启
