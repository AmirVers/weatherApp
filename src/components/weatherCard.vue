<script setup>
import weatherForecast from './weatherForecast.vue'
import weatherMoreInfo from './weatherMoreInfo.vue'
import { ref } from 'vue'

let moreInfo = ref(false)
const emit = defineEmits(['deletePlace'])
const handleCloseInfo = () => {
  moreInfo.value = false
}
const removePlace = (placeName) => {
  emit('deletePlace', placeName)
  moreInfo.value = false
}

const hoursTime = (place) => {
  if (new Date(place.location.localtime).getHours() < 10) {
    return `0${new Date(place.location.localtime).getHours()}`
  }
  return new Date(place.location.localtime).getHours()
}

const minutesTime = (place) => {
  if (new Date(place.location.localtime).getMinutes() < 10) {
    return `0${new Date(place.location.localtime).getMinutes()}`
  }
  return new Date(place.location.localtime).getMinutes()
}

defineProps({
  place: Object
})
</script>
<template>
  <div
    :class="place.current.is_day === 1 ? 'bg-day' : 'bg-night'"
    class="text-white p-8 mt-5 rounded-lg shadow-lg relative overflow-hidden"
  >
    <div class="mb-2 flex justify-between items-center">
      <div class="flex items-center justify-center gap-2">
        <h1 class="text-3xl">{{ place.location.name }}</h1>
      </div>
      <div class="flex items-center justify-center gap-2">
        <h1 class="text-3xl">{{ hoursTime(place) }} : {{ minutesTime(place) }}</h1>
      </div>
    </div>

    <div class="text-center flex-1">
      <img :src="place.current.condition.icon" alt="icon" width="200" class="mx-auto -mb-10" />
      <h1 class="text-9xl mb-2">{{ Math.round(place.current.temp_c) }}&deg;</h1>
      <p class="text-2xl">{{ place.current.condition.text }}</p>
    </div>

    <div class="w-full h-px bg-gradient-to-r from-white/0 via-white/90 to-white/0 my-10"></div>

    <div v-for="(place, index) in place.forecast.forecastday" :key="index">
      <weatherForecast :place="place" />
    </div>

    <Transition name="fade">
      <div v-if="moreInfo">
        <weatherMoreInfo
          @closeInfo="handleCloseInfo"
          @removePlace="removePlace(place.location.name)"
          :place="place.current"
        />
      </div>
    </Transition>

    <div class="flex justify-end items-center gap-1 mt-10">
      <button @click="moreInfo = true">More</button>
    </div>
  </div>
</template>

<style scoped>
.bg-day {
  background-color: #4791db;
  background-image: linear-gradient(62deg, #358ce2 0%, #e0c3fc 100%);
}
.bg-night {
  background-color: #07223d;
  background-image: linear-gradient(62deg, #0a2a4a 0%, #270845 100%);
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
