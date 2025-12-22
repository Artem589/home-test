<script setup>
import IconHeart from "../icons/IconHeart.vue";

const props = defineProps({
  score: {
    type: Number,
    default: 0
  }
})
</script>

<template>
  <div class="likes">
    <span class="likes__score">{{ props.score }}</span>
    <icon-heart />
  </div>
</template>

<style scoped>
.likes {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  padding: 12px 24px;

  border-radius: 36px;
  background-color: #CCE8FF;
  color: #008BFE;
  box-shadow: 0 0 4px 0 #00000026;
}

.likes__score {
  font-size: 16px;
  line-height: 24px;
  font-weight: 700;
}
</style>