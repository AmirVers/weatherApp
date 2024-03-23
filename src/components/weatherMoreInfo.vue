<script setup>
import xMark from '../assets/xmark.svg'
import droplet from '../assets/droplet.svg'
import fan from '../assets/fan.svg'
import sun from '../assets/sun.svg'
import temperature from '../assets/temperature.svg'
import umbrella from '../assets/umbrella.svg'
import wind from '../assets/wind.svg'
import trash from '../assets/trash.svg'

const emit = defineEmits(['closeInfo'])

defineProps({
  place: Object
})
</script>

<template>
  <div
    class="absolute bg-white/80 backdrop-blur-sm text-slate-900 inset-x-0 bottom-0 rounded-t-lg p-8"
  >
    <div class="flex justify-end mb-10">
      <button class="p-1">
        <xMark @click="emit('closeInfo')" class="translate-x-1/4" />
      </button>
    </div>

    <div class="flex items-center justify-between gap-6 mb-20">
      <div class="text-center flex-1">
        <wind class="translate-x-full" />
        <p class="text-xl font-bold">{{ place.wind_kph }} km/h</p>
        <p>wind</p>
      </div>

      <div class="text-center flex-1">
        <droplet class="translate-x-full" />
        <p class="text-xl font-bold">{{ place.humidity }}</p>
        <p>humidity</p>
      </div>

      <div class="text-center flex-1">
        <umbrella class="translate-x-2/4 h-16" />
        <p class="text-xl font-bold">{{ place.precip_in }}</p>
        <p>precipitation</p>
      </div>
    </div>
    <div class="flex items-center justify-between gap-6 mb-10">
      <div class="text-center flex-1">
        <fan class="translate-x-full" />
        <p class="text-xl font-bold">{{ place.wind_degree }} °</p>
        <p>direction</p>
      </div>

      <div class="text-center flex-1">
        <temperature class="translate-x-full" />
        <p class="text-xl font-bold">{{ place.feelslike_c }} °C</p>
        <p>Feels</p>
      </div>

      <div class="text-center flex-1 mb-2">
        <sun class="translate-x-full w-[67px]" />
        <p class="text-xl font-bold">{{ place.uv }}</p>
        <p>UV index</p>
      </div>
    </div>

    <div class="flex justify-between items-center">
      <h3 class="text-slate-900/50">last update: {{ place.last_updated }}</h3>
      <button @click="$emit('removePlace')"><trash /></button>
    </div>
  </div>
</template>
