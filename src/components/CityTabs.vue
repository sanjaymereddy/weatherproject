<template>
    <div>
      <nav>
        <button v-bind:class="showSelected(city)" v-for="city in cities" :key="city" @click="selectCity(city)">
          {{ city }}
        </button>
        <input type="text" v-model="searchQuery" @keyup.enter="searchCity" placeholder="Search city" />
        <button @click="refreshData">Refresh</button>
      </nav>
    </div>
  </template>
  
  <script>
  export default {
    name: 'CityTabs',
    data() {
      return {
        cities: ['Rio de Janeiro', 'Beijing', 'Los Angeles'],
        searchQuery: '',
        selectedCity: 'Los Angeles',
      };
    },
    methods: {
      selectCity(city) {
        this.selectedCity = city;
        this.$emit('citySelected', city);
      },
      showSelected(city) {
        return this.selectedCity === city ? 'selected' : '';
      },
  
      searchCity() {
        this.selectedCity = this.searchQuery;
        this.$emit('citySelected', this.searchQuery);
        this.searchQuery = '';
      },
      refreshData() {
        this.$emit('citySelected', this.selectedCity);
      },
    },
  };
  </script>
  
  <style>
  nav {
    display: flex;
    justify-content: space-around;
    align-items: center;
    background-color: #3f51b5;
    color: white;
    padding: 10px;
  }
  
  button {
    background: none;
    border: none;
    color: white;
    font-size: 16px;
    cursor: pointer;
  }
  
  button:hover {
    text-decoration: underline;
  }
  
  input {
    background: none;
    border: none;
    border-bottom: 1px solid white;
    color: white;
    font-size: 16px;
    padding: 5px;
    margin-left: 10px;
  }
  .selected {
    background-color: green;
  }
  </style>
  