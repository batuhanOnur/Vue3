<template>
<span>With reactive:</span>
  <button @click="increment">
    {{ state.count }}
  </button>

  <span>With ref:</span>
  <button @click="incrementRef">
    {{ refNumber }}
  </button>

  <div v-for="item in state.arr" :key="item" ref="itemRefs">
    {{ item }}
  </div>

  <p>Has published books:</p>
  <span>{{ publishedBooksMessage }}</span>
  
  <div ref="input">

  </div>


  <Child ref="childRef" :title="title"/>
</template>

<script setup>
import { reactive, nextTick, ref, computed, onMounted, onUpdated, watch } from 'vue';
import Child from './components/Child.vue'

  // It only works for object types, It cannot hold primitive types such as string, number or boolean.
  const state = reactive({ count: 0, arr: ['foo', 'bar'] })
  // allows us to create reactive "refs" that can hold any value type 
  const refNumber = ref(2); 
  const itemRefs = ref([])

  //component ref
  const childRef = ref(null);

  // watchers
  const x = ref(0)
  const input = ref(null)

  // props
  const title="batuan";

  function increment() {
    state.count++;
    x.value++;
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
  
  /* COMPUTED */
  const author = reactive({
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
})

// a computed ref
  const publishedBooksMessage = computed(() => {
    return author.books.length > 0 ? 'Yes' : 'No'
  })

  onMounted(()=>{
    console.log('on mounted ref', refNumber.value);
    console.log('ref', input)
    console.log(itemRefs.value)
    console.log('componentRef', childRef.value.a) // child component'den dataya erişme
    childRef.value.log() // child function çağırma
  })

  onUpdated(()=>{
    console.log('updated')
  })

  // single ref watch
  watch(x,(newX, oldX) => {
    console.log(`old x is ${oldX} and new x is ${newX}`)
  })

  // getter for reactive
  watch(
    () => state.count,
    (count) => {
      console.log(`count is: ${count}`)
    }
  )

/*
  // watchEffect
  const url = ref('https://...')
  const data = ref(null)

  watchEffect(async () => {
    const response = await fetch(url.value)
    data.value = await response.json()
  })
*/

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
