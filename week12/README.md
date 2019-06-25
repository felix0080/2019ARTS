# Algorithm
1. 给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。
    给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。
    输入："23"
    输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
    ```golang
    func init() {
        a = make([][]rune,10,10)
        for i:=2;i<10;i++{
            switch i {
            case 2:
                a[i]=[]rune{'a','b','c'}
            case 3:
                a[i]=[]rune{'d','e','f'}
            case 4:
                a[i]=[]rune{'g','h','i'}
            case 5:
                a[i]=[]rune{'j','k','l'}
            case 6:
                a[i]=[]rune{'m','n','o'}
            case 7:
                a[i]=[]rune{'p','q','r','s'}
            case 8:
                a[i]=[]rune{'t','u','v'}
            case 9:
                a[i]=[]rune{'w','x','y','z'}
            default:
                panic("invalid number")
            }
        }
    }
    var a [][]rune
    func letterCombinations(digits string) []string {
        if digits == ""{
            return nil
        }
        var tmp [][]rune
        for _,value:=range digits{
            i,err:=strconv.Atoi(string(value))
            if err != nil {
                panic(err)
            }
            tmp = append(tmp,a[i])
        }
        return huisu(0,len(tmp),tmp)
    }
    func huisu(index,len int,as [][]rune) []string {
        if index == len-1 {
            var s []string
            for _,value:=range as[index]{
                s = append(s,string(value))
            }
            return s
        }
        strs := huisu(index+1,len,as)
        var s []string
        for _,value:=range as[index]{
            for _,last:=range strs {
                s = append(s,string(value)+last)
            }
        }
        return s
    }
    ```
# Review
1.  [go并发]( https://www.ardanlabs.com/blog/2018/12/scheduling-in-go-part3.html)

    1. 介绍了，什么时候适合用多核并发来提升性能，什么时候多核并发非但提升不了性能，反而增加运行时长，什么时候单核多协程能提升性能， 什么时候多核多协程也提升不了性能
    2. 介绍了两种类型的并发，IO-Bound,CPU-Bound.以及各自的并发机制，针对每种型也举了例子
    3. 讲的很好

# Tip
1. 使用 litmus 来测试
2. [2进制包的大小分析](https://github.com/knz/go-binsize-viz)
3. [针对2进制的压缩](https://github.com/upx/upx)

# Share
1. 点评V语言
   1. 号称Rust,Go的优势结合体，有小，快，等优点。但当前没有win,不远肯定会有支持，虽然还是最初版本，但可以预见将吸引一部分gopher。
    
   