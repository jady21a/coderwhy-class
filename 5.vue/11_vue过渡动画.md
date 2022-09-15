react 是通过第三方库 react-transition-group 实现动画
vue 则是内置了动画api

# Transition 
具体实现需要自己编写, transition 只是自动加了类名 
```js 
<template>
  <div class="app">
    <div>
      <button @click="isShow = !isShow">切换</button>
    </div>

    <transition name="why">
      <h2 v-if="isShow">哈哈哈哈</h2>
    </transition>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const isShow = ref(false)

</script>

<style scoped>
h2 {
  display: inline-block;
}

.why-enter-from,
.why-leave-to {
  opacity: 0;
  transform: scale(0.6);
}

.why-enter-to,
.why-leave-from {
  opacity: 1;
  transform: scale(1);
}

.why-enter-active,
.why-leave-active {
  transition: all 2s ease;
}

</style>
```


143.-->1h19min
