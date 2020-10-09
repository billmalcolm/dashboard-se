<script>
  import { onMount } from "svelte";

  const url =
    "http://api.openweathermap.org/data/2.5/weather?lat=42.9723&lon=-88.0037&appid=5d15af8ebf8d890b4d0bca7b1433040d";

  const src = "http://openweathermap.org/img/wn/";

  let weather = {};
  function convertKtoF(k) {
    let p1 = k - 273.15;
    let p2 = (p1 * 9) / 5;
    let f = p2 + 32;
    return Math.round(f);
  }

  onMount(async () => {
    const response = await fetch(url);
    let data = await response.json();

    weather = {
      temp: convertKtoF(data.main.temp),
      sky: data.weather[0].description,
      icon: src + data.weather[0].icon + ".png",
    };
  });
</script>

<style>
  aside {
    display: flex;
    justify-content: right;
    align-items: center;
    height: 50px;
    padding-right: 5%;
    background-color: darkseagreen;
  }
</style>

<aside aria-label="Weather">
  <p>{weather.temp}&deg;</p>
  <img src={weather.icon} alt={weather.sky} />
  <p>{weather.sky}</p>
</aside>
