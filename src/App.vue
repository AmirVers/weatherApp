<script setup>
import { ref } from 'vue'

import searchWeather from './components/searchWeather.vue'
import weatherCard from './components/weatherCard.vue'

const places = ref([])

const pushWeather = (data) => {
  places.value.push(data)
}
const deleteCard = (name) => {
  if (confirm('Are you sure you want to delete this card?')) {
    places.value = places.value.filter((p) => p.location.name !== name)
  }
}
</script>
<template>
  <div class="content">
    <div class="flex justify-center">
      <searchWeather @get-weather="pushWeather" />
    </div>

    <div class="grid grid-cols-2 gap-4">
      <div v-for="(place, index) in places" :key="index">
        <weatherCard :place="place" @deletePlace="deleteCard" />
      </div>
    </div>
  </div>
</template>
