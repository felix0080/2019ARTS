# Algorithm

1. Consider an array of integers a. Let min(a) be its minimal element, and let avg(a) be its mean.Define the center of the array a as array b such that:
    1. b is formed from a by erasing some of its elements.
    2. For each i, |b[i] - avg(a)| < min(a).
    3. b has the maximum number of elements among all the arrays satisfying the above requirements.
    4. Given an array of integers, return its center.

```golang
//Answer

func arrayCenter(a []int)([]int ){
    lens:= len(a)
    if lens==0{
        return a
    }
    min,avg := getMinAndAvg(a,lens)
    for i:=0;i<lens;i++{
        sub:=float64(a[i])-avg
        if sub<0{
            sub=-sub
        }
        if sub>=min{
            a=append(a[:i],a[i+1:]...)
            i--
            lens--
        }
    }
    return a
}
func getMinAndAvg(a []int,lens int)(float64,float64){       
    min:=a[0]
    var avg float64
    var sum float64
    for i:=0;i<lens;i++{
        sum=sum+float64(a[i])
        if a[i]<min{
            min=a[i]
        }
    }
    avg=float64(sum)/float64(lens)
    return float64(min),avg
}

```