---
title: 数组去重的n种方法
date: 2021-06-25
tags: 面试
categories: JS
---

## 方法1 （双重遍历）

# 1.
原理：第一层遍历数组，第二层再次遍历数组从i+1开始 当arr[i]===arr[j]的时候，删掉j，j--

```
let arr = [1, 2, 3, 3, 3, 2, 5, 5, 6, 4, 1]
for (let i = 0; i < arr.length; i++) {
  for (let j = i + 1; j < arr.length; j++) {
    if (arr[i] === arr[j]) {
      arr.splice(j, 1)
      // 因为splice删除后 后面元素往前移动了，j要减一
      j--
    }
  }
}
console.log(arr) // [1, 2, 3, 5, 6, 4] 
```
# 2.
原理：设置个标志位，让源数组和去重后数组进行对比，如果相同则证明是重复的，标志位为true，如果没有则为false，把这个数放到去重后数组当中
```
let arr = [1, 2, 3, 3, 3, 2, 5, 5, 6, 4, 1]
let uniqueArr = []
for (let i = 0; i < arr.length; i++) {
  if (arr.indexOf(arr[i]) === i) {
    uniqueArr.push(arr[i])
  }
}
console.log(uniqueArr) // [1, 2, 3, 5, 6, 4] 
```
## 方法二（indexOf）

思路：indexof返回的下标和遍历的下标进行对比，如果相等证明没有，如果不等证明有重复的

```
let arr = [1, 2, 3, 3, 3, 2, 5, 5, 6, 4, 1]
let uniqueArr = []
for (let i = 0; i < arr.length; i++) {
  if (arr.indexOf(arr[i]) === i) {
    uniqueArr.push(arr[i])
  }
}
console.log(uniqueArr) // [1, 2, 3, 5, 6, 4] 
```

## 方法三 （include）

思路：include返回布尔值，如果为true说明有重复的，如果为false放到数组中返回

```
let arr = [1, 2, 3, 3, 3, 2, 5, 5, 6, 4, 1]
let uniqueArr = []
for (let i = 0; i < arr.length; i++) {
  if (!uniqueArr.includes(arr[i])) {
    uniqueArr.push(arr[i])
  }
}
console.log(uniqueArr) // [1, 2, 3, 5, 6, 4] 
```

## 方法四（set)

思路：利用set函数，他内部的元素都是唯一的，没有重复值，再展开变成数组

```
let arr = [1, 2, 3, 3, 3, 2, 5, 5, 6, 4, 1]
let uniqueArr= [...new Set(arr)]
console.log(uniqueArr) // [1, 2, 3, 5, 6, 4] 
```

## 方法五（map）

思路：用map的get和set方法，先get判断有没有，没有的set进去，之后push到数组中

```
let arr = [1, 2, 3, 3, 3, 2, 5, 5, 6, 4, 1]
let uniqueArr = []
let map = new Map()
for (let i = 0; i < arr.length; i++) {
  if (!map.get(arr[i])) {
    map.set(arr[i], true)
    uniqueArr.push(arr[i])
  }
}
console.log(uniqueArr) // [1, 2, 3, 5, 6, 4]
```

## 方法六（hasOwnProperty）

思路：主要是利用对象的hasOwnProperty函数，如果对象存在有待检验的key，那么hasOwnProperty(key)就返回true,否则返回false。把数组的元素存进对象中，hasOwnProperty(元素)如果返回true, 则证明uniqueArr已经存在该元素了，无需再push了。
```
let arr = [1, 2, 3, 3, 3, 2, 5, 5, 6, 4, 1]
let uniqueArr = []
let obj = {}
for (let i = 0; i < arr.length; i++) {
  if (!obj.hasOwnProperty(typeof arr[i] + arr[i])) {
    obj[typeof arr[i] + arr[i]] = true
    uniqueArr.push(arr[i])
  }
}
console.log(uniqueArr) // [1, 2, 3, 5, 6, 4]
```

## 方法七（sort）
思路：排序后判断相邻的两个数是否相等，不相等push进数组
```
let arr = [1, 2, 3, 3, 3, 2, 5, 5, 6, 4, 1]
let uniqueArr = []
arr.sort() 
for (let i = 0; i < arr.length; i++) {
  if(arr[i] !== arr[i + 1]) {
    uniqueArr.push(arr[i])
  }
}
console.log(uniqueArr) // [1, 2, 3, 4, 5, 6]
```

## 方法八（reduce）
思路：主要是利用reduce函数，先排序，然后传入一个新数组，然后判断如果是新数组的length等于0 或者新数组的元素和遍历元素对比，如果不等就则push元素。
```
let arr = [1, 2, 3, 3, 3, 2, 5, 5, 6, 4, 1]
let uniqueArr = arr.sort().reduce((acc, cur, i) => {
  if (acc.length === 0 || acc[acc.length - 1] !== cur) {
    acc.push(cur)
  }
  return acc
}, [])

console.log(uniqueArr) // [1, 2, 3, 4, 5, 6]
```