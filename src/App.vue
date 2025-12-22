<script setup>
import ScoreLikes from "./components/ScoreLikes.vue";
import CardWord from "./components/CardWord.vue";
import {ref} from "vue";


const isTurn = ref(false)

const cards = ref([
  {
    isTurn: false,
    ruText: 'непризнанный',
    enText: 'unadmitted',
  },
  {
    isTurn: false,
    ruText: 'тычинка',
    enText: 'stamen',
  }
])

const turnCard = (card) => {
  card.isTurn = true
  console.log(card)
}
</script>

<template>
  <div>
    <header class="header">
      <div class="container">
        <div class="header__inner">
          <span class="header__title">Запомни слово</span>
          <score-likes :score="100"/>
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
                       :ru-text="card.ruText"
                       :en-text="card.enText"
                       :count="index + 1"
                       @click-turn="turnCard(card)"
                       @change-status="console.log($event)"
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



