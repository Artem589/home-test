<script setup>
import Button from "./Button.vue";
import IconLocation from "../icons/IconLocation.vue";
import {ref, onMounted, onBeforeMount, onUpdated, watch, watchEffect, onWatcherCleanup} from 'vue'
import Input from "./Input.vue";

const props = defineProps({
  isChangeCity: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits({
  selectCity(payload) {
    return payload
  },
  changeCity(payload) {
    return payload
  }

})

const cityName = ref('Moscow')
const isEdited = ref(false)

const select = () => {
  emit('selectCity', cityName.value)
  change()
}
const change = () => {
  isEdited.value = !isEdited.value
}

const count = ref(0)

// watch(cityName, (newVal, oldVal) => {
//   console.log(cityName.value)
//   onWatcherCleanup(() => {
//     console.log('cleanup')
//   })
//
// })
//
// watch(count, (newVal) => {
//   const timer = setTimeout(() => {
//     console.log('Delayed:', newVal)
//   }, 1000)
//
// })

onMounted(() => {
  emit('selectCity', cityName.value)
})
</script>

<template>
  <div class="city-select">

    <div class="city-select__input" v-if="isEdited">
      <Input v-model="cityName" @keydown.enter="select" placeholder="Введите город"/>
      <Button @click="select">Сохранить</Button>
    </div>


    <Button v-else @click="change">
      <icon-location/>
      Изменить город
    </Button>

  </div>


  <!--  <button @click="select">Изменить</button>-->
</template>

<style scoped>
.city-select {
  display: flex;
  justify-content: center;
  align-items: center;
}

.city-select__input {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 15px;
}

</style>