<template>
  <div id="app">
    <header>
      <h1>Simple Weather</h1>
      <!-- CityTabs -->
      <city-tabs @citySelected="fetchWeatherData" />
    </header>
      <!-- Weather Forecast -->
    <weather-forecast :weatherData="weatherData" />
  </div>
</template>

<script>
import CityTabs from './components/CityTabs.vue';
import WeatherForecast from './components/WeatherForecast.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    CityTabs,
    WeatherForecast,
  },
  data() {
    return {
      weatherData: null,
    };
  },
  methods: {
    // get weather data
    async fetchWeatherData(city) {
      const apiKey = '482944e26d320a80bd5e4f23b3de7d1f';
      const url = `https://api.openweathermap.org/data/2.5/forecast?q=${city}&appid=${apiKey}`;
      try {
        const response = await axios.get(url);
        this.weatherData = response.data;
      } catch (error) {
        console.error('Error fetching weather data:', error);
      }
    },
  },
  mounted() {
    // Initial method
    this.fetchWeatherData('Los Angeles'); // Default city
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
header {
  background-color: #3f51b5;
  color: white;
  padding: 20px;
}
h1 {
  margin: 0;
}
</style>
