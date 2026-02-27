<template>
  <button class="button">
    <div class="button__icon">
      <slot name="icon" />
      <slot name="text" />
    </div>
    <slot />
  </button>
</template>

<style scoped lang="scss">
.button {
  border: none;
  border-radius: var(--border-radius-button);
  background: var(--color-bg);
  padding: 16px 10px;
  font-family: var(--font), sans-serif;
  color: var(--color-primary);
  cursor: pointer;
  font-size: 24px;
  font-weight: 400;
  line-height: 36px;
  width: 315px;
}

</style>