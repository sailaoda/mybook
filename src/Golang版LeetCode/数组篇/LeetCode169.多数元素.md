# LeetCode169.[多数元素](https://leetcode-cn.com/problems/majority-element/)

## 题目描述：

给定一个大小为 n 的数组，找到其中的多数元素。多数元素是指在数组中出现次数 大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

##  示例：

示例 1：

```
输入：[3,2,3]
输出：3
```

示例 2：

```
输入：[2,2,1,1,1,2,2]
输出：2
```

## 算法代码：

```go
func majorityElement(nums []int) int {
    major := 0
    count := 0
    for _,num := range nums{
        if count == 0 {
            major = num
        }
        if major == num {
            count ++
        }else{
            count --
        }
    }
    return najor
}
```

## 算法思路：

摩尔投票法：利用相互抵消的概念

排序法： 排序之后的中间值一定为众数

```go
func majorityElement(nums []int) int {
    sort.Ints(nums)
    index := len(nums)
    return nums[len/2]
}
```

