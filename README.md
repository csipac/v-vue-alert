# v-vue-alert

# Requirements
- [Vue.js](https://github.com/vuejs/vue) `2.x`

# Installation
```bash
# npm
$ npm install v-vue-alert

$ npm run dev
```

# Usage

inside the file
/src/main.js

```javascript
import Vue from 'vue'
import VAlert from 'v-vue-alert'
import App from './App'

Vue.use(VAlert)

new Vue({
  el: '#app',
  template: '<App/>',
  components: { App }
})


```
VExample.vue

```html
<template>
  <div>
    <h1>Example component</h1>
    <button class="btn btn-default" @click="showAlert">v-vue-alert</button>
  </div>
</template>

<script>
export default {
  methods: {
    showAlert () {
      this.$alert.show({
        message: 'Clicked the button!'
      })
    }
  }
}
</script>
```
# License

[The MIT License](http://opensource.org/licenses/MIT)
