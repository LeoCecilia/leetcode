## 题目
Given a singly linked list, determine if it is a palindrome.

Follow up:
Could you do it in O(n) time and O(1) space?

## 思路分析
先将后半部分进行逆序，然后再一一比较前后半部分是否都相等，若不等则返回false;否则返回true.

注意不能直接用递归的方式进行逆序，不然会出现循环链表的

## 代码实现
``` javascript
var isPalindrome = function(head) {
    function reverseLink(head){
        var pre = null;
        var Head = null;
        while(head){
            var next = head.next;
            head.next = pre;
            pre = head;
            head = next;
        }
        return pre;
    }
    if(!head||!head.next){
        return true;
    }
    var slow = head,
        fast = head;
    while(fast.next&&fast.next.next){
        fast = fast.next.next;
        slow = slow.next;
    }
    slow.next = reverseLink(slow.next);
    slow = slow.next;
    while(slow){
        if(slow.val!==head.val){
            return false;
        }
        slow = slow.next;
        head = head.next;
    }
    return true;
};
```
## 同样的算法ES6的耗时更少(95Ms)
``` javascript
const reverse = head => {
  if (!head || !head.next) return head;
  let pv = null;
  let cur = head;
  while (cur) {
    const t = cur.next;
    cur.next = pv;
    pv = cur;
    cur = t;
  }
  return pv;
};
const isPalindrome = head => {
  if (!head || !head.next) return true;
  // split
  let slow = head;
  let fast = head;
  while (fast.next && fast.next.next) {
    slow = slow.next;
    fast = fast.next.next;
  }
  fast = slow.next;
  slow.next = null;
  // reverse sec
  let rev = reverse(fast);
  // compare
  while (head && rev) {
    if (head.val !== rev.val) return false;
    head = head.next;
    rev = rev.next;
  }
  return true;
};
```
