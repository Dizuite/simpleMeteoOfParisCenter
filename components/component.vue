<template>
  <main>
    <p>The current temperature in specific location (lat: 48.85, long: 2.35 (center of Paris)) is <span v-if="temperature">{{ temperature }}</span>°C</p>
  </main>
</template>

<script>
export default {
  data() {
    return {
      temperature: null
    }
  },
  async mounted() {
    let openMeteoData = await $fetch( `/v1/forecast`, {
      method: 'GET',
      baseURL: 'https://api.open-meteo.com',
      params: {
        latitude: 48.85,
        longitude: 2.35,
        hourly: 'temperature_2m',
        current_weather: true
      }
    });

    this.temperature = openMeteoData.current_weather.temperature;
  }
}
</script>