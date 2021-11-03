<script lang="ts">
  import type { WeatherDataInterface } from "../interfaces/Weather";

  import Loading from "./Loading.svelte";
  import WeatherData from "./WeatherData.svelte";

  let city = "";
  const key = "b1dc0ba9ad09b02d69ece4944f6b4cbc";
  const getWeather = async (city: string = "mexico city") => {
    const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${key}&units=metric`;
    //Limpiar campos trim, espacios en blanco
    if (city.trim() === "") {
      throw new Error("City is required");
    }

    try {
      const response: Response = await fetch(url);

      const data: WeatherDataInterface = await response.json();
      if (!response.ok) {
        throw new Error("No existe");
      }
      return data;
    } catch (error) {
      throw new Error(error);
    }
  };

  let promise = getWeather();

  const handleSubmit = () => {
    promise = getWeather(city);
    city = "";
  };
</script>

<div class="container">
  <div class="row">
    <div class="col-12 mb-3">
      <form on:submit|preventDefault={handleSubmit}>
        <label>
          City: <input bind:value={city} type="text" class="form-control" />
        </label>

        <button type="submit" class="btn btn-info">Search</button>
      </form>
    </div>

    {#await promise}
      <Loading />
    {:then weather}
      <WeatherData {weather} />
    {:catch error}
      <div class="alert alert-danger" role="alert">
        {error}
      </div>
    {/await}
  </div>
</div>
