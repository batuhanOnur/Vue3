<template>
  <button @click="increment">
    {{ state.count }}
  </button>

  <span>Ad: {{ state.name }}</span>
  <div v-for="item in state.arr" :key="item">
    {{ item }}
  </div>
</template>

<script setup>
import { reactive } from 'vue';

  const state = reactive({ count: 0, arr: ['foo', 'bar'] })

  function increment() {
    state.count++;
    state.arr.push('baz')
  }

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
