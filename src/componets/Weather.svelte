<script lang="ts">
  import CityInfo from "./CityInfo.svelte";
  import ErrorAlert from "./ErrorAlert.svelte";
  import Loading from "./Loading.svelte";
  import MaxMinTemp from "./MaxMinTemp.svelte";

  let city = "";
  const getWeatherData = async (city: string = "Jaboticabal") => {
    if (city.trim() === "") {
      throw new Error("El campo de busqueda esta en blanco");
    }
    const res = await fetch(
      `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=4b8335036073eddbe43ccf6d59157d39&units=metric&lang=sp`
    );
    const data = await res.json();
    console.log(data);
    if (data.cod == "404") {
      throw new Error("Ciudad no existe");
    }
    return data;
  };
  let weather = getWeatherData();
  const handleSumit = () => {
    weather = getWeatherData(city);
    city = "";
  };
  /* const keys = "4b8335036073eddbe43ccf6d59157d39";
  const url =
    "https://api.openweathermap.org/data/2.5/weather?q=&appid=4b8335036073eddbe43ccf6d59157d39&units=metric";
  const imagesrc =
    "https://openweathermap.org/img/w/" +
    preston.list[i].weather[0].icon +
    ".png"; */
</script>

<div class="container">
  <label for="city"
    >City:
    <input type="text" bind:value={city} class="form-control" required />
  </label><br />
  <button class="btn btn-primary mt-3" on:click={handleSumit}>Search</button>

  <!--<button class="btn btn-primary mt-1" on:click={handleSumit} type="button">
    <span
      class="spinner-border spinner-border-sm"
      role="status"
      aria-hidden="true" //no es apropiado para este
    />
    Search...
  </button>-->

  <div class="row">
    {#await weather}
      <Loading />
    {:then weather}<!--puede llamarse de otra forma, asi se va a chamar el objeto-->
      <div class=" col-12 col-md-6  animate__animated animate__fadeInUp">
        <CityInfo {weather} />
      </div>
      <div class=" col-12 col-md-6 animate__animated animate__fadeInUp">
        <br /><br />
        <MaxMinTemp {weather} />
      </div>
    {:catch error}
      <ErrorAlert {error} />
      <!--Funciona muy bien con los throw new Error('algo')-->
    {/await}
  </div>
</div>
