<script lang="ts">
  import type { WeatherDataInterface } from "../interfaces/Weather";

  export let weather: WeatherDataInterface;
</script>

<div class="col-12 col-md-6 animate__animated animate__fadeInUp">
  <h1>
    <img
      class="bg-secondary"
      src={`http://openweathermap.org/img/wn/${weather.weather[0].icon}@2x.png`}
      alt={weather.name}
    />
    {weather.main.temp}
  </h1>
  <h4>
    City: <span class="fw-bold">{weather.name},{weather.sys.country}</span>
  </h4>
  <h4>
    Weather: <span class="fw-bold">{weather.weather[0].description}</span>
  </h4>
</div>
<div class="col-12 col-md-6 animate__animated animate__fadeInUp">
  <h4>
    Max Temperature: <span class="fw-bold text-danger"
      >{weather.main.temp_max}°C</span
    >
  </h4>
  <h4>
    Min Temperature: <span class="fw-bold text-primary"
      >{weather.main.temp_min}°C</span
    >
  </h4>
</div>
