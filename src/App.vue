<script setup>
import Button from "./components/Button.vue";
import Test from "./components/Test.vue";
import Stat from "./components/Stat.vue";
import CitySelect from "./components/CitySelect.vue";
import Error from "./components/Error.vue";
import {computed, nextTick, onMounted, ref} from "vue";
import IconSun from "./icons/weather/IconSun.vue";
import IconRain from "./icons/weather/IconRain.vue";
import IconCloud from "./icons/weather/IconCloud.vue";
import CardDay from "./components/CardDay.vue";


const API_URL = "https://api.weatherapi.com/v1"
const API_KEY = import.meta.env.VITE_WEATHER_API_KEY


const cityName = ref('Moscow')
const data = ref()
const errorMessage = ref()


const errorMap = new Map([
  [1006, "Указанный город не найден"]
])

const dataModified = computed((prev) => {

  return [
    {
      label: 'Влажность',
      stat: `${data.value.current.humidity}%`,
    },
    {
      label: 'Облачность',
      stat: `${data.value.current.cloud}%`
    },
    {
      label: 'Ветер',
      stat: `${data.value.current.wind_kph}км/ч`
    },
  ]
})

const dataWeather = computed(() => {
  if (!data.value) {
    return []
  }

  return data.value.forecast.forecastday.map(item => {
    return {
      weatherCode: item.day?.condition?.code,
      temp: item.day?.avgtemp_c,
      date: new Date(item.date)
    }
  })
})

console.log('dataWeather', dataWeather.value)

const errorDisplay = computed(() => {
  return errorMap.get(errorMessage.value?.error?.code)
})


const getCity = async (city) => {
  const params = new URLSearchParams({
    q: city,
    lang: 'ru',
    key: API_KEY,
    days: 3,
  })

  const response = await fetch(`${API_URL}/forecast.json?${params.toString()}`)

  if (response.status !== 200) {
    errorMessage.value = await response.json()
    console.log(errorMessage.value.error.code)
    data.value = null
    return
  }

  errorMessage.value = null
  data.value = await response.json()
}

const daysWeathers = ref([
  {
    date: new Date(),
    temperature: '25',
    active: true,
    weatherCode: 1000
  },
  {
    date: new Date(),
    temperature: '22',
    active: false,
    weatherCode: 1003,
  },
  {
    date: new Date(),
    temperature: '18',
    active: false,
    weatherCode: 1009,
  },
  {
    date: new Date(),
    temperature: '24',
    active: false,
    weatherCode: 1003,
  }
])

const activeCard = (card) => {
  daysWeathers.value.forEach(c => c.active = false)
  card.active = true
}
</script>

<template>
  <main class="main">
    <Error :error-message="errorDisplay"/>
    <div v-if="data">
      <div class="main__stat-list">
        <template v-for="data in dataModified" :key="data.label" >
          <Stat :stat="data.stat" :label="data.label"/>
        </template>
      </div>

      <div class="main__cards-days">
        <template v-for="(card,index) in dataWeather" :key="dataWeather.date">
          <CardDay :weather-code="card.weatherCode" :date="card.date" :temperature="card.temp"
                   @active-card="activeCard(card)"/>
        </template>
      </div>
    </div>


    <CitySelect class="main__city-select" @select-city="getCity" @change-city="getCity"/>
  </main>

  <!--  <test />-->
  <IconSun :size="30" color="red"/>
  <IconRain color="green" :size="30"/>
  <IconCloud color="yellow" :size="30"/>
</template>

<style scoped>
.main {
  background-color: var(--color-bg-main);
  padding: 60px 50px;
  border-radius: 25px;
  max-width: 500px;
  width: fit-content;
}

.main__city-select {
  margin-top: 70px;
}

.main__stat-list {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.main__cards-days {
  display: flex;
  justify-content: space-between;
  gap: 1px;
  margin-top: 80px;
}
</style>


