# Algorithm
1. 给定 n 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。
```golang
func trap(height []int) int {
	topindex:=findTop(height)
	ret:=0
	l:=len(topindex)
	if l == 0{
		return 0
	}else if l == 1 {
		top:=0
		for i:=0;i<=topindex[0];i++{
			if height[top]<=height[i] {
				if i-top <= 1 {
					top=i
					continue
				}
				ti:=0
				for j := top; j<i;j++  {
					ti+=height[j]
				}
				ti+=height[top]
				ret+=height[top]*(i-top+1)-ti
				top=i
			}
		}
		top=len(height)-1
		for i:=top;i>=topindex[0];i--{
			if height[top]<=height[i] {
				if top-i <= 1 {
					top=i
					continue
				}
				ti:=0
				for j := top; j>i;j--  {
					ti+=height[j]
				}
				ti+=height[top]
				ret+=height[top]*(top-i+1)-ti
				top=i
			}
		}
		return ret
	}else if l > 1{
		top:=0
		for i:=0;i<=topindex[0];i++{
			if height[top]<=height[i] {
				if i-top <= 1 {
					top=i
					continue
				}
				ti:=0
				for j := top; j<i;j++  {
					ti+=height[j]
				}
				ti+=height[top]
				ret+=height[top]*(i-top+1)-ti
				top=i
			}
		}
		ti:=0
		f1:=topindex[0]
		f2:=topindex[1]
		for j := f1; j<f2;j++{
			ti+=height[j]
		}
		ti+=height[f1]
		ret+=height[f1]*(f2-f1+1)-ti
		top=len(height)-1
		for i:=top;i>=topindex[1];i--{
			if height[top]<=height[i] {
				if top-i <= 1 {
					top=i
					continue
				}
				ti:=0
				for j := top; j>i;j--  {
					ti+=height[j]
				}
				ti+=height[top]
				ret+=height[top]*(top-i+1)-ti
				top=i
			}
		}

	}
	return ret
}
func findTop(height []int)[]int{
	if len(height)==0 {
		return nil
	}
	topindex:=[]int{0}
	top := 0
	for index,value:=range height{
		if value > top {
			top = value
			topindex=[]int{index}
		}else if top == value {
			if len(topindex)==1 {
				topindex=append(topindex,index)
			}else{
				topindex[1]=index
			}

		}
	}
	return topindex
}
```
# Review
[Golang’s Real-time GC in Theory and Practice](https://making.pusher.com/golangs-real-time-gc-in-theory-and-practice/?spm=a2c4e.11153940.blogcont573819.32.b9e922bd8nwhPY)
 1. 文章介绍了使用白灰黑来标记指针
    1. root引用为主引用将不会移除，类似于全局变量或者层级较高的变量
		2. 期初都是在白集合中，后续主指针内部指向的地址均标记于灰集合
		3. GC开始扫描之前将主引用移到灰中，扫描第一个时，将主引用移到黑色集合
		4. 不断减少灰色集合的数量，将黑色引用指向的灰色集合且没有指向其他引用向黑色集合移动
		5. 最后灰色集合会变空，此时白色集合可丢弃，在下一轮到来的时候移除白色集群中引用
		6. 调换黑白集群
# Tip
### 写一句话
  1. Devops 是将开发，运维，测试的三国鼎立局面混合为秦始皇一统天下的局面
	那是什么将三个不相干的东西驱动起来成为一个可以自运转的系统，是以CI/CD为主要驱动，以版本控制自动化构建测试为基本工具，以平台管理为环境，为三个基本齿轮，我们只需要开发人员旋转CI/CD这个齿轮，将带动其他齿轮联动，整个集成环境就开始运转形成了非常敏捷的Devops工作流
	学会使用devops是非常重要的

# Share
[GC is bad but you shouldn’t feel bad](https://syslog.ravelin.com/gc-is-bad-and-you-should-feel-bad-e9bdd9324f0)
