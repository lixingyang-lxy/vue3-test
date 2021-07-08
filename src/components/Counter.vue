<template>
  <h1>{{ msg }}</h1>
  <button @click="handleClick">counter is: {{ counter }}</button>
  <p>{{counter}}</p>
  <p>{{doubleCounter}}</p>
  <p>{{msg2}}</p>
  <p ref="desc"></p>
</template>

<script>
import { reactive, onMounted, computed, onUnmounted, ref, toRefs, watch } from 'vue'

export default {
  name: 'Counter',
  props: {
    msg: String
  },
  handleClick() {
    console.log('bug')
    counter++
  },
  setup() {
    const { counter, doubleCounter } = useCounter()
    const msg2 = ref("some message")
    const desc = ref(null)
    watch(counter, (val, oldVal) => {
      const p = desc.value
      p.textContext = `counter change from ${oldVal} to ${val}`
    })
    return {
      counter, 
      doubleCounter,
      msg2,
      desc
    }
  }
}
function useCounter() {
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
  return toRefs(data)
}
</script>
