<script setup>
const today = new Date()
</script>

<template>
  {{ today.toLocaleDateString('ru-RU')}}
</template>


