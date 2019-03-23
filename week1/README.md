# Algorithm

1. Consider an array of integers a. Let min(a) be its minimal element, and let avg(a) be its mean.Define the center of the array a as array b such that:
    1. b is formed from a by erasing some of its elements.
    2. For each i, |b[i] - avg(a)| < min(a).
    3. b has the maximum number of elements among all the arrays satisfying the above requirements.
    4. Given an array of integers, return its center.

```golang
//Answer
func arrayCenter(a []int)([]int ){
    lens:= len(a)
    if lens==0{
        return a
    }
    min,avg := getMinAndAvg(a,lens)
    for i:=0;i<lens;i++{
        sub:=float64(a[i])-avg
        if sub<0{
            sub=-sub
        }
        if sub>=min{
            a=append(a[:i],a[i+1:]...)
            i--
            lens--
        }
    }
    return a
}
func getMinAndAvg(a []int,lens int)(float64,float64){       
    min:=a[0]
    var avg float64
    var sum float64
    for i:=0;i<lens;i++{
        sum=sum+float64(a[i])
        if a[i]<min{
            min=a[i]
        }
    }
    avg=float64(sum)/float64(lens)
    return float64(min),avg
}

```
2. 设置一个全局变量，A线程的变量值为1，A线程执行前判断变量是不是1，执行完之后把变量修改为2，B线程执行前先判断变量是不是2，不是则不执行B线程，C线程同理
```golang
//Answer 
//鸣谢微信好友出了这道题
func Thread()  {
   var a,b,c,d chan struct{}
   a=make(chan struct{})
   b=make(chan struct{})
   c=make(chan struct{})
   d=make(chan struct{})

   go func() {
      for  {
         <-a
         fmt.Println("A")
         time.Sleep(1*time.Second)
         b<- struct{}{}
      }
   }()
   go func() {
      for  {
         <-b
         fmt.Println("B")
         time.Sleep(1*time.Second)
         c<- struct{}{}
      }
   }()
   go func() {
      for  {
         <-c
         fmt.Println("C")
         time.Sleep(1*time.Second)
         a<- struct{}{}
      }
   }()
   a<- struct{}{}
   <-d
}
```
# Review
https://medium.com/google-cloud/kubernetes-nodeport-vs-loadbalancer-vs-ingress-when-should-i-use-what-922f010849e0

  1. sandeep 说的很明确，在生产环境中，我们要尽量使用ingress为service做负载均衡及公开服务，因为nodeport具有端口数量限制，端口使用不充分，IP不稳定的因素，负载均衡有ip开销限制，kube-proxy需要使用有身份的用户输入kubectl命令，故首推ingress。
  2. 但是我有个自己的看法
    1. ingress是L7的，并且在路由查询上会消耗时间，对QPS要求高的应用可能会延迟10ms以上，
    2. 还有这是多个应用共用的，虽然可以做负载均衡，但service流量过大难免会影响其他的service，多租户可能需要特定的ingress插件支持了
# Tip
  1. 如果发现笔记本空间不足，我们可以购买一个移动硬盘，现在我用的很舒服
  2. 不会的尽量自己解决
# Share
  1. [kubernetes 最佳实践](https://medium.com/google-cloud/kubernetes-best-practices-season-one-11119aee1d10)
  2. [istio-autoscaling](https://medium.com/google-cloud/kubernetes-autoscaling-with-istio-metrics-76442253a45a)