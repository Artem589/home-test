<script setup>
import IconSun from "../icons/weather/IconSun.vue";
import {ref, computed} from 'vue'
import IconCloud from "../icons/weather/IconCloud.vue";
import IconRain from "../icons/weather/IconRain.vue";


const props = defineProps({
  weatherCode: {
    type: Number,
    default: 1000
  },
  date: {
    type: Date,
    default: 'Вт'
  },
  temperature: {
    type: String,
    default: '30'
  },
  active: {
    type: Boolean,
    default: false
  }
})

const emits = defineEmits(['active-card'])

const classList = computed(() => {
  const baseClass = 'card-day'

  return {
    [baseClass]: true,
    [`${baseClass}--active`]: props.active,
  }
})

const iconWeather = computed(() => {
  switch (props.weatherCode) {
    case 1000:
      return IconSun
    case 1003:
      return IconCloud
    case 1009:
      return IconRain
    default:
      return IconSun
  }
})
</script>

<template>
  <button :class="classList" @click="emits('active-card')">
    <component
        class="card-day__icon"
        :is="iconWeather"
    />
    <span class="card-day__day">{{ props.date.toLocaleDateString('ru-RU', {weekday: "short"}) }}</span>
    <span class="card-day__temp">{{ `${props.temperature} °C` }}</span>
  </button>
</template>

<style scoped lang="scss">
.card-day {
  $base: &;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 15px;
  padding: 20px 25px;

  font-size: 20px;
  line-height: 100%;
  font-weight: 400;

  color: var(--color-primary);
  background-color: var(--color-bg-card);
  cursor: pointer;
  width: fit-content;
  transition: 250ms ease-in-out;
  transition-property: background-color, color;

  box-shadow: 1px 2px 4px 0 var(--color-bg-main);
  border-radius: 10px;
  border: none;

  &:hover:not(&--active) {
    background-color: var(--color-hover-card);
  }

  &--active {
    color: var(--color-bg-card);
    background-color: var(--color-primary);

    #{$base}__icon {
      :deep(path) {
        fill: var(--color-bg-card);
      }
    }
  }

  &__temp {
    font-weight: 700;
  }
}
</style>