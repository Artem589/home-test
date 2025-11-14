<script setup>
const today = new Date()

const day = today.getDate()
const month = today.getMonth()
const year = today.getFullYear()
</script>

<template>
  {{ `${day}.${month}.${year}` }}
</template>


