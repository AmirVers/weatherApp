<script setup>
import searchIcon from '../assets/search.svg'
import { reactive } from 'vue'
import axios from 'axios'

const emit = defineEmits(['getWeather'])
const searchWeather = reactive({
  query: '',
  result: null
})

const getLocation = async () => {
  try {
    const data = await axios.get(
      `http://api.weatherapi.com/v1/search.json?key=514391cc226c4328912181522241603&q=${searchWeather.query}`
    )
    searchWeather.result = data.data
  } catch (error) {
    console.log(error)
  }
}
const getWeather = async (id) => {
  try {
    const data = await axios.get(
      `http://api.weatherapi.com/v1/forecast.json?key=514391cc226c4328912181522241603&q=${id}&days=3&aqi=no&alerts=no`
    )
    emit('getWeather', data.data)
    searchWeather.query = ''
    searchWeather.result = null
  } catch (error) {
    console.log(error)
  }
}
</script>
<template>
  <div class="mt-1">
    <form class="relative">
      <searchIcon
        class="absolute -translate-y-1/2 top-1/2 left-3 flex items-center pointer-events-none w-6"
      />

      <input
        @input="getLocation"
        v-model="searchWeather.query"
        type="text"
        class="pl-12 bg-gray-100 border-2 border-gray-200 rounded-xl pr-24 py-3"
        placeholder="Search for a city"
      />
    </form>
    <div v-if="searchWeather.query" class="bg-gray-200 rounded-lg mt-2">
      <div v-for="location in searchWeather.result" :key="location.id">
        <button
          @click="getWeather(location.name)"
          class="px-4 py-2 transition w-full rounded-lg hover:bg-indigo-200"
        >
          {{ location.name }}, {{ location.country }}
        </button>
      </div>
    </div>
  </div>
</template>
