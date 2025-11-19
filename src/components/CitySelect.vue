<script setup>
import Button from "./Button.vue";
import IconLocation from "../icons/IconLocation.vue";
import {ref} from 'vue'

const emit = defineEmits({
  selectCity(payload) {
    console.log(`Validating payload ${payload}`)
    return payload
  }
})

const select = () => {
 emit('selectCity')
}
</script>

<template>
  <div class="city-select">

    <div class="city-select__input" v-if="change">
      <input type="text" class="input" placeholder="Введите город">
      <Button>Сохранить</Button>
    </div>

    <Button v-else>
      <icon-location/>
      Изменить город
    </Button>
  </div>


  <button @click="select" on>Изменить</button>
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

.input {
  padding: 15px 18px;
  background-color: #272E37;
  border-radius: 10px;
  border: none;
  height: 100%;

  color: #FFFFFF;
}

.input::placeholder {
  color: #3F4958;
}

</style>