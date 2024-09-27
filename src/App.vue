<script setup>
import { ref } from 'vue'
import SearchInput from './components/SearchField.vue'

const locations = ref([])

function addLocation(data) {
  locations.value.push(data)
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

    <div>
      <p v-for="location in locations">{{ location.location.name }}</p>
    </div>
  </main>
</template>
