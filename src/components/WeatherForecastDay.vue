<script setup>
defineProps({
  forecastDay: Object
})
</script>

<template>
  <div class="mb-2 flex items-center justify-between">
    <table class="w-full">
      <tbody>
        <tr>
          <td class="w-1/3">
            {{ new Date(forecastDay.date).toLocaleDateString('en-us', { weekday: 'long' }) }}
          </td>

          <td class="w-1/3">
            <img :src="forecastDay.day.condition.icon" alt="icon" width="30" class="mx-auto" />
          </td>

          <td class="w-1/3 text-right">
            {{ Math.round(forecastDay.day.maxtemp_f) }}&deg; -
            {{ Math.round(forecastDay.day.mintemp_f) }}&deg;
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
