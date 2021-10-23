# 剑指Offer30.[包含min函数的栈](https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/)

## 题目描述：

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

 

## 示例:

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```



## 提示：

各函数的调用总次数不超过 20000 次



## 算法代码：

```go
type MinStack struct {
    stack []int
    minstack []int

}


/** initialize your data structure here. */
func Constructor() MinStack {
    return MinStack{
        stack: []int{},
        minstack: []int{math.MaxInt64},
    }
}


func (this *MinStack) Push(x int)  {
    this.stack = append(this.stack , x)
    this.minstack = append(this.minstack , min(this.minstack[len(this.minstack) - 1] , x))
}


func (this *MinStack) Pop()  {
    
    this.minstack = this.minstack[:len(this.minstack) - 1]
    
    this.stack = this.stack[:len(this.stack) - 1]
}


func (this *MinStack) Top() int {
    return this.stack[len(this.stack) - 1]
}


func (this *MinStack) Min() int {
    return this.minstack[len(this.minstack) - 1]
}

func min(x int , y int )  int {
    if x >= y {
        return y
    }else {
        return x
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Push(x);
 * obj.Pop();
 * param_3 := obj.Top();
 * param_4 := obj.Min();
 */

```



## 算法思路：

利用一个辅助栈来存放较小值，在辅助栈的栈顶总是为所有元素的最小值。



## 注意：

不能直接返回`return MinStack{}`

```go
func Constructor() MinStack {
    return MinStack{
        stack: []int{},
        minstack: []int{math.MaxInt64},
    }
}
```

当测试用例如下时：

```go
["MinStack","push","push","push","top","pop","min","pop","min","pop","push","top","min","push","top","min","pop","min"]
[[],[2147483646],[2147483646],[2147483647],[],[],[],[],[],[],[2147483647],[],[],[-2147483648],[],[],[],[]]
```

直接返回`return MinStack{}`会发生错误。
