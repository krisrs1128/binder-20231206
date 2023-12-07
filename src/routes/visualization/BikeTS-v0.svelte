<script>
import * as d3 from "d3";

let series = [],
  height = 300,
  width = 500;

// load the data
function load_data() {
  d3.json("https://raw.githubusercontent.com/krisrs1128/stat992_f23/main/examples/week6/week6-4/bike.json")
    .then((d) => {
      series = d.series
    })
} 

load_data()

// define scales and line generator
let scales = {
  hour: d3.scaleLinear()
    .domain([0, 23])
    .range([0, width]),
  count: d3.scaleLinear()
    .domain([0, 1000])
    .range([height, 0])
}

let generator = d3.line()
    .x(d => scales.hour(d.hr))
    .y(d => scales.count(d.count));
</script>

<svg width={width} height={height}>
  {#each series as d}
    <path d={generator(d)}/>
  {/each}
</svg>

<style>
  path {
    fill: none;
    stroke: black;
  }
</style>