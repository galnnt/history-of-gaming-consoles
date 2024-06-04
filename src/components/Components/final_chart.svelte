<script>
  import { onMount } from "svelte";
  import { scaleOrdinal } from "d3-scale";
  import { arc, pie } from "d3-shape";
  import { select } from "d3-selection";
  import { interpolateRainbow } from "d3-scale-chromatic";
  
  let data = [
    { company: "Nintendo", value: 0 },
    { company: "Sony", value: 0 },
    { company: "Microsoft", value: 0 },
    { company: "Sega", value: 0 },
    { company: "Atari", value: 0 },
    { company: "Coleco", value: 0 },
    { company: "Magnavox", value: 0 },
    { company: "Mattel", value: 0 },
    { company: "Philips", value: 0 },
    { company: "NEC", value: 0 },
    { company: "Bandai", value: 0 },
    { company: "Nokia", value: 0 },
  ];

  let generation = 1;

  const salesData = {
    1: [
      { company: "Nintendo", value: 3.00 },
      { company: "Coleco", value: 1.00 },
      { company: "Magnavox", value: 0.33 }
    ],
    2: [
      { company: "Atari", value: 8.00 },
      { company: "Coleco", value: 1.00 },
      { company: "Mattel", value: 1.00 },
      { company: "Nintendo", value: 1.10 }
    ],
    3: [
      { company: "Atari", value: 1.00 },
      { company: "Sega", value: 2.10 },
      { company: "Nintendo", value: 84.06 }
    ],
    4: [
      { company: "Sega", value: 15.74 },
      { company: "Philips", value: 2.00 },
      { company: "Nintendo", value: 26.10 },
      { company: "Atari", value: 0.50 },
      { company: "NEC", value: 1.50 }
    ],
    5: [
      { company: "Nintendo", value: 34.99 },
      { company: "Sony", value: 10.85 },
      { company: "Sega", value: 1.65 }
    ],
    6: [
      { company: "Bandai", value: 1.50 },
      { company: "Sega", value: 2.50 },
      { company: "Nokia", value: 1.00 },
      { company: "Sony", value: 24.93 },
      { company: "Nintendo", value: 23.31 },
      { company: "Microsoft", value: 8.50 }
    ],
    7: [
      { company: "Nintendo", value: 128.34 },
      { company: "Sony", value: 21.30 },
      { company: "Microsoft", value: 24.00 }
    ],
    8: [
      { company: "Nintendo", value: 60.45 },
      { company: "Microsoft", value: 14.00 },
      { company: "Sony", value: 21.50 }
    ],
    9: [
      { company: "Sony", value: 6.50 },
      { company: "Microsoft", value: 3.73 }
    ]
  };

  const width = 500;
  const height = 500;
  const radius = Math.min(width, height) / 2;

  const color = scaleOrdinal()
    .domain(data.map(d => d.company))
    .range(interpolateRainbow);

  const pieGenerator = pie().value(d => d.value);
  const arcGenerator = arc().innerRadius(0).outerRadius(radius);

  const updateData = (generation) => {
    data = salesData[generation];
    updateChart();
  };

  const updateChart = () => {
    const svg = select("#pie-chart");

    // Remove previous chart elements
    svg.selectAll("*").remove();

    const chartGroup = svg
      .attr("width", width)
      .attr("height", height)
      .append("g")
      .attr("transform", `translate(${width / 2}, ${height / 2})`);

    chartGroup
      .selectAll("path")
      .data(pieGenerator(data))
      .enter()
      .append("path")
      .attr("d", arcGenerator)
      .attr("fill", d => color(d.data.company));

    chartGroup
      .selectAll("text")
      .data(pieGenerator(data))
      .enter()
      .append("text")
      .attr("transform", d => `translate(${arcGenerator.centroid(d)})`)
      .attr("dy", "0.35em")
      .style("text-anchor", "middle")
      .text(d => d.data.company);
  };

  onMount(() => {
    updateData(generation);
  });

  $: updateData(generation);
</script>

<div>
  <input type="range" min="1" max="9" bind:value={generation} />
  <svg id="pie-chart"></svg>
</div>

<style>
  input {
    width: 100%;
  }
</style>
