<template>
<span>With reactive:</span>
  <button @click="increment">
    {{ state.count }}
  </button>

  <span>With ref:</span>
  <button @click="incrementRef">
    {{ refNumber }}
  </button>

  <div v-for="item in state.arr" :key="item">
    {{ item }}
  </div>
</template>

<script setup>
import { reactive, nextTick, ref } from 'vue';

  // It only works for object types, It cannot hold primitive types such as string, number or boolean.
  const state = reactive({ count: 0, arr: ['foo', 'bar'] })
  // allows us to create reactive "refs" that can hold any value type 
  const refNumber = ref(0);

  function increment() {
    state.count++;
    // state.arr.push('baz')
    nextTick(() => {
    })
  }

  const books = reactive([ref('Vue 3 Guide')])
  console.log(books[0].value)

  const map = reactive(new Map([['count', ref(0)]]))
  console.log(map.get('count').value)

  /*const obj = {
    foo: ref(1),
    bar: ref(2)
  }*/

  function incrementRef(){
    refNumber.value++;
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
