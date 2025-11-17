<script setup>

</script>

<template>
  <button class="button">
    <slot />
  </button>
</template>

<style scoped>
.button {
  border: none;
  border-radius: var(--border-radius-button);
  background: var(--color-bg);
  padding: 16px 10px;
  font-family: var(--font), sans-serif;
  font-size: 24px;
  color: var(--color-primary);
  cursor: pointer;
  width: 315px;
  line-height: 36px;
}

</style>