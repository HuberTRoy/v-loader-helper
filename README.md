<h2 align="center">v-loader-helper</h2>

# Intro
v-loader-helper is a loading helper for Vue.js, to help you implement loading easily and comfortable.

# Feature

- Customize loading style.
- Switch loading state automatically.

# Quick Start

### 1. Install:
```
npm install v-loader-helper
```

### 2. Require:
```
import vloader from 'v-loader-helper'

...

Vue.use(vloader)

```

### 3. Use in component:
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

# Usage

### 1. Config options. 
```
import vloader from 'v-loader-helper'
import myLoadingStyle from './myLoadingStyle.vue'

...

Vue.use(vloader, { 
    componentName: 'loader-helper', // It is v-loader-helper name registed in Vue. Default is 'v-loader'.
    component: myLoadingStyle       // It is your customize loading component that will show when loading state is 'loading'.
})
```

### 2. Bind source for check loading.
```
<v-loader :source="msg">
    <div>{{ msg }}</div>
</v-loader>
```
v-loader will check the bind source when it change, if it was changed v-loader will switch the loading state to `hide`.

It is convenient to the page first load.

### 3. Bind urls.
```
<v-loader :source="msg" :urls="['/', '/test', '/test/']">
    <div>{{ msg }}</div>
</v-loader>
```
Urls should connect to source. 
v-loader will switch the loading state to `show` when the user made a HTTP request that URL in your registed urls.

