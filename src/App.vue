<script setup>
import Button from "./components/Button.vue";
import Stat from "./components/Stat.vue";
import Test from "./components/Test.vue";

import CitySelect from "./components/CitySelect.vue";
import {computed, nextTick, onMounted, ref} from "vue";

const cityName = ref('Moscow')

const data = ref({
  humidity: 90
})

const dateT = ref(new Date )

const date = computed(() => dateT.value)

const getCity = (city) => {
  cityName.value = city
  data.value.humidity = 20
}

const dataModified = computed( (prev) => {
  console.log(prev)
  return {
    label: 'Влажность',
    stat: `${data.value.humidity}%`
  }
})

onMounted( () => {

  setInterval(() => {
  dateT.value = new Date()
  },1000)
})
</script>

<template>
<!--  <main class="main">-->
<!--    <div id="city">-->
<!--      {{  date }}-->
<!--      {{ cityName }}-->

<!--    </div>-->
<!--    <Stat v-bind="dataModified"/>-->
<!--    <Stat stat="0 %"/>-->
<!--    &lt;!&ndash;    <Button>&ndash;&gt;-->
<!--    &lt;!&ndash;      <icon-location />&ndash;&gt;-->
<!--    &lt;!&ndash;      Кнопка&ndash;&gt;-->
<!--    &lt;!&ndash;    </Button>&ndash;&gt;-->

<!--    <CitySelect @select-city="getCity" @change-city="getCity"/>-->
<!--  </main>-->
<test ></test>
</template>

<style scoped>
.main {
  background-color: var(--color-bg-main);
  padding: 60px 50px;
  border-radius: 25px;
}
</style>


