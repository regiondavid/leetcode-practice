### 题目
>You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

>You may assume the two numbers do not contain any leading zero, except the number 0 itself.

>Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
>Output: 7 -> 0 -> 8
### 解法一
``` js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
    function test(ob){
        var arr = [];
        function change(ee) {
            arr.push(ee.val);
            if(ee.next!=undefined) {
                change(ee.next);
            }
        }
        change(ob);
        return arr;
    }
    var l3 = test(l1);
    var l4 = test(l2);
    var result = [];
    var index = false;
    var pp = l4.length - l3.length;
    if(pp>0 ) {
        for(var j=0;j<pp;j++){
            l3.push(0);
        }
    } else if (pp<0) {
        for(var z=0;z<-pp;z++){
            l4.push(0);   
        }
    }
    for(var i=0;i<l3.length;i++){
        var tt = l3[i]+l4[i];
        if (index) tt++;
        if(tt<10) {
            result.push(tt);
            index=false;
        }else {
            result.push(tt-10);
            index = true;
            if(i==l3.length-1) result.push(1)
        }
    }
    return result;
};
```
### 解法二
```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
    function test(ob){
        var arr = new Array();
        function change(ee) {
            arr.push(ee.val);
            if(ee.next!=undefined) {
                change(ee.next)
            }
        }
        change(ob);
        return arr;
    };
    var l3 = test(l1).reverse();
    var l4 = test(l2).reverse();
    var num1 = parseInt(l3.reduce(function(val, rss) {
        return val.toString() + rss.toString();
    }));
    var num2 = parseInt(l4.reduce(function(val, rss) {
        return val.toString() + rss.toString();
    }));
    var num3 = num1 + num2;
    return num3;
    var num4 = num3.toString().split("");
    var result = num4.map(function(ele){
        return parseInt(ele);
    });
    return result.reverse();
};
```
### 注：
解法一 accept；
解法一其实还可以再简化，直接不用数组了，直接通过next去判断然后替换掉之前的。

解法二理论上是可以的，在数据量较小的时候结果正确。但是当数据量增多时，会导致转化成的num自动转化成类似`123123e3112321`的形式，导致最后反转成字符串的时候不是我们所预期的那样。

PS：争取把频率提高到一周两道！