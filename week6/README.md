# Algorithm
1. 给定一个字符串 (s) 和一个字符模式 (p) ，实现一个支持 '?' 和 '*' 的通配符匹配。
    '?' 可以匹配任何单个字符。
    '*' 可以匹配任意字符串（包括空字符串）。
    两个字符串完全匹配才算匹配成功。
    说明:
    s 可能为空，且只包含从 a-z 的小写字母。
    p 可能为空，且只包含从 a-z 的小写字母，以及字符 ? 和 *。
    ```golang
    func isMatch(s,p string)bool{
        slen:=len(s)
        plen:=len(p)
        line:=make([][]bool,plen+1,plen+1)
        for i:=0;i<len(line);i++{
            line[i]=make([]bool,slen+1,slen+1)
        }
        line[0][0] = true
        for j:=1;j<=plen;j++{
            if p[j-1] == '*' {
                line[j][0]=line[j-1][0]
                for i := 1 ; i <= slen ; i++ {
                    line[j][i]=line[j-1][i]||line[j][i-1]
                }
            }else if p[j-1] == '?' {
                line[j][0]=false
                for i := 1 ; i <= slen ; i++ {
                    line[j][i]=line[j-1][i-1]
                }
            }else {
                line[j][0]=false
                for i := 1 ; i <= slen ; i++ {
                    line[j][i]=line[j-1][i-1]&& (p[j-1]==s[i-1])
                }
            }
        }
        return line[plen][slen]
    }

    ```
# Review
[The Product Managers’ Guide to Continuous Delivery and DevOps](https://www.mindtheproduct.com/2016/02/what-the-hell-are-ci-cd-and-devops-a-cheatsheet-for-the-rest-of-us/)
1. 本文讲述了使用 devops 持续集成和持续发布场景以及简单的介绍

# Tip
1. 使用HttpDNS 替代UDP dns，绕过本地dns服务器，防止解析不准确（大多使用于移动应用）

# Share
1. [choose kong rather than nginx](https://medium.com/arvind-internet/open-sourcing-tcp-plugin-for-kong-d89e9fb270c3)
    选择kong 来做nginx集群管理，直接调用kong的接口
2. [conf manager for nginx cluster](https://github.com/felix0080/subnginx)
    正在开发，还未完成（直接使用nginx集群而不是kong,这个需求促使我写此应用，替代ansible）