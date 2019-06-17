# Algorithm
1. 一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

    机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

    问总共有多少条不同的路径？
    例如，上图是一个7 x 3 的网格。有多少可能的路径？

    说明：m 和 n 的值均不超过 100。

    示例 1:

    输入: m = 3, n = 2
    输出: 3
    解释:
    从左上角开始，总共有 3 条路径可以到达右下角。
    1. 向右 -> 向右 -> 向下
    2. 向右 -> 向下 -> 向右
    3. 向下 -> 向右 -> 向右
    示例 2:

    输入: m = 7, n = 3
    输出: 28
    ```golang
        func uniquePaths(m int, n int) int {
        arr:=make([][]int,m,m)
        for i := 0 ; i < m ; i++  {
            arr[i]=make([]int,n,n)
        }
        for i := 0 ; i < m ; i++{
            if i == 0 {
                for j := 0; j < n; j++ {
                    arr[0][j]=1
                }
                continue
            }
            arr[i][0] = 1
            for j := 1; j < n; j++ {
                arr[i][j]=arr[i-1][j]+arr[i][j-1]
            }
        }
        return arr[m-1][n-1]
    }
    ```
2. 反转一个单链表。

    示例:

    输入: 1->2->3->4->5->NULL
    输出: 5->4->3->2->1->NULL
    进阶:
    你可以迭代或递归地反转链表。你能否用两种方法解决这道题？
    ```golang
        func reverseList(head *ListNode) *ListNode {
            var left,right *ListNode
            if head ==nil{
                return nil
            }
            for {
                right=head.Next
                head.Next=left
                if right == nil {
                    return head
                }
                left=head
                head=right
                right=head.Next
            }
        }
        func reverseList1(head *ListNode) *ListNode {
            if head==nil {
                return nil
            }
            next:=head.Next
            head.Next=nil
            if next == nil{
                return head
            }
            list:=reverseList1(next)
            next.Next=head
            return list
        }
    ```

# Review

  1. [go调度器](https://povilasv.me/go-scheduler/)
  本文简单介绍了GO调度器的机制
  ![协程调度周期](https://povilasv.me/wp-content/uploads/2017/04/go-sched-Page-1-768x495.png)
  详细介绍了当前M执行完后的窃取机制
    
  2. [netpoller，网路和系统调用调度行为的区别](https://morsmachine.dk/netpoller)
  3. 使用go tool trace 分析调度行为 [go tool trace](https://www.ardanlabs.com/blog/2015/02/scheduler-tracing-in-go.html)
  讲的不错，值得观赏。

# Tip

   1. 遇到网路性能问题，抓包分析

# Share

   1. [go调度器](https://povilasv.me/go-scheduler/)
   2. [netpoller，网路和系统调用调度行为的区别](https://morsmachine.dk/netpoller)
   3. [go tool trace](https://www.ardanlabs.com/blog/2015/02/scheduler-tracing-in-go.html)
  