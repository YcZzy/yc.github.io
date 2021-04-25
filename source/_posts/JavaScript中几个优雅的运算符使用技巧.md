---
title: JavaScript中几个优雅的运算符使用技巧
date: 2021-04-25 11:18:11
tags: JS
---

## 可选链接运算符【？.】

```
let data;
console.log(data?.children?.[0]?.title) // undefined

data  = {children: [{title:'codercao'}]}
console.log(data?.children?.[0]?.title) // codercao
```
# 对于方法的调用你可以这样写

```
object.runsOnlyIfMethodExists?.()
```
```
let parent = {
    name: "parent",
    friends: ["p1", "p2", "p3"],
    getName: function() {
      console.log(this.name)
    }
  };
  
  parent.getName?.()   // parent
  parent.getTitle?.()  //不会执行
  
```
# 与无效合并一起使用
```
let title = data?.children?.[0]?.title ?? 'codercao';
console.log(title); // codercao
```
## 逻辑空分配（?? =）

逻辑空值运算符仅在空值（空值或未定义）时才将值分配给expr1，表达方式
```
expr1 ??= expr2

```

## 逻辑或分配（|| =）

此逻辑赋值运算符仅在左侧表达式为 falsy值时才赋值。Falsy与null有所不同，因为falsy可以是任何一种值：false，0，“”，null，undefined和NaN等

在我们想要保留现有值（如果不存在）的情况下，这很有用，否则我们想为其分配默认值。例如，如果搜索请求中没有数据，我们希望将元素的内部HTML设置为默认值。否则，我们要显示现有列表。这样，我们避免了不必要的更新和任何副作用，例如解析，重新渲染，失去焦点等。我们可以简单地使用此运算符来使用JavaScript更新HTML：

```
document.getElementById('search').innerHTML ||= '<i>No posts found matching this search.</i>'
```

## 逻辑与分配（&& =）

此逻辑赋值运算符仅在左侧为真时才赋值

```
x &&= y
```
等同于
```
x && (x = y)
```