<script lang="ts">
  export let weather;
</script>

<img
  src="https://openweathermap.org/img/w/{weather.weather[0].icon}.png"
  alt="Icon of {weather.weather[0].description}"
/>
<h1>{weather.main.temp} °C</h1>
<h4>
  City:<span class="fw-bold">{weather.name}, {weather.sys.country}</span>
</h4>
<h4>
  Weather: <span class="fw-bold"> {weather.weather[0].description}</span>
</h4>
