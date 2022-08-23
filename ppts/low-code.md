---
theme: ./theme
highlighter: shiki
monaco: false
title: Low-Code Engine 低代码引擎
---

# Low-Code Engine 低代码引擎

<p class="pl-160 text-25px">
  —— Knight Chen
</p>

<!--
12213
-->

---

# 目录

- Low-Code Engine 是什么？
- 如何基于 Low-Code Engine 搭建低代码平台
- Low-Code Engine 架构

---

# Low-Code Engine 是什么？

> Low-Code Engine 是一款为低代码平台开发者提供的，具备强大定制扩展能力的低代码设计器研发框架。

<div class="flex w-full pt-3">
<div class="w-1/2 pr-5">

**Low-Code Engine 的核心是设计器, 其主要包含两部分**

- 插件（设计器扩展能力）

- 画布 (跨平台能力）

</div>
<div class="w-1/2 pl-5">

<img src="/images/low-code/designer-parts.png" />

</div>
</div>

---

# 如何使用 Low-Code Engine 设计器

官方提供了 demo 仓库，介绍了 Low-Code Engine 的一些基本用法

<https://github.com/alibaba/lowcode-demo>

下面是一段 Low-Code Engine 的启动代码

```ts
import { init, plugins } from '@alilc/lowcode-engine';
import DataSource from '@alilc/lowcode-plugin-datasource-pane';

(async function main() {
  await plugins.register(DataSource);

  init(document.getElementById('lce-container')!, {
    enableCondition: true,
    enableCanvasLock: true,
    simulatorUrl: [
      'https://alifd.alicdn.com/npm/@alilc/lowcode-react-simulator-renderer@latest/dist/js/react-simulator-renderer.js',
      'https://alifd.alicdn.com/npm/@alilc/lowcode-react-simulator-renderer@latest/dist/css/react-simulator-renderer.css',
    ],
  });
})();
```

---

# 设计器定制

这些功能点背后都是可扩展项目，如下图所示

<img class="w-8/10" src="/images/low-code/desinger-custom.png" />

---

# Low-Code Engine 基础架构

<div class="flex w-full pt-3">
<div class="w-1/5 pr-5">

- 设计器核心

  - 项目模型

  - 骨架

  - 资产

- 插件

- 画布

</div>
<div class="w-4/5">

<img src="/images/low-code/jiagou.png" />

</div>
</div>


---
layout: cover
---

# 谢谢观看
