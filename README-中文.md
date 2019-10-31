<h2 align="center">v-loader-helper</h2>

# 简介
v-loader-helper 可以帮助你更爽的构建Loading部分。

# 功能

- 自定义Loading样式(当然也有默认的).
- 无需手动做Loading判断，自动切换Loading状态.

# 快速开始

### 1. 安装
```
npm install v-loader-helper
```

### 2. 导入
```
import vloader from 'v-loader-helper'

...

Vue.use(vloader)

```

### 3. 放在组件里
```
<template>
  <div id="app">
    <v-loader :source="msg" :urls="['/']">
      <div @click="getRoot">{{ msg }}</div>
    </v-loader>
  </div>
</template>

<script>
import axios from "axios"

export default {
  data() {
    return {
      msg: ""
    }
  },
  methods: {
    getRoot() {
      axios.get("/").then(() => {
        this.msg = "clicl to test" + Math.floor(Math.random() * 100)
      })
    }
  },
  mounted () {
    this.getRoot()
  }
}
</script>


```

# 更详细的使用

### 1. 一些配置参数 
```
import vloader from 'v-loader-helper'
import myLoadingStyle from './myLoadingStyle.vue'

...

Vue.use(vloader, { 
    componentName: 'loader-helper', // Vue注册时使用的tag名称，默认是`v-loader`。
    component: myLoadingStyle       // 你自定义的酷炫Loading。
})
```

### 2. 绑定资源
```
<v-loader :source="msg">
    <div>{{ msg }}</div>
</v-loader>
```
v-loader 会根据绑定的资源自动将Loading状态切换到`hide`。

在仅需要首次加载有Loading的地方使用可以仅仅配置它。

### 3. 绑定URL
```
<v-loader :source="msg" :urls="['/', '/test', '/test/']">
    <div>{{ msg }}</div>
</v-loader>
```
绑定的URL务必与绑定的资源有关联。
v-loader会在用户发起相关请求后自动将Loading状态设置为`show`。
