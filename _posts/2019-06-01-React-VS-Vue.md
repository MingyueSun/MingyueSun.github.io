---
layout:     post                    # 使用的布局（不需要改）
title:      React VS Vue            # 标题 
subtitle:                           #副标题
date:       2019-06-01              # 时间
author:     smy                     # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - React
---

## React与vue的对比
### 组件化方面
1. 什么是模块化：是从代码的角度来进行分析的；把一些可复用的代码，抽离为单个的模块；便于项目的维护和开发；
2. 什么是组件化： 是从UI界面的角度 来进行分析的；把一些可复用的UI元素，抽离为单独的组件；便于项目的维护和开发；
3. 组件化的好处：随着项目规模的增大，手里的组件越来越多；很方便就能把现有的组件，拼接为一个完整的页面
4. Vue提倡模板渲染输出动态的内容，它通过 .vue 文件，来创建对应的组件
- template 结构
- script 行为
- style 样式

5. React中有组件化的概念，但是，并没有像vue这样的组件模板文件；React中，一切都是以JS来表现的，用JSX语法书写

### 数据更新

Vue宣称可以更快地计算出Virtual DOM的差异，这是由于它在渲染过程中，会跟踪每一个组件的依赖关系，不需要重新渲染整个组件树。

而对于React而言，每当应用的状态被改变时，全部子组件都会重新渲染。当然，这可以通过shouldComponentUpdate这个生命周期方法来进行控制，但Vue将此视为默认的优化。

### props

React它依赖一个“单一数据源”作为它的“状态”。而在Vue中，props略有不同。它们一样是在组件中被定义，但Vue依赖于模板语法，你可以通过模板的循环函数更高效地展示传入的数据。

### 状态管理

#### 状态管理 vs 对象属性

React应用中的状态是（React）关键的概念。也有一些配套框架被设计为管理一个大的state对象，如Redux。此外，state对象在React应用中是不可变的，意味着它不能被直接改变，在React中需要使用setState()方法去更新状态。

在Vue中，state对象并不是必须的，数据由data属性在Vue对象中进行管理。

而在Vue中，则不需要使用如setState()之类的方法去改变它的状态，在Vue对象中，data参数就是应用中数据的保存者。

### 开发团队方面

1. React是由FaceBook前端官方团队进行维护和更新的；因此，React的维护开发团队，技术实力比较雄厚；
2. Vue：第一版，主要是有作者 尤雨溪 专门进行维护的，当 Vue更新到 2.x 版本后，也有了一个以 尤雨溪 为主导的开源小团队，进行相关的开发和维护；

### 社区方面

1. 在社区方面，React由于诞生的较早，所以社区比较强大，一些常见的问题、坑、最优解决方案，文档、博客在社区中都是可以很方便就能找到的；
2. Vue是近两年才火起来的，所以，它的社区相对于React来说，要小一些，可能有的一些坑，没人踩过；

### 移动APP开发体验方面

1. Vue，结合 Weex 这门技术，提供了 迁移到 移动端App开发的体验（Weex，目前只是一个 小的玩具， 并没有很成功的 大案例；）
2. React，结合 ReactNative，也提供了无缝迁移到 移动App的开发体验（RN用的最多，也是最火最流行的）