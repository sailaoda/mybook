# LeetCode15.[三数之和](https://leetcode-cn.com/problems/3sum/)

## 题目描述：

给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有和为 0 且不重复的三元组。

## 注意：

答案中不可以包含重复的三元组。

## 示例： 

示例 1：

```
输入：nums = [-1,0,1,2,-1,-4]
输出：[[-1,-1,2],[-1,0,1]]
```

示例 2：

```
输入：nums = []
输出：[]
```

示例 3：

```
输入：nums = [0]
输出：[]
```

## 提示：

```
0 <= nums.length <= 3000
-105 <= nums[i] <= 105
```

## 算法代码：

```go
func threeSum(nums []int) [][]int {
    n := len(nums)
    sort.Ints(nums)
    //ans := make([][]int, 0)
    ans := [][]int{}

    // 枚举 a
    for first := 0; first < n; first++ {
        // 需要和上一次枚举的数不相同
        if first > 0 && nums[first] == nums[first - 1] {
            continue
        }
        // c 对应的指针初始指向数组的最右端
        third := n - 1
        target := -1 * nums[first]
        // 枚举 b
        for second := first + 1; second < n; second++ {
            // 需要和上一次枚举的数不相同
            if second > first + 1 && nums[second] == nums[second - 1] {
                continue
            }
            // 需要保证 b 的指针在 c 的指针的左侧
            for second < third && nums[second] + nums[third] > target {
                third--
            }
            // 如果指针重合，随着 b 后续的增加
            // 就不会有满足 a+b+c=0 并且 b<c 的 c 了，可以退出循环
            if second == third {
                break
            }
            if nums[second] + nums[third] == target {
                ans = append(ans, []int{nums[first], nums[second], nums[third]})
            }
        }
    }
    return ans
}

```

## 算法思路：

排序加双指针的思想

## 算法改进：

```go
func threeSum(nums []int)[][]int{
	n := len(nums)
    sort.Ints(nums)
    ans := [][]int{}
    for first := 0 ; first < n - 2 ; first ++ {
        n1 := nums[first]
        if n1 > 0 {
            break
        }
        if first > 0 && nums[first] == nums[first - 1] {
            continue
        }
        second , third := first + 1 , n - 1
        for second < third {
            n2 , n3 := nums[second] , nums[third]
            if n1 + n2 + n3 == 0 {
                ans = append(ans , []int {n1 , n2 , n3})
                for second < third && nums[second] == n2 {
                    second ++
                }
                for second < third && nums[third] == n3 {
                    third --
                }
            }else if n1 + n2 + n3 < 0 {
                second ++
            }else {
                third --
            }
        }
    }
    return ans
}
```

