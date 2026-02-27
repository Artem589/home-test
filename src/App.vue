<script setup>
import ScoreLikes from "./components/ScoreLikes.vue";
import CardWord from "./components/CardWord.vue";
import {onMounted, ref, watch} from "vue";
import BaseButton from "./components/BaseButton.vue";


const score = ref(0)
const data = ref([])
const cards = ref([])

const turnCard = (card) => {
  card.state = 'opened'
}

const changeStatus = (card, status) => {
  if (status === 'success') {
    score.value = score.value + 10
  }
  if (status === 'fail') {
    score.value = score.value - 4
  }
  card.status = status
}

const restartCards = () => {
  score.value = 0
  getRandomWords()
}

const getRandomWords = async () => {
  try {
    const response = await fetch('http://localhost:8080/api/random-words');

    data.value = await response.json()
  } catch (error) {
    console.error('Ошибка при получении данных:', error);
  }
}

watch((data), (newData) => {

  cards.value = newData.map((item, index) => {
        return {
          index,
          isTurn: false,
          translation: item.translation,
          word: item.word,
          state: 'closed',
          status: 'pending',
        }
      },
  )
})

</script>

<template>
  <div>
    <header class="header">
      <div class="container">
        <div class="header__inner">
          <span class="header__title">Запомни слово</span>
          <score-likes :score/>
        </div>
      </div>
    </header>

    <main class="main">
      <div class="container">
        <div class="main__inner">
          <div v-if="data.length">
            <div class="main__cards">
              <card-word v-for="(card, index) in cards"
                         :key="index"
                         :is-turn="card.isTurn"
                         :translation="card.translation"
                         :word="card.word"
                         :state="card.state"
                         :status="card.status"
                         :count="index + 1"
                         @click-turn="turnCard(card)"
                         @change-status="changeStatus(card,$event)"
              />

            </div>
            <div class="main__button-restart">
              <base-button @click="restartCards">Начать заново</base-button>
            </div>
          </div>

          <div v-else class="main__bottom">
            <base-button @click="getRandomWords">Начать игру</base-button>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<style scoped>
.header__inner {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 62px 0 66px;
  height: 121px;
}

.header__title {
  font-weight: 700;
  font-size: 16px;
  line-height: 24px;
  letter-spacing: 0.12em;
  text-transform: uppercase;

  color: var(--color-primary-text);
}

.container {
  width: 100%;
  max-width: 1440px;
  margin: 0 auto;
}

.main__inner {
  padding: 0 62px 0 66px;
}

.main__cards {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 107px 66px;
}

.main__bottom {
  display: flex;
  flex-direction: column;
  align-content: center;
  justify-content: center;
  flex-wrap: wrap;
  height: 80vh;
  font-size: 32px;
  color: red;
  text-align: center;
}

.main__button-restart {
  display: flex;
  justify-content: center;
  text-align: center;
  margin: 100px 0 65px 0;
}
</style>



