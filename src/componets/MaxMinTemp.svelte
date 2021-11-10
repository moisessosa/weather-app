<script lang="ts">
  export let weather;
  /*if (weather.main.temp_max < weather.main.feels_like) {
    document.querySelector(".like").classList.add("text-danger");
  } else {
    document.querySelector(".like").classList.add("text-primary");
  }*/
</script>

<h4>
  Maximun Temperature: <span class="fw-bold text-danger"
    >{weather.main.temp_max} °C</span
  >
</h4>
<h4>
  Minumun Temperature: <span class="fw-bold text-primary"
    >{weather.main.temp_min} °C</span
  >
</h4>
<h4>
  Sensacion Termica: <span class="fw-bold like"
    >{weather.main.feels_like} °C</span
  >
</h4>
