---
title: add-two-numbers
date: 2021-06-28
tags: 算法
categories: 每日一题
---
## Title（Medium）

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

示例：
Example 1:
``
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
``
Example 2:
``
Input: l1 = [0], l2 = [0]
Output: [0]
``
Example 3:
``
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
``
## Analyze

思路：根据 sum 的值来决定是否要处理进位

题解：

```

// Keyword: single linked list

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
  let flag = 0
  let head = null,
      temp = null
  while (l1 || l2) {
    let sum = flag
    if (l1) {
      sum += l1.val
      l1 = l1.next
    }

    if (l2) {
      sum += l2.val
      l2 = l2.next
    }

    const list = new ListNode(sum % 10)
    if (head === null) {
      head = list
      temp = list
    } else {
      temp.next = list
      temp = list
    }

    // 处理进位
    flag = 0
    if (sum >= 10) {
      flag = 1
    }
  }

  if (flag === 1) {
    const result = new ListNode(1)
    temp.next = result
    temp = result
  }
  return head
}


```