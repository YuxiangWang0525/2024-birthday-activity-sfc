# 2024-birthday-activity-sfc
个人网站2024生日活动组件开源 - Open source of personal website 2024 birthday activity component  
# 这是什么
如果你参加了我今年的在线生日活动,你应该知道这是什么,就是你看到的蓝蛋糕点进去变成一个终端和你对话  

## 怎么运行
首先 这是一个Vue SFC(单文件组件) 不能够独立运行在浏览器上,你需要做的是创建一个Vue项目。  
**注意 这是一个Vue 3的单文件组件,请务必创建Vue 3的项目,使用Vue 2甚至更低的版本会导致无法正常运行**  
### 创建项目
``` shell
yarn create vite my-vue-app --template vue
```
**这个项目是纯Vue+JavaScript编写的,没有一行TypeScript代码。如果你只是想装一下,那就没必要创建vue-ts项目**
## 应用组件
生成好了你会发现目录结构中有个src目录,展开目录后你一定能看到components目录和App.vue  
你要做的就是把Main.vue丢进去,按里面的注释指引修改一下里面的内容  
然后打开App.vue 输入如下代码  

``` Vue
<script>
<script setup>
import MainComponents from './components/Main.vue';
<script>
</script>

<template>
<MainComponents />
</template>
```
## 启动Vite开发服务器查看效果
``` shell
yarn dev
```
访问http://localhost:5173/ 你应该能看到空空的蛋糕在页面上
**恭喜你 你成功部署了这个项目**
