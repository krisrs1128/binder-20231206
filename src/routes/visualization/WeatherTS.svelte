<script>
import * as d3 from "d3";
export let dates;

let scatter = [],
  brush,
  brushElement,
  height = 300,
  width = 300;

function load_data() {
  d3.json("https://raw.githubusercontent.com/krisrs1128/stat992_f23/main/examples/week6/week6-4/bike.json")
    .then((d) => {
      scatter = d.scatter
    })
} 

function filter_dates(ev, scatter, scales) {
  let [[x0, y0], [x1, y1]] = ev.selection;
  x0 = scales.x.invert(x0);
  y0 = scales.y.invert(y0);
  x1 = scales.x.invert(x1);
  y1 = scales.y.invert(y1);

  let dates = [];
  for (let i = 0; i < scatter.length; i++) {
    let di = scatter[i]
    if (di.temp > x0 && di.hum > y0 && di.temp < x1 && di.hum < y1) {
      dates.push(di.dteday)
    }
  }
  return dates
}

load_data()
let scales = {}

$: scales = {
    x: d3.scaleLinear()
      .domain([0, 1])
      .range([0, width]),
    y: d3.scaleLinear()
      .domain([0, 1])
      .range([0, height])
}
$: brush = d3.brush()
    .extent([[0, 0], [width, height]])
    .on("brush", ev => {
      dates = filter_dates(ev, scatter, scales)
    });
$: if (brushElement && width != null) {
  d3.select(brushElement).call(brush)
}
</script>

<svg width={width} height={height}>
{#each scatter as d}
  <circle cx={scales.x(d.temp)} cy={scales.y(d.hum)}/>
{/each}
<g bind:this={brushElement} width={width} height={height}/>
</svg>

<style>
  circle {
    r: 4;
    fill: #0c0c0c;
  }
</style>