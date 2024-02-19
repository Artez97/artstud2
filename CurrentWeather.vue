<template>
    <div>
        <h2>Current Weather</h2>
        <div>Temperature: {{ weather.main.temp }}°C</div>
        <div>Humidity: {{ weather.main.humidity }}%</div>
        <div>Wind Speed: {{ weather.wind.speed }} m/s</div>
        <img :src="'http://openweathermap.org/img/wn/' + weather.weather[0].icon + '.png'" alt="Weather Icon">
    </div>
</template>

<script setup>
const props = defineProps({
    weather: Object
});
</script>