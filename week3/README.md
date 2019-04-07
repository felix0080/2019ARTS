# Algorithm
  1. Find the smallest round number that is not less than a given value.
    Example
    For value = 122, the output should be
    nearestRoundNumber(value) = 130.
  ```golang
  func nearestRoundNumber(value int) int {
    mod:=value % 10
    if mod==0 {
      return value
    }
    return value+10-mod
  }
  ```
  2. When migrating data from a source storage system to a target storage system, the number one focus is avoiding data corruption at all cost. In order to meet these high standards, various rounds of tests are run checking for corrupted blocks as well as successfully migrated lengthy regions.  
  We are going to represent the source storage system and target storage system as sequential arrays sourceArray and destinationArray respectively, where sourceArray[i] represents binary data of the ith source block as an integer, and destinationArray[i] represents binary data of the ith destination block, where the data should be migrated, also as an integer. Given the content of the source and the migrated content of the target, find the length and the starting block of the longest uncorrupted data segment (segment = subsequent blocks).
  If there is no uncorrupted segment, return an array containing 0 and 0 respectively.
  ```golang
  func longestUncorruptedSegment(sourceArray []int, destinationArray []int) []int {
    lenght := len(sourceArray)
    laststart:=0
    start:=0
    lastsum:=0
    sum:=0
    isStop:=false
    for i := 0 ; i < lenght ; i++ {
      if sourceArray[i] == destinationArray[i]{
        if isStop {
          sum = 0
          isStop=!isStop
          start = i
        }
        sum++
      }else {
        if isStop {
          continue
        }else{
          isStop=!isStop
          if sum>lastsum {
            lastsum = sum
            laststart = start
          }
        }
      }

    }
    if sum>lastsum {
      lastsum = sum
      laststart = start
    }
    return []int{
      lastsum,laststart,
    }
  }
  ```
# Review
[Helm package manager](https://medium.com/@gajus/the-missing-ci-cd-kubernetes-component-helm-package-manager-1fe002aac680)
  1. 文章讲述了helm的概念
    1. 为了方便部署，维护，升级有状态应用而生的包管理工具
    2. helm，charts,release 的概念
    3. helm 的组成 是由helm客户端和helm tiller server组成的
  2. 介绍了安装方法
  3. 从hello world开始介绍了helm的用法
    1. 介绍了一个chart 必须包含有 Chart.yaml,且其中必须包含至少 name,version两个属性
    2. 介绍一个chart必须定义一组模板用于生成kubernetes manifests
    3. 介绍了release的常用方法
      1. install 生成一个release
      2. ls 列出已部署的release
      3. status 查看release的状态
      4. delete 删除
      5. rollback 回复之前的版本
  4. 介绍了模板的使用方法
    1. 使用values.yaml 文件来定义全局变量，通过.Values来访问对象 比如{{ .Values.image.repository }}
    2. 可使用带参数的命令覆盖 values
  5. 介绍了预定义的value
  6. 介绍了 _helpers.tpl 的用法以及场景
  7. 最后介绍了如何避免有些文件不更新的解决方法
# Tip
### VMware下虚拟机 下创建新分区方法
  1. 先在VMware下拓展磁盘
  2. 启动虚拟机后 fdisk->n->3>w->reboot
### VMware下虚拟机 添加新磁盘方法
  1. 先在VMware下创建一块新磁盘
  2. 启动虚拟机后 fdisk->n->1>w->reboot

# Share
1. [subcharts-and-global-values](https://github.com/helm/helm/blob/master/docs/chart_template_guide/subcharts_and_globals.md#subcharts-and-global-values)