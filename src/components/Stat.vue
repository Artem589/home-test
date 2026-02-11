<script setup>

defineProps({
  label: {
    type: String,
    default: 'Осадки'
  },
  stat: {
    type: String,
    default: '0'
  },
})

</script>

<template>
  <div class="stat">
    <div class="label">{{ label }}</div>
    <div class="value">{{ stat }}</div>
  </div>
</template>

<style scoped>
.stat {
  display: flex;
  justify-content: space-between;
  font-size: 28px;
  gap: 16px;
}

.label{
  text-transform: uppercase;
  font-weight: 700;
}

.value {
  font-weight: 500;
}
</style>