<script>
import WeatherTS from "./WeatherTS.svelte";
import BikeTS from "./BikeTS.svelte";
let dates = [];
</script>

<h1>
Linked Time Series
</h1>

<div id="parent" style="display:flex">
  <div style="flex:6">
    <WeatherTS bind:dates/>
  </div>
  <div style="flex:6">
    <BikeTS bind:dates/>
  </div>
</div>