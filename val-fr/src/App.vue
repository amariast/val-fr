<template>
  <div class="cities-container">
    <template v-for="(city, index) in cities" :key="city">
        <CitiesCard :name="city" :style="{ 'grid-area': `city${index}` }"></CitiesCard>
    </template>
  </div>
</template>

<script setup>
  import { ref } from 'vue'
  import CitiesCard from './components/CitiesCard.vue'

  const cities = ref(['paris', 'rome', 'berlin', 'madrid', 'amsterdam', 'london', 'warsaw'])
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400&display=swap');
  .cities-container {
    display: grid;
    max-width: 1000px;
    place-items: center;
    gap: 20px;
    margin: 0 auto;
    overflow: overlay;
  }

  @media (min-width: 1281px) {
    .cities-container {
      grid-template-columns: repeat(4, 1fr);
      grid-template-areas: "city0 city0 city0 city0""city1 city1 city2 city3""city4 city5 city6 city6";
    }
  }

  @media (min-width: 768px) and (max-width: 1280px) {
    .cities-container {
      grid-template-columns: repeat(2, 1fr);
      grid-template-areas: "city0 city0 ""city1  city2""city3  city4""city5 city6";
    }
  }

  @media (min-width: 375px) and (max-width: 768px) {
    .cities-container {
      grid-template-columns: 1fr;
      grid-template-areas: "city0"" city0 ""city1 "" city2""city3  ""city4""city5"" city6";
    }
  }

  * {
    font-family: 'Roboto', sans-serif;
  }
</style>
