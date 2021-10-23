# 剑指Offer24.[反转链表](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/)

## 题目描述：

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

 

## 示例:

```
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```



## 限制：

0 <= 节点个数 <= 5000



## 算法代码：

```go
// 递归
func reverseList(head *ListNode) *ListNode {
    if head == nil || head.Next == nil {
        return head
    }
    var p = reverseList(head.Next)
    head.Next.Next = head
    head.Next = nil
    return p
}
```



## 算法思路：

常规的递归思路。



## 算法优化：

链表节点中有两个元素：

- 值
- 指针

```go
type ListNode struct {
    Val  int
    Next *ListNode
}
```

Next指向下一个节点

![img](https://cdn.jsdelivr.net/gh/sailaoda/sai_img//img/3/1455942-20181108222904421-264942785.png)

那么这道题其实就是把指针指向前一个节点

| 位置调换次数 | pre             | cur           | whole              |
| ------------ | --------------- | ------------- | ------------------ |
| 0            | nil             | 1->2->3->4->5 | 1->2->3->4->5      |
| 1            | 1->nil          | 2->-3>->4->5  | 2->3->4->5->1->nil |
| 2            | 2->1->nil       | 3->4->5       | 3->4->5->2->1->nil |
| 3            | 3->2->1->nil    | 4->5          | 4->5->3->2->1->nil |
| 4            | 4->3->2->1->nil | 5             | 5->4->3->2->1->nil |

可以看出来

- pre是cur的最前面那位（pre = cur）
- cur就是当前位的后面链表元素（cur = cur.Next）
- cur.Next肯定是接pre（cur.Next = pre）



## 优化代码：

```go
//反转链表的实现
func reversrList(head *ListNode) *ListNode {
    cur := head
    var pre *ListNode = nil
    for cur != nil {
        pre, cur, cur.Next = cur, cur.Next, pre //这句话最重要
    }
    return pre
}
```

![算法优化](https://cdn.jsdelivr.net/gh/sailaoda/sai_img//img/3/image-20211018151759382.png)

