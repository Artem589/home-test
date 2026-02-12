<script setup>
import {onMounted, onUnmounted, onUpdated} from "vue";

const data = defineModel({type: String, required: true})

</script>

<template>
  <input type="text" class="input" v-model="data">
</template>

<style scoped>
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