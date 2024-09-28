<script setup>
defineProps({
  location: Object
})
</script>

<template>
  <div
    class="absolute bg-white/80 backdrop-blur-sm text-slate-900 inset-x-0 bottom-0 rounded-t-lg p-8"
  >
    <div class="flex justify-end mb-10">
      <button @click="$emit('close-info')" class="p-1">
        <i class="fa-solid fa-xmark text-xl"></i>
      </button>
    </div>

    <div class="flex items-center justify-between gap-6 mb-20">
      <div class="text-center flex-1">
        <i class="fa-solid fa-wind mb text-2xl"></i>
        <p class="text-xl font-bold">{{ location.current.wind_mph }} mph</p>
        <p>wind</p>
      </div>

      <div class="text-center flex-1">
        <i class="fa-solid fa-droplet mb text-2xl"></i>
        <p class="text-xl font-bold">{{ location.current.humidity }}%</p>
        <p>humidity</p>
      </div>

      <div class="text-center flex-1">
        <i class="fa-solid fa-umbrella mb text-2xl"></i>
        <p class="text-xl font-bold">{{ location.current.precip_in }} in</p>
        <p>precipitation</p>
      </div>
    </div>
    <div class="flex items-center justify-between gap-6 mb-10">
      <div class="text-center flex-1">
        <i class="fa-solid fa-fan mb text-2xl"></i>
        <p class="text-xl font-bold">{{ location.current.wind_dir }}</p>
        <p>wind direction</p>
      </div>

      <div class="text-center flex-1">
        <i class="fa-solid fa-temperature-half mb text-2xl"></i>
        <p class="text-xl font-bold">{{ Math.round(location.current.feelslike_f) }}&deg;</p>
        <p>feels like</p>
      </div>

      <div class="text-center flex-1">
        <i class="fa-solid fa-sun mb text-2xl"></i>
        <p class="text-xl font-bold">{{ location.current.uv }}</p>
        <p>UV index</p>
      </div>
    </div>

    <div class="flex justify-between items-center">
      <h3 class="text-slate-900/50">last update: {{ location.current.last_updated }}</h3>
      <button @click="$emit('delete-location')">
        <i class="fa-solid fa-trash"></i>
      </button>
    </div>
  </div>
</template>
