<template>
  <h1>{{ msg }}</h1>
  <button @click="handleClick">counter is: {{ data.counter }}</button>
  <p>{{data.counter}}</p>
  <p>{{data.doubleCounter}}</p>
  <p>{{msg2}}</p>
</template>

<script>
import { reactive, onMounted, computed, onUnmounted, ref } from 'vue'

export default {
  name: 'Counter',
  props: {
    msg: String
  },
  handleClick() {
    console.log('bug')
    data.counter++
  },
  setup() {
    const data = reactive({
      counter: 1,
      doubleCounter: computed(() => data.counter * 2)
    })
    let timer 
    onMounted(() => {
      timer = setInterval(() => {
        data.counter++ 
      }, 1000);
    })
    onUnmounted(() => {
      clearInterval(timer)
    })
    const msg2 = ref("some message")
    return {
      data,
      msg2
    }
  }
}
</script>
