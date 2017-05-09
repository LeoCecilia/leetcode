``` javascript
var partition = function(head, x) {
    var lessHead = new ListNode(0),  
        greaterHead = new ListNode(0),
        node = head,
        less = lessHead,
        greater = greaterHead;  
        while (node != null) {  
            //这里挺重要的
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
