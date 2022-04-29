---
title: "Deeper React"
date: 2022-03-03T22:55:40+08:00
draft: true
lastmod: 
image: "cover.webp"
categories:
    - Notes
tags:
    - Programming
    - Front-end Development Libraries
    - React
---

## React Hook

**使用 Hook 的原因**

1. Class 组件共用状态逻辑需要抽离 HOC 反复打包，易造成洋葱地狱
2. 同一个功能的事件可能需要拆到 `componentDidMount`、`componentWillUnmount`、`componentDidUpdate` 生命周期三部分，增加功能维护困难性
3. `this` 里到底有什么？

** State Hook & Effect Hook**

用 Hook 声明组件自身的状态（`useState`）和产生效果（`useEffect`）：

> **动态秒表**
> 组件：表的界面
> 状态：秒数
> 效果：变动效果等

```react
import { useState, useEffect, useRef } from 'react'

cosnt [data, setData] = useState("defaultData");
setData(prev => prev + "newData");

useEffect(() => console.log("Data has been changed!"), [data]); // 绑定 data 状态，渲染完一定会执行一次

const status = useRef(false);
useEffect(() => {
    if (!status) { return; } // 防止初次渲染执行
    fetchData().then(data => status.current = true);
});
```

**`Callback`、`Memo`、`Context`、React Router、Redux**

Context：管理共用的状态

Redux：超大型应用的 Context

## References

- [【前端速成】React 快速入門｜Tiktok工程師帶你入門前端｜布魯斯前端](https://www.youtube.com/watch?v=zqV7NIFGDrQ)