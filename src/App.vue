<script setup>
import Button from "./components/Button.vue";
import Stat from "./components/Stat.vue";

import CitySelect from "./components/CitySelect.vue";

const data = {
  label: 'Влажность',
  stat: '90%'
}

const getCity = (city) => {
  console.log(city)
}
</script>

<template>
  <main class="main">
<!--    <Stat v-bind="data"/>-->
<!--    <Stat stat="0 %"/>-->
<!--    <Button>-->
<!--      <icon-location />-->
<!--      Кнопка-->
<!--    </Button>-->

    <CitySelect @select-city="getCity"/>
  </main>

</template>

<style scoped>
.main {
  background-color: var(--color-bg-main);
  padding: 60px 50px;
  border-radius: 25px;
}
</style>


