<script setup>
import { ref } from 'vue'

const emit = defineEmits(['location-data'])

const searchTerm = ref({
  query: '',
  timeout: null,
  results: null
})

function handleSearch() {
  clearTimeout(searchTerm.value.timeout)
  searchTerm.value.timeout = setTimeout(async () => {
    if (searchTerm.value.query !== '') {
      const res = await fetch(
        `http://api.weatherapi.com/v1/search.json?key=${import.meta.env.VITE_WEATHER_API_KEY}&q=${searchTerm.value.query}`
      )

      const data = await res.json()

      searchTerm.value.results = data

      console.log(searchTerm.value.results)
    } else {
      searchTerm.value.results = null
    }
  }, 500)
}

async function getWeather(id) {
  const res = await fetch(
    `http://api.weatherapi.com/v1/forecast.json?key=${import.meta.env.VITE_WEATHER_API_KEY}&q=id:${id}&days=3&aqi=no&alerts=no`
  )

  const data = await res.json()

  emit('location-data', data)
  searchTerm.value.query = ''
  searchTerm.value.results = null
}
</script>

<template>
  <div>
    <form>
      <div class="bg-white border border-indigo-600/300 rounded-lg shadow-lg flex items-center">
        <i class="fa-solid fa-magnifying-glass p-2 text-indigo-600"></i>
        <input
          type="text"
          placeholder="Search for a location"
          class="rounded-r-lg p-2 border-0 outline-0 focus:ring-2 focus:ring-indigo-600 ring-inset w-full"
          v-model="searchTerm.query"
          @input="handleSearch"
        />
      </div>
    </form>

    <div class="bg-white my-2 rounded-lg shadow-lg">
      <div v-if="searchTerm.results">
        <div v-for="place in searchTerm.results" :key="place.id">
          <button
            @click="getWeather(place.id)"
            class="px-3 my-2 hover:text-indigo-600 hover:font-bold w-full text-left"
          >
            {{ place.name }}, {{ place.region }}, {{ place.country }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
