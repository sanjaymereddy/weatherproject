<template>
    <div v-if="weatherData">
      <div class="next-hours">
        <h2>Next hours</h2>
        <div class="hourly-forecast" v-for="forecast in hourlyForecasts" :key="forecast.dt">
          <div class="hourly-time">{{ formatTime(forecast.dt) }}</div>
          <div class="hourly-temp">{{ formatTemp(forecast.main.temp) }}°</div>
          <div class="hourly-icon"><img :src="getIconUrl(forecast.weather[0].icon)" /></div>
          <div class="hourly-desc">{{ forecast.weather[0].description }}</div>
        </div>
      </div>
      <div class="next-days">
        <h2>Next 5 days</h2>
        <div class="daily-forecast" v-for="forecast in dailyForecasts" :key="forecast.dt">
          <div class="daily-date">{{ formatDate(forecast.dt) }}</div>
          <div class="daily-temp">{{ formatTemp(forecast.main.temp) }}°</div>
          <div class="daily-icon"><img :src="getIconUrl(forecast.weather[0].icon)" /></div>
          <div class="daily-desc">{{ forecast.weather[0].description }}</div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'WeatherForecast',
    props: ['weatherData'],
    computed: {
      hourlyForecasts() {
        return this.weatherData ? this.weatherData.list.slice(0, 5) : [];
      },
      dailyForecasts() {
        return this.weatherData ? this.weatherData.list.filter((_, index) => index % 8 === 0).slice(0, 5) : [];
      },
    },
    methods: {
      formatTime(timestamp) {
        const date = new Date(timestamp * 1000);
        return date.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
      },
      formatDate(timestamp) {
        const date = new Date(timestamp * 1000);
        return date.toLocaleDateString([], { weekday: 'short', month: 'short', day: 'numeric' });
      },
      formatTemp(kelvin) {
        return (kelvin - 273.15).toFixed(1);
      },
      getIconUrl(icon) {
        return `http://openweathermap.org/img/wn/${icon}.png`;
      },
    },
  };
  </script>
  
  <style>
  .next-hours, .next-days {
    margin: 20px;
  }
  
  .hourly-forecast, .daily-forecast {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    border-bottom: 1px solid #ddd;
  }
  
  .hourly-forecast {
    padding: 10px 0;
  }
  
  .hourly-time, .hourly-temp, .hourly-icon, .hourly-desc,
  .daily-date, .daily-temp, .daily-icon, .daily-desc {
    flex-basis: 20%;
    text-align: center;
  }
  
  .hourly-desc, .daily-desc {
    word-wrap: break-word;
    white-space: normal;
  }
  
  img {
    width: 40px;
    height: 40px;
  }
  
  h2 {
    margin-bottom: 20px;
  }
  </style>
  