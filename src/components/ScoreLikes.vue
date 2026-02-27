<script setup>
import IconHeart from "../icons/IconHeart.vue";
import { computed } from 'vue'

const props = defineProps({
  score: {
    type: Number,
    default: 0
  }
})

const classList = computed(() => {
  const baseClass = 'likes'

  return {
    [baseClass]: true,
    [`${baseClass}--minus`]: props.score < 0
  }

})
</script>

<template>
  <div :class="classList">
    <span class="likes__score">{{ props.score }}</span>
    <icon-heart />
  </div>
</template>

<style scoped lang="scss">
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

  &--minus {
    color: red;
  }
}

.likes__score {
  font-size: 16px;
  line-height: 24px;
  font-weight: 700;
}
</style>