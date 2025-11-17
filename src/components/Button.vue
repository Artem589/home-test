<script setup>

</script>

<template>
  <button class="button">
    <div class="button__icon">
      <slot name="icon" />
      <slot name="text" />
    </div>
    <slot />
  </button>
</template>

<style scoped>
.button {
  border: none;
  border-radius: 16px;
  background: var(--gradient);
  padding: 14px;
  font-family: var(--font), sans-serif;
  font-size: 20px;
  font-weight: 600;
  color: var(--color-primary);
  cursor: pointer;
}

.button:hover {
  background: var(--gradient-inverted);
}

</style>