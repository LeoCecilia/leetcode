## 题目
Reverse a singly linked list.<br>
Hint: A linked list can be reversed either iteratively or recursively.

## 解题思路
使用递归来将链表翻转，首先一直递归到链表的最后一个元素，然后`head.next.next = head;`反指向`head`，从而实现反转，然后`head.next = null;`

## 代码实现
- 递归
  ``` javascript
    var reverseList = function(head) {
      if(!head||!head.next)
          return head;
      var node = reverseList(head.next);
      head.next.next = head;
      head.next = null;
      return node;
    };
  ```

- 循环遍历
  ``` javascript
    var reverseList = function(head) {
        if(head === null)
            return head;
        var p = head;
        p = head.next;
        head.next = null;
        while(p!==null) {
            var pTmp = p.next;//多用一个变量去存储那个值，傻逼了
            p.next = head;
            head = p;
            p = pTmp;
        }
        return head;
    };
  ```
