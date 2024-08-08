<template>
    <div class="weather-current">
      <h2>Current Weather in {{ city }}</h2>
      <p><strong>Temperature:</strong> {{ weather.main.temp }} °C</p>
      <p><strong>Humidity:</strong> {{ weather.main.humidity }} %</p>
      <p><strong>Conditions:</strong> {{ weather.weather[0].description }}</p>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      weather: Object,
      city: String
    }
  };
  </script>
  
  <style scoped>
  .weather-current {
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
  
  p {
    font-size: 1.1rem;
    margin: 5px 0;
  }
  </style>
  