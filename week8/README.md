# Algorithm
1. 给定一个只包含 '(' 和 ')' 的字符串，找出最长的包含有效括号的子串的长度。

    示例 1:

    输入: "(()"
    输出: 2
    解释: 最长有效括号子串为 "()"
    示例 2:

    输入: ")()())"
    输出: 4
    解释: 最长有效括号子串为 "()()" 
    ```golang
    func longestValidParenthesesdp(s string) int {
        var lens = len(s)
        if lens < 1{
            return 0
        }
        ms:=make([]int,lens,lens)
        value:=make([]int,lens+1,lens+1)
        ms[0]=0
        for i:=1;i<lens;i++{
            if s[i] == ')'{
                if s[i-1] == '(' {
                    if i > 1 {
                        ms[i]=ms[i-2]+2
                    }else{
                        ms[i]=2
                    }
                    value[ms[i]]=1
                }else if s[i-1]==')'{
                    if ms[i-1] != 0{
                        left:=i-ms[i-1]-1
                        if left>=0 && s[left] == '(' {
                            leftleft:=0
                            if  left>0{
                                leftleft=ms[left-1]
                            }
                            ms[i]=2+leftleft+ms[i-1]
                            value[ms[i]]=1
                        }
                    }
                }
            }
        }
        for i:=lens;i>=0;i--{
            if value[i]==1 {
                return i
            }
        }
        return 0
    }
    func longestValidParenthesests(s string) int {
        var lens = len(s)
        left:=NewByteStack(lens)
        ms:=make([]int,lens,lens)
        for index,b:=range s{
            if b == '(' {
                left.Push(index)
            }
            if b == ')' {
                leftindex:=left.Pop()
                if leftindex != -1 {
                    ms[leftindex]=1
                    ms[index]=1
                }
            }
        }
        max:=0
        tmp:=0
        for i:=0;i<lens;i++{
            if ms[i]==1{
                tmp ++
            }else{
                if tmp > max {
                    max=tmp
                }
                tmp=0
            }
        }
        if tmp > max {
            max=tmp
        }
        return max
    }
    type Stack interface {
        Push(byte byte) bool
        Len()int
        Pop()byte
    }
    type IStack struct {
        len int
        max int
        data []int
    }
    func NewByteStack(size int) *IStack {
        return &IStack{
            len:0,
            max:size,
            data:make([]int,size,size),
        }
    }

    func (b *IStack)Pop() int{
        if b.len == 0 {
            return -1
        }
        b.len--
        out:=b.data[b.len]
        b.data[b.len]=-1
        return out
    }

    func (b *IStack)Len() int {
        return b.len
    }

    func (b *IStack)Push(byte int)  bool{
        if b.len < b.max {
            b.data[b.len]=byte
            b.len++
            return true
        }
        return false
    }
    ```

# Review

1. [diving-into-golang-channels-e9e610d586e8](https://itnext.io/diving-into-golang-channels-e9e610d586e8)

    读完之后我并不认同作者观点，并已经做出了comment.
    I think the big reason why the first read method is slow is that the first read method has a lock, while the second read method does not have a lock(you just start a thread), and the comparison is not rigorous. In my opinion, the second method cannot solve the problem of multithreaded linear execution in concurrency, but is over-designed.

# Tip

1. 并不是所有的文章都是有意义的，需要泛读之后，要根据自己的所有知识来评判，觉得好就选择精读

# Share

1. 分享一篇有关cuda 编程的书 <<nvidia-cuda-progreammer-guide1.1>>