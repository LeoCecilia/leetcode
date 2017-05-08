## 题目
Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

For example,
Given `1->2->3->3->4->4->5`, return `1->2->5`.
Given `1->1->1->2->3`, return `2->3`.

## 思路分析
链表是一种递归的数据结构，该题可用递归实现，每当`head.val===head.next.val`的时候，便开始进行循环，直到`head.val!==head.next.val`，然后返回`deleteDuplicates(head.next);`

## 代码实现
``` javascript
var deleteDuplicates = function(head) {
    if(head===null)
        return head;
    if(head.next!==null&&(head.val === head.next.val)){
        while(head.next!==null&&(head.val === head.next.val)){
            head = head.next;
        }
        return deleteDuplicates(head.next);
        //这里是说先前节点 = 现在的head.next。
        //但是不能直接用head.next = deleteDuplicates(head.next);
    }else{
        head.next = deleteDuplicates(head.next);
    }
    return head;
};
```
