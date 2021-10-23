# 剑指Offer06.[从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

## 题目描述：

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

 

## 示例 ：

```
输入：head = [1,3,2]
输出：[2,3,1]
```



## 限制：

`0 <= 链表长度 <= 10000`



## 算法代码：

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */

//直接递归反转
func reversePrint(head *ListNode) []int {
    if head == nil {return nil}
    return append(reversePrint(head.Next) , head.Val)
}
```

```go
func reversePrint(head *ListNode) []int {
    // 1.遍历链表时直接Val添加到数组头部:时间复杂度O(N) | 空间复杂度O(1)
    ans := []int{}
    for head != nil {
        ans = append([]int{head.Val}, ans...)
        head = head.Next
    }
    return ans
}
```



## 算法思路：

1. 递归法
2. 辅助栈法
3. 直接顺序获取值放到数组，再反转结果



## 算法改进：（数组索引）

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reversePrint(head *ListNode) []int {
    if head == nil {
        return nil
    }

    res := []int{}
    for head != nil {
        res = append(res, head.Val)
        head = head.Next
    }

    for i, j := 0, len(res)-1; i < j; {
        res[i], res[j] = res[j], res[i]
        i++
        j--
    }

    return res
}
```

![算法优化](https://cdn.jsdelivr.net/gh/sailaoda/sai_img//img/3/image-20211018151657921.png)



