<script setup>
import { ref } from 'vue'
import BorderLine from './BorderLine.vue'
import WeatherForecastDay from './WeatherForecastDay.vue'
import WeatherInfo from './WeatherInfo.vue'
defineProps({
  location: Object
})

const emit = defineEmits(['delete-card'])

const showDetails = ref(false)

function deleteCard(name) {
  if (confirm('Delete location?')) {
    emit('delete-card', name)
    showDetails.value = false
  }
}
</script>

<template>
  <div
    :class="[{ 'bg-day': location.current.is_day }, { 'bg-night': !location.current.is_day }]"
    class="text-white p-10 rounded-lg shadow-lg gap-6 mb-6 relative overflow-hidden"
  >
    <div class="mb-2 flex justify-between items-center">
      <div class="flex items-center justify-center gap-2">
        <i class="fa-solid fa-location-dot"></i>
        <h1 class="text-3xl">{{ location.location.name }}</h1>
      </div>
      <div class="flex items-center justify-center gap-2">
        <i class="fa-solid fa-clock"></i>
        <h1 class="text-3xl">
          {{ new Date(location.location.localtime).getHours() }}:{{
            ('0' + new Date(location.location.localtime).getMinutes()).slice(-2)
          }}
        </h1>
      </div>
    </div>

    <div class="text-center flex-1">
      <img :src="location.current.condition.icon" alt="icon" width="200" class="mx-auto -mb-10" />
      <h1 class="text-9xl mb-2 -mr-8">{{ Math.round(location.current.temp_f) }}&deg;</h1>
      <p class="text-2xl">{{ location.current.condition.text }}</p>
    </div>

    <BorderLine />

    <div v-for="(forecastDay, i) in location.forecast.forecastday" :key="i">
      <WeatherForecastDay :forecastDay="forecastDay" />
    </div>

    <Transition name="fade">
      <div v-show="showDetails">
        <WeatherInfo
          :location="location"
          @close-info="showDetails = false"
          @delete-location="deleteCard(location.location.name)"
        />
      </div>
    </Transition>

    <div class="flex justify-end items-center gap-1 mt-10">
      <button @click="showDetails = true">
        More <i class="fa-solid fa-arrow-right text-sm -mb-px"></i>
      </button>
    </div>
  </div>
</template>

<style scoped>
.bg-day {
  background-color: #8ec5fc;
  background-image: linear-gradient(62deg, #8ec5fc 0%, #e0c3fc 100%);
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
