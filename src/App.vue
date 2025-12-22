<script setup>
import ScoreLikes from "./components/ScoreLikes.vue";
import CardWord from "./components/CardWord.vue";
import {ref} from "vue";


const score = ref(100)

const cards = ref([
  {
    isTurn: false,
    translation: 'непризнанный',
    word: 'unadmitted',
    state: 'closed',
    status: 'pending',
  },
  {
    isTurn: false,
    translation: 'тычинка',
    word: 'stamen',
    state: 'closed',
    status: 'pending',
  }
])

const turnCard = (card) => {
  card.state = 'opened'
}

const changeStatus = (card, status) => {
  card.status = status
}
</script>

<template>
  <div>
    <header class="header">
      <div class="container">
        <div class="header__inner">
          <span class="header__title">Запомни слово</span>
          <score-likes :score />
        </div>
      </div>
    </header>

    <main class="main">
      <div class="container">
        <div class="main__inner">
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
</style>



