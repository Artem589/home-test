<script setup>
const props = defineProps({
  errorMessage: {
    type: String,
    default: ''
  }
})
</script>

<template>
<div class="error" v-if="props.errorMessage">
  {{ props.errorMessage}}
</div>
</template>

<style scoped>
.error {
  color: red;
  text-align: center;
  font-size: 30px;
  margin-top: -30px;
}
</style>