<script>
import * as d3 from "d3";
export let dates;

let scatter = [],
  height = 300,
  width = 300;

function load_data() {
  d3.json("https://raw.githubusercontent.com/krisrs1128/stat992_f23/main/examples/week6/week6-4/bike.json")
    .then((d) => {
      scatter = d.scatter
    })
} 

load_data()

let scales = {
    x: d3.scaleLinear()
      .domain([0, 1])
      .range([0, width]),
    y: d3.scaleLinear()
      .domain([0, 1])
      .range([0, height])
}
</script>

<svg width={width} height={height}>
{#each scatter as d}
  <circle cx={scales.x(d.temp)} cy={scales.y(d.hum)}/>
{/each}
</svg>

<style>
  circle {
    r: 4;
    fill: #0c0c0c;
  }
</style>