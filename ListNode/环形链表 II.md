## 判断链表是否有环

<br/>

可以使用快慢指针法，分别定义 fast 和 slow 指针，从头结点出发，fast指针每次移动两个节点，slow指针每次移动一个节点，如果 fast 和 slow指针在途中相遇 ，说明这个链表有环。

为什么fast 走两个节点，slow走一个节点，有环的话，一定会在环内相遇呢，而不是永远的错开呢

首先第一点：fast指针一定先进入环中，如果fast指针和slow指针相遇的话，一定是在环中相遇，这是毋庸置疑的。

这是因为fast是走两步，slow是走一步，**其实相对于slow来说，fast是一个节点一个节点的靠近slow的，所以fast一定可以和slow重合。**

<br/>

![](https://tva1.sinaimg.cn/large/008eGmZEly1goo4xglk9yg30fs0b6u0x.gif)

## 如果有环，如何找到这个环的入口

<br/>

假设从头结点到环形入口节点 的节点数为x。 环形入口节点到 fast指针与slow指针相遇节点 节点数为y。 从相遇节点 再到环形入口节点节点数为 z。

![](https://img-blog.csdnimg.cn/20210318162938397.png)

<br/>

那么相遇时： slow指针走过的节点数为: x + y， fast指针走过的节点数：x + y + n (y + z)，n为fast指针在环内走了n圈才遇到slow指针， （y+z）为 一圈内节点的个数A。

因为fast指针是一步走两个节点，slow指针一步走一个节点， 所以 fast指针走过的节点数 = slow指针走过的节点数 * 2：

(x + y) * 2 = x + y + n (y + z)

两边消掉一个（x+y）: x + y = n (y + z)

因为要找环形的入口，那么要求的是x，因为x表示 头结点到 环形入口节点的的距离。

所以要求x ，将x单独放在左面：x = n (y + z) - y ,

再从n(y+z)中提出一个 （y+z）来，整理公式之后为如下公式：x = (n - 1) (y + z) + z 注意这里n一定是大于等于1的，因为 fast指针至少要多走一圈才能相遇slow指针。

这个公式说明什么呢？

先拿n为1的情况来举例，意味着fast指针在环形里转了一圈之后，就遇到了 slow指针了。

当 n为1的时候，公式就化解为 x = z，

**这就意味着，从头结点出发一个指针，从相遇节点 也出发一个指针，这两个指针每次只走一个节点， 那么当这两个指针相遇的时候就是 环形入口的节点。**

![](https://tva1.sinaimg.cn/large/008eGmZEly1goo58gauidg30fw0bi4qr.gif)
```python 
def detectCycle(head: ListNode):
    fast, slow = head, head
    # 这里的条件是取决于快指针及其下一个元素存在
    while fast and fast.next:
        # 定义快慢指针，每次快指针移动两个，慢指针移动一个
        fast = fast.next.next
        slow = slow.next
        # 如果快慢指针相遇，则证明有环
        if slow == fast:
            # 重新定义两个指针，index1为头指针 ，index2 为相遇时的元素
            index1, index2 = head, slow
            # index1 index2 再次相遇的时候就是环的入口
            # 详情见：https://www.programmercarl.com/0142.%E7%8E%AF%E5%BD%A2%E9%93%BE%E8%A1%A8II.html#%E6%80%9D%E8%B7%AF
            while index1 != index2:
                # 每次移动一个
                index1 = index1.next
                index2 = index2.next
            return index1
    # 如果没有环，则返回none
    return None
```
