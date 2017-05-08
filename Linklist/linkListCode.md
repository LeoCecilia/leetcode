## 前言
为了能够更好地了解链表，调试链表，减少bug，新建这一说明文档来存储链表的代码库，用以提升自己的编码技术

## 链表数据结构
``` javascript
function ListNode(val) {
	this.val = val;
	this.next = null;
}
```

## 创建链表
``` javascript
//arr
function createLinkedList(arr) {
	var head = new ListNode(arr[0]);
	head1 = head;
	for(var i = 1;i<arr.length;i++) {
       head.next = new ListNode(arr[i]);
	   head = head.next;
    }
}
```

最近发现即便创建链表之后，在chrome开发者工具中调试仍不是很得心应手，看来还是得去画链表，来想清楚对于怎么操作链表
