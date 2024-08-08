<template>
  <div id="app" class="container">
    <h1>Weather App</h1>
    <div class="input-group mb-3">
      <input v-model="city" class="form-control" placeholder="Enter city name" />
      <button @click="getWeather" class="btn btn-primary">Get Weather</button>
    </div>

    <div v-if="currentWeather" class="mt-4">
      <WeatherCurrent :weather="currentWeather" :city="city" />
    </div>
    <div v-if="forecastWeather" class="mt-4">
      <WeatherForecast :forecast="forecastWeather" :city="city" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import WeatherCurrent from './components/WeatherCurrent.vue';
import WeatherForecast from './components/WeatherForecast.vue';

export default {
  data() {
    return {
      city: '',
      currentWeather: null,
      forecastWeather: null
    };
  },
  components: {
    WeatherCurrent,
    WeatherForecast
  },
  methods: {
    async getWeather() {
      const apiKey = 'a0ad1d357def2efe5a64b30087f4cf20';
      try {
        const currentResponse = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=${apiKey}`);
        this.currentWeather = currentResponse.data;

        const forecastResponse = await axios.get(`https://api.openweathermap.org/data/2.5/forecast?q=${this.city}&units=metric&appid=${apiKey}`);
        this.forecastWeather = forecastResponse.data.list.filter((_, index) => index % 8 === 0); // Getting daily forecast
      } catch (error) {
        console.error(error);
      }
    }
  }
};
</script>

<style scoped>
body {
  background-image: url('@/assets/R.jpeg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  margin: 0;
  font-family: 'Arial', sans-serif;
  color: #333;
}

#app {
  text-align: center;
  margin-top: 50px;
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  background-color: rgba(255, 255, 255, 0.8); /* Semi-transparent background */
}

h1 {
  font-size: 2.5rem;
  margin-bottom: 20px;
  color: #007bff;
}

.input-group {
  display: flex;
  justify-content: center;
  align-items: center;
}

.form-control {
  width: 300px;
  padding: 10px;
  border: 1px solid #007bff;
  border-radius: 5px;
  margin-right: 10px;
  font-size: 1rem;
}

.btn {
  padding: 10px 20px;
  font-size: 1rem;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.btn:hover {
  background-color: #0056b3;
}

.mt-4 {
  margin-top: 40px;
}
</style>
