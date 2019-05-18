# Algorithm
1. 给定一个非空字符串 s 和一个包含非空单词列表的字典 wordDict，判定 s 是否可以被空格拆分为      一个或多个在字典中出现的单词。

    说明：

    拆分时可以重复使用字典中的单词。
    你可以假设字典中没有重复的单词。
    示例 1：

    输入: s = "leetcode", wordDict = ["leet", "code"]
    输出: true
    解释: 返回 true 因为 "leetcode" 可以被拆分成 "leet code"。
    示例 2：

    输入: s = "applepenapple", wordDict = ["apple", "pen"]
    输出: true
    解释: 返回 true 因为 "applepenapple" 可以被拆分成 "apple pen apple"。
        注意你可以重复使用字典中的单词。
    示例 3：

    输入: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
    输出: false
    ```golang
    
    func isExist(str string,wordDict []string) bool {
        for i:=0;i<len(wordDict);i++{
            if str == wordDict[i] {
                return true
            }
        }
        return false
    }
    func wordBreak(s string, wordDict []string) bool {
        lens:=len(s)+1
        barr:=make([]bool,lens)
        barr[0]=true
        for i := 1; i < lens; i++ {
            for j := 0; j < i; j++ {
                if barr[j]&&isExist(s[j:i],wordDict){
                    barr[i]=true
                    break
                }
            }
        }
        return barr[lens-1]
    }
    ```

# Review