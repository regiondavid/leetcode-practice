## Two Sum

#### leetcode link
[Two Sum](https://leetcode.com/problems/two-sum/#/description)
#### question description
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

#### Example:
``` js
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
#### source code in js
``` js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    var result = [];
    
    var numold = nums.slice(0);
    nums.some(function(ele, index) {
        var test = numold.slice(0);
        test.splice(index,1);
        var tag = test.some(function(element){
            if (element + ele == target) {
                result.push(index);
                if(ele == element) {
                    var nextindex = numold.indexOf(element,index+1);
                    result.push(nextindex)
                } else {
                    var insert = numold.indexOf(element);
                    result.push(insert);
                }
                return true;
            }
        })
        return tag;
    });
    return result;
};
```
#### thinking
尝试做的第一道题，东改西改最终通过了2333。踩得最大的一个坑就是js数组的浅复制和深复制。现在这个也是最基础的一种做法。刚看了答案，还有另外两种，可惜都是JAVA版的。。。让我这个JAVA小白去研究研究再写出JS版的学习学习。