<script setup>


</script>

<template>
  <button class="button" type="button">
    <slot/>
  </button>
</template>

<style scoped>
.button {
  padding: 15px;
  outline: 2px solid blue;
  border-radius: 14px;
  transition: all 0.5s ease-in-out;
  cursor: pointer;

  color: #272E37;
  background-color: antiquewhite;
  border: none;
  box-shadow: 8px 5px 5px gray;
}

.button:hover {
transform: scale(1.1);
}
</style>