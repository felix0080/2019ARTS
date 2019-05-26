# Algorithm
1. 给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。
	示例:
	输入: [-2,1,-3,4,-1,2,1,-5,4],
	输出: 6
	解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
	进阶:
	如果你已经实现复杂度为 O(n) 的解法，尝试使用更为精妙的分治法求解。
    ```golang
    
    func maxSubArraydpdp(nums []int) int {
	num:=len(nums)
	ret:=nums[0]
	sum:=ret
	for i:= 1;i<num;i++{
		nextsum:=sum+nums[i]
		if nums[i] < nextsum {
			sum=nextsum
		}else{
			sum=nums[i]
		}
		if sum > ret {
			ret=sum
		}
	}
	return ret
}
    ```

# Review
1. [locks-versus-channels-concurrent-go](https://opensource.com/article/18/7/locks-versus-channels-concurrent-go)
	介绍了使用memory channel 分别有什么优势和劣势
# Tip
1. [Huawei and google](https://onezero.medium.com/the-huawei-disaster-reveals-googles-iron-grip-on-android-b1ccee34504d)
    科技生产力的重要性

# Share
1. [locks-versus-channels-concurrent-go](https://opensource.com/article/18/7/locks-versus-channels-concurrent-go)
2. [Huawei and google](https://onezero.medium.com/the-huawei-disaster-reveals-googles-iron-grip-on-android-b1ccee34504d)