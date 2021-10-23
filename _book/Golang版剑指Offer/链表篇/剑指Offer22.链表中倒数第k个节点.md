# 剑指Offer22.[链表中倒数第k个节点](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)

## 题目描述：

输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。

例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。这个链表的倒数第 3 个节点是值为 4 的节点。

 

## 示例：

```
给定一个链表: 1->2->3->4->5, 和 k = 2.

返回链表 4->5.
```



## 算法思路：

1. ### 快慢指针法：

   快指针先走k，然后快慢指针一起走，快指针走到终点时，慢指针即为所求。

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func getKthFromEnd(head *ListNode, k int) *ListNode {
    var slow , fast *ListNode = head , head
    for i := 0 ; i < k ;{
        fast = fast.Next
        i ++
    }
    if fast == nil {
        return head
    }
    for fast != nil {
        slow = slow.Next
        fast = fast.Next
    }
    return slow
}
```

![image-20211018161140668](https://cdn.jsdelivr.net/gh/sailaoda/sai_img//img/3/image-20211018161140668.png)

2. ### 数组索引法

```go 
func getKthFromEnd(head *ListNode, k int) *ListNode {
    var res []*ListNode
    for head != nil {
        res = append(res , head)
        head = head.Next
    }
    l := len(res)
    if l >= k {
        return res[l - k]
    }

    return nil
}

```

![image-20211018190424786](https://cdn.jsdelivr.net/gh/sailaoda/sai_img//img/3/image-20211018190424786.png)

以空间换时间。 空间都不大行。



3. ### 遍历递归

```go
func getKthFromEnd(head *ListNode, k int) *ListNode {
    if head == nil {
        return nil
    }
    node ,_ := getKthFromEndre(head,k)
    return node
    
}

func getKthFromEndre(head *ListNode, k int) (*ListNode, int) {
    if head == nil {
        return nil,0 //遍历到最后返回0，开始往上+1判断是否等于k，等于的话直接返回node
    }
    node, res := getKthFromEndre(head.Next, k)
    if res == k {
        return node, res
    }
    res++
    return head, res
}
```

![image-20211018200136155](https://cdn.jsdelivr.net/gh/sailaoda/sai_img//img/3/image-20211018200136155.png)

