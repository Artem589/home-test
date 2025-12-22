<script setup>
import {computed, nextTick, reactive, ref} from 'vue'

const isReady = ref(11)
let count =  reactive(3)
const changeReady = async () => {
  isReady.value = true
  const DOM = document.querySelector('#tick')
  console.log('DOM', DOM.innerHTML)
  console.log('DOM', DOM.innerHTML)
  await nextTick()
}

const change = () => {isReady.value  = isReady.value + 10 }
const plusCounter = computed(() => count * 2)

console.log('count', count.value)
console.log(isReady)



</script>

<template>
  <div id="tick">
    {{ isReady }}
<!--    {{plusCounter}}-->
  </div>
  <button @click="changeReady">Изменить статус</button>
  <button @click="change">Посчитать</button>
</template>
