<template>
    <div class="weather-forecast">
      <h2>5-Day Forecast for {{ city }}</h2>
      <div class="forecast">
        <div v-for="(item, index) in forecast" :key="index" class="forecast-item">
          <p><strong>Date:</strong> {{ new Date(item.dt * 1000).toLocaleDateString() }}</p>
          <p><strong>Temp:</strong> {{ item.main.temp }} °C</p>
          <p><strong>Humidity:</strong> {{ item.main.humidity }} %</p>
          <p><strong>Conditions:</strong> {{ item.weather[0].description }}</p>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      forecast: Array,
      city: String
    }
  };
  </script>
  
  <style scoped>
  .weather-forecast {
    text-align: left;
    background-color: rgba(255, 255, 255, 0.8);
    padding: 15px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  
  h2 {
    font-size: 1.5rem;
    margin-bottom: 10px;
    color: #007bff;
  }
  
  .forecast {
    display: flex;
    flex-direction: column;
  }
  
  .forecast-item {
    margin-bottom: 15px;
    padding: 10px;
    border-bottom: 1px solid #ddd;
  }
  
  .forecast-item:last-child {
    border-bottom: none;
  }
  
  p {
    font-size: 1.1rem;
    margin: 5px 0;
  }
  </style>
  