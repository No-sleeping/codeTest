输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
```python
def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
    # 准备虚拟节点
    dummy = ListNode(None)
    dummy.next = head
    # 定义fast指针和slow指针，初始值为虚拟头结点
    fast, slow = dummy, dummy
    # fast首先走n步
    for _ in range(n):
        fast = fast.next
    # fast和slow同时移动，直到fast指向末尾
    while (fast.next != None) :
        fast = fast.next
        slow = slow.next
    # 删除slow指向的下一个节点
    # fast 走到结尾后，slow的下一个节点为倒数第N个节点
    slow.next = slow.next.next
    return dummy.next
```
