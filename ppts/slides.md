---
theme: ./theme
highlighter: shiki
monaco: false
---

# Vue 前端技术框架分享

<p class="pl-110">
  —— Knight Chen
</p>

---

# 概览

1. 框架调研
   - 影响力
   - 社区
   - 用人成本
   - 学习成本
   - 性能
1. Vue 脚手架搭建
1. 组件文档
1. 工具链（cli）

---

# 满意度调研

<img src="/images/slides/1.png" />

<p class="text-right">来自 stateofjs 2020 年全球调研统计数据</p>

### 满意率：会再次使用 / (会再次使用 + 不会再次使用)

---

# 关注度排行

<img src="/images/slides/2.png" />

<p class="text-right">来自 stateofjs 2020 年全球调研统计数据</p>

### 关注率：想学习 / (想学习 + 不感兴趣)

---

# 用人成本

<div class="w-full h-full flex">
  <div class="w-1/2 h-full">
    <ol class="mt-15">
      <li>
        国内使用 Angular 的企业少，导致国内 Angular 开发者同步减少。
      </li>
      <li>
        国内绝大多数前端开发者都会 Vue 或 React 一种，并学习了解过另一种，招聘较为容易
      </li>
    </ol>
  </div>
  <div ref="chart" class="w-100 h-100"></div>
</div>

<script setup>
import * as echarts from 'echarts';
import { ref, onMounted } from 'vue';

const chart = ref(null);

onMounted(() => {
  echarts.init(chart.value).setOption({
    tooltip: {
      trigger: 'item'
    },
    series: [
      {
        type: 'pie',
        radius: '50%',
        data: [
          { value: 41.33, name: 'Vue' },
          { value: 51, name: 'React' },
          { value: 4.33, name: 'Angular' },
        ]
      }
    ],
    animation: false
  })
})
</script>

---

# 性能

<div class="flex w-full h-[calc(100%-2.5rem)]">
  <div class="w-1/3 h-full">
    <img class="w-full h-full object-fill" src="/images/slides/3.png" />
  </div>
  <div ref="chart" class="w-2/3 h-full flex flex-col">
    <div class="pl-20 w-full h-full">
      <img class="w-full h-2/3 object-fill" src="/images/slides/4.png" />
      <p>js-framework-benchmark 报告结果</p>
      <p>结果显示，Vue3.x 在性能方面有巨大的提升，渲染性能对比 Vue >  React ~ Angular</p>
    </div>
  </div>
</div>

---

# 调研总结

|         | 满意度 | 关注度 | 学习成本 | 用人成本 | 社区 | 性能 |
| ------- | ------ | ------ | -------- | -------- | ---- | ---- |
| Vue     | 高     | 高     | 低       | 低       | 高   | 高   |
| React   | 高     | 高     | 中       | 低       | 高   | 高   |
| Angular | 低     | 低     | 高       | 高       | 低   | 中   |

---

# Vue 脚手架

<div class="flex items-center justify-center h-60 w-full">
  <div class="flex flex-col items-center w-20">
    <img class="w-20" src="/images/slides/vite.svg" />
    <span class="text-4xl font-bold mt-2">Vite</span>
  </div>
  <div class="text-6xl mx-30">+</div>
  <div class="flex flex-col items-center w-62">
    <img class="w-20" src="/images/slides/antd.svg" />
    <span class="text-4xl font-bold mt-2">Ant Design Vue</span>
  </div>
</div>

<div class="flex justify-center h-60 w-full">
<div class="mr-30">

### Website

- 约定式路由
- 可配置页面布局
- 样式管理
- 开发文档
- 初始化、构建脚本

</div>

<div class="mr-30">

### UI Library

- 样式管理
- 初始化、构建脚本
- 组件文档生成
- 版本管理

</div>

<div>

### Monorepo

- by 项目定制

</div>

</div>

#####

---

# 约定式路由

<div></div>

根据目录自动生成路由，避免繁琐的配置

```ts {all|2,6|2,5|2,3-4|all}
- src
  - pages
    - user
      - create.vue    ----->    /user/create
    - home.vue        ----->    /home
    - index.vue       ----->    /
```

页面配置信息

```vue
<template>
  <div>{{ $route.meta.name }}</div>
</template>

<route lang="yaml">
meta:
  name: index
redirect: /home
</route>
```

---

# 可配置页面布局

<div></div>

在 layouts 目录下创建布局组件

```ts
- src
  - layouts
    - home.vue     ----->    home
    - panel.vue    ----->    panel
```

<br />

<div class="flex justify-between">
<div class="w-1/2 mr-10">

在 layout 组件中添加布局内容

```vue
<template>
  <div class="flex justify-center">
    <div>
      layout content
    </div>
    <router-view><router-view/>
  </div>
</template>
```

</div>
<div class="w-1/2">

在页面的 meta 中配置 layout 属性即可启用布局配置

```vue
<template>
  <div>page content</div>
</template>

<route lang="yaml">
meta:
  layout: home
</route>
```

</div>
</div>

---

# WindiCSS

<div class="flex justify-between">
<div class="w-3/5 mr-8">

```html
<div class="w-100 h-100 flex text-3xl text-white dark:text-black">
  <div class="w-1/2 h-full bg-red-400 dark:bg-gray-400">
    <span>1</span>
  </div>
  <div class="w-1/2 h-full flex flex-col">
    <div class="w-full flex-1 bg-green-400 dark:bg-gray-400">
      <span>2</span>
    </div>
    <div class="w-full flex-1 bg-blue-400 dark:bg-gray-400">
      <span>3</span>
    </div>
  </div>
</div>
```

</div>
<div class="w-1/2">

<div class="w-100 h-100 flex text-3xl text-white dark:text-black">
  <div class="w-1/2 h-full bg-red-400 dark:bg-gray-400">
    <span>1</span>
  </div>
  <div class="w-1/2 h-full flex flex-col">
    <div class="w-full flex-1 bg-green-400 dark:bg-gray-400">
      <span>2</span>
    </div>
    <div class="w-full flex-1 bg-blue-400 dark:bg-gray-400">
      <span>3</span>
    </div>
  </div>
</div>

</div>
</div>

---

# 工具链

- 命令行工具
- 脚手架初始化
- 打包构建
- 文档生成
- 自定义插件
