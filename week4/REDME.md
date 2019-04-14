# Algorithm

1. 设计一个堆
```golang
type Heap struct {
	Count int
	heap [10]int
}
func (this *Heap)RemoveTop(){
	if this.Count < 1 {
		return
	}
	if this.Count == 1 {
		this.heap[1]=0
		return
	}
	fmt.Println(this.heap)
	this.heap[1] = this.heap[this.Count]
	this.heap[this.Count]=0
	this.heapify()
func (this *Heap)Sort(){
	for this.Count>1{
		fmt.Println(this.Count)
		this.heap[1],this.heap[this.Count]=this.heap[this.Count],this.heap[1]
		this.Count--
		this.heapify()
	}
}
func (this *Heap)heapify()  {
	i:=1
	for true{
		fmt.Println(this.heap)
		left:=i*2
		right:=i*2+1
		if right <= this.Count {
			top:=this.heap[i]
			leftv:=this.heap[left]
			rightv:=this.heap[right]
			if leftv > rightv {
				if leftv > top{
					this.heap[i],this.heap[left]=this.heap[left],this.heap[i]
					i=left
					continue
				}
				break
			}else{
				if rightv > top{
					this.heap[i],this.heap[right]=this.heap[right],this.heap[i]
					i=right
					continue
				}
				break
			}
		}else {
			break
		}

	}
}
func (this *Heap)Insert(num int){
	c:=this.Count+1
	if c > len(this.heap) {
		return
	}
	this.heap[c] = num
	parent:= c / 2
	temp:=c
	for parent >0 && this.heap[parent] < this.heap[temp] {
		this.heap[parent],this.heap[temp]=this.heap[temp],this.heap[parent]
		temp=parent
		parent = parent / 2
	}
	this.Count=c
}
```
# Review
[Handling 1 Million Requests per Minute with Golang](https://medium.com/smsjunk/handling-1-million-requests-per-minute-with-golang-f70ac505fcaa)
 1. 文章介绍了使用golang来开发大规模并发程序
    关键点在于巧妙的结合了worker和分发，还不错
# Tip
### 写一句话
  1. 身体是革命的本钱

# Share
[kubernetes tip](https://towardsdatascience.com/key-kubernetes-concepts-62939f4bc08e)
  1. 可帮助初学者快速的过一遍k8s