<script setup>
import {computed} from 'vue'
import IconClose from "../icons/IconClose.vue";
import IconSuccess from "../icons/IconSuccess.vue";

const props = defineProps({
  isTurn: {
    type: Boolean,
    default: false
  },
  translation: {
    type: String,
    default: 'непризнанный'
  },
  word: {
    type: String,
    default: 'unadmitted'
  },
  state: {
    type: String,
    default: 'closed'
  },
  status: {
    type: String,
    default: 'pending'
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

const cardText = computed(() => props.state === 'opened' ? props.translation : props.word)
const countCard = computed(() => props.count < 10 ? `0${props.count}` : props.count)
</script>

<template>
  <div class="card">
    <div class="card__inner">
      <div>
        <icon-success class="card__status-icon" v-if="props.status === 'success'"/>
        <icon-close class="card__status-icon" v-if="props.status === 'fail'"/>
      </div>
      <div class="card__count">{{ countCard }}</div>
      <div class="card__value">{{ cardText }}</div>
      <div class="card__action" v-if="props.state === 'closed'" @click="turnCard">
        Перевернуть
      </div>
      <div class="card__status-change" v-if="props.state === 'opened' && props.status === 'pending'">
        <icon-close class="card__icon" @click="changeStatus('fail')"/>
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

.card__status-icon {
  position: absolute;
  left: 50%;
  top: -15px;
  transform: translateX(-50%);
  width: 30px;
  height: 30px;
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

  cursor: pointer;
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
  cursor: pointer;
}
</style>