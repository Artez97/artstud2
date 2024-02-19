<template>
    <div>
        <h1>Weather Widget</h1>
        <form @submit.prevent="fetchWeather">
            <input type="text" v-model="city" placeholder="Enter city name" required>
            <button type="submit">Get Weather</button>
        </form>
        <div v-if="error" class="error">{{ error }}</div>
        <div v-if="weather">
            <current-weather :weather="weather.current"></current-weather>
            <forecast :forecast="weather.forecast"></forecast>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';

const city = ref('');
const weather = ref(null);
const error = ref('');

const fetchWeather = async () => {
    try {
        const response = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${city.value}&appid=YOUR_API_KEY&units=metric`);
        const forecastResponse = await axios.get(`https://api.openweathermap.org/data/2.5/forecast?q=${city.value}&appid=YOUR_API_KEY&units=metric`);
        weather.value = {
            current: response.data,
            forecast: forecastResponse.data.list.filter((item, index) => index % 8 === 0) // Assuming forecast is every 3 hours, so we filter to get every 24 hours
        };
        error.value = '';
    } catch (err) {
        error.value = 'Error fetching weather data. Please try again.';
        weather.value = null;
    }
};
</script>

<style>
.error {
    color: red;
}
</style>