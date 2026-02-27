<script setup>
import {ref, computed, onBeforeUpdate} from 'vue'

const isShowContent = ref(false)

const buttonLabel = computed(() => isShowContent.value ? 'Скрыть' : 'Показать')

</script>

<template>
  <button @click="isShowContent = !isShowContent">{{ buttonLabel }}</button>
  <p v-if="isShowContent">Добро пожаловать в Vue 3!</p>
</template>
