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
2. 你将会获得一系列视频片段，这些片段来自于一项持续时长为 T 秒的体育赛事。这些片段可能有所重叠，也可能长度不一。
    视频片段 clips[i] 都用区间进行表示：开始于 clips[i][0] 并于 clips[i][1] 结束。我们甚至可以对这些片段自由地再剪辑，例如片段 [0, 7] 可以剪切成 [0, 1] + [1, 3] + [3, 7] 三部分。

    我们需要将这些片段进行再剪辑，并将剪辑后的内容拼接成覆盖整个运动过程的片段（[0, T]）。返回所需片段的最小数目，如果无法完成该任务，则返回 -1 。

    

    示例 1：

        输入：clips = [[0,2],[4,6],[8,10],[1,9],[1,5],[5,9]], T = 10
        输出：3
        解释：
        我们选中 [0,2], [8,10], [1,9] 这三个片段。
        然后，按下面的方案重制比赛片段：
        将 [1,9] 再剪辑为 [1,2] + [2,8] + [8,9] 。
        现在我们手上有 [0,2] + [2,8] + [8,10]，而这些涵盖了整场比赛 [0, 10]。
        示例 2：

        输入：clips = [[0,1],[1,2]], T = 5
        输出：-1
        解释：
        我们无法只用 [0,1] 和 [0,2] 覆盖 [0,5] 的整个过程。
        示例 3：

        输入：clips = [[0,1],[6,8],[0,2],[5,6],[0,4],[0,3],[6,7],[1,3],[4,7],[1,4],[2,5],[2,6],[3,4],[4,5],[5,7],[6,9]], T = 9
        输出：3
        解释： 
        我们选取片段 [0,4], [4,7] 和 [6,9] 。
        示例 4：

        输入：clips = [[0,4],[2,8]], T = 5
        输出：2
        解释：
        注意，你可能录制超过比赛结束时间的视频。
# Review

1. [w-b](https://github.com/golang/proposal/blob/master/design/17503-eliminate-rescan.md)

  读至Other considerations之前，总体讲述为何要混合垃圾回收，因为要减少re-scan的时间，也就是STW的时间，也讲到了混合垃圾回收的变体和实现原理
  大概就是让堆栈直接变黑，那当然不用再去扫描了，这样就缩短了白对象的来源，且不用re-scan了，不过也是会有少量的STW，但是是可以容忍的。基本上就是一种折中。对性能的折中。貌似文章中提到了并发的混合，那篇文章下周再看。


# Tip

1. 使用go mod 规范化版本管理。且突然感觉世界很清爽无比。


# Share

1. (go mod)[https://github.com/golang/go/wiki/Modules]