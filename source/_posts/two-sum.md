---
title: two-sum
date: 2021-06-24
tags: 算法
categories: 每日一题
---
## Title（Easy）

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那两个整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

示例：

``
给定 nums = [2, 7, 11, 15], target = 9
``
因为 nums[0] + nums[1] = 2 + 7 = 9 所以返回 [0, 1]

## Analyze

题解1：暴力法

```

var twoSum = function(nums,target){
    var length = nums.length;
    for(var x=0;x<length;x++){
        for(var y=0;y<length;y++){
            if(nums[x]+nums[y]===target){
                var arr = [];
                arr.push(x);
                arr.push(y);
                return arr;
            }
        }
    }
}

```
时间复杂度O(n^2)
空间复杂度O(1)

题解2：哈希表

    思路：遍历一次数组，查询当前哈希表中是否有和当前索引值nums[i]随影的匹配值target-nums[i]
        若有，则返回他们两个值的索引
        若没有，则将当前索引值和下标存入哈希表中

```
var twoSum = function (nums,target){
    let numsObj={};
    for (let i=0;i<nums.length;i++){
        let current=nums[i];
        let match = target-current;
        if(match in numsObj){
            return [i,numsObj[match]]
        }
        numsObj[current] = i
    }
}

```
时间复杂度: O(n)
空间复杂度: O(n)

题解3：使用 Map, 思路同哈希表

```
var twoSum = function(nums, target) {
  var map = new Map()

  for (let i = 0; i < nums.length; i++) {
    const targetValue = target - nums[i]
    const getTargetValue = map.get(targetValue)
    if (typeof(getTargetValue) === 'number') {
      return [i, getTargetValue]
    }
    map.set(nums[i], i)
  }
}
```
时间复杂度: O(n)
空间复杂度: O(n)
