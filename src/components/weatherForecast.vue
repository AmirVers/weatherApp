<script setup>
defineProps({
  place: Object
})
</script>

<template>
  <div class="mb-2 flex items-center justify-between">
    <table class="w-full">
      <tr>
        <td class="w-1/3">
          {{
            new Date(place.date).toLocaleDateString('en-us', {
              weekday: 'long'
            })
          }}
        </td>

        <td class="w-1/3">
          <img :src="place.day.condition.icon" alt="icon" width="30" class="mx-auto" />
        </td>

        <td class="w-1/3 text-right">
          {{ Math.round(place.day.maxtemp_c) }}&deg; / {{ Math.round(place.day.mintemp_c) }}&deg;
        </td>
      </tr>
    </table>
  </div>
</template>
