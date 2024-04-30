<script setup>
import SearchInput from './components/SearchInput.vue';
import WeatherCard from './components/WeatherCard.vue';
import { ref } from 'vue';

const places = ref([])

const addPlace = (data) => {
  places.value.push(data)
}

const deletePlace = (name) => {
  if (confirm('Are you sure?')) {
    places.value = places.value.filter(p => p.location.name !== name)
  }
  
}

</script>

<template>
  <main>
    <div class="text-center mb-6">
      {{ new Date().toLocaleDateString('en-us', {
        weekday: 'long',
        year: 'numeric',
        month: 'long',
        day: 'numeric'
      }) }}
    </div>

    <div>
      <SearchInput @place-data="addPlace" />
    </div>
    <div class="grid grid-cols-2 gap-4">
      <div v-for="(place, index) in places" :key="index">
        <WeatherCard :place="place" @delete-place="deletePlace" />
      </div>
    </div>
  </main>
</template>