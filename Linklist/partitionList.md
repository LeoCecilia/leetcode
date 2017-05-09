## 题目
Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

For example,
Given 1->4->3->2->5->2 and x = 3,
return 1->2->2->4->3->5.

## 题目解析
该题是给定一个链表和一个数值，链表中小于该数值的node放在链表左边，反之，放在链表右边

## 思路分析
遍历链表，遇到小于该数值的元素挂在lessHead上，反之则该在greaterHead上，要注意的是不能写`node = node.next`这行代码，因为比较完之后，`less.next = null`;此时`node.next = null`，故因现将其储存起来

## 代码实现
``` javascript
var partition = function(head, x) {
    var lessHead = new ListNode(0),  
        greaterHead = new ListNode(0),
        node = head,
        less = lessHead,
        greater = greaterHead;  
        while (node != null) {  
            //因为less.next = null,故后面node.next亦会等于空，故要事先获得node.next的值
            var next = node.next;  
            if (node.val < x) {  
                less.next = node;  
                less = less.next;  
                less.next = null;  
            } else {  
                greater.next = node;  
                greater = greater.next;  
                greater.next = null;  
            }  
            node = next;  
        }  
        less.next = greaterHead.next;  
        return lessHead.next;  

};
```
