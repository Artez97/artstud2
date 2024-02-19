<template>
    <div>
        <h2>Weather Forecast</h2>
        <div v-for="day in forecast" :key="day.dt">
            <div>{{ new Date(day.dt * 1000).toLocaleDateString() }}</div>
            <div>Temperature: {{ day.main.temp }}°C</div>
            <div>Humidity: {{ day.main.humidity }}%</div>
            <div>Wind Speed: {{ day.wind.speed }} m/s</div>
            <img :src="'http://openweathermap.org/img/wn/' + day.weather[0].icon + '.png'" alt="Weather Icon">
        </div>
    </div>
</template>

<script setup>
const props = defineProps({
    forecast: Array
});
</script>