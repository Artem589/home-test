<script setup>
import {computed} from 'vue'
import IconClose from "../icons/IconClose.vue";
import IconSuccess from "../icons/IconSuccess.vue";

const props = defineProps({
  isTurn: {
    type: Boolean,
    default: false
  },
  ruText: {
    type: String,
    default: 'непризнанный'
  },
  enText: {
    type: String,
    default: 'unadmitted'
  },
  count: {
    type: Number,
    default: 0
  }
})

const emit = defineEmits(['click-turn', 'change-status'])


const turnCard = () => {
  emit('click-turn')
}

const changeStatus = (status) => {
  emit('change-status', status)
}

const cardText = computed(() => props.isTurn ? props.ruText : props.enText)
const countCard = computed(() => props.count < 10 ? `0${props.count}` : props.count)
</script>

<template>
  <div class="card">
    <div class="card__inner">
      <div class="card__count">{{ countCard }}</div>
      <div class="card__value">{{ cardText }}</div>
      <div class="card__action" v-if="!props.isTurn" @click="turnCard">
        Перевернуть
      </div>
      <div class="card__status-change" v-else>
        <icon-close class="card__icon" @click="changeStatus('error')"/>
        <icon-success class="card__icon" @click="changeStatus('success')"/>
      </div>
    </div>
  </div>

</template>

<style scoped>
.card {
  box-sizing: border-box;
  width: 250px;
  height: 376px;
  padding: 28px 19px;
  border-radius: 16px;
  box-shadow: 0 0 16px 0 #0000001A;
  background-color: var(--color-primary);
}

.card__inner {
  box-sizing: border-box;
  position: relative;
  width: 100%;
  height: 100%;
  border-radius: 12px;
  border: 1px solid #CCE8FF;
}

.card__count {
  position: absolute;
  top: -9px;
  left: 16px;
  font-size: 14px;
  width: 16px;
  height: 16px;
  background-color: var(--color-primary);

}

.card__value {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-size: 18px;
  line-height: 100%;
  letter-spacing: 0;

  width: 100%;
  height: 100%;
}

.card__action {
  position: absolute;
  bottom: -10px;
  left: 50%;
  padding: 0 4px;
  transform: translateX(-50%);

  font-size: 12px;
  font-weight: 700;
  line-height: 18px;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--color-primary-text);
  background-color: var(--color-primary);
}

.card__status-change {
  position: absolute;
  bottom: -12px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 32px;
  padding: 0 8px;
  background-color: var(--color-primary);
}

.card__icon {
  width: 24px;
  height: 24px;
}
</style>