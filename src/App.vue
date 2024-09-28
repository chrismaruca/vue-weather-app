<script setup>
import { ref } from 'vue'
import SearchInput from './components/SearchField.vue'
import WeatherCard from './components/WeatherCard.vue'

const locations = ref([])

function addLocation(data) {
  locations.value.push(data)
}

function deleteLocation(name) {
  locations.value = locations.value.filter((l) => l.location.name != name)
}
</script>

<template>
  <main>
    <div class="text-center mb-6">
      {{
        new Date().toLocaleDateString('en-US', {
          weekday: 'long',
          year: 'numeric',
          month: 'long',
          day: 'numeric'
        })
      }}
    </div>

    <div>
      <SearchInput @location-data="addLocation" />
    </div>

    <div class="grid grid-cols-2 gap-4">
      <div v-for="(location, i) in locations" :key="i">
        <WeatherCard :location="location" @delete-card="deleteLocation" />
      </div>
    </div>
  </main>
</template>
