# Algorithm
1. 假设你正在爬楼梯。需要 n 阶你才能到达楼顶。
   每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？
    注意：给定 n 是一个正整数。
    示例 1：
    输入： 2
    输出： 2
    解释： 有两种方法可以爬到楼顶。
    1.  1 阶 + 1 阶
    2.  2 阶
    示例 2：
    输入： 3
    输出： 3
    解释： 有三种方法可以爬到楼顶。
    1.  1 阶 + 1 阶 + 1 阶
    2.  1 阶 + 2 阶
    3.  2 阶 + 1 阶
    ```golang
    func main() {
        t1:=time.Now()
        fmt.Println(climbStairs(40))
        t2:=time.Now()
        fmt.Println(climbStairsdp(40))
        t3:=time.Now()
        fmt.Println(t2.Sub(t1)) 1.5s
        fmt.Println(t3.Sub(t2)) 0s
    }
    func climbStairs(n int) int {
        return clib(0,n)
    }
    func climbStairsdp(n int) int {
        intn:=make([]int , n+1,n+1)
        intn[1]=1
        intn[2]=2
        for i:=3;i<len(intn);i++{
            intn[i]=intn[i-1]+intn[i-2]
        }
        return intn[n]
    }
    func clib(i,n int) int {
        if i > n {
            return 0
        }
        if i == n {
            return 1
        }
        return clib(i+1,n)+clib(i+2,n)
    }
    ```
# Review
[gpu-share](https://github.com/AliyunContainerService/gpushare-scheduler-extender/blob/master/docs/designs/designs.md)
1. 本文介绍了GPU虚拟化的实现方式（隔离性不好）

# Tip
1. 干净的框架就是应用层抽象架构，一个好的架构可以很好的拓展，开发[分享一篇go框架有关文章](https://hackernoon.com/golang-clean-archithecture-efd6d7c43047)

# Share
1. [分享一篇go框架有关文章](https://hackernoon.com/golang-clean-archithecture-efd6d7c43047)